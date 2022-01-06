---
layout: single
title: "WPF : 14. RadioButton을 ToggleButton형태로 만드는 법"
categories:
 - WPF
---


`Template`을 따로 정의하지 않고, `ToggleButton`처럼 보이는 `RadioButton`을 만들여면, `Style`에 `ToggleButton`타입을 지정하면 된다.

```xml
<RadioButton Content="라디오 토글 버튼" 
             Style="{StaticResource {x:Type ToggleButton}}" 
             HorizontalAlignment="Center" 
             VerticalAlignment="Center"/>
```

![image](https://user-images.githubusercontent.com/38006679/148468702-cccf77ce-2f51-40a9-8f51-67a1bec780f1.png){: .align-center}

추가적은 속성을 스타일에 추가하려면 `BaseOn`속성에 타입을 지정해주면 된다.

```xml
<StackPanel.Resources>
    <Style x:Key="toggleBtn" TargetType="{x:Type RadioButton}" 
           BasedOn="{StaticResource {x:Type ToggleButton}}">
        <Setter Property="Foreground" Value="White"/>
    </Style>
</StackPanel.Resources>

<RadioButton Content="라디오 토글 버튼" 
             Style="{StaticResource toggleBtn}" 
             HorizontalAlignment="Center" 
             VerticalAlignment="Center"/>
```