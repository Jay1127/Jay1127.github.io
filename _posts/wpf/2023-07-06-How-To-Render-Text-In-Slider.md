---
layout: single
title: "WPF : 31. Slider에 텍스트 표시하는 법"
description: Slider에 텍스트 표시하는 법
categories:
 - WPF
---


## TextRenderSlider, TextRenderTickBar 구현

`Slider`에 표시할 텍스트 목록을 속성으로 정의한다. `TickBar`에도 동일하게 속성을 정의해주며, `OnRender`함수를 오버라이드해서 표시할 텍스트를 그려준다.

```csharp
public class TextRenderSlider : Slider
{
    // 슬라이더에 표시할 텍스트
    public ObservableCollection<string> Texts
    {
        get { return (ObservableCollection<string>)GetValue(TextsProperty); }
        set { SetValue(TextsProperty, value); }
    }

    public static readonly DependencyProperty TextsProperty =
        DependencyProperty.Register("Texts", typeof(ObservableCollection<string>), typeof(TextRenderSlider),
            new FrameworkPropertyMetadata(null, new PropertyChangedCallback(OnTextsPropertyChanged)));

    private static void OnTextsPropertyChanged(DependencyObject o, DependencyPropertyChangedEventArgs e)
    {

    }
}

public class TextRenderTickBar : TickBar
{
    // 틱바에 표시할 텍스트
    public ObservableCollection<string> Texts
    {
        get { return (ObservableCollection<string>)GetValue(TextsProperty); }
        set { SetValue(TextsProperty, value); }
    }

    public static readonly DependencyProperty TextsProperty =
        DependencyProperty.Register("Texts", typeof(ObservableCollection<string>), typeof(TextRenderTickBar),
            new FrameworkPropertyMetadata(null, new PropertyChangedCallback(OnTextsPropertyChanged)));

    private static void OnTextsPropertyChanged(DependencyObject o, DependencyPropertyChangedEventArgs e)
    {
        var control = o as TextRenderTickBar;
        control.InvalidateVisual();
    }

    protected override void OnRender(DrawingContext dc)
    {
        if (Texts is null)
        {
            return;
        }

        double range = this.Maximum - this.Minimum;

        for (int i = 0; i <= range; i += (int)TickFrequency)
        {
            if (i >= Texts.Count)
            {
                continue;
            }

            var text = Texts[i];
            var formattedText = new FormattedText(
                text,
                CultureInfo.GetCultureInfo("en-us"),
                FlowDirection.LeftToRight,
                new Typeface("Verdana"),
                15,
                Brushes.Black,
                VisualTreeHelper.GetDpi(this).PixelsPerDip);
            formattedText.TextAlignment = TextAlignment.Center;
						
            // 표시할 좌표 계산
            var x = ReservedSpace * 0.5 + (ActualWidth - ReservedSpace) / (range / TickFrequency) * i;
            dc.DrawText(formattedText, new Point(x, 5));
        }

        base.OnRender(dc);
    }
}
```

`Slider`의 `Template`을 정의하고, 미리 정의한 `Texts`속성에 표시할 텍스트를 바인딩한다.

```xml
<Grid>
    <Grid.Resources>
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

        <Style x:Key="CircularSlider" TargetType="{x:Type local:TextRenderSlider}">
            <Setter Property="SnapsToDevicePixels" Value="true" />
            <Setter Property="OverridesDefaultStyle" Value="true" />
            <Setter Property="IsTabStop" Value="false" />
            <Setter Property="Focusable" Value="false" />
            <Setter Property="TickPlacement" Value="Both"/>
            <Setter Property="Template">
                <Setter.Value>
                    <ControlTemplate TargetType="{x:Type local:TextRenderSlider}">
                        <Grid>
                            <Grid.RowDefinitions>
                                <RowDefinition Height="Auto" />
                                <RowDefinition Height="Auto"
                                               MinHeight="{TemplateBinding MinHeight}" />
                                <RowDefinition Height="Auto" />
                            </Grid.RowDefinitions>
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
                            <!-- 텍스트를 표시할 TickBar 선언 및 바인딩 -->
                            <local:TextRenderTickBar x:Name="BottomTick"
                                                     Texts="{TemplateBinding Texts}"
                                                     SnapsToDevicePixels="True"
                                                     Grid.Row="2"
                                                     Fill="{TemplateBinding Foreground}"
                                                     Placement="Bottom"
                                                     Height="4"
                                                     Visibility="Collapsed" />
                        </Grid>
                        <ControlTemplate.Triggers>
                            <Trigger Property="TickPlacement" Value="BottomRight">
                                <Setter TargetName="BottomTick"
                                        Property="Visibility"
                                        Value="Visible" />
                            </Trigger>
                            <Trigger Property="TickPlacement" Value="Both">
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
    
    <!-- Slider 선언 및 표시할 텍스트 바인딩 -->
    <local:TextRenderSlider TickPlacement="Both"
                            Margin="20"
                            Style="{StaticResource CircularSlider}"
                            Texts="{Binding TickTexts}"/>
</Grid>
```

![image](https://github.com/Jay1127/Jay1127.github.io/assets/38006679/2fc6adc0-7142-48cd-85cd-51478c004fbb)