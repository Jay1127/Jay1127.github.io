---
layout: single
title: "WPF : 35. ScrollViewer내 DataGrid의 스크롤이 안되는 경우 해결방법"
description: ScrollViewer, DataGrid, WPF DataGrid Scroll in ScrollViewer
categories:
 - WPF
---

`ScrollViewer`내 `DataGrid`를 생성한 경우, `DataGrid`를 마우스 휠을 이용해서 스크롤이 안되는 문제가 발생한다.  `PreviewMouseWheel` 이벤트를 다음과 같이 구현해서 문제를 해결할 수 있다.

```xml
<ScrollViewer Height="350">
    <Grid>
        <DataGrid ItemsSource="{Binding Items}"
                  PreviewMouseWheel="DataGrid_MouseWheel"/>
    </Grid>
</ScrollViewer>
```

<br/>

```csharp
private void DataGrid_MouseWheel(object sender, MouseWheelEventArgs e)
{
    var dataGrid = sender as DataGrid;
    var scrollViewer = (dataGrid.Parent as Grid).Parent as ScrollViewer;

    var args = new MouseWheelEventArgs(e.MouseDevice, e.Timestamp, e.Delta);
    args.RoutedEvent = ScrollViewer.MouseWheelEvent;
    scrollViewer.RaiseEvent(args);
}
```