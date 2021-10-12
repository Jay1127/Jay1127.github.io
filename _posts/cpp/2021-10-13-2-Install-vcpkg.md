---
layout: single
title: "C++ : 2. vcpkg 설치 방법"
categories:
 - Cpp
---

### 1. Git에서 `vcpkg` 다운로드

```powershell
> git clone https://github.com/microsoft/vcpkg.git
```

<br/>

### 2. `bootstrap-vcpkg.bat` 배치 파일 실행

![image](https://user-images.githubusercontent.com/38006679/137043258-26188f66-62f2-4c86-8805-09cf44a737c8.png){: .align-center}

<br/>

### 3. 환경변수 등록 후 명령창에서 `vcpkg`입력하여 설치 확인

![image](https://user-images.githubusercontent.com/38006679/137043307-7e4691f9-5395-4b7a-9181-28a8a2aebe9b.png){: .align-center}

<br/>

<div class="notice--info" markdown="1"> 
💡 <strong>패키지 설치 시 참고사항</strong><br/>
`vcpkg`로 패키지를 설치하려면 Visual Studio 언어팩에서 `영문판`이 설치되어 있어야 한다.
</div>