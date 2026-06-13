# Discussion: 프로젝트 로컬 권한 allowlist 조정

## Status (상태)

closed

## Summary (요약)

이 논의는 opencode가 세션을 다시 시작할 때 같은 명령어 권한을 다시 물어보는 불편함을 줄이기 위한 프로젝트 로컬 권한 설정 전략을 정리합니다.

최종 결론은 승인 기록 자체를 저장하려고 하기보다, `opencode.json`의 `permission` 규칙에 안전한 읽기/조회 명령 allowlist를 명시하는 것입니다.

## Background (배경)

사용자는 opencode 세션을 재접속하거나 재실행하면 이전에 승인했던 명령어를 다시 승인해야 해서 불편하다고 했습니다. 여기서 말하는 세션은 `.project-context/sessions/`의 Markdown 체크포인트가 아니라, opencode가 실행 중인 작업 세션입니다.

현재 확인한 `opencode.json`에는 이미 프로젝트 로컬 `permission` 설정이 있습니다.

현재 주요 설정:

- `read`, `glob`, `grep`, `list`: `allow`
- `edit`: `ask`
- `task`, `todowrite`, `question`, `skill`: `allow`
- `webfetch`, `websearch`: `ask`
- `external_directory`: 기본 `ask`, 민감 디렉토리 `deny`
- `bash`: 기본 `ask`, 일부 명령 `allow`, 위험 명령 `deny`

현재 `bash` allow 후보에는 `ls*`, `pwd`, `git status*`, `git diff*`, `git log*`, `git branch*`, `npm test*`, `pnpm test*`, `bun test*`, `pytest*`가 포함되어 있습니다.

## Context (맥락)

opencode의 권한 승인 UI에서 사용자가 한 번 승인한 선택이 세션을 넘어 프로젝트 로컬에 자동 저장되는지는 현재 설정 파일 표면에서는 명확한 별도 캐시 항목으로 보이지 않습니다.

다만 프로젝트 로컬 `opencode.json`의 `permission` 규칙은 재시작 후에도 적용됩니다. 따라서 반복적으로 승인하는 안전 명령은 승인 기록 저장이 아니라 프로젝트 권한 규칙으로 명시하는 것이 현실적입니다.

opencode permission 규칙은 broad rule을 먼저 두고, 더 구체적인 allow/deny rule을 뒤에 두는 방식이 안전합니다. per-tool object에서는 마지막으로 매칭되는 규칙이 우선합니다.

## Scope (범위)

포함:

- 승인 캐시와 프로젝트 permission 규칙의 차이 정리
- 현재 `opencode.json` permission 설정 평가
- 안전한 shell 명령 allowlist 후보 작성
- ask/deny로 유지할 명령 범위 정리
- 확정 시 반영 대상과 검증 방법 정리

제외:

- 지금 즉시 `opencode.json` 수정
- global config `~/.config/opencode/opencode.json` 수정
- opencode 내부 권한 승인 캐시 구현
- 권한 UI 또는 plugin hook 구현
- 모든 bash 명령을 allow로 여는 설정

## Constraints (제약)

- 이 하네스는 의도 정렬과 계약 경계 보호가 목표이므로 전체 `permission: "allow"`는 지양합니다.
- `bash` 전체 allow는 파괴적 명령, 네트워크, 설치, git 상태 변경을 넓게 허용할 수 있으므로 지양합니다.
- 안전한 명령이라도 shell pattern이 너무 넓으면 상태 변경 명령까지 포함될 수 있습니다.
- 설정 변경 후에는 opencode를 재시작해야 합니다.
- 프로젝트 로컬 설정은 이 템플릿을 사용하는 다른 프로젝트에도 영향을 줄 수 있으므로 기본값은 보수적으로 유지해야 합니다.

## Analysis (분석)

사용자가 느끼는 불편함은 설정이 보수적인 것도 일부 원인이지만, 더 근본적으로는 세션 중 승인한 권한이 다음 opencode 세션에 자동으로 이어지지 않는 동작 때문일 가능성이 큽니다.

이를 완화하는 방법은 세 가지입니다.

옵션 A: 전체 권한을 allow로 엽니다.

- 장점: 권한 질문이 거의 사라집니다.
- 단점: 이 하네스의 안전성과 드리프트 제어 목적에 맞지 않습니다.
- 단점: shell 명령과 편집이 과하게 열릴 수 있습니다.

옵션 B: 안전한 조회/검증 명령만 프로젝트 로컬 allowlist에 추가합니다.

- 장점: 재접속 후에도 자주 쓰는 안전 명령은 묻지 않습니다.
- 장점: edit, git 상태 변경, install, destructive command는 계속 ask/deny로 유지할 수 있습니다.
- 단점: allowlist에 없는 명령은 계속 물어봅니다.
- 단점: allowlist 유지보수 비용이 있습니다.

옵션 C: 현재 설정을 유지합니다.

- 장점: 보수적입니다.
- 단점: 반복 승인 불편이 계속됩니다.
- 단점: 현재 `git branch*`처럼 너무 넓은 allow가 섞여 있을 수 있습니다.

추천은 옵션 B입니다.

## Current Permission Review (현재 권한 설정 검토)

현재 설정에서 좋은 점:

- 파일 읽기와 검색 도구는 allow라 탐색 비용이 낮습니다.
- `edit`은 ask라 파일 변경 전에 사용자가 통제할 수 있습니다.
- `bash` 기본값이 ask라 예측하지 못한 명령은 승인 대상입니다.
- `rm`, `git reset --hard`, `git clean`, `sudo` 같은 위험 명령이 deny로 잡혀 있습니다.

현재 설정에서 재검토할 점:

- `git branch*`는 조회뿐 아니라 브랜치 생성/삭제/이름 변경까지 포함할 수 있으므로 너무 넓습니다.
- `npm test*`, `pnpm test*`, `bun test*`, `pytest*`는 일반적으로 검증 명령이지만 프로젝트 스크립트나 테스트가 임의 코드를 실행할 수 있습니다.
- `ls*`는 보통 안전하지만, shell alias나 옵션 확장까지 고려하면 `ls`와 `ls *` 정도로 좁힐 수 있습니다.

## Safe Shell Allowlist Candidate (안전한 shell allowlist 후보)

강한 추천 allow:

```text
pwd
date
git status
git status --short
git status --porcelain
git diff
git diff --stat
git diff --staged
git diff --staged --stat
git log --oneline
git log --oneline -10
git log --oneline -1
git branch --show-current
```

조건부 allow 후보:

```text
ls
ls *
git diff -- <path>
git diff --staged -- <path>
git show --stat
git show --name-only
```

검증 명령 후보:

```text
npm test*
pnpm test*
bun test*
pytest*
```

검증 명령은 일반적으로 개발 워크플로우에 필요하지만, 프로젝트 스크립트나 테스트 코드가 임의 동작을 할 수 있습니다. 템플릿 기본값에서는 ask로 둘지 allow로 둘지 선택이 필요합니다.

기본 ask 유지 후보:

```text
git add*
git commit*
git push*
git pull*
git merge*
git rebase*
git checkout*
git switch*
git branch*
npm install*
pnpm install*
bun install*
uv add*
uv sync*
python*
node*
mkdir*
cp*
mv*
```

deny 유지 후보:

```text
rm *
rm -rf *
git reset --hard*
git clean *
git checkout -- *
git restore *
sudo *
chmod -R *
chown -R *
```

## Permission Config Candidate (설정 후보)

권장 방향은 현재 설정을 유지하되 `bash` allowlist를 더 좁고 명시적으로 조정하는 것입니다.

예시:

```json
"permission": {
  "read": "allow",
  "glob": "allow",
  "grep": "allow",
  "list": "allow",
  "edit": "ask",
  "task": "allow",
  "todowrite": "allow",
  "question": "allow",
  "webfetch": "ask",
  "websearch": "ask",
  "skill": "allow",
  "external_directory": {
    "*": "ask",
    "~/.ssh/**": "deny",
    "~/.gnupg/**": "deny",
    "~/secrets/**": "deny"
  },
  "bash": {
    "*": "ask",
    "pwd": "allow",
    "date": "allow",
    "ls": "allow",
    "ls *": "allow",
    "git status": "allow",
    "git status --short": "allow",
    "git status --porcelain": "allow",
    "git diff": "allow",
    "git diff --stat": "allow",
    "git diff --staged": "allow",
    "git diff --staged --stat": "allow",
    "git log --oneline": "allow",
    "git log --oneline -10": "allow",
    "git log --oneline -1": "allow",
    "git branch --show-current": "allow",
    "rm *": "deny",
    "rm -rf *": "deny",
    "git reset --hard*": "deny",
    "git clean *": "deny",
    "git checkout -- *": "deny",
    "git restore *": "deny",
    "sudo *": "deny"
  }
}
```

주의: 위 후보에서 `git branch*`는 제거하는 편이 좋습니다. 브랜치 조회는 `git branch --show-current`만 allow하고, 브랜치 생성/삭제/이름 변경은 ask로 둡니다.

## Recommended Strategy / Plan / Options (추천 전략/계획/옵션)

추천안은 다음과 같습니다.

- 프로젝트 로컬 `opencode.json`에 안전한 shell allowlist를 명시합니다.
- 전체 `permission: "allow"`는 사용하지 않습니다.
- `read`, `glob`, `grep`, `list`는 계속 allow로 둡니다.
- `edit`은 ask로 유지합니다.
- `bash`는 기본 ask로 유지합니다.
- 안전한 git 조회 명령과 `pwd`, `date`, 제한된 `ls`만 allow합니다.
- `git branch*`는 제거하고 `git branch --show-current`만 allow합니다.
- 테스트 명령은 사용자의 선호에 따라 allow 또는 ask를 선택합니다. 기본 템플릿에서는 ask가 더 보수적입니다.
- 위험한 상태 변경/삭제/권한 명령은 deny로 유지하거나 보강합니다.

## Decision Candidate (결정 후보)

아직 확정 전이지만 현재 결정 후보는 다음과 같습니다.

- opencode 세션 승인 기록 자체를 프로젝트에 저장하려고 하지 않고, 프로젝트 로컬 `permission` 규칙으로 반복 승인을 줄입니다.
- safe shell allowlist는 조회/상태 확인 명령 중심으로 둡니다.
- `git branch*`는 allowlist에서 제거합니다.
- 테스트 명령 allow 여부는 사용자에게 확인합니다.
- 설정 변경은 `opencode.json`에 반영하고, 적용을 위해 opencode 재시작이 필요하다고 안내합니다.

## Questions (질문)

- 테스트 명령(`npm test*`, `pnpm test*`, `bun test*`, `pytest*`)을 allow로 둘까요, ask로 되돌릴까요?
  답변: 기본 템플릿에서는 ask로 둡니다.
- `ls*`를 유지할까요, `ls`와 `ls *` 정도로 좁힐까요?
  답변: `ls`와 `ls *`로 좁힙니다.
- `git show --stat`, `git show --name-only`도 allow할까요?
  답변: 이번 기본 allowlist에는 넣지 않습니다.
- `python --version`, `node --version`, `npm --version`, `pnpm --version`, `bun --version`, `uv --version` 같은 버전 조회 명령도 allow할까요?
  답변: 이번 기본 allowlist에는 넣지 않습니다.
- 이 정책을 `README.md`나 `AGENTS.md`에도 짧게 문서화할까요, 아니면 `opencode.json` 설정만으로 충분할까요?
  답변: 이번에는 `opencode.json`만 수정합니다.

## Open Issues (열린 쟁점)

- opencode 자체가 세션 승인 기록을 별도 저장하는 공식 기능을 제공하는지는 추가 확인이 필요합니다.
- shell pattern이 실제로 어느 수준까지 세밀하게 매칭되는지 확인이 필요합니다.
- 너무 좁게 잡으면 불편함이 계속되고, 너무 넓게 잡으면 하네스의 안전성이 떨어집니다.

## Resolution (정리 결과)

사용자 승인에 따라 다음 결론으로 확정합니다.

- opencode 세션 승인 기록 자체를 프로젝트에 저장하려고 하지 않고, 프로젝트 로컬 `permission` 규칙으로 반복 승인을 줄입니다.
- `read`, `glob`, `grep`, `list`는 allow로 유지합니다.
- `edit`은 ask로 유지합니다.
- `bash`는 기본 ask로 유지합니다.
- `bash` allowlist는 `pwd`, `date`, 제한된 `ls`, 안전한 git 조회 명령으로 좁힙니다.
- `git branch*`는 제거하고 `git branch --show-current`만 allow합니다.
- 테스트 명령은 기본 템플릿에서 ask로 둡니다.
- 위험한 삭제, hard reset, clean, restore, sudo, recursive chmod/chown은 deny로 유지 또는 보강합니다.
- 이번 반영 대상은 `opencode.json`입니다.
- 설정 변경 후 opencode 재시작이 필요합니다.

## Absorption Target (흡수 대상)

다음 설정으로 흡수합니다.

- `opencode.json`

## References (근거 및 영향 문서)

근거:

- 사용자 요청: opencode 세션 재접속 후 반복 권한 승인 불편
- `opencode.json`
- opencode permission 설정 규칙

영향:

- `opencode.json`
- 사용자 승인 빈도
- 프로젝트 로컬 opencode 보안/편의성 균형
