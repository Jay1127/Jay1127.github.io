---
layout: single
title: "WPF : 24. ScrollBar 커스터마이징(Template)"
categories:
 - WPF
---

## **ScrollBar Template 정의**

- `ScrollBar`의 `Template`을 이미지처럼 두 개의 `RepeatButton`과 `Track`으로 구성한다.
- `Template`을 구성하는 `Control`의 `Template`과 `Style`을 변경하여 외형을 수정한다.
- `ScrollBar`의 기존 동작을 가져오기 위해서, `Track`은 `ScrollBar`의 `TemplatePart`에 지정된 이름을 명시하고, 각 `Button`은 `ScroolBar`에 정의된 `Command`를 연결한다.

![image](https://user-images.githubusercontent.com/38006679/155634062-17416c7b-c326-4824-ba5e-97ae1b1cacdd.png){: .align-center}

```xml
<!-- ScrollBar Template 정의 -->
<ControlTemplate x:Key="VerticalScrollBar"
                 TargetType="{x:Type ScrollBar}">
    <Grid Background="LightGray">
        <Grid.RowDefinitions>
            <RowDefinition MaxHeight="{DynamicResource {x:Static SystemParameters.VerticalScrollBarButtonHeightKey}}" />
            <RowDefinition Height="0.00001*" />
            <RowDefinition MaxHeight="{DynamicResource {x:Static SystemParameters.VerticalScrollBarButtonHeightKey}}" />
        </Grid.RowDefinitions>
        <RepeatButton Content="▲"
                      Style="{StaticResource LineButtonStyle}"
                      Command="ScrollBar.LineUpCommand" />
        <Track Grid.Row="1"
               x:Name="PART_Track"
               IsDirectionReversed="True">
            <Track.DecreaseRepeatButton>
                <RepeatButton Command="ScrollBar.PageUpCommand"
                              Style="{StaticResource PageButtonStyle}" />
            </Track.DecreaseRepeatButton>
            <Track.Thumb>
                <Thumb Background="SkyBlue" />
            </Track.Thumb>
            <Track.IncreaseRepeatButton>
                <RepeatButton Command="ScrollBar.PageDownCommand"
                              Style="{StaticResource PageButtonStyle}" />
            </Track.IncreaseRepeatButton>
        </Track>
        <RepeatButton Grid.Row="2"
                      Content="▼"
                      Style="{StaticResource LineButtonStyle}"
                      Command="ScrollBar.LineDownCommand" />
    </Grid>
</ControlTemplate>

<!-- Track의 RepeatButton Template 정의 -->
<Style TargetType="{x:Type RepeatButton}" x:Key="PageButtonStyle">
    <Setter Property="Focusable"
            Value="False" />
    <Setter Property="Template">
        <Setter.Value>
            <ControlTemplate TargetType="{x:Type RepeatButton}">
                <Border Background="Transparent" />
            </ControlTemplate>
        </Setter.Value>
    </Setter>
</Style>

<!-- 최상단,하단의 RepeatButton Template 정의 -->
<Style TargetType="{x:Type RepeatButton}"
       x:Key="LineButtonStyle">
    <Setter Property="Focusable"
            Value="False" />
    <Setter Property="TextElement.Foreground"
            Value="Blue" />
    <Setter Property="Template">
        <Setter.Value>
            <ControlTemplate TargetType="{x:Type RepeatButton}">
                <Border Background="SkyBlue"
                        BorderBrush="Black"
                        BorderThickness="1"
                        CornerRadius="3">
                    <ContentPresenter HorizontalAlignment="Center"
                                      VerticalAlignment="Center" />
                </Border>
            </ControlTemplate>
        </Setter.Value>
    </Setter>
</Style>

<Style TargetType="{x:Type ScrollBar}">
    <Style.Triggers>
        <Trigger Property="Orientation"
                 Value="Vertical">
            <Setter Property="Width"
                    Value="18" />
            <Setter Property="Height"
                    Value="Auto" />
            <Setter Property="Template"
                    Value="{StaticResource VerticalScrollBar}" />
        </Trigger>
    </Style.Triggers>
</Style>
```

```xml
<Border BorderBrush="Black"
        BorderThickness="1">
    <ScrollViewer>
        <Grid Height="5000"/>
    </ScrollViewer>
</Border>
```
<div style="line-height : 0.3">
<br/>
</div>

<div class="notice--info" markdown="1"> 
💡 `<RowDefinition Height="0.00001*" />`를 지정한 이유
<div style="line-height : 0.3">
<br/>
</div>

[https://stackoverflow.com/questions/31124249/odd-row-column-dimensions-in-scrollbar-template](https://stackoverflow.com/questions/31124249/odd-row-column-dimensions-in-scrollbar-template)
</div>