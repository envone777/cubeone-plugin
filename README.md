# 큐브원 AI 플러그인 (cubeone-plugin)

큐브원(CubeOne)을 AI(Claude Code, Codex)에 연결하는 플러그인 마켓입니다.
AI가 쓴 네이버 블로그 글을 큐브원 검수를 거쳐 **임시저장 초안**으로 보냅니다.

- 마켓 이름: `cubeone`
- 플러그인 이름: `cubeone-blog` (설치 id `cubeone-blog@cubeone`)
- 이 저장소에는 서버 코드가 없습니다. MCP 서버 주소와 스킬만 담은 설정 묶음입니다. 실제 MCP 서버는 큐브원 웹 앱입니다.
- 비밀 값(토큰, 사용자별 주소)은 들어 있지 않습니다. 사용자 인증은 연결할 때 브라우저 승인(OAuth)으로 합니다.
- 글쓰기 규칙은 서버(`get_writing_guide`)가 줍니다. 이 저장소에는 없습니다.

> **현재 상태:** 공개 서버 주소가 아직 정해지지 않았습니다. 주소는 자리표시자 `https://CUBEONE_HOST.invalid/api/mcp` 입니다(`.invalid`는 실제로 연결되지 않는 예약 도메인). 서버와 OAuth가 배포되면 실제 주소로 바꿉니다.

## 구성

```
.claude-plugin/marketplace.json        # Claude Code 마켓 (Codex도 호환 형식으로 읽음)
.agents/plugins/marketplace.json       # Codex 마켓
plugins/cubeone-blog/
  .claude-plugin/plugin.json           # Claude Code 매니페스트
  plugin.json                          # Codex(이식형) 매니페스트
  .mcp.json                            # Claude Code MCP 설정 (type: http)
  mcp.json                             # Codex MCP 설정 (streamable-http + OAuth)
  skills/cubeone-blog/SKILL.md         # 도구 사용 순서와 규칙
```

## 설정 프롬프트

AI에 아래 프롬프트를 그대로 붙여 넣으세요.

### Codex

```
큐브원 블로그를 연결해 줘.
1. 플러그인을 설치해: `codex plugin marketplace add envone777/cubeone-plugin` 다음 `codex plugin add cubeone-blog@cubeone`
2. 플러그인을 다시 불러오거나, 안 되면 세션을 다시 시작하라고 알려 줘.
3. check_connection 을 호출해. 브라우저에 승인 화면이 열리면 「허용」을 누르라고 안내해 줘.
4. 연결 상태(확장 프로그램 연결, 네이버 로그인)를 보여 줘.
5. 끝나면 끝났다고 말해 줘.
```

### Claude Code

```
큐브원 블로그를 연결해 줘.
1. 플러그인을 설치해: `claude plugin marketplace add envone777/cubeone-plugin` 다음 `claude plugin install cubeone-blog@cubeone`
2. 이 세션에서 `/reload-plugins` 를 입력하라고 알려 줘(안 되면 Claude Code를 다시 시작).
3. check_connection 을 호출해. 브라우저에 승인 화면이 열리면 「허용」을 누르라고 안내해 줘.
4. 연결 상태(확장 프로그램 연결, 네이버 로그인)를 보여 줘.
5. 끝나면 끝났다고 말해 줘.
```

참고
- `codex plugin add` 는 Codex CLI 0.163.0 의 `codex plugin --help` 에 있는 명령입니다. 공식 문서 페이지는 아직 `codex plugin marketplace add` 와 앱 안 `/plugins` 설치만 설명합니다. 명령이 없는 버전이면 Codex에서 `/plugins` 를 열어 `cubeone-blog` 를 설치하세요.
- 저장소가 비공개인 동안에는 `owner/repo` 설치가 저장소 접근 권한이 있는 계정에서만 됩니다.

## 업데이트

- Claude Code: `claude plugin update cubeone-blog@cubeone`
- Codex: `codex plugin marketplace upgrade cubeone`

## 로컬에서 시험하기 (개발자용)

로컬 큐브원 서버(`http://127.0.0.1:3000/api/mcp`)로 시험할 때만 씁니다. 배포되는 기본값은 바꾸지 않습니다.

**Claude Code** — `.mcp.json` 주소는 환경 변수 `CUBEONE_MCP_URL` 로 덮어쓸 수 있습니다(`${VAR:-기본값}` 확장).

```bash
claude plugin marketplace add /path/to/cubeone-plugin
claude plugin install cubeone-blog@cubeone
CUBEONE_MCP_URL=http://127.0.0.1:3000/api/mcp claude
```

**Codex** — `mcp.json` 에는 환경 변수 덮어쓰기가 문서화되어 있지 않습니다. 플러그인은 스킬용으로 설치하고, 로컬 서버는 별도 이름으로 추가합니다.

```bash
codex plugin marketplace add /path/to/cubeone-plugin
codex plugin add cubeone-blog@cubeone
codex mcp add cubeone-dev --url http://127.0.0.1:3000/api/mcp
codex mcp login cubeone-dev
```

주의
- 개발용 사용자별 비밀 MCP 주소(`/api/mcp/<secret>`)는 이 저장소, 이슈, 스크린샷 어디에도 넣지 마세요.
- `localhost` 주소를 기본값으로 커밋하지 마세요.

## 라이선스

정해지지 않았습니다. `LICENSE` 를 보세요.
