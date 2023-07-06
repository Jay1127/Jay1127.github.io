---
layout: single
title: "WPF : 30. Slider 커스터마이징(Template)"
description: Slider 커스터마이징(Template)
categories:
 - WPF
---

## Slider Template 정의

`Slider`의 `Template`은 다음과 같은 컨트롤로 구성되며, 각 컨트롤의 `Template`을 변경하여 외형을 커스터마이징한다.

- TickBar(Top, Bottom)
- Track
    - RepeatButton(Increase, Decrease)
    - Thumb

![image](https://github.com/Jay1127/Jay1127.github.io/assets/38006679/a91e8ef5-3828-49a0-8548-4993adf169fb){: .align-center}{: width="300"}

<br/>

```xml
<Grid>
    <Grid.Resources>
        <!-- TrackBar의 RepeatButton 외형 변경 -->
        <Style x:Key="SliderRepeatButton" TargetType="{x:Type RepeatButton}">
            <Setter Property="SnapsToDevicePixels" Value="true" />
            <Setter Property="OverridesDefaultStyle" Value="true" />
            <Setter Property="IsTabStop" Value="false" />
            <Setter Property="Focusable" Value="false" />
            <Setter Property="Template">
                <Setter.Value>
                    <ControlTemplate TargetType="{x:Type RepeatButton}">
                        <Border  BorderThickness="1" BorderBrush="Black" Background="Black" Height="3"/>
                    </ControlTemplate>
                </Setter.Value>
            </Setter>
        </Style>

        <!-- TrackBar의 Thumb 외형 변경 -->
        <Style x:Key="SliderThumb" TargetType="{x:Type Thumb}">
            <Setter Property="SnapsToDevicePixels" Value="true" />
            <Setter Property="OverridesDefaultStyle" Value="true" />
            <Setter Property="IsTabStop" Value="false" />
            <Setter Property="Focusable" Value="false" />
            <Setter Property="Template">
                <Setter.Value>
                    <ControlTemplate TargetType="{x:Type Thumb}">
                        <Ellipse Width="15" Height="15" Fill="Red"/>
                    </ControlTemplate>
                </Setter.Value>
            </Setter>
        </Style>

        <Style x:Key="CircularSlider" TargetType="{x:Type Slider}">
            <Setter Property="SnapsToDevicePixels" Value="true" />
            <Setter Property="OverridesDefaultStyle" Value="true" />
            <Setter Property="IsTabStop" Value="false" />
            <Setter Property="Focusable" Value="false" />
            <Setter Property="Template">
                <Setter.Value>
                    <ControlTemplate TargetType="{x:Type Slider}">
                        <Grid>
                            <Grid.RowDefinitions>
                                <RowDefinition Height="Auto" />
                                <RowDefinition Height="Auto"
                                       MinHeight="{TemplateBinding MinHeight}" />
                                <RowDefinition Height="Auto" />
                            </Grid.RowDefinitions>
                            <TickBar x:Name="TopTick"
                                     SnapsToDevicePixels="True"
                                     Placement="Top"
                                     Height="4"
                                     Visibility="Collapsed"/>
                            <Track Grid.Row="1" x:Name="PART_Track">
                                <Track.DecreaseRepeatButton>
                                    <RepeatButton Command="Slider.DecreaseLarge" Style="{StaticResource SliderRepeatButton}" />
                                </Track.DecreaseRepeatButton>
                                <Track.Thumb>
                                    <Thumb Style="{StaticResource SliderThumb}"/>
                                </Track.Thumb>
                                <Track.IncreaseRepeatButton>
                                    <RepeatButton Command="Slider.IncreaseLarge" Style="{StaticResource SliderRepeatButton}" />
                                </Track.IncreaseRepeatButton>
                            </Track>
                            <TickBar x:Name="BottomTick"
                                     SnapsToDevicePixels="True"
                                     Grid.Row="2"
                                     Fill="{TemplateBinding Foreground}"
                                     Placement="Bottom"
                                     Height="4"
                                     Visibility="Collapsed" />
                        </Grid>
                        <ControlTemplate.Triggers>
                            <Trigger Property="TickPlacement" Value="TopLeft">
                                <Setter TargetName="TopTick"
                                        Property="Visibility"
                                        Value="Visible" />
                            </Trigger>
                            <Trigger Property="TickPlacement" Value="BottomRight">
                                <Setter TargetName="BottomTick"
                                        Property="Visibility"
                                        Value="Visible" />
                            </Trigger>
                            <Trigger Property="TickPlacement" Value="Both">
                                <Setter TargetName="TopTick"
                                        Property="Visibility"
                                        Value="Visible" />
                                <Setter TargetName="BottomTick"
                                        Property="Visibility"
                                        Value="Visible" />
                            </Trigger>
                        </ControlTemplate.Triggers>
                    </ControlTemplate>
                </Setter.Value>
            </Setter>
        </Style>
    </Grid.Resources>

    <Slider TickPlacement="Both"
            VerticalAlignment="Center"
            Style="{StaticResource CircularSlider}"/>
</Grid>
```

![image](https://github.com/Jay1127/Jay1127.github.io/assets/38006679/4d575102-12c7-403e-be1a-82dd5d37c833){: .align-center}