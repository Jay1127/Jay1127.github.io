---
layout: single
title: "WPF : 22. TextBox에 워터마크(Watermark) 만드는 법"
description: TextBox에 워터마크(Watermark) 만드는 법
categories:
 - WPF
---

## WatermarkAdorner

- `TextBox`위에 워터마크 외형을 표시해주는 `Adorner`를 정의한다.

```csharp
public class WatermarkAdorner : Adorner
{
    private readonly ContentPresenter child;

    protected override int VisualChildrenCount => 1;

    public WatermarkAdorner(UIElement adornedElement, object watermark) 
        : base(adornedElement)
    {
        this.IsHitTestVisible = false;

        child = new ContentPresenter
        {
            Content = watermark,
            Margin = ((Control)adornedElement).Padding
        };

        Binding binding = new Binding("Visibility");
        binding.Source = adornedElement;
        this.SetBinding(VisibilityProperty, binding);
    }

    protected override Visual GetVisualChild(int index)
    {
        return child;
    }

    protected override Size MeasureOverride(Size constraint)
    {
        var desiredSize = AdornedElement.RenderSize;
        child?.Measure(desiredSize);

        return desiredSize;
    }

    protected override Size ArrangeOverride(Size finalSize)
    {
        child.Arrange(new Rect(finalSize));
        return finalSize;
    }
}
```

## WatermarkService

- 워터마크를 지정할 `Attached Property`를 정의한다.
- `TextBox`의 `Text`값이 빈문자열인 경우 `WatermarkAdorner`를 추가하여 워터마크를 표시한다.
- `TextBox`의 `Text`에 문자가 입력된 경우 `WatermarkAdorner`를 제거하여 워터마크를 표시하지 않는다.

```csharp
public class WatermarkService
{
    /// <summary>
    /// 워터마크 속성
    /// </summary>
    public static readonly DependencyProperty WatermarkProperty =
        DependencyProperty.RegisterAttached("Watermark", typeof(object), typeof(WatermarkService),
            new PropertyMetadata(null, new PropertyChangedCallback(OnWatermarkChanged)));

    public static object GetWatermark(DependencyObject obj)
    {
        return (object)obj.GetValue(WatermarkProperty);
    }

    public static void SetWatermark(DependencyObject obj, object value)
    {
        obj.SetValue(WatermarkProperty, value);
    }

    private static void OnWatermarkChanged(DependencyObject d, DependencyPropertyChangedEventArgs e)
    {
        if (d is TextBox textBox)
        {
            textBox.Loaded += TextBox_Loaded;
            textBox.TextChanged += TextBox_TextChanged;
        }
    }

    /// <summary>
    /// 텍스트박스에 워터마크 렌더링(초기값이 ""인 경우에만)
    /// </summary>
    /// <param name="sender"></param>
    /// <param name="e"></param>
    private static void TextBox_Loaded(object sender, RoutedEventArgs e)
    {
        if (!CanRenderWatermark(sender as Control))
        {
            return;
        }

        RenderWatermark(sender as Control);
    }

    /// <summary>
    /// 텍스트박스에 타이핑하는 경우(텍스트가 "" 인 경우에만 워터마크 렌더링)
    /// </summary>
    /// <param name="sender"></param>
    /// <param name="e"></param>
    private static void TextBox_TextChanged(object sender, TextChangedEventArgs e)
    {
        var textBox = sender as Control;

        if (CanRenderWatermark(textBox))
        {
            RenderWatermark(textBox);
        }
        else
        {
            RemoveWatermark(textBox);
        }
    }

    /// <summary>
    /// 컨트롤에 워터마크 렌더링함.
    /// </summary>
    /// <param name="parent">렌더링할 컨트롤</param>
    private static void RenderWatermark(Control parent)
    {
        var layer = AdornerLayer.GetAdornerLayer(parent);

        if (layer != null)
        {
            layer.Add(new WatermarkAdorner(parent, GetWatermark(parent)));
        }
    }

    /// <summary>
    /// 컨트롤에서 워터마크 제거
    /// </summary>
    /// <param name="parent">워터마크 제거할 컨트롤</param>
    private static void RemoveWatermark(Control parent)
    {
        var layer = AdornerLayer.GetAdornerLayer(parent);

        if (layer == null)
        {
            return;
        }

        var adorners = layer.GetAdorners(parent)?.Where(adorner => adorner is WatermarkAdorner);

        if (adorners != null)
        {
            foreach (var adorner in adorners)
            {
                layer.Remove(adorner);
            }
        }
    }

    /// <summary>
    /// 컨트롤에 워터마크 추가할수 있는지 판단
    /// </summary>
    /// <param name="parent">워터마크 추가할 컨트롤</param>
    /// <returns></returns>
    private static bool CanRenderWatermark(object parent)
    {
        if (parent is TextBox textBox)
        {
            if (string.IsNullOrEmpty(textBox.Text))
            {
                return true;
            }
        }

        return false;
    }
}
```

## 사용법

```xml
<TextBox FontSize="30">
    <sc:WatermarkService.Watermark>
        <TextBlock FontSize="30" Opacity="0.5" Text="Input id"/>
    </sc:WatermarkService.Watermark>
</TextBox>
```

![_2020_05_06_16_10_41_230](https://user-images.githubusercontent.com/38006679/155426953-d9324ab6-75d1-43f3-9601-232428da7955.gif){: .align-center}
