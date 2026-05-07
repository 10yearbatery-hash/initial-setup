# Claude Code 워크플로우 시스템 구현 계획

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** superpowers 기반 개인 워크플로우 시스템 파일들을 생성한다.

**Architecture:** 루트 CLAUDE.md(포인터 역할) + .claude/rules/(5개 규칙 파일) + projects/_template/CLAUDE.md(새 프로젝트 템플릿). 모든 파일은 마크다운이며 superpowers 스킬 원칙에서 내용을 차용한다.

**Tech Stack:** 마크다운, Git

---

## 파일 구조

```
/home/gdg/러닝/
├── CLAUDE.md                          # 생성
├── .claude/
│   └── rules/
│       ├── coding.md                  # 생성
│       ├── testing.md                 # 생성
│       ├── debugging.md               # 생성
│       ├── verification.md            # 생성
│       └── project-setup.md           # 생성
└── projects/
    └── _template/
        └── CLAUDE.md                  # 생성
```

---

### Task 1: Git 초기화

**Files:**
- Create: `/home/gdg/러닝/.gitignore`

- [ ] **Step 1: git 초기화**

```bash
cd /home/gdg/러닝 && git init
```

Expected: `Initialized empty Git repository in /home/gdg/러닝/.git/`

- [ ] **Step 2: .gitignore 생성**

```
.superpowers/
.omc/
```

파일 경로: `/home/gdg/러닝/.gitignore`

- [ ] **Step 3: 첫 커밋**

```bash
git add .gitignore docs/
git commit -m "초기 설정: docs 구조 및 gitignore 추가"
```

---

### Task 2: 루트 CLAUDE.md 생성

**Files:**
- Create: `/home/gdg/러닝/CLAUDE.md`

- [ ] **Step 1: 파일 생성**

내용:

```markdown
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

---

## 프로젝트 지도

| 기능/프로젝트 | 파일 위치 |
|---|---|
| (새 프로젝트 생길 때마다 여기 추가) | |
```

- [ ] **Step 2: 검증**

```bash
grep "^## " /home/gdg/러닝/CLAUDE.md
```

Expected:
```
## 핵심 원칙
## 모델 규칙
## 작업 원칙
## 규칙 지도
## 프로젝트 지도
```

- [ ] **Step 3: 커밋**

```bash
git add CLAUDE.md
git commit -m "루트 CLAUDE.md 추가: 핵심 원칙, 모델 규칙, 지도"
```

---

### Task 3: coding.md 생성

**Files:**
- Create: `/home/gdg/러닝/.claude/rules/coding.md`

- [ ] **Step 1: 파일 생성**

내용:

```markdown
# 코딩 규칙

superpowers writing-plans + test-driven-development 기반.

## 원칙

- **YAGNI** — 지금 필요한 것만 만든다. "나중에 쓸 것 같아서"는 없다.
- **DRY** — 같은 코드를 반복하지 않는다. 중복이 보이면 분리한다.
- **파일 하나 = 역할 하나** — 각 파일은 하나의 명확한 역할을 가진다. 너무 많은 것을 하는 파일은 쪼갠다.
- **작은 파일 선호** — 파일이 커지면 역할이 섞인 신호다. 분리한다.
- **재사용 가능하게** — 컴포넌트는 여러 곳에서 쓸 수 있게 만든다. 특정 상황에만 동작하는 코드는 피한다.
- **자주 커밋** — 작은 단위마다 커밋한다. 커밋은 작업의 체크포인트다.

## 코드 짜기 전 확인

1. 어떤 파일을 생성/수정하는지 먼저 나열한다
2. 기존에 재사용할 수 있는 게 있는지 확인한다
3. 이 변경이 다른 파일에 영향을 주는지 확인한다

## 금지

- 동작하지 않는 코드를 커밋한다
- 이해하지 못한 코드를 그대로 붙여넣는다
- 파일 하나에 여러 역할을 넣는다
```

- [ ] **Step 2: 검증**

```bash
grep "^## " /home/gdg/러닝/.claude/rules/coding.md
```

Expected:
```
## 원칙
## 코드 짜기 전 확인
## 금지
```

- [ ] **Step 3: 커밋**

```bash
git add .claude/rules/coding.md
git commit -m "rules: coding.md 추가"
```

---

### Task 4: testing.md 생성

**Files:**
- Create: `/home/gdg/러닝/.claude/rules/testing.md`

- [ ] **Step 1: 파일 생성**

내용:

```markdown
# 테스트 규칙

superpowers test-driven-development 기반.

## 철칙

코드 짜기 전에 테스트를 먼저 작성한다.
테스트가 실패하는 걸 눈으로 확인한 후에 구현한다.

## Red-Green-Refactor 사이클

1. **RED** — 실패하는 테스트를 먼저 작성한다
2. **GREEN** — 테스트를 통과하는 최소한의 코드를 작성한다
3. **REFACTOR** — 테스트가 통과된 상태에서 코드를 정리한다

## 원칙

- 테스트 하나 = 동작 하나
- 테스트 이름은 무엇을 테스트하는지 명확히
- 테스트가 복잡하면 코드 설계가 복잡한 것 — 단순하게 만든다
- 버그를 고칠 때도 테스트 먼저

## 금지

- 코드 먼저 짜고 테스트 나중에 작성
- "수동으로 확인했어요" — 자동 테스트로 검증해야 한다
- 테스트 없이 완료 선언
```

- [ ] **Step 2: 검증**

```bash
grep "^## " /home/gdg/러닝/.claude/rules/testing.md
```

Expected:
```
## 철칙
## Red-Green-Refactor 사이클
## 원칙
## 금지
```

- [ ] **Step 3: 커밋**

```bash
git add .claude/rules/testing.md
git commit -m "rules: testing.md 추가"
```

---

### Task 5: debugging.md 생성

**Files:**
- Create: `/home/gdg/러닝/.claude/rules/debugging.md`

- [ ] **Step 1: 파일 생성**

내용:

```markdown
# 디버깅 규칙

superpowers systematic-debugging 기반.

## 철칙

오류 났을 때 바로 고치려 하지 않는다.
근본 원인을 먼저 찾는다.

## 4단계 프로세스

### 1단계: 원인 조사 (고치기 전에 반드시)
- 에러 메시지를 끝까지 읽는다
- 재현할 수 있는지 확인한다 (매번 발생하는가?)
- 최근에 무엇이 바뀌었는지 확인한다
- 여러 컴포넌트가 있으면 어느 단계에서 깨지는지 확인한다

### 2단계: 패턴 분석
- 비슷하게 작동하는 다른 코드가 있는가?
- 작동하는 것과 안 작동하는 것의 차이가 무엇인가?

### 3단계: 가설 검증
- "X 때문일 것이다"를 명확히 쓴다
- 가장 작은 변경으로 가설을 테스트한다
- 한 번에 하나씩만 바꾼다

### 4단계: 수정
- 근본 원인을 고친다 (증상이 아니라)
- 실패하는 테스트를 먼저 작성한다
- 수정 후 테스트가 통과하는지 확인한다

## 3번 시도해도 안 되면 멈춘다

3번 시도했는데 계속 실패하면:
- 추측을 멈춘다
- 아키텍처 자체를 의심한다
- 도움을 요청한다

## 금지

- 원인 모르고 코드 바꾸기
- 여러 곳을 동시에 수정하기
- 3번 이상 같은 방식으로 재시도하기
```

- [ ] **Step 2: 검증**

```bash
grep "^## " /home/gdg/러닝/.claude/rules/debugging.md
```

Expected:
```
## 철칙
## 4단계 프로세스
## 3번 시도해도 안 되면 멈춘다
## 금지
```

- [ ] **Step 3: 커밋**

```bash
git add .claude/rules/debugging.md
git commit -m "rules: debugging.md 추가"
```

---

### Task 6: verification.md 생성

**Files:**
- Create: `/home/gdg/러닝/.claude/rules/verification.md`

- [ ] **Step 1: 파일 생성**

내용:

```markdown
# 검증 규칙

superpowers verification-before-completion 기반.

## 철칙

증거 없이 완료 선언을 하지 않는다.
직접 실행하고 확인한 후에만 완료라고 말한다.

## 완료 선언 전 반드시

1. 확인 명령을 실행한다 — 실행하지 않으면 확인한 게 아니다
2. 출력 결과를 전체 읽는다 — 부분만 보지 않는다
3. 결과가 기대와 맞는지 확인한다
4. 그 다음에 완료라고 말한다

## 금지 표현

이 표현들은 검증 없이 쓸 수 없다:
- "됐을 것 같아요"
- "아마 작동할 거예요"
- "보기엔 맞는 것 같아요"
- "이전에 확인했어요"

## 검증 기준

| 주장 | 필요한 증거 |
|---|---|
| 기능이 작동한다 | 직접 실행한 결과 |
| 테스트가 통과한다 | 테스트 실행 출력 |
| 버그가 고쳐졌다 | 원래 문제 재현 후 해결 확인 |
| 요구사항을 충족한다 | 요구사항 항목별 체크 |
```

- [ ] **Step 2: 검증**

```bash
grep "^## " /home/gdg/러닝/.claude/rules/verification.md
```

Expected:
```
## 철칙
## 완료 선언 전 반드시
## 금지 표현
## 검증 기준
```

- [ ] **Step 3: 커밋**

```bash
git add .claude/rules/verification.md
git commit -m "rules: verification.md 추가"
```

---

### Task 7: project-setup.md 생성

**Files:**
- Create: `/home/gdg/러닝/.claude/rules/project-setup.md`

- [ ] **Step 1: 파일 생성**

내용:

```markdown
# 프로젝트 설정 규칙

새 프로젝트/기능을 만들 때 따르는 규칙.

## 새 프로젝트 CLAUDE.md 만드는 방법

`projects/기능명/CLAUDE.md` 파일을 만들고 아래 6개 섹션을 채운다.

### 1. 기능 설명 + 목표
이 기능이 무엇을 하는지 1~2줄.
이 기능의 목표가 무엇인지.

### 2. 기술 스택
이 기능에서 사용하는 언어, 라이브러리, 프레임워크.
전체 프로젝트 스택이 아닌 이 기능에서 쓰는 것만.

### 3. 관련 rules 참조
이 기능 작업할 때 봐야 할 rules 파일 목록.
예: 코드 작성 → .claude/rules/coding.md
예: 오류 발생 → .claude/rules/debugging.md

### 4. 주요 파일 위치
핵심 파일들이 어디 있는지.
예: 메인 로직 → src/features/auth/index.ts

### 5. 의존성
이 기능과 연결된 다른 기능/프로젝트.
예: "auth가 바뀌면 dashboard도 확인해야 한다"
처음엔 비어있고 작업하면서 채워나간다.

### 6. 절대 하면 안 되는 것
이 기능 작업할 때 금지 사항.
처음엔 비어있고 작업하면서 발견한 것을 추가한다.

## 새 프로젝트 시작 체크리스트

- [ ] `projects/기능명/` 폴더 생성
- [ ] `CLAUDE.md` 만들고 6개 섹션 채우기
- [ ] 루트 `CLAUDE.md`의 프로젝트 지도에 한 줄 추가
```

- [ ] **Step 2: 검증**

```bash
grep "^## \|^### " /home/gdg/러닝/.claude/rules/project-setup.md
```

Expected:
```
## 새 프로젝트 CLAUDE.md 만드는 방법
### 1. 기능 설명 + 목표
### 2. 기술 스택
### 3. 관련 rules 참조
### 4. 주요 파일 위치
### 5. 의존성
### 6. 절대 하면 안 되는 것
## 새 프로젝트 시작 체크리스트
```

- [ ] **Step 3: 커밋**

```bash
git add .claude/rules/project-setup.md
git commit -m "rules: project-setup.md 추가"
```

---

### Task 8: projects/_template/CLAUDE.md 생성

**Files:**
- Create: `/home/gdg/러닝/projects/_template/CLAUDE.md`

- [ ] **Step 1: 파일 생성**

내용:

```markdown
# [기능 이름]

한 줄 설명: 이 기능이 무엇을 하는지 + 목표.

---

## 기술 스택

이 기능에서 사용하는 언어/라이브러리/프레임워크.

## 관련 rules 참조

이 기능 작업할 때 봐야 할 rules 파일:
- 코드 작성 → .claude/rules/coding.md
- 테스트 → .claude/rules/testing.md
- 오류 발생 → .claude/rules/debugging.md
- 완료 확인 → .claude/rules/verification.md

## 주요 파일 위치

| 역할 | 경로 |
|---|---|
| (작업하면서 채워나간다) | |

## 의존성

이 기능과 연결된 다른 기능/프로젝트.
(처음엔 비어있고 작업하면서 채워나간다)

## 절대 하면 안 되는 것

(처음엔 비어있고 작업하면서 발견한 것을 추가한다)
```

- [ ] **Step 2: 검증**

```bash
grep "^## " /home/gdg/러닝/projects/_template/CLAUDE.md
```

Expected:
```
## 기술 스택
## 관련 rules 참조
## 주요 파일 위치
## 의존성
## 절대 하면 안 되는 것
```

- [ ] **Step 3: 커밋**

```bash
git add projects/
git commit -m "projects: _template CLAUDE.md 추가"
```

---

### Task 9: 전체 구조 최종 검증

- [ ] **Step 1: 모든 파일 존재 확인**

```bash
find /home/gdg/러닝 -name "CLAUDE.md" -o -name "*.md" -path "*rules*" | sort
```

Expected 출력:
```
/home/gdg/러닝/.claude/rules/coding.md
/home/gdg/러닝/.claude/rules/debugging.md
/home/gdg/러닝/.claude/rules/project-setup.md
/home/gdg/러닝/.claude/rules/testing.md
/home/gdg/러닝/.claude/rules/verification.md
/home/gdg/러닝/CLAUDE.md
/home/gdg/러닝/projects/_template/CLAUDE.md
```

- [ ] **Step 2: 루트 CLAUDE.md 섹션 확인**

```bash
grep "^##" /home/gdg/러닝/CLAUDE.md
```

Expected:
```
## 핵심 원칙
## 모델 규칙
## 작업 원칙
## 규칙 지도
## 프로젝트 지도
```

- [ ] **Step 3: 플레이스홀더 없는지 확인**

```bash
grep -r "TBD\|TODO\|미정\|나중에" /home/gdg/러닝/.claude/ /home/gdg/러닝/CLAUDE.md
```

Expected: 출력 없음 (플레이스홀더 없음)

- [ ] **Step 4: 최종 커밋**

```bash
git log --oneline
```

Expected: 9개 커밋 히스토리 확인
