---
layout: single
title: "WPF : 34. 컨트롤을 썸네일과 같이 드래그 드랍하는 법"
description: Drag Drop WPF Control With Thumbnail, WPF Drag Drop Effect, WPF Drag Drop Adorner
categories:
 - WPF
---

컨트롤을 썸네일과 같이 드래그 드랍을 하는 방법은 다음과 같다.

- 드래그 시작할 때, 컨트롤의 이미지 만들기
- 컨트롤의 이미지를 `Adorner`를 이용해서 이동하기

### Adorner 구현

```csharp
public class DraggableAdorner : Adorner
{
    private Rect renderSize;
    private Point offset;
    private ImageSource imageSource;

    public DraggableAdorner(FrameworkElement adornedElement) : base(adornedElement)
    {
        IsHitTestVisible = false;
        Opacity = 0.7;
        
        renderSize = new Rect(adornedElement.RenderSize);
        offset = new Point(-renderSize.Width / 2, -renderSize.Height / 2);
        imageSource = GetImgSource(adornedElement);
    }

    public void SetArrange(Visual visual)
    {
        System.Drawing.Point cursorPoint = System.Windows.Forms.Cursor.Position;
        Point point = visual.PointFromScreen(new Point(cursorPoint.X + offset.X, cursorPoint.Y + offset.Y));
        Arrange(new Rect(point, DesiredSize));
    }

    protected override void OnRender(DrawingContext drawingContext)
    {
        drawingContext.DrawImage(imageSource, renderSize);
    }

    private ImageSource GetImgSource(FrameworkElement element)
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

        return rtb;
    }
}
```

### 드래그 드랍 구현(DragDrop)

```csharp
  public partial class MainWindow : Window
  {
      private DraggableAdorner draggableAdorner;

      public MainWindow()
      {
          InitializeComponent();
      }

      private void SourceLabel_MouseMove(object sender, MouseEventArgs e)
      {
          var label = sender as Label;

          if (label is not null && e.LeftButton == MouseButtonState.Pressed)
          {
              AdornerLayer adornerLayer = AdornerLayer.GetAdornerLayer(label);
              draggableAdorner = new DraggableAdorner(label);
              adornerLayer.Add(draggableAdorner);

              var dataObject = new DataObject();
              dataObject.SetData(typeof(string), label.Content.ToString());
              DragDrop.DoDragDrop(label, dataObject, DragDropEffects.Copy);

              adornerLayer.Remove(draggableAdorner);
          }
      }

      private void SourceLabel_PreviewGiveFeedback(object sender, GiveFeedbackEventArgs e)
      {
          var label = sender as Label;

          if (label is not null)
          {
              draggableAdorner.SetArrange(label);
          }
      }

      private void TargetLabel_Drop(object sender, DragEventArgs e)
      {
          var label = sender as Label;
          if (label is not null)
          {
              var srcString = e.Data.GetData(typeof(string)).ToString();
              label.Content = srcString;
          }
      }
  }
```

```xml
<Grid Margin="30">
    <Grid.Resources>
        <Style TargetType="{x:Type Label}">
            <Setter Property="Background"
                    Value="LightCyan" />
            <Setter Property="Foreground"
                    Value="Green" />
            <Setter Property="BorderBrush"
                    Value="Blue" />
            <Setter Property="BorderThickness"
                    Value="1" />
            <Setter Property="FontWeight"
                    Value="Bold" />
            <Setter Property="Padding"
                    Value="20" />
            <Setter Property="HorizontalAlignment"
                    Value="Left" />
            <Setter Property="VerticalAlignment"
                    Value="Top" />
        </Style>
    </Grid.Resources>

    <StackPanel>
        <Label Content="Drag1"
               MouseMove="SourceLabel_MouseMove"
               PreviewGiveFeedback="SourceLabel_PreviewGiveFeedback" />
        <Label Content="Drag2"
               Margin="0,30,0,0"
               MouseMove="SourceLabel_MouseMove"
               PreviewGiveFeedback="SourceLabel_PreviewGiveFeedback" />
    </StackPanel>

    <Label Content="Drag Target"
           Drop="TargetLabel_Drop"
           AllowDrop="True"
           Margin="100,0,0,0" />

</Grid>
```

![녹화_2024_07_18_11_37_06_929](https://github.com/user-attachments/assets/b20fc0a4-cf2c-43e6-8a44-da9c82521882){: .align-center}
