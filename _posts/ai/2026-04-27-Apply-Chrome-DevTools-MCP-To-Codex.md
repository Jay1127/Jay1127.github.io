---
layout: single
title: "AI : 5. Chrome DevTools MCP를 Codex에 적용하는 법"
description: VS Code Codex에서 Chrome DevTools MCP 설치 및 옵션 정리
date: 2026-04-27 10:00:00 +0900
series_order: 5
categories:
 - AI
---

`Chrome DevTools MCP`는 Codex가 실제 Chrome 브라우저를 열고 화면, 콘솔, 네트워크, 성능 정보를 확인할 수 있게 해주는 MCP 서버다.

[https://github.com/ChromeDevTools/chrome-devtools-mcp](https://github.com/ChromeDevTools/chrome-devtools-mcp)


## 설치

VS Code Codex에서는 설정 화면에서 MCP 서버를 추가할 수 있다.  
아래 예시는 Windows 환경에서 Chrome DevTools MCP를 `STDIO` 서버로 등록하는 방법이다.

### 사전 준비

Chrome DevTools MCP를 사용하려면 다음이 필요하다.

- Node.js 20.19 이상
- npm
- 최신 안정 버전의 Chrome

### VS Code Codex에서 추가

1. VS Code 하단 패널에서 `CODEX` 탭을 연다.

2. 오른쪽 위의 톱니바퀴 버튼을 눌러 `Codex 설정`을 연다.

    ![VS Code Codex 설정 열기](/assets/images/chrome-devtools-mcp-open-codex-settings.png){: .align-center}{: width="900"}

3. 왼쪽 메뉴에서 `MCP 서버`를 선택한다.

4. `서버 추가`를 누른다.

    ![MCP 서버 목록과 서버 추가 버튼](/assets/images/chrome-devtools-mcp-server-list.png){: .align-center}{: width="900"}

5. 서버 유형과 설정값을 입력한다.

    - 서버 유형: `STDIO`
    - 서버 이름: `chrome-devtools`
    - 실행 명령: `C:\Program Files\nodejs\npx.cmd`
    - 인자: `-y`와 `chrome-devtools-mcp@latest`를 각각 추가한다.
    - 환경 변수: 비워둔다.
    - 작업 중인 디렉터리: 비워둔다.

    ![Chrome DevTools MCP 서버 설정](/assets/images/chrome-devtools-mcp-server-settings.png){: .align-center}{: width="900"}

6. 저장한 뒤 토글이 켜져 있는지 확인한다.

7. VS Code를 다시 실행하거나 Codex 확장을 새로고침한다.

여기까지 설정하면 VS Code Codex에서 Chrome DevTools MCP를 사용할 수 있다.

Chrome이 실행되지 않으면 환경 변수에 `SystemRoot`와 `PROGRAMFILES`를 추가해야 할 수 있다.  
이 경우 공식 Codex MCP 문서의 Windows 설정 예시를 확인한다.

## 자주 쓰는 옵션

Chrome DevTools MCP는 `인자` 항목에 실행 옵션을 추가할 수 있다.

- `--headless=true`
  브라우저 창을 띄우지 않고 실행한다.
- `--isolated=true`
  임시 Chrome 프로필을 사용한다.
- `--no-usage-statistics`
  사용 통계 수집을 끈다.
- `--no-performance-crux`
  성능 분석 중 CrUX 데이터를 요청하지 않는다.

예를 들어, 임시 Chrome 프로필을 사용하려면 인자를 다음과 같이 추가한다.

```text
-y
chrome-devtools-mcp@latest
--isolated=true
```

브라우저 창을 띄우지 않으려면 다음과 같이 입력한다.

```text
-y
chrome-devtools-mcp@latest
--headless=true
```

## 사용 방법

설정이 끝나면 Codex에게 다음처럼 요청한다.

```text
http://localhost:4000 페이지를 열어서 콘솔 에러와 화면 렌더링을 확인해줘.
```

```text
http://localhost:4000 페이지의 LCP와 네트워크 요청을 확인해줘.
```
