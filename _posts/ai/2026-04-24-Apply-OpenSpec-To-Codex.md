---
layout: single
title: "AI : 3. OpenSpec을 Codex에 적용하는 법"
description: Codex에서 OpenSpec 설치 및 주요 명령 정리
series_order: 3
categories:
 - AI
---

`OpenSpec`은 코드를 바로 수정하기 전에 변경 제안과 스펙부터 정리하게 도와주는 스펙 기반 개발 도구다.

[https://github.com/Fission-AI/OpenSpec](https://github.com/Fission-AI/OpenSpec)

## 설치

먼저 OpenSpec을 전역으로 설치한다.

    ```bash
    npm install -g @fission-ai/openspec@latest
    ```

### 방법 1. 대화형 초기화

1. 프로젝트 폴더로 이동한 뒤 초기화를 진행한다.

    ```bash
    openspec init
    ```

2. 초기화 과정에서 사용할 도구로 `Codex`를 선택한다.

3. 초기화가 끝나면 기본 프로필인 `core`가 적용된다.

### 방법 2. 비대화형 초기화

1. 프로젝트 폴더에서 다음 명령으로 Codex용 설정을 바로 생성한다.

    ```bash
    openspec init --tools codex
    ```

2. 프로필을 바꿨다면 다음 명령으로 다시 반영한다.

    ```bash
    openspec update
    ```

여기까지는 터미널에서 실행하고, 이후 `/opsx:*` 명령은 Codex 대화창에서 사용한다.

### 설치 후 생성되는 위치

Codex용 프롬프트 파일은 `~/.codex/prompts/` 아래에 들어가고, 프로젝트 스펙 파일은 저장소의 `openspec/` 폴더 아래에 만들어진다.

## 자주 쓰는 명령어

기본 프로필인 `core`에서는 다음 명령을 사용한다.

- `/opsx:propose`
  새 변경 폴더(change)를 만들고 변경 제안서, 변경 스펙, 설계 문서, 작업 목록을 한 번에 만든다.
- `/opsx:explore`
  구현 전에 아이디어와 방향을 먼저 정리한다.
- `/opsx:apply`
  작업 목록에 맞춰 구현을 진행한다.
- `/opsx:archive`
  완료된 변경 사항을 보관 폴더(archive)로 옮기고 기본 스펙에 반영한다.

확장 워크플로우를 쓰려면 프로필을 변경한 뒤 `openspec update`를 실행해야 한다.
프로필을 바꾸면 Codex용 `/opsx:*` 프롬프트도 다시 생성해야 하기 때문이다.

- `/opsx:new`
  새 변경 폴더의 기본 구조만 먼저 만든다.
- `/opsx:continue`
  현재 상태를 보고 다음 문서 묶음을 이어서 만든다.
- `/opsx:ff`
  확장 프로필에서 변경 제안서, 변경 스펙, 설계 문서, 작업 목록을 빠르게 한 번에 만든다.
- `/opsx:verify`
  구현 결과가 문서 내용과 맞는지 검증한다.
- `/opsx:sync`
  변경 스펙을 기본 스펙과 동기화한다.
- `/opsx:bulk-archive`
  여러 변경 사항을 한 번에 보관 폴더(archive)로 옮긴다.

## 워크플로우

OpenSpec의 기본 흐름은 다음과 같다.

### 1. 변경 제안 생성

먼저 어떤 변경을 할지 변경 폴더와 초기 문서를 만든다.

- `/opsx:propose`

더 세분화해서 진행하고 싶다면 먼저 변경 폴더만 만들 수도 있다.

- `/opsx:new`

### 2. 스펙과 작업 문서 정리

변경 제안이 만들어지면 변경 제안서, 변경 스펙, 설계 문서, 작업 목록을 정리한다.

- `/opsx:continue`
- `/opsx:ff`

`/opsx:propose`는 기본 흐름에서 바로 문서를 만들 때 주로 쓰고, `/opsx:ff`는 확장 프로필에서 문서를 빠르게 일괄 생성할 때 사용한다.

### 3. 구현

정리한 작업 목록을 기준으로 실제 구현을 진행한다.

- `/opsx:apply`

### 4. 검증

구현 결과가 문서와 맞는지 확인한다.

- `/opsx:verify`

### 5. 반영 및 정리

완료한 변경 사항을 보관 폴더(archive)로 옮기고 기본 스펙에 반영한다.

- `/opsx:archive`

## 폴더 구조

`openspec init` 이후 프로젝트에는 보통 다음 구조가 생성된다.

```text
openspec/
├── specs/
│   └── <domain>/
│       └── spec.md
├── changes/
│   └── <change-name>/
│       ├── proposal.md
│       ├── design.md
│       ├── tasks.md
│       └── specs/
│           └── <domain>/
│               └── spec.md
└── config.yaml
```

- `specs/`
  현재 시스템 동작을 설명하는 기준 스펙
- `changes/`
  변경 단위별 작업 폴더
- `proposal.md`
  왜 이 변경을 하는지 정리하는 문서
- `design.md`
  구현 방법을 정리하는 문서
- `tasks.md`
  구현 체크리스트
- `changes/<change-name>/specs/`
  무엇이 바뀌는지 기록하는 변경 스펙
