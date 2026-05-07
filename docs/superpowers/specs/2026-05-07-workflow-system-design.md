# Claude Code 개인 워크플로우 시스템 설계

## 목표

Claude Code를 활용해 프로젝트를 통제 가능하게 운영하기 위한 개인 워크플로우 시스템.
비개발자가 superpowers 스킬 기반으로 프로젝트를 이해하고, 추적하고, 예측할 수 있게 한다.

---

## 핵심 철학

- 최소로 시작하고, 사후 평가로 채워나간다
- 많이 하는 것보다 하나를 제대로 만들고 쌓는다
- 이해하지 못한 것은 추가하지 않는다

---

## 전체 구조

```
프로젝트 루트/
├── CLAUDE.md                      # 루트 — 포인터 역할만
├── .claude/
│   └── rules/
│       ├── coding.md
│       ├── testing.md
│       ├── debugging.md
│       ├── verification.md
│       └── project-setup.md
└── projects/
    └── 기능명/
        └── CLAUDE.md              # 기능별 전용 컨텍스트
```

---

## 1. 루트 CLAUDE.md 구조

```markdown
# [서비스 이름]

한 줄 설명: 이 서비스가 무엇을 하는지.

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

---

## 프로젝트 지도

| 기능/프로젝트 | 파일 위치 |
|---|---|
| (새 프로젝트 생길 때마다 여기 추가) | |
```

---

## 2. Rules 파일 5개

각 파일은 superpowers 스킬에서 핵심만 뽑아 담는다.

| 파일 | 출처 스킬 | 역할 |
|---|---|---|
| `coding.md` | writing-plans + TDD | 코드 짜기 전에 읽는 행동 지침 |
| `testing.md` | test-driven-development | 테스트 전에 읽는 행동 지침 |
| `debugging.md` | systematic-debugging | 오류 났을 때 읽는 행동 지침 |
| `verification.md` | verification-before-completion | 완료 전에 읽는 행동 지침 |
| `project-setup.md` | (이 설계) | 새 프로젝트 CLAUDE.md 만드는 방법 |

---

## 3. 프로젝트별 CLAUDE.md 구조

새 기능/프로젝트 시작할 때마다 `projects/기능명/CLAUDE.md` 생성.

```markdown
# [기능 이름]

한 줄 설명: 이 기능이 무엇을 하는지 + 목표.

---

## 기술 스택
이 기능에서 사용하는 언어/라이브러리/프레임워크.

## 관련 rules 참조
이 기능 작업할 때 봐야 할 rules 파일 목록.
예: 코드 짜면 → .claude/rules/coding.md
예: 오류 나면 → .claude/rules/debugging.md

## 주요 파일 위치
어떤 파일이 어디 있는지.

## 의존성
이 기능과 연결된 다른 프로젝트/기능.
예: "auth가 바뀌면 여기도 확인해야 한다"

## 절대 하면 안 되는 것
작업하면서 발견한 금지 사항. 처음엔 비어있고 채워나간다.
```

---

## 4. 워크플로우 사이클

```
1. /superpowers:brainstorming    (Opus)   — 무엇을 왜 만드는지 명확히
2. /superpowers:writing-plans    (Opus)   — 어떻게 만들지 단계 정의
3. /superpowers:executing-plans  (Sonnet) — 계획대로 단계별 실행
4. /superpowers:verification     (Sonnet) — 제대로 됐는지 확인
5. /superpowers:requesting-code-review (Opus) — 개선점 찾기
6. 사후 평가 ("사후 평가 해줘")          — 아래 항목 검토
```

---

## 5. 사후 평가 루틴

작업 하나 끝날 때마다 반드시 수행.

```
🧠 이해
□ 무엇이 바뀌었나?
□ 왜 그렇게 됐나?
□ 예상과 달랐던 점은?

📍 추적
□ 새로 생긴 의존성은?
□ 제거해야 할 것들은?
□ CLAUDE.md 업데이트 필요?

💡 개선
□ 이번에 헷갈렸던 부분은?
□ Claude 지시가 모호했던 게 있나?
□ rules에 추가할 규칙 생겼나?

🤖 자동화
□ 반복적으로 한 게 있나?
□ 매번 같은 지시를 했나?
□ hook으로 처리할 수 있나?
```

---

## 시스템이 자라는 방식

```
CLAUDE.md 하나
→ 평가 → rules/coding.md 추가
→ 평가 → 기능별 CLAUDE.md 추가
→ 평가 → hook 자동화
→ 반복
```

필요하다고 느껴질 때만 추가한다. 이해하지 못한 것은 추가하지 않는다.
