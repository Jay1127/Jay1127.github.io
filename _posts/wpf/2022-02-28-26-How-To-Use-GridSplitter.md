---
layout: single
title: "WPF : 26. GridSplitter 사용법"
description: GridSplitter 사용법
categories:
 - WPF
---

### GridSplitter로 Grid의 열 크기 조절하는 법

1. 크기 조절할 `Grid`의 열 사이에 `GridSplitter`를 추가한다.(COL1)
2. 열의 크기를 조절할 경우 `HorizontalAlignment="Center" VerticalAlignment="Stretch"`로 설정한다. (행의 크기를 조절할 경우 `HorizontalAlignment="Stretch" VerticalAlignment="Center"`로 설정한다.)

![image](https://user-images.githubusercontent.com/38006679/155905368-5f0dd894-38f6-4a48-bb7e-fc9a57736633.png)


### 소스코드

```xml
<Grid.ColumnDefinitions>
    <ColumnDefinition/>
    <ColumnDefinition Width="Auto" />
    <ColumnDefinition/>
</Grid.ColumnDefinitions>
```

```xml
<GridSplitter Grid.Column="1"
              HorizontalAlignment="Center"
              VerticalAlignment="Stretch"
              Width="5"/>
```

### 참고

[https://docs.microsoft.com/ko-kr/dotnet/framework/wpf/controls/how-to-resize-columns-with-a-gridsplitter](https://docs.microsoft.com/ko-kr/dotnet/framework/wpf/controls/how-to-resize-columns-with-a-gridsplitter)