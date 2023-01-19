---
layout: single
title: "WPF : 5. CheckBox의 체크 마크 색상 바꾸는 법"
description: CheckBox의 체크 마크 색상 바꾸는 법
categories:
 - WPF
---

`CheckBox`는 체크 마크의 색상에 대한 프로퍼티를 가지고 있지 않다. 따라서, 체크 마크의 색상을 바꾸려면 `CheckBox`의 `Template`을 새로 정의해야 한다.

## 의존속성(Dependency Property) 정의

체크 마크의 색상을 지정할 프로퍼티를 정의한다. 

```csharp
public class SimpleCheckBox : CheckBox
{
    public SolidColorBrush AccentColor
    {
        get { return (SolidColorBrush)GetValue(AccentColorProperty); }
        set { SetValue(AccentColorProperty, value); }
    }
    
    public static readonly DependencyProperty AccentColorProperty =
        DependencyProperty.Register("AccentColor", typeof(SolidColorBrush), typeof(SimpleCheckBox),
            new PropertyMetadata(new SolidColorBrush(Colors.Red)));
}
```

## Template 정의

`BulletDecorator`를 이용하여 `CheckBox`의 `Template`을 재정의한다. `Bullet`은 체크마크 영역이며, `Child`는 `Content`를 표시하는 영역을 나타낸다. 체크 마크의 색상을 변경하려면 `Bullet`에 정의된 `Path`의 색상을 미리 정의한 의존속성과 바인딩하면 된다.

```xml
<Style TargetType="{x:Type local:SimpleCheckBox}">
    <Setter Property="Height" Value="15"/>
    <Setter Property="Template">
        <Setter.Value>
            <ControlTemplate TargetType="{x:Type local:SimpleCheckBox}">
                <BulletDecorator Background="Transparent"
                                 VerticalAlignment="{TemplateBinding VerticalContentAlignment}" 
                                 HorizontalAlignment="{TemplateBinding HorizontalContentAlignment}">
                    <BulletDecorator.Bullet>
                        <Border x:Name="Border"
                                Width="15"
                                Height="15"
                                CornerRadius="0"
                                BorderThickness="{TemplateBinding BorderThickness}"
                                BorderBrush="{TemplateBinding BorderBrush}"
                                Background="{TemplateBinding Background}">
                            <Grid>
                                <Path Visibility="Visible"
                                  Width="Auto"
                                  Height="Auto"
                                  x:Name="CheckMark"
                                  SnapsToDevicePixels="False"
                                  StrokeThickness="2" 
                                  Stretch="Fill"
                                  Data="M 0 3 L 5.7 13 M 4.9 13 L 12 0"
                                  Stroke="{Binding AccentColor, RelativeSource={RelativeSource TemplatedParent}}">
                                </Path>
                            </Grid>
                        </Border>
                    </BulletDecorator.Bullet>
                    <ContentPresenter Margin="4,0,0,0"/>
                </BulletDecorator>
                <ControlTemplate.Triggers>
                    <Trigger Property="IsChecked" Value="false">
                        <Setter TargetName="CheckMark" Property="Visibility" Value="Collapsed"/>
                    </Trigger>
                </ControlTemplate.Triggers>
            </ControlTemplate>
        </Setter.Value>
    </Setter>
</Style>
```

## 사용법

```xml
<local:SimpleCheckBox Content="ColoredCheckBox" 
                      IsChecked="True" 
                      AccentColor="Blue"/>
```

![image](https://user-images.githubusercontent.com/38006679/147318392-938d8ff8-2e29-410e-b006-25046ff7fd01.png){: .align-center}
