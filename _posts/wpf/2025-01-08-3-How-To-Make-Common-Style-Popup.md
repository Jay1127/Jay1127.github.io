---
layout: single
title: "WPF : 37. 공통 스타일 윈도우(팝업) 만드는 법"
description: Make common style window popup in wpf
categories:
 - WPF
---

```csharp
[TemplatePart(Name = "PART_CloseButton", Type = typeof(Button))]
public class DialogShell : Window
{
    static DialogShell()
    {
        DefaultStyleKeyProperty.OverrideMetadata(typeof(DialogShell), new FrameworkPropertyMetadata(typeof(DialogShell)));
    }

    public DialogShell()
    {
    }

    public override void OnApplyTemplate()
    {
        base.OnApplyTemplate();

        var closeButton = GetTemplateChild("PART_CloseButton") as Button;
        closeButton.Click += (s, e) => Close();
    }
}
```

<br/>

```xml
<Style TargetType="{x:Type local:DialogShell}"
       x:Key="">
    <Setter Property="WindowStyle"
            Value="None" />
    <Setter Property="ResizeMode"
            Value="NoResize" />
    <Setter Property="WindowChrome.WindowChrome">
        <Setter.Value>
            <WindowChrome CaptionHeight="50" />
        </Setter.Value>
    </Setter>
    <Setter Property="Template">            
        <Setter.Value>
            <ControlTemplate TargetType="{x:Type local:DialogShell}">
                <AdornerDecorator>
                    <Border BorderBrush="Black"
                            BorderThickness="1"
                            Background="White">
                        <Grid>
                            <Grid.RowDefinitions>
                                <RowDefinition Height="50" />
                                <RowDefinition />
                            </Grid.RowDefinitions>

                            <Grid>
                                <Border Background="Brown" />
                                <TextBlock Text="{TemplateBinding Title}"/>
                                <Button x:Name="PART_CloseButton"
                                        Content="x"
                                        Width="30"
                                        Height="30"
                                        HorizontalAlignment="Right"
                                        Margin="0,0,10,0" />
                            </Grid>

                            <ContentPresenter Grid.Row="1" />
                        </Grid>
                    </Border>
                </AdornerDecorator>
            </ControlTemplate>
        </Setter.Value>
    </Setter>
</Style>
```