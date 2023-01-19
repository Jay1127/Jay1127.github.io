---
layout: single
title: ".NET : 2. Dialog의 Filter 설정하는 법"
description: Dialog의 Filter 설정하는 법
categories:
 - CSharp
---

## 사용 방법

```csharp
dialog.Filter = "표시할 이름1|*.확장자1|표시할 이름2|*.확장자2-1; *.확장자2-2|모든파일|*.*;
```
<br/>

- 예시 1

```csharp
dialog.Filter = "stl files (*.stl)|*.stl|obj files (*.obj)|*.obj";
```

![image](https://user-images.githubusercontent.com/38006679/135944983-f785e82b-6ea7-4e0f-b973-1e4b3f6bc6e9.png){: .align-center}

<br/>
- 예시 2

```csharp
dialog.Filter = "3d files(*.stl; *obj)|*.stl; *obj";
```

![image](https://user-images.githubusercontent.com/38006679/135945003-4b22bc69-b97e-4ae1-b559-96141a931939.png){: .align-center}