---
layout: single
title: "WPF : 33. 컨트롤을 이미지 파일로 저장하는 법"
description: Capture WPF Control To Image, RenderTargetBitmap, PngBitmapEncorder
categories:
 - WPF
---


```csharp
public void Capture(FrameworkElement element)
{
    double dpi = 96;
    double width = element.ActualWidth;
    double height = element.ActualHeight;

    DrawingVisual drawingVisual = new DrawingVisual();
    using (DrawingContext dc = drawingVisual.RenderOpen())
    {
        VisualBrush vb = new VisualBrush(element);
        dc.DrawRectangle(vb, null, new Rect(new System.Windows.Point(), new System.Windows.Size(width, height)));
    }

    RenderTargetBitmap rtb = new RenderTargetBitmap((int)Math.Round(width), (int)Math.Round(height), dpi, dpi, PixelFormats.Default);
    rtb.Render(drawingVisual);

    PngBitmapEncoder enc = new PngBitmapEncoder();
    enc.Frames.Add(BitmapFrame.Create(rtb));
    using (Stream stm = File.Create("label.png"))
    {
        enc.Save(stm);
    }
}
```