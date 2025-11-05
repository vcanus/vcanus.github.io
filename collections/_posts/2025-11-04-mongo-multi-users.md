---
layout: post
title: "MongoDB 유저별 커넥션 전략"
date: 2025-11-04T00:00:00Z
authors: ["SG Lee"]
categories: ["Development"]
description: "MongoDB 유저별독립 커넥션 전략 가이드"
thumbnail: "/assets/images/gen/blog/blog-5-thumbnail.webp"
image: "/assets/images/gen/blog/blog-5-large.webp"
---

# MongoDB: 유저별 독립 커넥션 전략 완벽 가이드

**작성일:** 2025-11-04  
**버전:** 1.0  
**목적:** 유저별 별도 데이터베이스 + 독립 커넥션으로 동시성 문제 해결

---

## 목차

1. [문제 정의](#1-문제-정의)
2. [연결 방식 비교](#2-연결-방식-비교)
3. [유저별 독립 커넥션 구현](#3-유저별-독립-커넥션-구현)
4. [연결 풀 전략](#4-연결-풀-전략)
5. [동시성 처리](#5-동시성-처리)
6. [성능 최적화](#6-성능-최적화)
7. [실전 예제](#7-실전-예제)

---

## 1. 문제 정의

### 1.1 시나리오

```
유저별로 별도의 데이터베이스 사용
- User A → user_a_db
- User B → user_b_db
- User C → user_c_db
...
- User N → user_n_db (N = 수천~수만)
```

### 1.2 단일 연결 방식의 문제점

```python
# ❌ 단일 연결 + useDb() 방식
client = MongoClient("mongodb://localhost:27017/")

# 요청 1: User A
db_a = client['user_a_db']
db_a.posts.insert_one({...})  # 연결 점유

# 요청 2: User B (동시에 발생)
db_b = client['user_b_db']
db_b.posts.insert_one({...})  # 같은 연결 사용 → 대기!

# 요청 3, 4, 5... (동시 요청 증가)
# → 연결 풀이 고갈되고 병목 발생
```

**문제점:**
1. **동시성 제한**: 하나의 연결에 여러 DB 요청이 순차 처리
2. **연결 풀 경쟁**: 모든 유저가 같은 연결 풀 공유
3. **성능 저하**: 유저 수가 증가하면 대기 시간 증가
4. **불공평한 리소스 배분**: 특정 유저의 무거운 쿼리가 다른 유저 영향

### 1.3 해결 방안: 유저별 독립 커넥션

```python
# ✅ 유저별 독립 연결 방식
connections = {
    'user_a': MongoClient("mongodb://localhost:27017/", maxPoolSize=10),
    'user_b': MongoClient("mongodb://localhost:27017/", maxPoolSize=10),
    'user_c': MongoClient("mongodb://localhost:27017/", maxPoolSize=10),
}

# 요청 1: User A
client_a = connections['user_a']
db_a = client_a['user_a_db']
db_a.posts.insert_one({...})  # 독립 연결 풀 사용

# 요청 2: User B (동시 발생)
client_b = connections['user_b']
db_b = client_b['user_b_db']
db_b.posts.insert_one({...})  # 독립 연결 풀 사용 → 대기 없음!
```

**장점:**
1. ✅ 유저 간 완전한 격리
2. ✅ 동시성 극대화
3. ✅ 특정 유저의 부하가 다른 유저에게 영향 없음
4. ✅ 유저별 연결 풀 크기 조정 가능

---

## 2. 연결 방식 비교

### 2.1 방식 1: 단일 연결 + useDb() ❌

```python
"""
단일 MongoClient로 여러 DB 접근
"""

client = MongoClient("mongodb://localhost:27017/", maxPoolSize=100)

def get_user_db(user_id: str):
    return client[f'user_{user_id}_db']

# 모든 유저가 같은 연결 풀(100개) 공유
db_a = get_user_db('user_a')
db_b = get_user_db('user_b')
```

**장점:**
- 구현 간단
- 연결 수 적음 (1개 클라이언트)
- 메모리 사용 적음

**단점:**
- ❌ 동시성 제한 (연결 풀 100개를 모든 유저가 공유)
- ❌ 유저 간 간섭 (한 유저의 슬로우 쿼리가 전체 영향)
- ❌ 확장성 제한
- ❌ 유저별 QoS(Quality of Service) 불가능

**적합한 경우:**
- 유저 수 < 10
- 동시 접속 < 50
- 트래픽 예측 가능
- 단순한 애플리케이션

### 2.2 방식 2: 유저별 독립 연결 ✅

```python
"""
유저별 독립 MongoClient 생성
"""

class UserConnectionManager:
    def __init__(self):
        self.connections = {}
        self.lock = threading.RLock()
    
    def get_client(self, user_id: str) -> MongoClient:
        """유저별 독립 클라이언트 반환"""
        with self.lock:
            if user_id not in self.connections:
                self.connections[user_id] = MongoClient(
                    "mongodb://localhost:27017/",
                    maxPoolSize=10  # 유저당 10개 연결
                )
        return self.connections[user_id]
    
    def get_database(self, user_id: str):
        """유저 DB 반환"""
        client = self.get_client(user_id)
        return client[f'user_{user_id}_db']

# 각 유저가 독립 연결 풀(10개) 사용
manager = UserConnectionManager()
db_a = manager.get_database('user_a')  # 독립 연결 풀
db_b = manager.get_database('user_b')  # 독립 연결 풀
```

**장점:**
- ✅ 유저 간 완전한 격리
- ✅ 동시성 극대화
- ✅ 유저별 QoS 가능 (Premium 유저는 더 큰 풀)
- ✅ 특정 유저 장애 격리
- ✅ 무한 확장 가능

**단점:**
- ⚠️ 연결 수 증가 (유저당 N개)
- ⚠️ 메모리 사용 증가
- ⚠️ 관리 복잡도 증가

**적합한 경우:**
- 유저 수 > 10
- 동시 접속 > 50
- 높은 동시성 요구
- 유저별 SLA 보장 필요

### 2.3 방식 3: 하이브리드 (그룹별 연결) 🔀

```python
"""
유저를 그룹으로 묶어서 그룹별 연결
"""

def get_user_group(user_id: str) -> str:
    """해시로 유저 그룹 결정"""
    return f"group_{hash(user_id) % 10}"  # 10개 그룹

class GroupConnectionManager:
    def __init__(self):
        self.connections = {}
        # 10개 그룹 = 10개 클라이언트
        for i in range(10):
            self.connections[f'group_{i}'] = MongoClient(
                "mongodb://localhost:27017/",
                maxPoolSize=50  # 그룹당 50개
            )
    
    def get_database(self, user_id: str):
        group = get_user_group(user_id)
        client = self.connections[group]
        return client[f'user_{user_id}_db']

# 유저를 10개 그룹으로 분산
# 총 연결 수 = 10 * 50 = 500
```

**장점:**
- ✅ 적당한 격리 수준
- ✅ 연결 수 제한 (그룹 수로 제한)
- ✅ 관리 가능한 복잡도

**단점:**
- ⚠️ 같은 그룹 내 유저는 간섭 가능
- ⚠️ 그룹 불균형 시 문제

**적합한 경우:**
- 중간 규모 (100-1000 유저)
- 연결 수 제한 필요
- 완벽한 격리는 불필요

### 2.4 성능 비교

```
시나리오: 1000명 동시 접속, 각자 1초간 쿼리

┌─────────────────────┬──────────────┬──────────────┬──────────────┐
│      방식            │ 연결 수      │ 처리 시간    │ 격리 수준    │
├─────────────────────┼──────────────┼──────────────┼──────────────┤
│ 단일 연결            │ 100          │ ~10초        │ ⭐           │
│ (maxPoolSize=100)    │              │ (순차 처리)  │              │
├─────────────────────┼──────────────┼──────────────┼──────────────┤
│ 그룹별 연결          │ 500          │ ~2초         │ ⭐⭐⭐       │
│ (10 그룹 * 50)       │              │              │              │
├─────────────────────┼──────────────┼──────────────┼──────────────┤
│ 유저별 연결          │ 10,000       │ ~1초         │ ⭐⭐⭐⭐⭐   │
│ (1000 유저 * 10)     │              │ (병렬 처리)  │              │
└─────────────────────┴──────────────┴──────────────┴──────────────┘
```

---

## 3. 유저별 독립 커넥션 구현

### 3.1 기본 구현 (Python)

```python
"""
유저별 독립 연결 관리자 - 프로덕션 수준

Copyright (c) 2024 VCANUS
"""

import threading
import weakref
import time
from typing import Dict, Optional
from pymongo import MongoClient
from pymongo.database import Database
import logging

logger = logging.getLogger(__name__)


class UserConnectionManager:
    """
    유저별 독립 MongoDB 연결 관리
    
    특징:
    - 유저별 독립 MongoClient 생성
    - 연결 풀 자동 관리
    - Thread-safe
    - 자동 정리 (idle timeout)
    - 메모리 효율적 (weak reference 옵션)
    """
    
    def __init__(
        self,
        connection_string: str,
        user_pool_size: int = 10,
        idle_timeout: int = 3600,  # 1시간
        use_weak_ref: bool = False,
        **mongo_options
    ):
        """
        Args:
            connection_string: MongoDB 연결 문자열
            user_pool_size: 유저당 연결 풀 크기
            idle_timeout: 유휴 연결 타임아웃 (초)
            use_weak_ref: WeakValueDictionary 사용 여부
            **mongo_options: MongoClient 추가 옵션
        """
        self.connection_string = connection_string
        self.user_pool_size = user_pool_size
        self.idle_timeout = idle_timeout
        
        # 연결 저장소
        if use_weak_ref:
            # 약한 참조 - 사용 안할 때 자동 GC
            self._clients: Dict[str, MongoClient] = weakref.WeakValueDictionary()
        else:
            # 강한 참조 - 명시적 제거 전까지 유지
            self._clients: Dict[str, MongoClient] = {}
        
        # 마지막 접근 시간 추적
        self._last_access: Dict[str, float] = {}
        
        # Thread-safe 락
        self._lock = threading.RLock()
        
        # 기본 MongoDB 옵션
        self.mongo_options = {
            'maxPoolSize': user_pool_size,
            'minPoolSize': 1,
            'maxIdleTimeMS': idle_timeout * 1000,
            'connectTimeoutMS': 5000,
            'serverSelectionTimeoutMS': 5000,
            **mongo_options
        }
        
        # 정리 스레드 시작
        self._cleanup_thread = threading.Thread(
            target=self._cleanup_idle_connections,
            daemon=True
        )
        self._cleanup_thread.start()
        
        logger.info(
            f"UserConnectionManager initialized: "
            f"pool_size={user_pool_size}, idle_timeout={idle_timeout}s"
        )
    
    def get_client(self, user_id: str) -> MongoClient:
        """
        유저의 독립 MongoClient 반환
        
        없으면 새로 생성, 있으면 재사용
        
        Args:
            user_id: 유저 ID
            
        Returns:
            MongoClient 인스턴스
        """
        with self._lock:
            # 접근 시간 업데이트
            self._last_access[user_id] = time.time()
            
            # 기존 클라이언트 확인
            if user_id in self._clients:
                client = self._clients[user_id]
                
                # 연결 상태 확인
                try:
                    client.admin.command('ping')
                    logger.debug(f"Reusing connection for user: {user_id}")
                    return client
                except Exception as e:
                    logger.warning(f"Dead connection for {user_id}, recreating: {e}")
                    # 죽은 연결 제거
                    del self._clients[user_id]
            
            # 새 클라이언트 생성
            logger.info(f"Creating new connection for user: {user_id}")
            client = MongoClient(
                self.connection_string,
                **self.mongo_options
            )
            
            self._clients[user_id] = client
            return client
    
    def get_database(self, user_id: str, db_name: Optional[str] = None) -> Database:
        """
        유저의 데이터베이스 반환
        
        Args:
            user_id: 유저 ID
            db_name: 데이터베이스 이름 (기본값: user_{user_id}_db)
            
        Returns:
            Database 인스턴스
        """
        client = self.get_client(user_id)
        
        if db_name is None:
            db_name = f"user_{user_id}_db"
        
        return client[db_name]
    
    def close_user_connection(self, user_id: str) -> bool:
        """
        특정 유저의 연결 종료
        
        Args:
            user_id: 유저 ID
            
        Returns:
            성공 여부
        """
        with self._lock:
            if user_id in self._clients:
                try:
                    self._clients[user_id].close()
                    del self._clients[user_id]
                    
                    if user_id in self._last_access:
                        del self._last_access[user_id]
                    
                    logger.info(f"Closed connection for user: {user_id}")
                    return True
                except Exception as e:
                    logger.error(f"Failed to close connection for {user_id}: {e}")
                    return False
            
            return False
    
    def _cleanup_idle_connections(self):
        """
        유휴 연결 자동 정리 (백그라운드 스레드)
        """
        while True:
            time.sleep(60)  # 1분마다 체크
            
            try:
                with self._lock:
                    now = time.time()
                    idle_users = []
                    
                    for user_id, last_access in self._last_access.items():
                        if now - last_access > self.idle_timeout:
                            idle_users.append(user_id)
                    
                    for user_id in idle_users:
                        logger.info(f"Closing idle connection for user: {user_id}")
                        self.close_user_connection(user_id)
            
            except Exception as e:
                logger.error(f"Error in cleanup thread: {e}")
    
    def get_stats(self) -> dict:
        """
        연결 통계 조회
        
        Returns:
            통계 정보
        """
        with self._lock:
            return {
                'total_connections': len(self._clients),
                'user_pool_size': self.user_pool_size,
                'idle_timeout': self.idle_timeout,
                'active_users': list(self._clients.keys()),
                'total_potential_connections': len(self._clients) * self.user_pool_size
            }
    
    def close_all(self):
        """모든 연결 종료"""
        with self._lock:
            logger.info(f"Closing all {len(self._clients)} connections...")
            
            for user_id, client in list(self._clients.items()):
                try:
                    client.close()
                except Exception as e:
                    logger.error(f"Error closing connection for {user_id}: {e}")
            
            self._clients.clear()
            self._last_access.clear()
            
            logger.info("All connections closed")
    
    def __enter__(self):
        return self
    
    def __exit__(self, exc_type, exc_val, exc_tb):
        self.close_all()


# ============= 사용 예시 =============

if __name__ == "__main__":
    logging.basicConfig(level=logging.INFO)
    
    # 매니저 초기화
    manager = UserConnectionManager(
        connection_string="mongodb://localhost:27017/",
        user_pool_size=10,  # 유저당 10개 연결
        idle_timeout=3600   # 1시간 유휴 시 자동 종료
    )
    
    # User A - 독립 연결
    db_a = manager.get_database('user_a')
    db_a.posts.insert_one({
        'title': 'Hello from User A',
        'content': 'First post'
    })
    
    # User B - 독립 연결 (User A와 간섭 없음)
    db_b = manager.get_database('user_b')
    db_b.posts.insert_one({
        'title': 'Hello from User B',
        'content': 'First post'
    })
    
    # User C - 독립 연결
    db_c = manager.get_database('user_c')
    db_c.posts.insert_one({
        'title': 'Hello from User C',
        'content': 'First post'
    })
    
    # 통계 확인
    stats = manager.get_stats()
    print(f"\nConnection Stats:")
    print(f"  Total connections: {stats['total_connections']}")
    print(f"  Active users: {stats['active_users']}")
    print(f"  Potential connections: {stats['total_potential_connections']}")
    
    # 특정 유저 연결 종료
    manager.close_user_connection('user_a')
    
    # 모든 연결 종료
    manager.close_all()
```

### 3.2 Flask 통합

```python
"""
Flask 애플리케이션과 통합
"""

from flask import Flask, g, request, jsonify
from functools import wraps

app = Flask(__name__)

# 전역 매니저
connection_manager = UserConnectionManager(
    connection_string="mongodb://localhost:27017/",
    user_pool_size=10,
    idle_timeout=3600
)


def get_user_id_from_request() -> str:
    """
    요청에서 유저 ID 추출
    
    우선순위:
    1. JWT 토큰
    2. X-User-ID 헤더
    3. 쿼리 파라미터
    """
    # 방법 1: JWT에서 추출
    auth_header = request.headers.get('Authorization')
    if auth_header and auth_header.startswith('Bearer '):
        token = auth_header[7:]
        # payload = decode_jwt(token)
        # return payload['user_id']
    
    # 방법 2: 헤더
    user_id = request.headers.get('X-User-ID')
    if user_id:
        return user_id
    
    # 방법 3: 쿼리 파라미터
    user_id = request.args.get('user_id')
    if user_id:
        return user_id
    
    raise ValueError("User ID not found in request")


def require_user_db(f):
    """
    유저 DB 주입 데코레이터
    
    각 유저마다 독립 연결 사용
    """
    @wraps(f)
    def decorated_function(*args, **kwargs):
        try:
            # 유저 ID 추출
            user_id = get_user_id_from_request()
            
            # 독립 연결로 DB 가져오기
            g.user_id = user_id
            g.db = connection_manager.get_database(user_id)
            
            return f(*args, **kwargs)
        
        except ValueError as e:
            return jsonify({'error': str(e)}), 400
        
        except Exception as e:
            logger.error(f"Database error: {e}", exc_info=True)
            return jsonify({'error': 'Internal server error'}), 500
    
    return decorated_function


# ============= API 엔드포인트 =============

@app.route('/api/posts', methods=['GET'])
@require_user_db
def get_posts():
    """포스트 목록 조회"""
    posts = list(g.db.posts.find({}, {'_id': 0}).limit(20))
    return jsonify({
        'user_id': g.user_id,
        'posts': posts
    })


@app.route('/api/posts', methods=['POST'])
@require_user_db
def create_post():
    """포스트 생성"""
    data = request.get_json()
    
    # 유저의 독립 DB에 저장
    result = g.db.posts.insert_one(data)
    
    return jsonify({
        'user_id': g.user_id,
        'post_id': str(result.inserted_id),
        'message': 'Post created successfully'
    }), 201


@app.route('/api/posts/<post_id>', methods=['GET'])
@require_user_db
def get_post(post_id):
    """포스트 조회"""
    from bson import ObjectId
    
    post = g.db.posts.find_one({'_id': ObjectId(post_id)})
    
    if not post:
        return jsonify({'error': 'Post not found'}), 404
    
    post['_id'] = str(post['_id'])
    return jsonify({
        'user_id': g.user_id,
        'post': post
    })


# ============= 관리자 엔드포인트 =============

@app.route('/admin/connections', methods=['GET'])
def get_connection_stats():
    """연결 통계"""
    stats = connection_manager.get_stats()
    return jsonify(stats)


@app.route('/admin/connections/<user_id>', methods=['DELETE'])
def close_user_connection(user_id):
    """특정 유저 연결 종료"""
    success = connection_manager.close_user_connection(user_id)
    
    if success:
        return jsonify({'message': f'Connection closed for {user_id}'})
    else:
        return jsonify({'error': f'No connection found for {user_id}'}), 404


if __name__ == '__main__':
    app.run(debug=True)
```

### 3.3 FastAPI 통합

```python
"""
FastAPI 애플리케이션과 통합
"""

from fastapi import FastAPI, Depends, Header, HTTPException
from typing import Optional
from pydantic import BaseModel

app = FastAPI()

# 전역 매니저
connection_manager = UserConnectionManager(
    connection_string="mongodb://localhost:27017/",
    user_pool_size=10
)


# ============= Pydantic 모델 =============

class Post(BaseModel):
    title: str
    content: str
    tags: Optional[list] = []


# ============= Dependency =============

async def get_user_database(
    x_user_id: str = Header(..., description="User ID")
):
    """
    유저 독립 DB 의존성
    
    각 유저마다 독립 연결 사용
    """
    if not x_user_id:
        raise HTTPException(
            status_code=400,
            detail="X-User-ID header is required"
        )
    
    # 독립 연결로 DB 반환
    db = connection_manager.get_database(x_user_id)
    
    return {
        'user_id': x_user_id,
        'db': db
    }


# ============= API 엔드포인트 =============

@app.get("/api/posts")
async def get_posts(
    user_data = Depends(get_user_database),
    limit: int = 20
):
    """포스트 목록 조회"""
    posts = list(
        user_data['db'].posts
        .find({}, {'_id': 0})
        .limit(limit)
    )
    
    return {
        'user_id': user_data['user_id'],
        'posts': posts
    }


@app.post("/api/posts", status_code=201)
async def create_post(
    post: Post,
    user_data = Depends(get_user_database)
):
    """포스트 생성"""
    result = user_data['db'].posts.insert_one(post.dict())
    
    return {
        'user_id': user_data['user_id'],
        'post_id': str(result.inserted_id),
        'message': 'Post created successfully'
    }


@app.get("/api/posts/{post_id}")
async def get_post(
    post_id: str,
    user_data = Depends(get_user_database)
):
    """포스트 조회"""
    from bson import ObjectId
    
    post = user_data['db'].posts.find_one({'_id': ObjectId(post_id)})
    
    if not post:
        raise HTTPException(status_code=404, detail="Post not found")
    
    post['_id'] = str(post['_id'])
    return {
        'user_id': user_data['user_id'],
        'post': post
    }


# ============= 관리자 엔드포인트 =============

@app.get("/admin/connections")
async def get_connection_stats():
    """연결 통계"""
    return connection_manager.get_stats()


@app.delete("/admin/connections/{user_id}")
async def close_user_connection(user_id: str):
    """특정 유저 연결 종료"""
    success = connection_manager.close_user_connection(user_id)
    
    if success:
        return {'message': f'Connection closed for {user_id}'}
    else:
        raise HTTPException(
            status_code=404,
            detail=f'No connection found for {user_id}'
        )
```

---

## 4. 연결 풀 전략

### 4.1 풀 크기 결정

```python
"""
유저별 연결 풀 크기 계산
"""

def calculate_pool_size(
    concurrent_users: int,
    requests_per_user: int = 5,
    available_connections: int = 10000
) -> tuple:
    """
    적절한 풀 크기 계산
    
    Args:
        concurrent_users: 동시 접속 유저 수
        requests_per_user: 유저당 동시 요청 수
        available_connections: 서버에서 허용하는 최대 연결 수
        
    Returns:
        (user_pool_size, max_users)
    """
    # 1. 이상적인 유저당 풀 크기
    ideal_pool_size = requests_per_user
    
    # 2. 서버 제약 고려
    max_users_with_ideal = available_connections // ideal_pool_size
    
    if max_users_with_ideal >= concurrent_users:
        # 충분한 연결 수
        return (ideal_pool_size, concurrent_users)
    else:
        # 연결 수 부족 - 풀 크기 줄임
        adjusted_pool_size = available_connections // concurrent_users
        return (adjusted_pool_size, concurrent_users)


# 예시
concurrent_users = 1000
pool_size, max_users = calculate_pool_size(
    concurrent_users=concurrent_users,
    requests_per_user=5,
    available_connections=10000
)

print(f"Recommended pool size: {pool_size}")
print(f"Max users supported: {max_users}")
print(f"Total connections: {pool_size * max_users}")

# 출력:
# Recommended pool size: 5
# Max users supported: 1000
# Total connections: 5000
```

### 4.2 동적 풀 크기 조정

```python
"""
유저 등급별 다른 풀 크기
"""

class TieredUserConnectionManager(UserConnectionManager):
    """
    등급별 차등 연결 풀
    """
    
    def __init__(self, connection_string: str, **options):
        super().__init__(connection_string, **options)
        
        # 등급별 풀 크기
        self.tier_pool_sizes = {
            'free': 3,
            'basic': 5,
            'premium': 10,
            'enterprise': 20
        }
    
    def get_user_tier(self, user_id: str) -> str:
        """
        유저 등급 조회 (실제로는 DB에서 가져와야 함)
        """
        # TODO: 실제 구현에서는 DB 조회
        # 여기서는 예시로 user_id 기반 반환
        if user_id.startswith('ent_'):
            return 'enterprise'
        elif user_id.startswith('pre_'):
            return 'premium'
        elif user_id.startswith('bas_'):
            return 'basic'
        else:
            return 'free'
    
    def get_client(self, user_id: str) -> MongoClient:
        """등급에 맞는 풀 크기로 클라이언트 생성"""
        with self._lock:
            if user_id in self._clients:
                return self._clients[user_id]
            
            # 유저 등급 확인
            tier = self.get_user_tier(user_id)
            pool_size = self.tier_pool_sizes.get(tier, 5)
            
            logger.info(
                f"Creating connection for user {user_id} "
                f"(tier: {tier}, pool_size: {pool_size})"
            )
            
            # 등급별 풀 크기로 생성
            client = MongoClient(
                self.connection_string,
                maxPoolSize=pool_size,
                minPoolSize=1
            )
            
            self._clients[user_id] = client
            self._last_access[user_id] = time.time()
            
            return client


# 사용
manager = TieredUserConnectionManager(
    connection_string="mongodb://localhost:27017/"
)

# Free tier: 3개 연결
db_free = manager.get_database('user_123')

# Premium tier: 10개 연결
db_premium = manager.get_database('pre_user_456')

# Enterprise tier: 20개 연결
db_enterprise = manager.get_database('ent_user_789')
```

### 4.3 연결 풀 모니터링

```python
"""
연결 풀 상태 모니터링
"""

class MonitoredUserConnectionManager(UserConnectionManager):
    """
    모니터링 기능 추가
    """
    
    def __init__(self, *args, **kwargs):
        super().__init__(*args, **kwargs)
        
        # 메트릭 저장
        self.metrics = {
            'total_connections_created': 0,
            'total_connections_closed': 0,
            'connection_errors': 0,
            'slow_queries': 0
        }
    
    def get_client(self, user_id: str) -> MongoClient:
        """연결 생성 추적"""
        with self._lock:
            if user_id not in self._clients:
                self.metrics['total_connections_created'] += 1
        
        return super().get_client(user_id)
    
    def close_user_connection(self, user_id: str) -> bool:
        """연결 종료 추적"""
        result = super().close_user_connection(user_id)
        
        if result:
            self.metrics['total_connections_closed'] += 1
        
        return result
    
    def get_pool_stats(self, user_id: str) -> dict:
        """
        특정 유저의 연결 풀 통계
        """
        try:
            client = self._clients.get(user_id)
            
            if not client:
                return {'error': 'No connection found'}
            
            # MongoDB 서버 상태 조회
            server_status = client.admin.command('serverStatus')
            
            return {
                'user_id': user_id,
                'connections': server_status.get('connections', {}),
                'pool_size': self.user_pool_size,
                'last_access': self._last_access.get(user_id, 0)
            }
        
        except Exception as e:
            logger.error(f"Failed to get pool stats: {e}")
            return {'error': str(e)}
    
    def get_all_metrics(self) -> dict:
        """전체 메트릭 조회"""
        stats = self.get_stats()
        
        return {
            **stats,
            **self.metrics,
            'avg_connections_per_user': (
                stats['total_potential_connections'] / stats['total_connections']
                if stats['total_connections'] > 0
                else 0
            )
        }
```

---

## 5. 동시성 처리

### 5.1 동시 요청 처리 테스트

```python
"""
동시성 테스트: 단일 연결 vs 독립 연결
"""

import concurrent.futures
import time
from pymongo import MongoClient


# ============= 테스트 1: 단일 연결 =============

def test_single_connection():
    """단일 MongoClient로 여러 유저 처리"""
    client = MongoClient("mongodb://localhost:27017/", maxPoolSize=100)
    
    def process_user(user_id: int):
        db = client[f'user_{user_id}_db']
        start = time.time()
        
        # 시뮬레이션: 1초 걸리는 쿼리
        db.posts.insert_one({'user_id': user_id, 'timestamp': start})
        time.sleep(0.1)  # 쿼리 시뮬레이션
        
        return time.time() - start
    
    # 100명 동시 처리
    start_time = time.time()
    
    with concurrent.futures.ThreadPoolExecutor(max_workers=100) as executor:
        futures = [executor.submit(process_user, i) for i in range(100)]
        results = [f.result() for f in concurrent.futures.as_completed(futures)]
    
    total_time = time.time() - start_time
    
    print(f"\n=== Single Connection ===")
    print(f"Total time: {total_time:.2f}s")
    print(f"Avg per user: {sum(results)/len(results):.2f}s")
    print(f"Max wait: {max(results):.2f}s")
    
    client.close()


# ============= 테스트 2: 독립 연결 =============

def test_independent_connections():
    """유저별 독립 MongoClient"""
    manager = UserConnectionManager(
        connection_string="mongodb://localhost:27017/",
        user_pool_size=10
    )
    
    def process_user(user_id: int):
        db = manager.get_database(f'user_{user_id}')
        start = time.time()
        
        # 시뮬레이션: 1초 걸리는 쿼리
        db.posts.insert_one({'user_id': user_id, 'timestamp': start})
        time.sleep(0.1)
        
        return time.time() - start
    
    # 100명 동시 처리
    start_time = time.time()
    
    with concurrent.futures.ThreadPoolExecutor(max_workers=100) as executor:
        futures = [executor.submit(process_user, i) for i in range(100)]
        results = [f.result() for f in concurrent.futures.as_completed(futures)]
    
    total_time = time.time() - start_time
    
    print(f"\n=== Independent Connections ===")
    print(f"Total time: {total_time:.2f}s")
    print(f"Avg per user: {sum(results)/len(results):.2f}s")
    print(f"Max wait: {max(results):.2f}s")
    
    manager.close_all()


# 실행
if __name__ == "__main__":
    print("Running concurrency tests...")
    
    test_single_connection()
    test_independent_connections()
    
    # 예상 결과:
    # Single Connection - Total time: ~2-3s (병목 발생)
    # Independent Connections - Total time: ~1s (병렬 처리)
```

### 5.2 부하 테스트 시나리오

```python
"""
실전 부하 테스트
"""

import asyncio
import aiohttp
import time


async def load_test(
    base_url: str,
    num_users: int,
    requests_per_user: int
):
    """
    부하 테스트
    
    Args:
        base_url: API 서버 URL
        num_users: 동시 유저 수
        requests_per_user: 유저당 요청 수
    """
    
    async def user_requests(session, user_id):
        """단일 유저의 요청들"""
        headers = {'X-User-ID': f'user_{user_id}'}
        timings = []
        
        for _ in range(requests_per_user):
            start = time.time()
            
            async with session.post(
                f'{base_url}/api/posts',
                json={'title': f'Post from user {user_id}'},
                headers=headers
            ) as response:
                await response.json()
            
            timings.append(time.time() - start)
        
        return timings
    
    # 모든 유저 동시 실행
    start_time = time.time()
    
    async with aiohttp.ClientSession() as session:
        tasks = [
            user_requests(session, user_id)
            for user_id in range(num_users)
        ]
        
        all_timings = await asyncio.gather(*tasks)
    
    total_time = time.time() - start_time
    
    # 통계
    flat_timings = [t for timings in all_timings for t in timings]
    
    print(f"\n=== Load Test Results ===")
    print(f"Total users: {num_users}")
    print(f"Requests per user: {requests_per_user}")
    print(f"Total requests: {len(flat_timings)}")
    print(f"Total time: {total_time:.2f}s")
    print(f"Requests/sec: {len(flat_timings)/total_time:.2f}")
    print(f"Avg response time: {sum(flat_timings)/len(flat_timings):.3f}s")
    print(f"Min response time: {min(flat_timings):.3f}s")
    print(f"Max response time: {max(flat_timings):.3f}s")
    
    # 백분위수
    sorted_timings = sorted(flat_timings)
    p50 = sorted_timings[len(sorted_timings) // 2]
    p95 = sorted_timings[int(len(sorted_timings) * 0.95)]
    p99 = sorted_timings[int(len(sorted_timings) * 0.99)]
    
    print(f"P50: {p50:.3f}s")
    print(f"P95: {p95:.3f}s")
    print(f"P99: {p99:.3f}s")


# 실행
if __name__ == "__main__":
    asyncio.run(load_test(
        base_url="http://localhost:5000",
        num_users=100,
        requests_per_user=10
    ))
```

---

## 6. 성능 최적화

### 6.1 연결 재사용 최대화

```python
"""
연결 재사용 전략
"""

class OptimizedConnectionManager(UserConnectionManager):
    """
    최적화된 연결 관리
    """
    
    def __init__(self, *args, **kwargs):
        # 재사용 카운터
        self.reuse_count = {}
        super().__init__(*args, **kwargs)
    
    def get_client(self, user_id: str) -> MongoClient:
        """재사용 추적"""
        client = super().get_client(user_id)
        
        # 재사용 카운트
        with self._lock:
            if user_id not in self.reuse_count:
                self.reuse_count[user_id] = 0
            else:
                self.reuse_count[user_id] += 1
        
        return client
    
    def get_reuse_stats(self) -> dict:
        """재사용 통계"""
        with self._lock:
            total_reuses = sum(self.reuse_count.values())
            total_connections = len(self.reuse_count)
            
            return {
                'total_connections': total_connections,
                'total_reuses': total_reuses,
                'avg_reuses_per_connection': (
                    total_reuses / total_connections
                    if total_connections > 0
                    else 0
                ),
                'reuse_rate': (
                    total_reuses / (total_reuses + total_connections)
                    if (total_reuses + total_connections) > 0
                    else 0
                )
            }
```

### 6.2 메모리 최적화

```python
"""
메모리 사용 최적화
"""

import sys
import gc


class MemoryEfficientConnectionManager(UserConnectionManager):
    """
    메모리 효율적인 연결 관리
    """
    
    def __init__(
        self,
        connection_string: str,
        max_connections: int = 100,  # 최대 연결 수 제한
        **kwargs
    ):
        self.max_connections = max_connections
        super().__init__(connection_string, **kwargs)
    
    def get_client(self, user_id: str) -> MongoClient:
        """최대 연결 수 제한"""
        with self._lock:
            # 연결 수 제한 체크
            if (user_id not in self._clients and 
                len(self._clients) >= self.max_connections):
                
                # LRU: 가장 오래 사용 안한 연결 제거
                oldest_user = min(
                    self._last_access.items(),
                    key=lambda x: x[1]
                )[0]
                
                logger.info(
                    f"Max connections reached. "
                    f"Closing LRU connection: {oldest_user}"
                )
                
                self.close_user_connection(oldest_user)
                
                # 강제 GC
                gc.collect()
        
        return super().get_client(user_id)
    
    def get_memory_usage(self) -> dict:
        """메모리 사용량 조회"""
        import psutil
        import os
        
        process = psutil.Process(os.getpid())
        mem_info = process.memory_info()
        
        return {
            'rss_mb': mem_info.rss / 1024 / 1024,
            'vms_mb': mem_info.vms / 1024 / 1024,
            'connections': len(self._clients),
            'avg_memory_per_connection': (
                mem_info.rss / len(self._clients) / 1024 / 1024
                if len(self._clients) > 0
                else 0
            )
        }
```

### 6.3 캐싱 전략

```python
"""
쿼리 결과 캐싱
"""

from functools import lru_cache
from datetime import datetime, timedelta


class CachedDatabaseWrapper:
    """
    DB 래퍼 with 캐싱
    """
    
    def __init__(self, db, cache_ttl: int = 300):
        self.db = db
        self.cache_ttl = cache_ttl
        self._cache = {}
        self._cache_times = {}
    
    def find_one_cached(self, collection: str, query: dict):
        """캐시된 find_one"""
        cache_key = f"{collection}:{str(query)}"
        
        # 캐시 확인
        if cache_key in self._cache:
            cache_time = self._cache_times[cache_key]
            if datetime.now() - cache_time < timedelta(seconds=self.cache_ttl):
                return self._cache[cache_key]
        
        # 캐시 미스 - DB 조회
        result = self.db[collection].find_one(query)
        
        # 캐싱
        self._cache[cache_key] = result
        self._cache_times[cache_key] = datetime.now()
        
        return result
    
    def invalidate_cache(self, collection: str = None):
        """캐시 무효화"""
        if collection:
            # 특정 컬렉션만
            keys_to_remove = [
                k for k in self._cache.keys()
                if k.startswith(f"{collection}:")
            ]
            for key in keys_to_remove:
                del self._cache[key]
                del self._cache_times[key]
        else:
            # 전체 캐시
            self._cache.clear()
            self._cache_times.clear()
```

---

## 7. 실전 예제

### 7.1 블로그 플랫폼

```python
"""
유저별 독립 블로그 DB
"""

class BlogPlatform:
    """
    멀티 유저 블로그 플랫폼
    
    각 유저마다 독립 DB 사용
    """
    
    def __init__(self):
        self.connection_manager = UserConnectionManager(
            connection_string="mongodb://localhost:27017/",
            user_pool_size=10,
            idle_timeout=3600
        )
    
    def create_post(self, user_id: str, title: str, content: str):
        """포스트 생성"""
        db = self.connection_manager.get_database(user_id)
        
        post = {
            'title': title,
            'content': content,
            'created_at': datetime.now(),
            'updated_at': datetime.now(),
            'views': 0,
            'likes': 0
        }
        
        result = db.posts.insert_one(post)
        return str(result.inserted_id)
    
    def get_user_posts(self, user_id: str, page: int = 1, page_size: int = 10):
        """유저의 포스트 목록"""
        db = self.connection_manager.get_database(user_id)
        
        skip = (page - 1) * page_size
        
        posts = list(
            db.posts
            .find({}, {'_id': 0})
            .sort('created_at', -1)
            .skip(skip)
            .limit(page_size)
        )
        
        return posts
    
    def increment_views(self, user_id: str, post_id: str):
        """조회수 증가"""
        from bson import ObjectId
        
        db = self.connection_manager.get_database(user_id)
        
        db.posts.update_one(
            {'_id': ObjectId(post_id)},
            {'$inc': {'views': 1}}
        )
    
    def get_stats(self, user_id: str):
        """유저 통계"""
        db = self.connection_manager.get_database(user_id)
        
        return {
            'total_posts': db.posts.count_documents({}),
            'total_views': list(db.posts.aggregate([
                {'$group': {'_id': None, 'total': {'$sum': '$views'}}}
            ]))[0]['total'] if db.posts.count_documents({}) > 0 else 0,
            'total_likes': list(db.posts.aggregate([
                {'$group': {'_id': None, 'total': {'$sum': '$likes'}}}
            ]))[0]['total'] if db.posts.count_documents({}) > 0 else 0
        }


# 사용
blog = BlogPlatform()

# User A
post_id_a = blog.create_post(
    'user_a',
    'First Post',
    'Hello World!'
)

# User B (독립 DB, User A와 간섭 없음)
post_id_b = blog.create_post(
    'user_b',
    'My First Post',
    'Welcome to my blog!'
)

# 통계
stats_a = blog.get_stats('user_a')
print(f"User A stats: {stats_a}")
```

### 7.2 SaaS 애플리케이션

```python
"""
SaaS: 회사별 독립 DB
"""

class SaaSPlatform:
    """
    멀티 테넌트 SaaS 플랫폼
    
    각 회사마다 독립 DB
    """
    
    def __init__(self):
        self.connection_manager = TieredUserConnectionManager(
            connection_string="mongodb://localhost:27017/"
        )
    
    def onboard_company(self, company_id: str, plan: str = 'basic'):
        """회사 온보딩"""
        db = self.connection_manager.get_database(company_id)
        
        # 초기 컬렉션 생성
        db.create_collection('users')
        db.create_collection('projects')
        db.create_collection('tasks')
        
        # 인덱스 생성
        db.users.create_index([('email', 1)], unique=True)
        db.projects.create_index([('name', 1)])
        db.tasks.create_index([('project_id', 1), ('status', 1)])
        
        # 메타데이터
        db._metadata.insert_one({
            'company_id': company_id,
            'plan': plan,
            'onboarded_at': datetime.now(),
            'status': 'active'
        })
        
        logger.info(f"Company {company_id} onboarded with {plan} plan")
    
    def add_user(self, company_id: str, email: str, name: str, role: str):
        """유저 추가"""
        db = self.connection_manager.get_database(company_id)
        
        user = {
            'email': email,
            'name': name,
            'role': role,
            'created_at': datetime.now()
        }
        
        result = db.users.insert_one(user)
        return str(result.inserted_id)
    
    def create_project(self, company_id: str, name: str, description: str):
        """프로젝트 생성"""
        db = self.connection_manager.get_database(company_id)
        
        project = {
            'name': name,
            'description': description,
            'created_at': datetime.now(),
            'status': 'active'
        }
        
        result = db.projects.insert_one(project)
        return str(result.inserted_id)
    
    def get_company_analytics(self, company_id: str):
        """회사 분석 데이터"""
        db = self.connection_manager.get_database(company_id)
        
        return {
            'company_id': company_id,
            'total_users': db.users.count_documents({}),
            'total_projects': db.projects.count_documents({}),
            'total_tasks': db.tasks.count_documents({}),
            'active_projects': db.projects.count_documents({'status': 'active'}),
            'completed_tasks': db.tasks.count_documents({'status': 'completed'})
        }


# 사용
saas = SaaSPlatform()

# Company A 온보딩
saas.onboard_company('company_a', plan='premium')
saas.add_user('company_a', 'alice@company-a.com', 'Alice', 'admin')
saas.create_project('company_a', 'Project Alpha', 'First project')

# Company B 온보딩 (독립 DB)
saas.onboard_company('company_b', plan='enterprise')
saas.add_user('company_b', 'bob@company-b.com', 'Bob', 'admin')

# 분석
analytics_a = saas.get_company_analytics('company_a')
print(f"Company A analytics: {analytics_a}")
```

---

## 8. 요약

### 8.1 핵심 포인트

| 항목 | 단일 연결 | 유저별 연결 |
|------|----------|-------------|
| **구현 복잡도** | ⭐ 낮음 | ⭐⭐⭐ 높음 |
| **동시성** | ⭐⭐ 제한적 | ⭐⭐⭐⭐⭐ 최대 |
| **격리 수준** | ⭐⭐ 낮음 | ⭐⭐⭐⭐⭐ 완벽 |
| **연결 수** | 적음 (100개) | 많음 (유저*10) |
| **메모리 사용** | 적음 | 많음 |
| **확장성** | 제한적 | 무한 |
| **QoS** | 불가능 | 가능 |

### 8.2 의사결정 트리

```
유저별 독립 DB 필요?
└─ YES
    │
    ├─ 동시 접속 < 50 → 단일 연결 + useDb()
    │   └─ 구현 간단, 비용 적음
    │
    ├─ 동시 접속 50-500 → 그룹별 연결
    │   └─ 균형잡힌 접근
    │
    └─ 동시 접속 > 500 → 유저별 독립 연결 ⭐
        └─ 최대 동시성, 완벽한 격리
```

### 8.3 최종 권장사항

#### 소규모 (< 50 동시 접속)
```python
# 단일 연결로 충분
client = MongoClient(uri, maxPoolSize=100)
db = client[f'user_{user_id}_db']
```

#### 중규모 (50-500 동시 접속)
```python
# 그룹별 연결
manager = GroupConnectionManager(groups=10)
db = manager.get_database(user_id)
```

#### 대규모 (> 500 동시 접속)
```python
# 유저별 독립 연결 ⭐
manager = UserConnectionManager(
    connection_string=uri,
    user_pool_size=10,
    idle_timeout=3600
)
db = manager.get_database(user_id)
```

---

## 9. 체크리스트

### 구현 전

- [ ] 동시 접속 유저 수 예측
- [ ] 유저당 평균 요청 수 분석
- [ ] 서버 연결 수 제한 확인
- [ ] 메모리 용량 확인
- [ ] 연결 방식 선택 (단일/그룹/유저별)

### 구현 중

- [ ] UserConnectionManager 구현
- [ ] 연결 풀 크기 설정
- [ ] 유휴 연결 자동 정리 구현
- [ ] 모니터링 시스템 구축
- [ ] 에러 처리 구현
- [ ] 로깅 시스템 구축

### 운영

- [ ] 연결 수 모니터링
- [ ] 메모리 사용량 모니터링
- [ ] 응답 시간 모니터링
- [ ] 동시성 테스트
- [ ] 부하 테스트
- [ ] 장애 대응 계획

---

**이 가이드가 도움이 되셨나요? 실전 경험과 피드백을 환영합니다!**

Copyright (c) 2024 VCANUS. All rights reserved.

