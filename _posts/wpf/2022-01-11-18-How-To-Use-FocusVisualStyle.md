---
layout: single
title: "WPF : 18. FocusVisualStyle 사용법"
description: FocusVisualStyle 사용법
categories:
 - WPF
---

```xml
<StackPanel Orientation="Horizontal"
            HorizontalAlignment="Center"
            VerticalAlignment="Center">
    <StackPanel.Resources>
        <Style x:Key="ButtonFocusVisual" TargetType="{x:Type Control}">
            <Setter Property="Template">
                <Setter.Value>
                    <ControlTemplate>
                        <Rectangle Margin="2"
                                   Stroke="Red"
                                   StrokeThickness="2" 
                                   StrokeDashArray="1 2"/>
                    </ControlTemplate>
                </Setter.Value>
            </Setter>
        </Style>
        
        <Style TargetType="{x:Type Button}">
            <Setter Property="Width"
                    Value="60" />
            <Setter Property="Height"
                    Value="60" />
            <Setter Property="Margin"
                    Value="20" />
        </Style>
    </StackPanel.Resources>

    <Button Content="Defualt" />
    <Button Content="Style" FocusVisualStyle="{StaticResource ButtonFocusVisual}"/>
    <Button Content="Null" FocusVisualStyle="{x:Null}"/>
</StackPanel>
```

- 기본값인 경우

![image](https://user-images.githubusercontent.com/38006679/148856665-767922f5-61a4-4e73-bb36-2a0768db1231.png){: .align-center}

- 스타일 적용한 경우

![image](https://user-images.githubusercontent.com/38006679/148856693-e011d290-8f9a-4898-b0d4-915bf6db8c50.png){: .align-center}

- Null값인 경우

![image](https://user-images.githubusercontent.com/38006679/148856717-3b78f396-158f-4204-a4e9-a8218301eab4.png){: .align-center}