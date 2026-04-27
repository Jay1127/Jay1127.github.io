---
layout: single
title: "AI : 4. Superpowers를 Codex에 적용하는 법"
description: Codex에서 Superpowers 설치 및 개발 흐름 정리
categories:
 - AI
---

`Superpowers`는 AI 코딩 에이전트가 설계, 계획, 테스트, 리뷰 흐름을 따르도록 도와주는 스킬 기반 개발 방법론이다.

[https://github.com/obra/superpowers](https://github.com/obra/superpowers)

## 설치

Superpowers는 사용하는 에이전트에 따라 설치 방법이 다르다.  
Codex에서는 Codex CLI 또는 Codex App에서 플러그인으로 설치할 수 있다.
플러그인 화면이 보이지 않는 환경에서는 공식 저장소의 Codex 설치 문서를 확인한다.

### 방법 1. Codex CLI에서 설치

1. Codex CLI에서 플러그인 화면을 연다.

    ```text
    /plugins
    ```

2. 검색창에서 `superpowers`를 검색한다.

    ```text
    superpowers
    ```

3. 검색 결과에서 `Install Plugin`을 선택한다.

4. 설치가 끝나면 Codex를 다시 실행한다.

5. 다시 `Plugins` 화면을 열어 `Superpowers`가 설치되어 있는지 확인한다.

### 방법 2. Codex App에서 설치

1. Codex App의 사이드바에서 `Plugins`를 연다.

2. 검색창에 `superpowers`를 입력한다.

    ![Superpowers 플러그인 검색 화면](/assets/images/superpowers-plugin.png){: .align-center}{: width="900"}

3. `Coding` 섹션에서 `Superpowers`를 찾는다.

4. `Superpowers` 옆의 `+` 버튼을 눌러 설치한다.

5. 설치 안내에 따라 진행한 뒤 Codex를 다시 실행한다.

6. 다시 `Plugins` 화면을 열어 `Superpowers`가 설치되어 있는지 확인한다.

## 기본 워크플로우

Superpowers의 기본 흐름은 다음과 같다.

### 1. 브레인스토밍

바로 코드를 수정하지 않고, 먼저 무엇을 만들지 질문과 답변을 통해 정리한다.

- `brainstorming`
  요구사항, 대안, 설계 방향을 먼저 정리하는 스킬

### 2. 작업 브랜치 준비

설계가 정리되면 별도의 작업 공간과 브랜치를 준비한다.

- `using-git-worktrees`
  독립된 작업 폴더와 브랜치를 만들어 작업을 분리하는 스킬

### 3. 구현 계획 작성

구현할 내용을 작은 작업 단위로 나누고, 각 작업의 대상 파일과 검증 방법을 정리한다.

- `writing-plans`
  구현 계획을 작은 작업 목록으로 나누는 스킬

### 4. 구현

작성된 계획을 기준으로 작업을 진행한다.

- `executing-plans`
  계획에 따라 작업을 순서대로 실행하는 스킬
- `subagent-driven-development`
  작업 단위를 서브 에이전트에게 나누어 맡기고 결과를 검토하는 스킬

### 5. 테스트 주도 개발

구현 전에 실패하는 테스트를 먼저 만들고, 최소한의 코드로 통과시킨 뒤 정리한다.

- `test-driven-development`
  RED, GREEN, REFACTOR 순서로 구현하는 스킬

### 6. 코드 리뷰

작업 중간 또는 완료 후 계획과 코드 품질을 기준으로 검토한다.

- `requesting-code-review`
  구현 결과를 검토하고 문제를 심각도 순서로 정리하는 스킬
- `receiving-code-review`
  리뷰 결과를 반영하고 다시 확인하는 스킬

### 7. 개발 브랜치 마무리

작업이 끝나면 테스트를 확인하고 병합, PR 생성, 작업 브랜치 유지, 폐기 중 다음 행동을 정한다.

- `finishing-a-development-branch`
  작업 브랜치를 마무리하고 정리하는 스킬

## 주요 스킬

Superpowers에는 작업 흐름에서 주로 사용되는 여러 스킬이 포함되어 있다.

### Testing

- `test-driven-development`
  테스트를 먼저 작성하고, 실패 확인 후 구현하는 흐름을 강제한다.

### Debugging

- `systematic-debugging`
  문제를 추측으로 고치지 않고 재현, 원인 파악, 수정, 검증 순서로 해결한다.
- `verification-before-completion`
  완료를 선언하기 전에 실제로 문제가 해결되었는지 확인한다.

### Collaboration

- `brainstorming`
  구현 전에 요구사항과 설계 방향을 정리한다.
- `writing-plans`
  작업을 작은 단위의 구현 계획으로 나눈다.
- `executing-plans`
  계획에 따라 작업을 실행한다.
- `dispatching-parallel-agents`
  독립적인 작업을 여러 에이전트에게 병렬로 맡긴다.
- `requesting-code-review`
  변경 내용을 리뷰한다.
- `receiving-code-review`
  리뷰 의견을 반영한다.
- `using-git-worktrees`
  독립된 작업 공간에서 브랜치별 작업을 진행한다.
- `finishing-a-development-branch`
  작업 완료 후 병합 또는 PR 준비를 진행한다.
- `subagent-driven-development`
  작업 단위별로 서브 에이전트를 사용해 구현과 검토를 진행한다.

### Meta

- `writing-skills`
  새로운 스킬을 작성하고 검증하는 방법을 정리한다.
- `using-superpowers`
  Superpowers 스킬 시스템의 사용 방법을 설명한다.

## 참고

Superpowers는 명령어 하나를 실행하는 도구라기보다는 Codex의 개발 습관을 바꾸는 플러그인에 가깝다.  
설치 후에는 코드를 바로 수정하기보다 먼저 설계, 계획, 테스트, 리뷰 흐름을 거치도록 유도한다.
