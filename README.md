# 큐브원 AI 플러그인 (cubeone-plugin)

큐브원(CubeOne)을 AI 앱(ChatGPT 데스크톱 앱의 Codex, Claude 데스크톱 앱·Claude Code)에 연결하는 플러그인입니다.
AI 채팅에서 네이버 블로그 글을 쓰면 큐브원 검수를 거쳐 **임시저장 초안**으로 보냅니다.

- 마켓 이름 `cubeone`, 플러그인 이름 `cubeone` (설치 id `cubeone@cubeone`)
- 들어 있는 것: MCP 서버 `cubeone` 주소와 사용 스킬 하나. 서버 코드·비밀 값(토큰, 사용자별 주소)은 없습니다.
- 사용자 인증은 처음 쓸 때 브라우저 승인(OAuth)으로 합니다. 큐브원 확장이 설치된 크롬에서 「허용」을 누르면 됩니다.
- 글쓰기 규칙의 원본은 서버(`get_writing_guide`)입니다.

> **MCP 주소:** 지금은 베타 주소 `https://insurance-portal-git-feat-n-84335b-bizmaster0111-5246s-projects.vercel.app/api/mcp` 입니다.
> 정식 출시 때 `https://cube1.kr/api/mcp` 로 바꾸고 버전을 올립니다 (`plugins/cubeone/.mcp.json`, `plugins/cubeone/mcp.json`).

## 설치

ChatGPT 데스크톱 앱(Codex)

```bash
codex plugin marketplace add envone777/cubeone-plugin
codex plugin add cubeone@cubeone
```

Claude 데스크톱 앱 · Claude Code

```bash
claude plugin marketplace add envone777/cubeone-plugin
claude plugin install cubeone@cubeone
```

설치한 뒤 플러그인을 다시 불러오거나(Claude Code `/reload-plugins`) 새 대화를 열고 "큐브원 연결 확인해 줘"라고 말하세요.
실제 고객용 설정 문장은 큐브원 웹의 「AI 연결」 화면에서 복사합니다.

## 구성

```
.claude-plugin/marketplace.json        # Claude Code 마켓 (Codex도 읽음)
.agents/plugins/marketplace.json       # Codex 마켓
plugins/cubeone/
  .codex-plugin/plugin.json            # Codex 매니페스트 (skills, mcpServers)
  .claude-plugin/plugin.json           # Claude Code 매니페스트
  plugin.json                          # 이식형 매니페스트 (agent-plugins.org)
  .mcp.json                            # MCP 서버 (type: http) — Claude Code·Codex 공통
  mcp.json                             # 이식형 MCP 설정 (streamable-http + OAuth)
  skills/cubeone/SKILL.md              # 사용 순서와 말투
```

## 업데이트

- Claude Code: `claude plugin update cubeone@cubeone`
- Codex: `codex plugin marketplace upgrade cubeone`

## 개발자용

- 매니페스트 4개(`.codex-plugin`, `.claude-plugin`, `plugin.json`, 마켓 2개)의 이름·버전·주소를 항상 같게 유지합니다.
- 로컬 서버로 시험할 때는 플러그인 주소를 바꾸지 말고 별도 이름으로 추가합니다: `codex mcp add cubeone-dev --url http://127.0.0.1:3000/api/mcp` 또는 `claude mcp add --transport http cubeone-dev http://127.0.0.1:3000/api/mcp`.
- 사용자별 비밀 주소(`/api/mcp/<secret>`), 토큰, 네이버 아이디는 이 저장소·이슈·스크린샷 어디에도 넣지 마세요. 이 저장소는 공개입니다.

---

## English

CubeOne plugin for Codex (ChatGPT desktop app) and Claude Code / Claude desktop. It bundles the `cubeone` MCP server (OAuth, no secrets) and one short skill; it writes Naver blog posts from the AI chat and sends them to CubeOne, which saves them as **drafts** (never published).

```bash
codex plugin marketplace add envone777/cubeone-plugin && codex plugin add cubeone@cubeone
claude plugin marketplace add envone777/cubeone-plugin && claude plugin install cubeone@cubeone
```

The MCP URL is currently the beta deployment; at launch it moves to `https://cube1.kr/api/mcp`. All rights reserved (see `LICENSE`).
