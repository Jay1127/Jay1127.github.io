---
layout: single
title: ".NET : 3. 빌드 이벤트(Build event)로 폴더 또는 파일 복사하기"
categories:
 - CSharp
---

### 빌드 이벤트 스크립트(bulid event script)

```
/*
Data내 모든 폴더, 파일을 CopyData폴더로 복사함.
/Y : 기존에 파일이 있는 경우 덮어씀.
/E : 해당 폴더 구조 내 모든 폴더와 파일을 복사함.
*/

xcopy "$(SolutionDir)..\\Data\\" "$(TargetDir)CopyData\\" /Y /E
xcopy "$(SolutionDir)..\\Data\\*.*" "$(TargetDir)CopyData\\" /Y /E
xcopy "$(SolutionDir)..\\Data" "$(TargetDir)CopyData\\" /Y /E
```

### xcopy명령어 사용법

![image](https://user-images.githubusercontent.com/38006679/135956938-c4f01db2-fc24-449a-a80f-4c32a716ef20.png)
