---
layout: single
title: "AI : 6. Spec Kit을 Codex에 적용하는 법"
description: Codex에서 Spec Kit 설치 및 사용 방법 정리
date: 2026-04-29 09:00:00 +0900
series_order: 6
categories:
 - AI
---

`Spec Kit`은 요구사항을 명세, 계획, 작업 목록으로 정리해 구현까지 이어가게 도와주는 Spec-Driven Development 툴킷이다.

[https://github.com/github/spec-kit](https://github.com/github/spec-kit)


## 사전 준비

Spec Kit 설치는 `uv` 기준으로 진행한다.
Windows에서는 PowerShell에서 다음 명령을 실행한다.

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

설치가 끝나면 새 터미널을 열고 `uv --version`으로 확인한다.

## 설치

먼저 `specify` CLI를 설치한 뒤, 작업 폴더에서 Codex 통합을 초기화한다.

### 방법 1. 현재 폴더에서 초기화

1. `specify` CLI를 설치한다.

    ```powershell
    uv tool install specify-cli --from git+https://github.com/github/spec-kit.git@v0.7.3
    ```

2. 작업 폴더에서 Spec Kit을 초기화한다.

    ```powershell
    specify init . --integration codex --script ps
    ```

3. 설치 상태를 확인한다.

    ```powershell
    specify version
    specify check
    ```

4. 초기화가 끝나면 `.agents/skills`와 `.specify` 폴더가 생성된다.

5. 초기화한 프로젝트 루트에서 Codex를 실행하면 `$speckit-*` 명령을 사용할 수 있다.

### 방법 2. 새 폴더를 만들면서 초기화

현재 폴더가 아니라 새 폴더를 만들면서 시작하려면 다음 명령을 사용한다.

```powershell
specify init my-project --integration codex --script ps
```

## 자주 쓰는 명령어

### 터미널에서 확인하는 명령

- `specify version`
  설치된 `specify` 버전을 확인한다.
- `specify check`
  필요한 도구와 Codex 통합 상태를 확인한다.

### Codex에서 호출하는 명령

- `$speckit-constitution`
  프로젝트 원칙과 개발 기준을 정리한다.
- `$speckit-specify`
  만들고 싶은 기능의 요구사항을 정리한다.
- `$speckit-plan`
  구현 계획과 기술 스택을 정리한다.
- `$speckit-tasks`
  구현 작업을 세부 항목으로 나눈다.
- `$speckit-implement`
  작업 목록을 기준으로 구현을 진행한다.

## 워크플로우

Codex에서는 Spec Kit 명령을 `$speckit-*` 형태로 호출한다.

### 1. 프로젝트 원칙 작성

먼저 프로젝트의 코드 품질, 테스트, UI 기준을 정리한다.

```text
$speckit-constitution 코드 품질, 테스트 기준, UI 일관성 원칙을 정리해줘.
```

### 2. 요구사항 명세 작성

다음으로 만들고 싶은 기능의 요구사항을 정리한다.

```text
$speckit-specify 사용자가 할 일을 생성, 수정, 삭제할 수 있는 간단한 Todo 앱을 만든다.
```

### 3. 구현 계획 작성

요구사항이 정리되면 기술 스택과 구현 계획을 만든다.

```text
$speckit-plan Vite와 React를 사용하고, 상태 관리는 최소한으로 구성한다.
```

### 4. 작업 목록 생성

구현 계획을 기준으로 작업을 세부 항목으로 나눈다.

```text
$speckit-tasks
```

### 5. 구현 진행

작업 목록이 만들어지면 이를 기준으로 구현을 진행한다.

```text
$speckit-implement
```
