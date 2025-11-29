---
layout: post
title: "AutoEncode 기반 시계열데이터 이상 진단"
date: 2025-11-29T00:00:00Z
authors: ["SG Lee"]
categories: ["Development"]
description: "AutoEncode 기반 시계열데이터 이상 진단"
thumbnail: "/assets/images/gen/blog/blog-5-thumbnail.webp"
image: "/assets/images/gen/blog/blog-5-large.webp"
---

구조 설명
핵심 컴포넌트:

AnomalyDetectorConfig - 하이퍼파라미터 관리 (dataclass 활용)
LSTMAutoEncoder - LSTM 기반 AutoEncoder

Encoder: 시퀀스 → 잠재 벡터 압축
Decoder: 잠재 벡터 → 시퀀스 재구성


AnomalyDetector - 이상 탐지기 래퍼 클래스

fit(): 정상 데이터로 학습
predict(): 재구성 오차 기반 이상 탐지
save()/load(): 모델 저장/로드



이상 탐지 원리:

정상 데이터로 학습된 AutoEncoder는 정상 패턴을 잘 재구성
이상 데이터는 재구성 오차가 높음
백분위 기반 임계값으로 이상 여부 판정

확장 포인트:

input_dim 조정으로 다변량 시계열 지원
Convolutional AutoEncoder로 변경 가능
Variational AutoEncoder (VAE)로 확장 가능
Attention 메커니즘 추가 가능


"""
Time Series Anomaly Detection using AutoEncoder (PyTorch)

기본 구조:
1. AutoEncoder 모델 (LSTM 기반)
2. 데이터 전처리 및 시퀀스 생성
3. 학습 및 평가
4. 이상 탐지 (재구성 오차 기반)
"""

import numpy as np
import torch
import torch.nn as nn
from torch.utils.data import Dataset, DataLoader
from typing import Tuple, Optional
from dataclasses import dataclass


@dataclass
class AnomalyDetectorConfig:
    """AutoEncoder 설정"""
    input_dim: int = 1              # 입력 feature 수
    hidden_dim: int = 64            # LSTM hidden 차원
    latent_dim: int = 32            # 잠재 공간 차원
    num_layers: int = 2             # LSTM 레이어 수
    sequence_length: int = 50       # 시퀀스 길이
    dropout: float = 0.2            # 드롭아웃 비율
    threshold_percentile: float = 95.0  # 이상 탐지 임계값 백분위


class TimeSeriesDataset(Dataset):
    """시계열 데이터셋"""
    
    def __init__(self, data: np.ndarray, sequence_length: int):
        self.data = torch.FloatTensor(data)
        self.sequence_length = sequence_length
    
    def __len__(self) -> int:
        return len(self.data) - self.sequence_length + 1
    
    def __getitem__(self, idx: int) -> torch.Tensor:
        return self.data[idx:idx + self.sequence_length]


class Encoder(nn.Module):
    """LSTM 기반 Encoder"""
    
    def __init__(self, config: AnomalyDetectorConfig):
        super().__init__()
        self.lstm = nn.LSTM(
            input_size=config.input_dim,
            hidden_size=config.hidden_dim,
            num_layers=config.num_layers,
            batch_first=True,
            dropout=config.dropout if config.num_layers > 1 else 0
        )
        self.fc = nn.Linear(config.hidden_dim, config.latent_dim)
    
    def forward(self, x: torch.Tensor) -> Tuple[torch.Tensor, Tuple]:
        # x: (batch, seq_len, input_dim)
        lstm_out, hidden = self.lstm(x)
        # 마지막 시점의 출력을 잠재 공간으로 매핑
        latent = self.fc(lstm_out[:, -1, :])
        return latent, hidden


class Decoder(nn.Module):
    """LSTM 기반 Decoder"""
    
    def __init__(self, config: AnomalyDetectorConfig):
        super().__init__()
        self.sequence_length = config.sequence_length
        self.hidden_dim = config.hidden_dim
        
        self.fc = nn.Linear(config.latent_dim, config.hidden_dim)
        self.lstm = nn.LSTM(
            input_size=config.hidden_dim,
            hidden_size=config.hidden_dim,
            num_layers=config.num_layers,
            batch_first=True,
            dropout=config.dropout if config.num_layers > 1 else 0
        )
        self.output = nn.Linear(config.hidden_dim, config.input_dim)
    
    def forward(self, latent: torch.Tensor) -> torch.Tensor:
        # latent: (batch, latent_dim)
        batch_size = latent.size(0)
        
        # 잠재 벡터를 시퀀스 길이만큼 반복
        hidden_init = self.fc(latent)
        decoder_input = hidden_init.unsqueeze(1).repeat(1, self.sequence_length, 1)
        
        lstm_out, _ = self.lstm(decoder_input)
        reconstructed = self.output(lstm_out)
        return reconstructed


class LSTMAutoEncoder(nn.Module):
    """LSTM AutoEncoder for Time Series Anomaly Detection"""
    
    def __init__(self, config: AnomalyDetectorConfig):
        super().__init__()
        self.config = config
        self.encoder = Encoder(config)
        self.decoder = Decoder(config)
    
    def forward(self, x: torch.Tensor) -> Tuple[torch.Tensor, torch.Tensor]:
        latent, _ = self.encoder(x)
        reconstructed = self.decoder(latent)
        return reconstructed, latent
    
    def encode(self, x: torch.Tensor) -> torch.Tensor:
        latent, _ = self.encoder(x)
        return latent
    
    def decode(self, latent: torch.Tensor) -> torch.Tensor:
        return self.decoder(latent)


class AnomalyDetector:
    """시계열 이상 탐지기"""
    
    def __init__(
        self,
        config: Optional[AnomalyDetectorConfig] = None,
        device: Optional[str] = None
    ):
        self.config = config or AnomalyDetectorConfig()
        self.device = device or ('cuda' if torch.cuda.is_available() else 'cpu')
        self.model = LSTMAutoEncoder(self.config).to(self.device)
        self.threshold: Optional[float] = None
        self.train_losses: list = []
    
    def _create_dataloader(
        self,
        data: np.ndarray,
        batch_size: int,
        shuffle: bool = True
    ) -> DataLoader:
        """데이터로더 생성"""
        # 데이터 정규화
        if data.ndim == 1:
            data = data.reshape(-1, 1)
        
        dataset = TimeSeriesDataset(data, self.config.sequence_length)
        return DataLoader(dataset, batch_size=batch_size, shuffle=shuffle)
    
    def fit(
        self,
        train_data: np.ndarray,
        epochs: int = 100,
        batch_size: int = 32,
        learning_rate: float = 1e-3,
        validation_data: Optional[np.ndarray] = None,
        verbose: bool = True
    ) -> 'AnomalyDetector':
        """모델 학습"""
        train_loader = self._create_dataloader(train_data, batch_size, shuffle=True)
        
        criterion = nn.MSELoss()
        optimizer = torch.optim.Adam(self.model.parameters(), lr=learning_rate)
        scheduler = torch.optim.lr_scheduler.ReduceLROnPlateau(
            optimizer, mode='min', factor=0.5, patience=10
        )
        
        self.model.train()
        self.train_losses = []
        
        for epoch in range(epochs):
            epoch_loss = 0.0
            
            for batch in train_loader:
                batch = batch.to(self.device)
                
                optimizer.zero_grad()
                reconstructed, _ = self.model(batch)
                loss = criterion(reconstructed, batch)
                loss.backward()
                optimizer.step()
                
                epoch_loss += loss.item()
            
            avg_loss = epoch_loss / len(train_loader)
            self.train_losses.append(avg_loss)
            scheduler.step(avg_loss)
            
            if verbose and (epoch + 1) % 10 == 0:
                print(f"Epoch [{epoch+1}/{epochs}], Loss: {avg_loss:.6f}")
        
        # 학습 데이터로 임계값 설정
        self._set_threshold(train_data)
        
        return self
    
    def _set_threshold(self, data: np.ndarray) -> None:
        """재구성 오차 기반 임계값 설정"""
        reconstruction_errors = self._compute_reconstruction_error(data)
        self.threshold = np.percentile(
            reconstruction_errors,
            self.config.threshold_percentile
        )
    
    def _compute_reconstruction_error(self, data: np.ndarray) -> np.ndarray:
        """재구성 오차 계산"""
        self.model.eval()
        
        if data.ndim == 1:
            data = data.reshape(-1, 1)
        
        loader = self._create_dataloader(data, batch_size=64, shuffle=False)
        errors = []
        
        with torch.no_grad():
            for batch in loader:
                batch = batch.to(self.device)
                reconstructed, _ = self.model(batch)
                
                # 시퀀스별 MSE 계산
                mse = torch.mean((batch - reconstructed) ** 2, dim=(1, 2))
                errors.extend(mse.cpu().numpy())
        
        return np.array(errors)
    
    def predict(self, data: np.ndarray) -> Tuple[np.ndarray, np.ndarray]:
        """
        이상 탐지 수행
        
        Returns:
            anomalies: 이상 여부 (True/False)
            scores: 이상 점수 (재구성 오차)
        """
        if self.threshold is None:
            raise RuntimeError("모델이 학습되지 않았습니다. fit()을 먼저 호출하세요.")
        
        scores = self._compute_reconstruction_error(data)
        anomalies = scores > self.threshold
        
        return anomalies, scores
    
    def save(self, path: str) -> None:
        """모델 저장"""
        torch.save({
            'model_state_dict': self.model.state_dict(),
            'config': self.config,
            'threshold': self.threshold,
        }, path)
    
    def load(self, path: str) -> 'AnomalyDetector':
        """모델 로드"""
        checkpoint = torch.load(path, map_location=self.device)
        self.config = checkpoint['config']
        self.model = LSTMAutoEncoder(self.config).to(self.device)
        self.model.load_state_dict(checkpoint['model_state_dict'])
        self.threshold = checkpoint['threshold']
        return self


# ============================================================
# 사용 예제
# ============================================================

def generate_sample_data(
    n_samples: int = 1000,
    anomaly_ratio: float = 0.05
) -> Tuple[np.ndarray, np.ndarray]:
    """샘플 데이터 생성 (정상 + 이상)"""
    np.random.seed(42)
    
    # 정상 데이터: 사인파 + 노이즈
    t = np.linspace(0, 10 * np.pi, n_samples)
    normal_data = np.sin(t) + 0.1 * np.random.randn(n_samples)
    
    # 이상 데이터 주입
    n_anomalies = int(n_samples * anomaly_ratio)
    anomaly_indices = np.random.choice(n_samples, n_anomalies, replace=False)
    
    data = normal_data.copy()
    data[anomaly_indices] += np.random.uniform(2, 4, n_anomalies) * np.sign(np.random.randn(n_anomalies))
    
    # 실제 이상 레이블
    labels = np.zeros(n_samples, dtype=bool)
    labels[anomaly_indices] = True
    
    return data, labels


def main():
    """사용 예제"""
    print("=" * 60)
    print("Time Series Anomaly Detection - AutoEncoder Example")
    print("=" * 60)
    
    # 1. 샘플 데이터 생성
    print("\n[1] 샘플 데이터 생성...")
    data, true_labels = generate_sample_data(n_samples=2000, anomaly_ratio=0.05)
    
    # 학습/테스트 분할
    split_idx = int(len(data) * 0.7)
    train_data = data[:split_idx]
    test_data = data[split_idx:]
    test_labels = true_labels[split_idx:]
    
    print(f"  - 학습 데이터: {len(train_data)} samples")
    print(f"  - 테스트 데이터: {len(test_data)} samples")
    
    # 2. 모델 설정 및 학습
    print("\n[2] 모델 학습...")
    config = AnomalyDetectorConfig(
        input_dim=1,
        hidden_dim=64,
        latent_dim=32,
        sequence_length=50,
        num_layers=2,
        threshold_percentile=95.0
    )
    
    detector = AnomalyDetector(config)
    detector.fit(
        train_data,
        epochs=50,
        batch_size=32,
        learning_rate=1e-3,
        verbose=True
    )
    
    # 3. 이상 탐지
    print("\n[3] 이상 탐지 수행...")
    anomalies, scores = detector.predict(test_data)
    
    # 시퀀스 길이로 인한 레이블 조정
    adjusted_labels = test_labels[config.sequence_length - 1:]
    
    # 4. 결과 출력
    print("\n[4] 결과")
    print(f"  - 탐지된 이상: {np.sum(anomalies)}")
    print(f"  - 실제 이상: {np.sum(adjusted_labels)}")
    print(f"  - 임계값: {detector.threshold:.6f}")
    print(f"  - 평균 이상 점수: {np.mean(scores):.6f}")
    print(f"  - 최대 이상 점수: {np.max(scores):.6f}")
    
    # 5. 모델 저장
    print("\n[5] 모델 저장...")
    detector.save("anomaly_detector.pt")
    print("  - 저장 완료: anomaly_detector.pt")
    
    print("\n" + "=" * 60)
    print("완료!")
    print("=" * 60)


if __name__ == "__main__":
    main()
