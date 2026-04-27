---
layout: single
title: "AI : 1. agent-skills(addyosmani)를 Codex에 적용하는 법"
description: Codex에서 agent-skills 설치 및 개발 흐름 정리, Harness Engineering
series_order: 1
categories:
 - AI
---

`agent-skills`는 AI 코딩 에이전트가 개발할 때 따라야 할 절차를 정리한 스킬 저장소이다.

[https://github.com/addyosmani/agent-skills](https://github.com/addyosmani/agent-skills)

## 설치

### 방법 1. git clone으로 추가

1. 저장소를 clone한다.

    ```bash
    git clone https://github.com/addyosmani/agent-skills.git
    ```

2. Codex의 skills 경로에 원하는 스킬 폴더를 복사한다.  
   예를 들어, `spec-driven-development`를 추가하려면 다음과 같이 복사한다.

    ```bash
    cp -r ./agent-skills/skills/spec-driven-development ~/.codex/skills/
    ```

3. Codex를 다시 실행한다.

즉, `git clone`만으로 바로 적용되는 것은 아니며, 원하는 스킬 폴더를 `~/.codex/skills` 아래에 넣어야 한다.

### 방법 2. $skill-installer 사용

1. Codex에서 `$skill-installer`를 실행한다.

2. 설치할 GitHub 경로를 입력한다.

    ```text
    $skill-installer install https://github.com/addyosmani/agent-skills/tree/main/skills/spec-driven-development
    ```

3. 설치가 끝나면 Codex를 다시 실행한다.

## 개발 흐름

`agent-skills`는 전체 개발 과정을 다음과 같이 나눈다.

- Define
- Plan
- Build
- Verify
- Review
- Ship

각 단계에 대응되는 스킬은 다음과 같다.

### Define(정의)

요구사항, 범위, 완료 조건을 먼저 정리하는 단계이다.

- `idea-refine`
  아이디어가 아직 모호할 때 정리하는 스킬
- `spec-driven-development`
  구현 전에 요구사항과 완료 조건을 먼저 정리하는 스킬

### Plan(계획)

작업을 작은 단위로 나누고 구현 순서를 정하는 단계이다.

- `planning-and-task-breakdown`
  큰 작업을 여러 단계로 분리하는 스킬

### Build(구현)

실제로 기능을 구현하는 단계이다.

- `incremental-implementation`
  기능을 한 번에 크게 만들지 않고 작은 단위로 나눠 구현하는 스킬
- `context-engineering`
  현재 작업에 필요한 문맥만 불러오도록 정리하는 스킬
- `frontend-ui-engineering`
  화면 작업 시 레이아웃, 접근성, 상태 처리까지 같이 다루는 스킬
- `api-and-interface-design`
  API나 모듈 경계를 설계할 때 사용하는 스킬

### Verify(검증)

구현한 결과가 제대로 동작하는지 확인하는 단계이다.

- `test-driven-development`
  테스트를 먼저 만들고 구현하는 스킬
- `browser-testing-with-devtools`
  브라우저 동작, 콘솔, 네트워크를 확인하는 스킬
- `debugging-and-error-recovery`
  재현, 원인 파악, 수정, 재발 방지 순서로 문제를 해결하는 스킬

### Review(검토)

구조, 품질, 누락된 문제를 점검하는 단계이다.

- `code-review-and-quality`
  정확성, 가독성, 구조, 보안, 성능 관점에서 점검하는 스킬
- `code-simplification`
  동작은 유지하면서 코드를 더 단순하게 정리하는 스킬
- `security-and-hardening`
  입력값 검증, 인증, 외부 연동 등 보안 항목을 점검하는 스킬
- `performance-optimization`
  병목 구간을 확인하고 필요한 부분만 최적화하는 스킬

### Ship(반영)

작업을 마무리하고 반영 준비를 하는 단계이다.

- `git-workflow-and-versioning`
  커밋, 브랜치, 변경 단위를 정리하는 스킬
- `ci-cd-and-automation`
  빌드, 테스트, 배포 자동화를 정리하는 스킬
- `documentation-and-adrs`
  작업 내용과 설계 결정을 문서로 남기는 스킬
- `shipping-and-launch`
  배포 전 확인 사항과 배포 절차를 점검하는 스킬
