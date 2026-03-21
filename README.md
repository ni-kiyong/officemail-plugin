# Officemail Plugin

AI 에이전트가 이메일을 읽고, 보내고, 관리할 수 있는 Claude Code 플러그인이자 MCP 서버입니다.

## 설치

### Claude Code (CLI)

```bash
claude plugin add ni-kiyong/officemail-plugin
```

### Claude Code 내부

```text
/plugin marketplace add ni-kiyong/officemail-plugin
/plugin install officemail@officemail
```

설치 후 설정 스킬을 실행하세요:

```text
/officemail:omail-setup
```

### Claude Desktop

Claude Desktop에서 MCP 서버로 사용할 수 있습니다.

1. `omail` 바이너리를 설치합니다:

```bash
curl -L -o omail https://github.com/ni-kiyong/officemail-plugin/releases/latest/download/omail-darwin-arm64
chmod +x omail
sudo mv omail /usr/local/bin/
```

2. 인증을 설정합니다:

```bash
omail auth setup
```

3. `claude_desktop_config.json`에 MCP 서버를 추가합니다:

```json
{
  "mcpServers": {
    "officemail": {
      "command": "omail",
      "args": ["mcp"]
    }
  }
}
```

Claude Desktop을 재시작하면 11개 도구(tools), 1개 리소스(resource),
2개 프롬프트(prompts)를 사용할 수 있습니다.

## 구성

- **Skills** — 이메일 관리를 위한 AI 에이전트 지시 파일
- **Hooks** — 첫 세션 시작 시 `omail` 실행파일 자동 설치
- **실행파일** — macOS, Linux, Windows (arm64, x64) 6개 플랫폼 빌드 제공

실행파일은 [릴리즈 페이지](https://github.com/ni-kiyong/officemail-plugin/releases)에서
다운로드할 수 있으며, 플러그인 설치 시 자동으로 다운로드됩니다.

## 수동 설치

```bash
curl -L -o omail https://github.com/ni-kiyong/officemail-plugin/releases/latest/download/omail-darwin-arm64
chmod +x omail
sudo mv omail /usr/local/bin/
```