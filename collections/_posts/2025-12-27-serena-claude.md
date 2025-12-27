---
layout: post
title: "Serena MCP 및 Claude 연동"
date: 2025-12-27T00:00:00Z
authors: ["SG Lee"]
categories: ["Development"]
description: "Serena MCP 및 Claude 연동"
thumbnail: "/assets/images/gen/blog/blog-5-thumbnail.webp"
image: "/assets/images/gen/blog/blog-5-large.webp"
---

# Serena MCP 연동 가이드

> Claude Code CLI 및 Claude Desktop에서 Serena를 MCP 서버로 연동하여 시맨틱 코드 분석 기능 활용하기

---

## 목차

1. [Serena 개요](#1-serena-개요)
2. [사전 요구사항](#2-사전-요구사항)
3. [Serena 설치](#3-serena-설치)
4. [Claude Code CLI 연동](#4-claude-code-cli-연동)
5. [Claude Desktop 연동](#5-claude-desktop-연동)
6. [설정 옵션 상세](#6-설정-옵션-상세)
7. [사용 예시](#7-사용-예시)
8. [트러블슈팅](#8-트러블슈팅)
9. [참고 자료](#9-참고-자료)

---

## 1. Serena 개요

### Serena란?

Serena는 Language Server 통합을 통해 **시맨틱 코드 이해**와 **지능적 편집 기능**을 제공하는 오픈소스 AI 코딩 에이전트 툴킷입니다.

### 주요 기능

| 기능 | 설명 |
|------|------|
| **시맨틱 코드 분석** | 심볼 수준에서 코드 구조와 관계 이해 |
| **프로젝트 메모리** | `.serena/memories/`에 프로젝트 정보 저장 |
| **토큰 절약** | 전체 파일 대신 필요한 부분만 분석 |
| **다국어 지원** | TypeScript, JavaScript, Python, Java, C# 등 |

### Claude Code에서 Serena가 필요한 이유

일반 AI는 응답 전에 모든 코드를 읽습니다. Serena는 인덱스를 먼저 생성하여 효율적으로 코드를 분석합니다.

```
┌─────────────────────────────────────────────────────────────────┐
│                      일반 AI 분석 방식                          │
│  "button.tsx 수정해줘" → button.tsx 파일만 확인                  │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│                    Serena + AI 분석 방식                        │
│  "button.tsx 수정해줘" → 사용 위치, 스타일 정의, 관련 컴포넌트   │
│                         모두 확인 후 일관성 있게 수정            │
└─────────────────────────────────────────────────────────────────┘
```

---

## 2. 사전 요구사항

### 필수 항목

- [ ] **uv** (Python 패키지 관리자)
- [ ] **Claude Code CLI** 또는 **Claude Desktop**
- [ ] **Git** (로컬 설치 시)

### uv 설치

```bash
# macOS (Homebrew)
brew install uv

# 또는 공식 설치 스크립트
curl -LsSf https://astral.sh/uv/install.sh | sh

# Windows (PowerShell)
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

### 설치 확인

```bash
uv --version
```

---

## 3. Serena 설치

### 방법 A: uvx로 직접 실행 (권장)

별도 설치 없이 바로 사용할 수 있습니다. 대부분의 사용자에게 권장합니다.

```bash
# 별도 설치 불필요, MCP 설정 시 자동 다운로드 및 캐시
uvx --from git+https://github.com/oraios/serena serena-mcp-server
```

**장점:**
- 설치 과정 불필요
- 자동 업데이트 (최신 버전 반영)
- 캐시되어 매번 다운로드하지 않음 (`~/.cache/uv/`)
- 관리 부담 없음

**참고:** Claude Code CLI나 Claude Desktop과 함께 MCP 모드로 사용할 경우, Serena는 도구만 제공하고 LLM 호출은 Claude가 담당합니다. 따라서 별도의 API 키 설정이 필요 없습니다.

### 방법 B: 로컬 설치

Serena를 단독 에이전트(Agno 모드)로 사용하거나, 설정 커스터마이징이 필요한 경우에만 권장합니다.

```bash
# 1. 원하는 위치에 클론
cd ~/workspace
git clone https://github.com/oraios/serena.git
cd serena

# 2. 설정 파일 복사 (선택)
cp src/serena/resources/serena_config.template.yml serena_config.yml

# 3. 환경 변수 설정 (Agno 모드 사용 시에만 필요)
# .env 파일에 API 키 설정
```

**장점:**
- `.env`, 설정 파일 커스터마이징 가능
- Agno 모드로 Serena 단독 에이전트 실행 가능
- 검증된 버전 유지 가능

**언제 필요한가?**
- Serena를 단독 에이전트로 사용할 때 (API 키 필요)
- `serena_config.yml` 커스터마이징이 필요할 때
- 특정 버전을 고정해서 사용해야 할 때

---

## 4. Claude Code CLI 연동

### 방법 A: uvx로 직접 실행 (권장)

```bash
claude mcp add serena --scope user -- uvx --from git+https://github.com/oraios/serena serena start-mcp-server --context=claude-code --project-from-cwd
```

### 방법 B: 로컬 설치 버전 사용

로컬에 Serena를 설치한 경우에만 사용:

```bash
claude mcp add serena --scope user -- uv run --directory ~/workspace/serena serena start-mcp-server --context=claude-code --project-from-cwd
```

### 설정 파일 직접 편집

`~/.claude.json` 파일:

**uvx 직접 실행 (권장):**

```json
{
  "mcpServers": {
    "serena": {
      "command": "uvx",
      "args": [
        "--from",
        "git+https://github.com/oraios/serena",
        "serena",
        "start-mcp-server",
        "--context=claude-code",
        "--project-from-cwd"
      ]
    }
  }
}
```

**로컬 설치 버전:**

```json
{
  "mcpServers": {
    "serena": {
      "command": "uv",
      "args": [
        "run",
        "--directory",
        "/Users/사용자명/workspace/serena",
        "serena",
        "start-mcp-server",
        "--context=claude-code",
        "--project-from-cwd"
      ]
    }
  }
}
```

### 연결 확인

```bash
claude mcp list
```

출력 예시:
```
serena: Scope: User
  Type: stdio
  Command: uv
  Args: run, --directory, /Users/사용자명/workspace/serena, serena, start-mcp-server, --context=claude-code, --project-from-cwd
```

---

## 5. Claude Desktop 연동

### 설정 파일 위치

```
macOS: ~/Library/Application Support/Claude/claude_desktop_config.json
Windows: %APPDATA%\Claude\claude_desktop_config.json
```

### 설정 파일 편집

**uvx 직접 실행 (권장):**

```json
{
  "mcpServers": {
    "serena": {
      "command": "uvx",
      "args": [
        "--from",
        "git+https://github.com/oraios/serena",
        "serena",
        "start-mcp-server"
      ]
    }
  }
}
```

**로컬 설치 버전:**

```json
{
  "mcpServers": {
    "serena": {
      "command": "/Users/사용자명/.local/bin/uv",
      "args": [
        "run",
        "--directory",
        "/Users/사용자명/workspace/serena",
        "serena",
        "start-mcp-server",
        "--context",
        "ide"
      ]
    }
  }
}
```

### uv 경로 확인

Claude Desktop은 쉘 환경을 상속하지 않을 수 있으므로 **절대 경로** 사용 권장:

```bash
which uv
# 예: /Users/사용자명/.local/bin/uv 또는 /opt/homebrew/bin/uv
```

### 재시작

설정 저장 후 **Claude Desktop 완전 종료 후 재시작** 필요

---

## 6. 설정 옵션 상세

### --context 옵션

| 값 | 용도 | 설명 |
|----|------|------|
| `claude-code` | Claude Code CLI | CLI 전용 최적화 |
| `ide` | IDE 통합 (Desktop, JetBrains 등) | 도구 중복 방지 |
| 미지정 | 범용 | 모든 도구 활성화 |

### --project 관련 옵션

| 옵션 | 설명 |
|------|------|
| `--project-from-cwd` | 현재 디렉토리를 프로젝트로 인식 (CLI 권장) |
| `--project /path/to/project` | 특정 경로를 프로젝트로 지정 |

### Scope 옵션 (Claude Code CLI)

| Scope | 저장 위치 | 용도 |
|-------|----------|------|
| `user` | `~/.claude.json` | 모든 프로젝트에서 사용 |
| `project` | 프로젝트/.mcp.json | 해당 프로젝트만 |
| (기본) | 프로젝트/.claude/ | 해당 프로젝트만 |

---

## 7. 사용 예시

### 기본 사용

```bash
cd ~/workspace/my-project
claude
```

Claude에게:
```
이 프로젝트의 구조를 분석해줘
```

Serena가 자동으로:
1. 프로젝트 인덱싱
2. `.serena/memories/`에 프로젝트 정보 저장
3. 시맨틱 분석 결과 제공

### 시맨틱 코드 분석

```
# 심볼 찾기
UserService 클래스의 모든 메서드를 보여줘

# 참조 찾기
login 함수를 호출하는 모든 코드를 찾아줘

# 관계 분석
이 클래스들 간의 의존성을 설명해줘
```

### 리팩토링

```
# 컴포넌트 분리
UserProfile 컴포넌트가 너무 크니 적절히 분리해줘

# 일관성 있는 수정
다크 모드 기능을 추가하고 모든 컴포넌트에 일관되게 적용해줘
```

### 여러 프로젝트 연동 분석

```bash
# workspace 전체를 분석하려면 workspace에서 실행
cd ~/workspace
claude

# 특정 프로젝트만 분석하려면 해당 폴더에서 실행
cd ~/workspace/vpy-util
claude
```

---

## 8. 트러블슈팅

### MCP 서버 연결 실패

**확인 사항:**
```bash
# uv 설치 확인
uv --version

# 로컬 설치 경로 확인
ls ~/workspace/serena

# MCP 목록 확인
claude mcp list
```

**해결:**
```bash
# MCP 제거 후 재추가
claude mcp remove serena
claude mcp add serena --scope user -- uvx --from git+https://github.com/oraios/serena serena start-mcp-server --context=claude-code --project-from-cwd
```

### Claude Desktop에서 Serena 인식 안 됨

**원인:** 환경 변수 미상속

**해결:** 설정 파일에서 uv 절대 경로 사용

```json
{
  "mcpServers": {
    "serena": {
      "command": "/opt/homebrew/bin/uv",
      "args": ["run", "--directory", "/Users/사용자명/workspace/serena", "serena", "start-mcp-server"]
    }
  }
}
```

### Language Server 관련 오류

일부 언어 서버는 추가 환경 변수가 필요할 수 있습니다:

```json
{
  "mcpServers": {
    "serena": {
      "command": "uv",
      "args": ["run", "--directory", "/Users/사용자명/workspace/serena", "serena", "start-mcp-server"],
      "env": {
        "DOTNET_ROOT": "/opt/homebrew/Cellar/dotnet/9.0.8/libexec"
      }
    }
  }
}
```

### 로컬 버전 업데이트

```bash
cd ~/workspace/serena
git pull
```

---

## 9. 참고 자료

### 공식 문서

- [Serena GitHub Repository](https://github.com/oraios/serena)
- [Serena Documentation](https://oraios.github.io/serena/)
- [Model Context Protocol](https://modelcontextprotocol.io/)

### 설정 파일 위치 요약

| 앱 | 설정 파일 위치 |
|----|---------------|
| Claude Code CLI | `~/.claude.json` |
| Claude Desktop (macOS) | `~/Library/Application Support/Claude/claude_desktop_config.json` |
| Claude Desktop (Windows) | `%APPDATA%\Claude\claude_desktop_config.json` |

### JetBrains MCP와 함께 사용

Serena와 JetBrains MCP를 함께 사용하면 더욱 강력합니다:

```json
{
  "mcpServers": {
    "jetbrains": {
      "command": "npx",
      "args": ["-y", "@jetbrains/mcp-proxy"]
    },
    "serena": {
      "command": "uvx",
      "args": [
        "--from",
        "git+https://github.com/oraios/serena",
        "serena",
        "start-mcp-server",
        "--context=claude-code",
        "--project-from-cwd"
      ]
    }
  }
}
```

| MCP 서버 | 역할 |
|----------|------|
| **JetBrains** | IDE 제어 (실행, 리팩토링, 디버깅) |
| **Serena** | 시맨틱 코드 분석, 심볼 탐색, 프로젝트 이해 |

---

## 부록: 빠른 시작 체크리스트

```bash
# 1. uv 설치 확인
uv --version

# 2. Claude Code CLI에 MCP 추가 (uvx 방식)
claude mcp add serena --scope user -- uvx --from git+https://github.com/oraios/serena serena start-mcp-server --context=claude-code --project-from-cwd

# 3. 확인
claude mcp list

# 4. 테스트
cd ~/workspace/my-project
claude
# → "이 프로젝트 구조를 분석해줘"
```

---

*문서 작성일: 2025년 12월*
*Serena MCP 연동 가이드 v1.0*
