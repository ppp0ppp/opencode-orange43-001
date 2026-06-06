# Bootstrap And Installation Guide

작성일: 2026-06-06

## 목적

이 문서는 이 opencode 기본 설정 템플릿을 다른 OS나 개발 환경으로 옮길 때 필요한 초기 설정, 설치, 검증 절차를 기록합니다.

## 구성 파일

- `opencode.json`: 로컬 opencode 설정. 프로젝트 루트에서 우선 적용됩니다.
- `AGENTS.md`: opencode가 읽는 공통 지시문입니다.
- `.opencode/skills/`: 프로젝트 로컬 skill입니다.
- `.opencode/plugins/`: 프로젝트 로컬 plugin입니다.
- `.opencode-context/`: 장기 맥락, 보고서, 결정, 세션, 계약 문서입니다.

## 기본 요구사항

- opencode CLI
- Git
- Python 3.10 이상
- `uv` 또는 `pipx`
- graphify CLI 패키지 `graphifyy`

현재 확인된 graphify CLI 버전은 `0.8.32`입니다.

## 새 환경 설치 순서

1. 저장소를 clone합니다.
2. 프로젝트 루트에서 opencode를 실행합니다.
3. 필요한 provider 인증을 진행합니다.
4. graphify CLI를 설치합니다.
5. opencode를 재시작합니다.
6. `opencode.json`이 로드되는지 확인합니다.

## graphify CLI 설치

권장 설치 방식은 `uv`입니다.

```bash
uv tool install graphifyy
graphify --version
```

대안으로 `pipx`를 사용할 수 있습니다.

```bash
pipx install graphifyy
graphify --version
```

`graphify` 명령이 PATH에 없으면 `~/.local/bin` 또는 OS별 Python script 경로가 PATH에 포함되어 있는지 확인합니다.

## graphify 프로젝트 통합 상태

현재 템플릿에는 다음이 포함되어 있습니다.

- `.opencode/skills/graphify/SKILL.md`
- `.opencode/skills/graphify/references/`
- `.opencode/plugins/graphify.js`
- `opencode.json`의 `plugin: [".opencode/plugins/graphify.js"]`
- `AGENTS.md`의 graphify 사용 지침

다시 생성해야 할 때만 아래 명령을 실행합니다.

```bash
graphify install --project --platform opencode
```

이 명령은 `AGENTS.md`, `.opencode/skills/graphify/`, `.opencode/plugins/graphify.js`, `.opencode/opencode.json`을 수정할 수 있습니다. 이 템플릿에서는 plugin 등록을 루트 `opencode.json`으로 통합했으므로, 명령 실행 후 `.opencode/opencode.json`이 생기면 내용을 확인하고 중복 설정을 정리합니다.

## graphify 산출물 정책

`graphify-out/`은 로컬 산출물이며 커밋하지 않습니다.

`.gitignore`는 다음을 포함합니다.

```gitignore
graphify-out/
```

그래프를 생성하려면 다음 중 하나를 사용합니다.

```bash
graphify .
```

또는 opencode에서:

```text
/graphify .
```

`graphify-out/graph.json`이 존재하면 코드베이스 질문에서 `graphify query`, `graphify path`, `graphify explain`을 우선 사용합니다.

## Hook And MCP Policy

git hook과 MCP 서버는 기본 활성화하지 않습니다.

활성화 전에 확인할 항목은 다음입니다.

- 어떤 hook이 설치되는지
- 커밋/체크아웃/병합 시 어떤 명령이 실행되는지
- 외부 API 호출 여부
- query log 경로
- 생성물이 어디에 저장되는지

명시적으로 활성화할 때만 아래 명령을 사용합니다.

```bash
graphify hook install
```

필요 없으면 제거합니다.

```bash
graphify hook uninstall
```

## Skills

현재 로컬 skill은 다음입니다.

- `git`: Conventional Commits와 브랜치/병합 흐름
- `git-worktree`: worktree 기반 환경 분리
- `tidy-tdd-first`: TDD와 Tidy First 개발 흐름
- `graphify`: knowledge graph 생성과 query/path/explain 사용

새 skill은 아래 구조로 추가합니다.

```text
.opencode/skills/<skill-name>/SKILL.md
```

`SKILL.md`에는 최소한 `name`과 `description` frontmatter를 둡니다.

## Plugins

현재 로컬 plugin은 다음입니다.

- `.opencode/plugins/graphify.js`

새 plugin은 추가 전에 출처, 라이선스, hook 종류, 네트워크 사용, 생성 파일, 권한 범위를 확인합니다. 자동 실행 hook, 외부 API 호출, 대량 파일 생성 기능은 사용자 확인 없이 활성화하지 않습니다.

## OS Notes

Linux와 macOS에서는 `uv tool install graphifyy`를 우선 사용합니다.

Windows PowerShell에서는 `/graphify .`가 경로로 해석될 수 있으므로 CLI에서는 `graphify .`를 사용합니다. opencode 내부 slash command로 사용할 때는 assistant 환경의 동작을 별도 확인합니다.

## Verification

설치 후 확인 명령은 다음입니다.

```bash
graphify --version
python3 -c "import json, pathlib; json.loads(pathlib.Path('opencode.json').read_text()); print('valid')"
git status --short
```

opencode 설정 파일, skill, plugin은 hot reload되지 않을 수 있으므로 변경 후 opencode를 재시작합니다.
