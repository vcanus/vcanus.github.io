---
layout: post
title: "Claude CLI 설치 및 MCP 서버 설정"
date: 2025-12-27T00:00:00Z
authors: ["SG Lee"]
categories: ["Development"]
description: "Claude CLI 설치 가이드"
thumbnail: "/assets/images/gen/blog/blog-5-thumbnail.webp"
image: "/assets/images/gen/blog/blog-5-large.webp"
---

# Claude Code CLI + JetBrains IDE 연동 가이드

> Claude Max 구독을 활용하여 JetBrains IDE(IntelliJ, PyCharm 등)를 제어하는 완벽 가이드

---

## 목차

1. [개요](#1-개요)
2. [사전 요구사항](#2-사전-요구사항)
3. [Claude Code CLI 설치](#3-claude-code-cli-설치)
4. [JetBrains MCP 서버 활성화](#4-jetbrains-mcp-서버-활성화)
5. [Claude Code CLI와 JetBrains 연결](#5-claude-code-cli와-jetbrains-연결)
6. [연결 확인 및 테스트](#6-연결-확인-및-테스트)
7. [실제 사용 예시](#7-실제-사용-예시)
8. [추가 MCP 서버 설정 (선택)](#8-추가-mcp-서버-설정-선택)
9. [트러블슈팅](#9-트러블슈팅)
10. [참고 자료](#10-참고-자료)

---

## 1. 개요

### 아키텍처

```
┌─────────────────────────────────────────────────────────────────┐
│                     Claude Code CLI                             │
│                   (MCP 클라이언트 역할)                          │
│                   Claude Max 구독 사용                           │
└─────────────────────────────────────────────────────────────────┘
                              │
                              │ MCP 프로토콜
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                  JetBrains MCP Server                           │
│                   (MCP 서버 역할)                                │
│         PyCharm, IntelliJ IDEA, WebStorm 등 내장                │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                     IDE 기능 제어                                │
│  파일 편집, 리팩토링, 테스트 실행, 디버깅, Run Configuration 등  │
└─────────────────────────────────────────────────────────────────┘
```

### 이 조합의 장점

| 항목 | 장점 |
|------|------|
| **비용 효율** | Claude Max 구독 직접 사용 (JetBrains AI 별도 비용 없음) |
| **모델 선택** | Claude Opus, Sonnet 등 원하는 모델 선택 가능 |
| **IDE 완전 제어** | 터미널에서 IDE의 모든 기능 사용 가능 |
| **터미널 친화적** | 개발 워크플로우에 자연스럽게 통합 |

---

## 2. 사전 요구사항

### 필수 항목

- [ ] **Claude Max 구독** (또는 Claude Pro / API 키)
- [ ] **Node.js 18+** 설치
- [ ] **JetBrains IDE** 2025.2 버전 이상
  - IntelliJ IDEA
  - PyCharm
  - WebStorm
  - GoLand
  - 기타 IntelliJ 기반 IDE

### Node.js 설치 확인

```bash
node --version
# v18.0.0 이상이어야 함

npm --version
```

Node.js가 없다면:

```bash
# macOS (Homebrew)
brew install node

# Ubuntu/Debian
sudo apt-get install nodejs npm

# Windows (Chocolatey)
choco install nodejs
```

---

## 3. Claude Code CLI 설치

### 3.1 전역 설치

```bash
npm install -g @anthropic-ai/claude-code
```

### 3.2 설치 확인

```bash
which claude
claude --version
```

### 3.3 첫 실행 및 인증

```bash
# 프로젝트 디렉토리로 이동
cd ~/your-project

# Claude Code 실행
claude
```

첫 실행 시 브라우저가 열리며 Claude 계정 인증을 요청합니다. Claude Max 계정으로 로그인하면 구독이 자동으로 연결됩니다.

### 3.4 인증 상태 확인

```bash
claude /status
```

---

## 4. JetBrains MCP 서버 활성화

JetBrains IDE 2025.2 버전부터 MCP 서버가 내장되어 있습니다.

### 4.1 IDE에서 MCP 서버 활성화

1. JetBrains IDE 실행 (PyCharm, IntelliJ 등)
2. **Settings/Preferences** 열기
   - macOS: `Cmd + ,`
   - Windows/Linux: `Ctrl + Alt + S`
3. **Tools → MCP Server** 이동
4. **Enable MCP Server** 체크박스 활성화
5. **Apply** 클릭

### 4.2 자동 설정 (권장)

Settings → Tools → MCP Server 화면에서:

1. **Clients Auto-Configuration** 섹션 확인
2. **Claude Code** 옆의 **Auto-Configure** 버튼 클릭
3. 자동으로 Claude Code의 설정 파일이 업데이트됨

### 4.3 Brave Mode 설정 (선택)

매번 확인 없이 명령을 실행하려면:

1. Settings → Tools → MCP Server
2. **Command execution** 섹션에서
3. **Run shell commands or run configurations without confirmation (brave mode)** 활성화
4. **Apply** 클릭

> ⚠️ **주의**: Brave Mode는 편리하지만, Claude가 확인 없이 명령을 실행할 수 있으므로 신중하게 사용하세요.

---

## 5. Claude Code CLI와 JetBrains 연결

### 5.1 MCP 서버 추가 (CLI 방식)

```bash
claude mcp add jetbrains -- npx -y @jetbrains/mcp-proxy
```

### 5.2 User Scope로 추가 (모든 프로젝트에서 사용)

```bash
claude mcp add jetbrains --scope user -- npx -y @jetbrains/mcp-proxy
```

### 5.3 설정 파일 직접 편집 (대안)

`~/.claude.json` 파일을 직접 편집:

```json
{
  "mcpServers": {
    "jetbrains": {
      "command": "npx",
      "args": ["-y", "@jetbrains/mcp-proxy"]
    }
  }
}
```

### 5.4 특정 IDE 포트 지정 (여러 IDE 사용 시)

여러 JetBrains IDE를 동시에 사용하는 경우:

```json
{
  "mcpServers": {
    "pycharm": {
      "command": "npx",
      "args": ["-y", "@jetbrains/mcp-proxy"],
      "env": {
        "IDE_PORT": "63342"
      }
    },
    "intellij": {
      "command": "npx",
      "args": ["-y", "@jetbrains/mcp-proxy"],
      "env": {
        "IDE_PORT": "63343"
      }
    }
  }
}
```

IDE 포트 확인: Settings → Build, Execution, Deployment → Debugger → Built-in Server Port

---

## 6. 연결 확인 및 테스트

### 6.1 MCP 서버 목록 확인

```bash
claude mcp list
```

출력 예시:
```
jetbrains: Scope: User
  Type: stdio
  Command: npx
  Args: -y, @jetbrains/mcp-proxy
```

### 6.2 연결 테스트

1. **JetBrains IDE가 실행 중인지 확인**
2. 프로젝트 디렉토리에서 Claude Code 실행:

```bash
cd ~/your-project
claude
```

3. Claude에게 테스트 명령:

```
현재 IDE에서 열린 파일 목록을 보여줘
```

### 6.3 IDE 내 터미널에서 연결 (대안)

JetBrains IDE의 내장 터미널에서:

```bash
claude
```

터미널에서 `/ide` 명령으로 IDE와 연결:

```
/ide
```

---

## 7. 실제 사용 예시

### 7.1 파일 작업

```
# 파일 읽기
현재 열린 파일 내용을 보여줘

# 파일 수정
ByteConv 클래스의 docstring을 업데이트해줘

# 새 파일 생성
test_singleton.py 테스트 파일을 생성해줘
```

### 7.2 코드 실행 및 테스트

```
# 테스트 실행
PyCharm에서 test_byte_conv.py 실행해줘

# 특정 테스트 메서드 실행
TestByteConvSingle 클래스의 test_int_conversion 테스트만 실행해줘

# Run Configuration 실행
'Main' Run Configuration을 실행해줘
```

### 7.3 리팩토링

```
# 리팩토링 제안
이 클래스를 리팩토링하고 diff로 보여줘

# 변수명 변경
`data` 변수를 `byte_data`로 이름 변경해줘

# 메서드 추출
이 코드 블록을 별도 메서드로 추출해줘
```

### 7.4 디버깅 및 분석

```
# 린트 에러 확인
현재 파일의 lint 에러를 수정해줘

# 프로젝트 구조 분석
이 프로젝트의 구조를 설명해줘

# 의존성 확인
이 모듈의 의존성을 분석해줘
```

### 7.5 Git 작업

```
# 변경사항 확인
Git 변경사항을 요약해줘

# 커밋 메시지 생성
현재 변경사항에 대한 커밋 메시지를 작성해줘
```

---

## 8. 추가 MCP 서버 설정 (선택)

### 8.1 GitHub 연동

```bash
# 환경변수 설정 (.zshrc 또는 .bashrc에 추가)
export GITHUB_TOKEN=ghp_your_token_here

# MCP 서버 추가
claude mcp add github --scope user -- npx -y @modelcontextprotocol/server-github
```

### 8.2 Filesystem 접근 확장

```bash
claude mcp add filesystem --scope user -- npx -y @modelcontextprotocol/server-filesystem ~/projects
```

### 8.3 Memory (대화 기억)

```bash
claude mcp add memory --scope user -- npx -y @modelcontextprotocol/server-memory
```

### 8.4 전체 설정 예시 (~/.claude.json)

```json
{
  "mcpServers": {
    "jetbrains": {
      "command": "npx",
      "args": ["-y", "@jetbrains/mcp-proxy"]
    },
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "ghp_your_token_here"
      }
    },
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/Users/username/projects"]
    },
    "memory": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-memory"]
    }
  }
}
```

---

## 9. 트러블슈팅

### 9.1 "Claude Code not found" 오류

**원인**: Claude Code CLI가 PATH에 없음

**해결**:
```bash
# npm 전역 경로 확인
npm config get prefix

# PATH에 추가 (.zshrc 또는 .bashrc)
export PATH="$PATH:$(npm config get prefix)/bin"

# 쉘 재시작
source ~/.zshrc
```

### 9.2 JetBrains MCP 서버 연결 실패

**확인 사항**:
1. JetBrains IDE가 실행 중인지 확인
2. MCP Server가 활성화되어 있는지 확인 (Settings → Tools → MCP Server)
3. IDE를 재시작

**포트 충돌 시**:
```json
{
  "mcpServers": {
    "jetbrains": {
      "command": "npx",
      "args": ["-y", "@jetbrains/mcp-proxy"],
      "env": {
        "IDE_PORT": "63342",
        "HOST": "127.0.0.1"
      }
    }
  }
}
```

### 9.3 Node.js 버전 문제

**오류**: MCP Proxy가 작동하지 않음

**해결**:
```bash
# Node.js 버전 확인
node --version

# 18 미만이면 업그레이드
brew upgrade node
# 또는
nvm install 18
nvm use 18
```

### 9.4 WSL 환경 설정

WSL에서 사용 시 추가 설정:

```json
{
  "mcpServers": {
    "jetbrains": {
      "command": "npx",
      "args": ["-y", "@jetbrains/mcp-proxy"],
      "env": {
        "IDE_PORT": "63342",
        "HOST": "호스트_Windows_IP"
      }
    }
  }
}
```

Windows IP 확인:
```bash
cat /etc/resolv.conf | grep nameserver | awk '{print $2}'
```

### 9.5 MCP 서버 제거 및 재설정

```bash
# 서버 제거
claude mcp remove jetbrains

# 다시 추가
claude mcp add jetbrains --scope user -- npx -y @jetbrains/mcp-proxy

# 확인
claude mcp list
```

---

## 10. 참고 자료

### 공식 문서

- [Claude Code 공식 문서](https://docs.anthropic.com/claude-code)
- [JetBrains MCP Server 문서](https://www.jetbrains.com/help/idea/mcp-server.html)
- [Model Context Protocol 공식 사이트](https://modelcontextprotocol.io/)

### MCP 서버 디렉토리

- [MCP.so](https://mcp.so/) - MCP 서버 검색
- [Smithery.ai](https://smithery.ai/) - MCP 서버 디렉토리
- [GitHub MCP Servers](https://github.com/modelcontextprotocol/servers) - 공식 MCP 서버 레포

### 관련 설정 파일 위치

| 파일 | 위치 | 용도 |
|------|------|------|
| Claude Code CLI 설정 | `~/.claude.json` | CLI의 MCP 서버 설정 |
| 프로젝트별 MCP 설정 | `프로젝트/.mcp.json` | 프로젝트 특화 MCP 설정 |
| Claude Desktop 설정 | `~/Library/Application Support/Claude/claude_desktop_config.json` | Desktop 앱 MCP 설정 (별개) |

---

## 부록: 빠른 시작 체크리스트

```bash
# 1. Node.js 확인
node --version  # 18+ 필요

# 2. Claude Code CLI 설치
npm install -g @anthropic-ai/claude-code

# 3. 설치 확인
claude --version

# 4. JetBrains IDE에서 MCP 서버 활성화
# Settings → Tools → MCP Server → Enable MCP Server ✓

# 5. Claude Code에 JetBrains 연결
claude mcp add jetbrains --scope user -- npx -y @jetbrains/mcp-proxy

# 6. 연결 확인
claude mcp list

# 7. 테스트 (IDE 실행 상태에서)
cd ~/your-project
claude
# → "현재 IDE에서 열린 파일을 보여줘"
```

---

*문서 작성일: 2025년 12월*
*Claude Code CLI + JetBrains MCP 연동 가이드 v1.0*

