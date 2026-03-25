# Officemail Plugin

AI 에이전트가 Officemail 서비스의 이메일과 캘린더를 읽고, 보내고, 관리할 수 있는 Claude Code 플러그인이자 MCP 서버입니다.
Officemail(Cyrus IMAP + Postfix 기반) 전용이며, 다른 이메일 서비스나 JMAP 서버에서는 동작하지 않습니다.

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

1. [릴리즈 페이지](https://github.com/ni-kiyong/officemail-plugin/releases)에서
   플랫폼에 맞는 `.mcpb` 파일을 다운로드합니다 (`officemail-{platform}.mcpb`)
2. 더블클릭하면 바이너리와 MCP 서버 설정이 자동으로 설치됩니다
3. 터미널에서 인증을 설정합니다:

    ```bash
    omail auth login --email you@company.com
    ```

4. Claude Desktop을 재시작하면 도구(tools)를 사용할 수 있습니다

## 업데이트

### Claude Code (CLI)

```bash
claude plugin update officemail
```

### Claude Code 내부

```text
claude plugin update officemail@officemail
```

또는 `/plugin` → Marketplaces 탭에서 업데이트할 수 있습니다.
업데이트 후 세션을 종료하고 다시 시작해야 변경 사항이 적용됩니다.
실행파일(`omail`)은 새 세션 시작 시 훅이 자동으로 업데이트합니다.

### Claude Desktop

[릴리즈 페이지](https://github.com/ni-kiyong/officemail-plugin/releases)에서
최신 `.mcpb` 파일을 다운로드하여 더블클릭하면 덮어쓰기 설치됩니다.

## 인증

인증 정보는 `~/.config/officemail/config.json`에 저장됩니다 (chmod 600).
Claude Code 플러그인, Claude Desktop MCP 서버, CLI 모두 같은 파일을 공유하므로
한 곳에서 인증하면 어디서든 사용할 수 있습니다.

```bash
omail auth login --email you@company.com   # OAuth 로그인 (브라우저 열림)
omail auth setup                           # 또는 수동 설정 (JMAP URL + 토큰)
omail doctor                               # 연결 확인
```

## 주요 기능

- **메일** — 읽기, 보내기, 답장, 전달, 검색, 분류, 플래그, 초안, 실시간 감시
- **캘린더** — 일정 CRUD, 반복 일정, 알림, 온라인 회의, 종일 일정,
  참석자 관리, RSVP, 캘린더 CRUD, 공유, 크로스 계정 복사, iCalendar 파싱

## 스킬

| 스킬 | 설명 |
|------|------|
| `omail` | 개요, 글로벌 플래그, 종료 코드, 보안 규칙, 스키마 |
| `omail-setup` | 인증 (OAuth/수동), 연결 진단 (doctor) |
| `omail-mcp` | MCP 서버 설정, 도구 목록, Claude Desktop 연동 |
| `omail-mail` | 메일 전체: 보내기, 답장, 분류, 읽기, 검색, 이동, 플래그, 초안, 감시 |
| `omail-calendar` | 캘린더 전체: 일정 CRUD, 반복, 알림, RSVP, 공유, 파싱 |

## 프롬프트 예시

Claude Code에서 자연어로 사용할 수 있습니다:

### 메일

- "안 읽은 메일 요약해줘"
- "오늘 온 메일 중 중요한 것만 알려줘"
- "`someone@example.com`에게 회의 일정 확인 메일 보내줘"
- "이 메일에 답장해줘: 참석하겠습니다"
- "지난주 예산 관련 메일 찾아줘"
- "새 메일이 오면 텔레그램으로 알려줘" (`+watch` 사용)

### 캘린더

- "이번 주 일정 알려줘"
- "내일 오후 2시에 팀 회의 잡아줘"
- "다음 주 월요일 비어있는 시간 알려줘"
- "반복 회의를 매주 금요일로 변경해줘"
- "다음 회의 초대에 수락으로 응답해줘"

### 설정

- "Officemail 로그인해줘"
- "연결 상태 확인해줘" (`doctor`)

## 구성

- **Skills** — 5개 도메인별 AI 에이전트 지시 파일
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
