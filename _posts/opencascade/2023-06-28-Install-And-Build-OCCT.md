---
layout: single
title: "OCCT : 1. Opencascade 설치 및 빌드(Visual Studio)"
description: Opencascade 설치 및 빌드(Visual Studio)
categories:
 - opencascade
---

[사이트](https://dev.opencascade.org/release)에서 윈도우용 OCCT 인스톨러를 다운로드 후 설치한다.

![image](https://github.com/Jay1127/Jay1127.github.io/assets/38006679/6c7de7c5-c7b3-4581-9a58-fccd26106119){: .align-center}{: width="500"}

<br/>

CMake에 소스 코드 경로(OCCT 설치 경로)와 빌드 파일을 생성할 위치를 지정한다.

![image](https://github.com/Jay1127/Jay1127.github.io/assets/38006679/dc2e2e34-5178-42aa-997e-a8882236e03f){: .align-center}{: width="700"}

<br/>

`Configure`버튼을 누른 후 Visual Studio의 버전을 명시한다.

![image](https://github.com/Jay1127/Jay1127.github.io/assets/38006679/1dc37c6a-7ba9-40e2-b213-e1215e0d4fb8){: .align-center}{: width="700"}

<br/>

다음과 같은 에러가 발생하면 `3RDPARTY_DIR`을 OCCT 설치 경로로 지정한다. 지정 후 `Configure`하면 나머지 경로는 자동으로 입력된다.

![image](https://github.com/Jay1127/Jay1127.github.io/assets/38006679/32761f82-a39d-45ef-bf73-53cf4880c6c9){: .align-center}{: width="700"}

![image](https://github.com/Jay1127/Jay1127.github.io/assets/38006679/55be4cf8-c7cf-497b-baa1-bcbe92f4c7ec){: .align-center}{: width="700"}

<br/>

`Generate`하면 Visual Studio 프로젝트 파일이 생성된다.

![image](https://github.com/Jay1127/Jay1127.github.io/assets/38006679/fe682956-9800-44b9-8b35-9c773f9dc906){: .align-center}{: width="500"}

<br/>

`ALL_BUILD`프로젝트를 빌드하면 라이브러리 파일을 생성된다.

![image](https://github.com/Jay1127/Jay1127.github.io/assets/38006679/8a92e867-1796-4403-aad9-4fbbf3d73e30){: .align-center}{: width="350"}