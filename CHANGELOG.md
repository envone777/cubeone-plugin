# 변경 기록

형식은 [Keep a Changelog](https://keepachangelog.com/ko/1.1.0/), 버전은 [SemVer](https://semver.org/lang/ko/)를 따릅니다.
매니페스트(`.codex-plugin/plugin.json`, `.claude-plugin/plugin.json`, `plugin.json`)의 `version` 은 항상 같게 유지합니다.

## [0.2.0] - 2026-11-24

### 바뀜
- 플러그인 이름 `cubeone-blog` → `cubeone` (설치 id `cubeone@cubeone`), 스킬 이름도 `cubeone`
- MCP 주소: 자리표시자 → 베타 `https://insurance-portal-git-feat-n-84335b-bizmaster0111-5246s-projects.vercel.app/api/mcp` (출시 때 `https://cube1.kr/api/mcp`)
- `.mcp.json` 의 `CUBEONE_MCP_URL` 환경 변수 덮어쓰기 제거 (Codex도 같은 파일을 읽음)
- 스킬을 짧게: 쉬운 말, `get_writing_guide` 먼저, 글감 다섯 개 + 6번 직접 입력, 보낸 글 관리는 채팅에서, AI 앱 자체 예약 기능 금지
- 라이선스: All rights reserved (공개 저장소)

### 추가
- Codex 매니페스트 `.codex-plugin/plugin.json`

## [0.1.0] - 2026-10-22

### 추가
- 마켓 `cubeone`, 플러그인 `cubeone-blog`, 스킬 `cubeone-blog`
- MCP 주소는 자리표시자 `https://CUBEONE_HOST.invalid/api/mcp` (서버 배포 전)
