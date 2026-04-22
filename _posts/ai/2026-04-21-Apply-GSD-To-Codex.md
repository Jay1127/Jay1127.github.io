---
layout: single
title: "AI : 2. GSD(get-shit-done)를 Codex에 적용하는 법"
description: Codex에서 GSD(get-shit-done) 설치 및 주요 명령 정리
categories:
 - AI
---

`GSD(get-shit-done)`는 메타 프롬프팅, 컨텍스트 엔지니어링, 스펙 기반 개발을 하나로 묶은 개발 워크플로우다.

[https://github.com/gsd-build/get-shit-done](https://github.com/gsd-build/get-shit-done)

## 설치

### 방법 1. 대화형 설치

1. 다음 명령을 실행한다.

    ```bash
    npx get-shit-done-cc@latest
    ```

2. 설치 대상에서 `Codex`를 선택한다.

3. 설치 범위는 `Global` 또는 `Local` 중 하나를 선택한다.

4. 설치가 끝나면 Codex에서 다음 명령으로 확인한다.

    ```text
    $gsd-help
    ```

### 방법 2. 비대화형 설치

1. 전역 설치는 다음 명령을 사용한다.

    ```bash
    npx get-shit-done-cc --codex --global
    ```

2. 현재 프로젝트에만 설치하려면 다음 명령을 사용한다.

    ```bash
    npx get-shit-done-cc --codex --local
    ```

## 자주 쓰는 명령어

- `$gsd-help`
  사용 가능한 명령과 사용법을 확인한다.
- `$gsd-new-project`
  질문과 조사를 바탕으로 요구사항과 로드맵을 정리하면서 새 프로젝트를 시작한다.
- `$gsd-discuss-phase 1`
  특정 단계에 들어가기 전에 요구사항과 구현 방향을 구체화한다.
- `$gsd-ui-phase 1`
  프론트엔드 단계에서 UI 명세 문서(UI-SPEC.md)를 만든다.
- `$gsd-plan-phase 1`
  해당 단계의 조사와 실행 계획 수립, 계획 검증을 진행한다.
- `$gsd-execute-phase 1`
  계획한 작업을 실행하고 결과를 확인한다.
- `$gsd-verify-work 1`
  구현 결과를 사용자가 직접 검증한다.
- `$gsd-ship 1`
  검증된 작업을 정리하고 PR을 준비하거나 바로 생성한다.
- `$gsd-progress`
  현재 진행 상태를 확인한다.
- `$gsd-quick`
  전체 계획 없이 빠르게 처리할 작업을 시작한다.

## 워크플로우

GSD의 전체 흐름은 다음과 같다.

### 1. 새 프로젝트 시작

질문에 답하고 필요한 조사를 거쳐 요구사항과 로드맵을 정리하면서 프로젝트를 시작한다.

- `$gsd-new-project`

기존 코드베이스가 있으면 먼저 구조와 규칙을 분석한 뒤 시작할 수 있다.

- `$gsd-map-codebase`
- `$gsd-new-project`

### 2. 단계별 요구사항 정리

각 단계에 들어가기 전에 요구사항과 구현 방향을 구체화한다.

- `$gsd-discuss-phase 1`

프론트엔드 단계라면 UI 명세 문서(UI-SPEC.md)를 먼저 만들 수 있다.

- `$gsd-ui-phase 1`

### 3. 계획 수립

GSD의 계획 단계에서는 조사부터 실행 계획 수립, 계획 검증까지 함께 진행한다.

- `$gsd-plan-phase 1`

이 단계에서 조사 결과와 작업 계획을 정리한다.

### 4. 구현 및 검증

계획된 작업을 실행하고, 이후 사용자가 직접 결과를 검증한다.

- `$gsd-execute-phase 1`
- `$gsd-verify-work 1`

### 5. 정리 및 PR 준비

검증이 끝난 작업을 정리하고 PR 생성 또는 다음 단계 진행으로 이어간다.

- `$gsd-ship 1`

각 단계에서 다음 작업을 자동으로 이어가려면 다음 명령을 사용할 수 있다.

- `$gsd-next`

## 참고

GSD는 프로젝트 루트에 `.planning/` 디렉터리를 만들고 단계별 산출물을 관리한다.  
따라서 기존 프로젝트에 적용할 때는, `.planning/` 디렉터리를 어떻게 운영할지 먼저 정하는 것이 좋다.
