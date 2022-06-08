---
layout: single
title: ".NET : 8. xcopy로 파일 복사 시, 파일 또는 디렉터리인지 물어보는 메세지 제외하는 법"
categories:
 - CSharp
---

다음과 같이 빌드 이벤트에서 `xcopy`명령어를 이용해서 파일을 복사하려는 경우, 파일 또는 디렉터리인지 물어보는 메세지를 출력하고, 파일이 복사되지 않는다.

```
xcopy "$(SolutionDir)\..\..\..\Data\A.dll" "$(TargetDir)\A.dll" /Y /I /E

> A.dll은 대상의 파일 이름입니까 아니면 디렉터리 이름입니까?
```

빌드 이벤트를 다음과 같이 수정하면, 메세지를 출력하지 않고 파일을 복사할 수 있다.

```
// 방법 1
xcopy "$(SolutionDir)\..\..\..\Data\A.dll" "$(TargetDir)\A.*" /Y /I /E

// 방법 2
xcopy "$(SolutionDir)\..\..\..\Data\A.dll" "$(TargetDir)\" /Y /I /E
```