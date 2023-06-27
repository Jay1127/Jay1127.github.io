---
layout: single
title: ".NET : 10. Error - Inspection of unmanaged type '*' requires unmanaged debugging to be enabled."
description: C++ 디버깅 에러
categories:
 - CSharp
---

C# 또는 C++/CLI 프로젝트에서 C++코드를 디버깅할 경우, 조사식에 다음과 같은 메세지가 출력되면서, 속성값을 확인할 수 없는 경우가 생긴다.

```
Inspection of unmanaged type '*' requires unmanaged debugging to be enabled. Please set the debugger type to 'Mixed' and try again
```

다음과 같이 설정하면, 디버깅할 때 C++코드의 내용을 확인할 수 있다.

- Project → Properties → Debug → Check “Enable native code debugging” (프로젝트 → 속성 → 디버그 → 네이티브 코드 디버깅 사용 체크)

![image](https://github.com/Jay1127/Jay1127.github.io/assets/38006679/099d60bc-d470-482f-9254-46a7f4d97261){: .align-center}