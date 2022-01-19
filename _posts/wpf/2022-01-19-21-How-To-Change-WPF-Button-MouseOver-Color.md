---
layout: single
title: "WPF : 21. Button에 MouseOver시 배경색 변경하는 법"
categories:
 - WPF
---

`Trigger`를 이용해 마우스가 `Button`위에 있는 경우, 배경색과 글자색을 변경한다.

```xml
<Button Content="Click" 
        FontSize="50" 
        FontWeight="Bold">
    <Button.Style>
        <Style TargetType="{x:Type Button}">
            <Style.Triggers>
                <Trigger Property="IsMouseOver" Value="True">
                    <Setter Property="Background" Value="Red"/>
                    <Setter Property="Foreground" Value="Blue"/>
                </Trigger>
            </Style.Triggers>
        </Style>
    </Button.Style>
</Button>
```

- 기본 상태

![image](https://user-images.githubusercontent.com/38006679/150038371-830f9441-0dae-47d7-975b-54bfae5a2403.png){: .align-center}


<div style="line-height : 0.8">
<br/>
</div>

- `MouseOver`된 경우

`MouseOver`된 경우 글자색은 변경되었지만, 배경색은 지정한 색상으로 변경되지 않았다. `Button`의 자체 `Template`에 지정된 `MouseOver` 색상이 지정돼있어서, `Trigger`를 이용해서 변경할 수 없다.

![image](https://user-images.githubusercontent.com/38006679/150038440-44aed673-962c-46ca-8775-17bb5a454078.png){: .align-center}

## 해결방법

`Button`의 `Template`을 재정의하여 기존의 스타일을 제거한 후 `Trigger`를 적용한다.

<div style="line-height : 0.8">
<br/>
</div>

- 의존 속성 정의
    - `MouseOver`시 지정할 색상을 정의한다.

```csharp
public class SimpleButton : Button
{
    public Brush MouseOverColor
    {
        get { return (Brush)GetValue(MouseOverColorProperty); }
        set { SetValue(MouseOverColorProperty, value); }
    }

    public static readonly DependencyProperty MouseOverColorProperty =
        DependencyProperty.Register("MouseOverColor", typeof(Brush), typeof(SimpleButton),
            new PropertyMetadata(new SolidColorBrush(Colors.Red)));

    public Brush MouseOverBorderColor
    {
        get { return (Brush)GetValue(MouseOverBorderColorProperty); }
        set { SetValue(MouseOverBorderColorProperty, value); }
    }

    public static readonly DependencyProperty MouseOverBorderColorProperty =
        DependencyProperty.Register("MouseOverBorderColor", typeof(Brush), typeof(SimpleButton),
            new PropertyMetadata(new SolidColorBrush(Colors.Red)));
}
```

- `Template` 정의

```xml
<Style TargetType="{x:Type local:SimpleButton}">
    <Setter Property="Template">
        <Setter.Value>
            <ControlTemplate TargetType="{x:Type local:SimpleButton}">
                <Grid>
                    <Border x:Name="baseBorder"
                            Width="{TemplateBinding Width}"
                            Height="{TemplateBinding Height}"
                            BorderBrush="{TemplateBinding BorderBrush}"
                            BorderThickness="{TemplateBinding BorderThickness}"
                            Background="{TemplateBinding Background}"/>
                    <ContentPresenter HorizontalAlignment="Center"
                                      VerticalAlignment="Center"/>
                </Grid>
                <ControlTemplate.Triggers>
                    <Trigger Property="IsMouseOver" Value="True">
                        <Setter TargetName="baseBorder" 
                                Property="Background" 
                                Value="{Binding MouseOverColor, RelativeSource={RelativeSource TemplatedParent}}"/>
                        <Setter TargetName="baseBorder" 
                                Property="BorderBrush" 
                                Value="{Binding MouseOverBorderColor, RelativeSource={RelativeSource TemplatedParent}}"/>
                    </Trigger>
                </ControlTemplate.Triggers>
            </ControlTemplate>                
        </Setter.Value>
    </Setter>
</Style>
```

- 사용법

```xml
<local:SimpleButton MouseOverColor="Red" 
                    MouseOverBorderColor="Green" 
                    Content="Click" 
                    FontSize="50" 
                    FontWeight="Bold"/>
```

- `MouseOver`된 경우

![image](https://user-images.githubusercontent.com/38006679/150038779-a55cacca-a97d-48b8-a64c-2dcdac39bda6.png){: .align-center}