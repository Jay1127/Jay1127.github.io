---
layout: single
title: "WPF : 19. WindowChrome을 이용한 Window 커스터마이징"
categories:
 - WPF
---

`Window`외형을 커스터마이징하려면,  `WindowStyle="None"` 지정하여 상단 캡션바를 없앤 후 스타일을 적용하는 방법이 있다. 하지만, 이 방법은 `Window`에서 기본적으로 제공해주는 상단 캡션바를 클릭하면 창이 최대화되고, 드래그하면 이동하고, 모서리를 드래그하여 크기를 조절해주는 기능을 다시 구현해야만 한다. 이러한 번거로움을 줄이면서 외형을 변경하려면 `Style`에서 `WindowChrome`속성을 정의해주면 된다.

## 윈도우 스타일 설정

`Window`가 최대화될 때, 모니터에 딱맞지 않고 넘어가서 잘리는 부분이 생기게 된다. `Trigger`를 이용해 최대화됐을 때, `BorderThickness`를 설정하여 이를 방지할 수 있다.

```xml
<Style TargetType="{x:Type Window}" x:Key="CustomWindowStyle">
    <Setter Property="WindowChrome.WindowChrome">
        <Setter.Value>
            <!-- WindowChrome 프로퍼티 설명은 다음 링크 참조 -->
            <!-- https://docs.microsoft.com/ko-kr/dotnet/api/system.windows.shell.windowchrome?view=windowsdesktop-6.0 -->
            <WindowChrome CaptionHeight="30"
                          CornerRadius="30"
                          GlassFrameThickness="0"
                          ResizeBorderThickness="3"
                          NonClientFrameEdges="None"/>
        </Setter.Value>
    </Setter>
    <Style.Triggers>
        <Trigger Property="WindowState" Value="Maximized">
            <Setter Property="BorderThickness" Value="{Binding Source={x:Static SystemParameters.WindowResizeBorderThickness}}"/>
        </Trigger>
    </Style.Triggers>
</Style>
```

## 윈도우 구현

`Window`의 캡션바 영역에 위치하는 `Control`은 `WindowChrome.IsHitTestVisibleInChrome`값을 `True`로 설정해야 클릭 이벤트가 발생한다.

```xml
<Window x:Class="StyleTemplates.MainWindow"
        xmlns="<http://schemas.microsoft.com/winfx/2006/xaml/presentation>"
        xmlns:x="<http://schemas.microsoft.com/winfx/2006/xaml>"
        xmlns:d="<http://schemas.microsoft.com/expression/blend/2008>"
        xmlns:mc="<http://schemas.openxmlformats.org/markup-compatibility/2006>"
        xmlns:local="clr-namespace:StyleTemplates"
        mc:Ignorable="d"
        Title="CustomeWindow" Height="450" Width="800" 
        Style="{StaticResource CustomWindowStyle}">
    <Grid>
        <Grid.RowDefinitions>
            <RowDefinition Height="30"/> <!--윈도우 캡션바 높이-->
            <RowDefinition Height="*"/>
        </Grid.RowDefinitions>

        <!--윈도우 캡션바-->
        <!--배경색을 바꾸거나 아이콘을 넣는 등 커스터마이징할 수 있음.--> 
        <DockPanel Background="Black" 
                   LastChildFill="False">
            <DockPanel.Resources>
                <Style TargetType="{x:Type Button}">
                    <Setter Property="DockPanel.Dock" Value="Right"/>
                    <Setter Property="Width" Value="30"/>
                    <!-- WindowChrome의 caption위에 있는 버튼을 클릭하려면 True로 설정해야 함. -->
                    <Setter Property="WindowChrome.IsHitTestVisibleInChrome" Value="True"/>
                    <Setter Property="Background" Value="Transparent"/>
                    <Setter Property="Foreground" Value="White"/>
                    <Setter Property="BorderThickness" Value="0"/>
                </Style>
            </DockPanel.Resources>
            <Button Content="X" Click="ButtonClose_Click"/>
            <Button Content="ㅁ" Click="ButtonMaximized_Click"/>
            <Button Content="_" Click="ButtonMinimize_Click"/>
        </DockPanel>
      
        <!-- define contents -->
    </Grid>
</Window>
```

```csharp
private void ButtonClose_Click(object sender, RoutedEventArgs e)
{
    Application.Current.Shutdown();
}

private void ButtonMaximized_Click(object sender, RoutedEventArgs e)
{
    if(WindowState == WindowState.Maximized)
    {
        WindowState = WindowState.Normal;
    }
    else
    {
        WindowState = WindowState.Maximized;
    }
}

private void ButtonMinimize_Click(object sender, RoutedEventArgs e)
{
    WindowState = WindowState.Minimized;
}
```

![image](https://user-images.githubusercontent.com/38006679/150036979-6ee69250-d91f-45dd-8c69-582075d928ed.png){: .align-center}