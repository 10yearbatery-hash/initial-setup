# Claude Code 개인 워크플로우 시스템

Claude Code를 활용해 프로젝트를 통제 가능하게 운영하기 위한 개인 워크플로우 시스템.

---

## 핵심 원칙

- 증거 없이 완료 선언 금지 — 직접 실행하고 확인한 후에만 완료라고 말한다
- 작은 단계로 쪼개기 — 한 단계는 2~5분 단위로
- 막히면 멈추고 물어보기 — 3번 시도해도 안 되면 추측하지 않는다
- 근본 원인 먼저 — 오류 나면 바로 고치려 하지 않는다
- 테스트 먼저 — 코드 짜기 전에 테스트를 먼저 작성한다
- YAGNI — 지금 필요한 것만 만든다
- 자주 리뷰 — 작은 단위마다 검토한다

---

## 모델 규칙

| 작업 유형 | 모델 | 예시 |
|---|---|---|
| 설계, 분석, 계획, 디버깅 | Opus | brainstorming, writing-plans, systematic-debugging |
| 코딩, 기능 구현, 수정 | Sonnet | executing-plans, 코드 작성 |
| 파일 탐색, 간단한 조회 | Haiku | 파일 찾기, 빠른 검색 |

superpowers 스킬 사용 시에도 동일하게 적용한다.

---

## 작업 원칙

1. 작업 시작 전 규칙 지도에서 해당 rules 파일을 읽는다
2. 새 프로젝트/기능을 만들 때는 `.claude/rules/project-setup.md`를 따른다
3. 작업 완료 후 프로젝트 지도를 업데이트한다

---

## 규칙 지도

| 작업 유형 | 읽어야 할 파일 |
|---|---|
| 코딩 작업 | `.claude/rules/coding.md` |
| 테스트 작업 | `.claude/rules/testing.md` |
| 디버깅 | `.claude/rules/debugging.md` |
| 완료 확인 | `.claude/rules/verification.md` |
| 새 프로젝트 시작 | `.claude/rules/project-setup.md` |
| GitHub push/PR | `.claude/rules/git-push.md` |

---

## 프로젝트 지도

| 기능/프로젝트 | 파일 위치 |
|---|---|
| (새 프로젝트 생길 때마다 여기 추가) | |
