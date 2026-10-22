# 변경 기록

형식은 [Keep a Changelog](https://keepachangelog.com/ko/1.1.0/), 버전은 [SemVer](https://semver.org/lang/ko/)를 따릅니다.
두 매니페스트(`.claude-plugin/plugin.json`, `plugin.json`)의 `version` 은 항상 같게 유지합니다.

## [0.1.0] - 2026-10-22

### 추가
- 마켓 `cubeone` (Claude Code `.claude-plugin/marketplace.json`, Codex `.agents/plugins/marketplace.json`)
- 플러그인 `cubeone-blog`: Claude Code 매니페스트와 Codex 이식형 매니페스트
- MCP 설정: Claude `.mcp.json`(`type: http`, `CUBEONE_MCP_URL` 로 덮어쓰기 가능), Codex `mcp.json`(`streamable-http` + OAuth CIMD)
- 스킬 `cubeone-blog` (한국어)
- MCP 주소는 자리표시자 `https://CUBEONE_HOST.invalid/api/mcp` (서버 배포 전)
