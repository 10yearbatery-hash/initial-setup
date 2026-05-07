# GitHub Push 규칙

superpowers finishing-a-development-branch 기반.

## 트리거

"push해줘", "깃허브에 올려줘" 등 GitHub push 요청이 오면 이 규칙을 따른다.

## 브랜치 전략

- 기능 단위로 `feature/작업명` 브랜치에서 작업한다
- 예: `feature/add-login`, `feature/fix-header`
- main 브랜치에 직접 push하지 않는다

## 실행 순서

1. **검증** — `superpowers:verification-before-completion` 실행
2. **코드 리뷰** — `superpowers:requesting-code-review` 실행
3. **PR 생성** — `superpowers:finishing-a-development-branch` 실행 (옵션 2: Push 후 PR 생성 선택)

## 금지

- 검증 없이 push
- 코드 리뷰 없이 push
- main 브랜치에 직접 push
