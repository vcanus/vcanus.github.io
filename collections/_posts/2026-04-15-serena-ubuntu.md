# Serena MCP Server 설치 가이드 (Ubuntu)

## 사전 요구사항

- Node.js 18 이상
- Claude Code CLI 설치됨
- `uv` 패키지 매니저

### uv 설치 (없으면)

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
source ~/.bashrc
```

---

## 설치

npm 패키지가 없으므로 GitHub에서 직접 설치합니다.

```bash
uvx --from git+https://github.com/oraios/serena serena --help
```

위 명령으로 정상 동작 확인 후 MCP 등록으로 진행합니다.

---

## Claude Code MCP 등록

```bash
claude mcp add serena -- uvx --from git+https://github.com/oraios/serena serena start-mcp-server
```

---

## 연결 확인

```bash
claude mcp list
```

아래처럼 `✓ Connected` 가 표시되면 성공입니다:

```
serena: uvx --from git+https://github.com/oraios/serena serena start-mcp-server - ✓ Connected
```

---

## 제거

```bash
claude mcp remove serena
```

---

## 참고

- GitHub: https://github.com/oraios/serena
- MCP 서버 시작 커맨드는 `serena start-mcp-server` (단순 `serena` 또는 `serena-mcp-server` 는 동작 안 함)
