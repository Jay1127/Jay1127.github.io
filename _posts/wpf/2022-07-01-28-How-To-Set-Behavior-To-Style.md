---
layout: single
title: "WPF : 28. Style에 Behavior 설정하는 법"
categories:
 - WPF
---


```csharp
public class Behaviors : List<Behavior>
{
}

public class Triggers : List<TriggerBase>
{
}

public static class SupplementaryInteraction
{
    public static Behaviors GetBehaviors(DependencyObject obj)
    {
        return (Behaviors)obj.GetValue(BehaviorsProperty);
    }

    public static void SetBehaviors(DependencyObject obj, Behaviors value)
    {
        obj.SetValue(BehaviorsProperty, value);
    }

    public static readonly DependencyProperty BehaviorsProperty =
        DependencyProperty.RegisterAttached(
            "Behaviors",
            typeof(Behaviors),
            typeof(SupplementaryInteraction),
            new UIPropertyMetadata(null, OnPropertyBehaviorsChanged));

    private static void OnPropertyBehaviorsChanged(DependencyObject d, DependencyPropertyChangedEventArgs e)
    {
        var behaviors = Interaction.GetBehaviors(d);
        foreach (var behavior in e.NewValue as Behaviors) behaviors.Add(behavior);
    }

    public static Triggers GetTriggers(DependencyObject obj)
    {
        return (Triggers)obj.GetValue(TriggersProperty);
    }

    public static void SetTriggers(DependencyObject obj, Triggers value)
    {
        obj.SetValue(TriggersProperty, value);
    }

    public static readonly DependencyProperty TriggersProperty =
          DependencyProperty.RegisterAttached(
               "Triggers",
               typeof(Triggers),
               typeof(SupplementaryInteraction),
               new UIPropertyMetadata(null, OnPropertyTriggersChanged));

    private static void OnPropertyTriggersChanged(DependencyObject d, DependencyPropertyChangedEventArgs e)
    {
        var triggers = Interaction.GetTriggers(d);
        foreach (var trigger in e.NewValue as Triggers) triggers.Add(trigger);
    }
}
```

```xml
<Grid>
    <Grid.Resources>
        <local:Behaviors x:Key="Behaviors" x:Shared="False">
            <local:TextBoxBehavior/>                
        </local:Behaviors>
        
        <Style TargetType="{x:Type TextBox}" x:Key="TextBoxStyle">
            <Setter Property="local:SupplementaryInteraction.Behaviors" Value="{StaticResource Behaviors}"/>
        </Style>
    </Grid.Resources>

    <TextBox Text="" Style="{StaticResource ResourceKey=TextBoxStyle}"/>
    <TextBox Text="" Style="{StaticResource ResourceKey=TextBoxStyle}"/>
    <TextBox Text="" Style="{StaticResource ResourceKey=TextBoxStyle}"/>
</Grid>
```

<br/>

[https://stackoverflow.com/questions/1647815/how-to-add-a-blend-behavior-in-a-style-setter](https://stackoverflow.com/questions/1647815/how-to-add-a-blend-behavior-in-a-style-setter)