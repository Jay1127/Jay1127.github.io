---
layout: single
title: "OCCT : 2. OCCT Viewer 초기 설정 및 호출(Winform, WPF)"
description: Opencascade, occt, occt viewer, winform, wpf
categories:
 - opencascade
---

## 프로젝트 설정

프로젝트(C++ or C++/CLI) 생성 후, 빌드 후 생성된 OCCT 라이브러리 경로를 설정한다.

- `\inc` : 헤더 파일을 폴더 경로
- `\win64\vc14\libd` : lib파일 폴더 경로

<br/>

빌드 이벤트를 이용해서, OCCT DLL파일과 외부 라이브러리 DLL파일을 출력 경로로 복사한다.

- `OCCT_DLL(win64\vc14\bind)` : OCCT DLL 폴더 경로
- `OCCT_THIRD_PARTY` : 외부 참조 DLL 폴더 경로(freetype.dll …)

```
SET OCCT_DLL=C:\OpenCASCADE\Build\win64\vc14\bind
SET OCCT_THIRD_PARTY=C:\OpenCASCADE\Build\win64\vc14\3rd

xcopy /Y /I /E %OCCT_DLL% $(TargetDir)
xcopy /Y /I /E %OCCT_THIRD_PARTY% $(TargetDir)
```

## 소스 코드

- OCCT Viewer 설정(C++/CLI)

```cpp
// Viewport.cpp

bool Viewport::Initialize(System::IntPtr handle)
{
    // graphic driver
    Handle(Aspect_DisplayConnection) displayConnection;
    _graphicDriver() = new OpenGl_GraphicDriver(displayConnection);

    // viewer 
    _viewer() = new V3d_Viewer(_graphicDriver());

    // view
    auto wntWindow = new WNT_Window(reinterpret_cast<HWND>(handle.ToPointer())); // window
    _view() = _viewer()->CreateView();
    _view()->SetWindow(wntWindow);

    if (!wntWindow->IsMapped())
    {
        wntWindow->Map();
    }

    // interactive context
    _aisContext() = new AIS_InteractiveContext(_viewer());
    _aisContext()->UpdateCurrentViewer();

    // update view
    _view()->Redraw();
    _view()->MustBeResized();

    return false;
}

void Viewport::Update()
{
    _view()->Redraw();
}

void Viewport::SetBackgroudColor(System::Drawing::Color backgroundColor)
{
    if (_view().IsNull())
    {
        return;
    }

    _view()->SetBackgroundColor(Quantity_TOC_RGB,
        backgroundColor.R / 255.0,
        backgroundColor.G / 255.0,
        backgroundColor.B / 255.0);
}
```

<br/>

- Winform인 경우

```csharp
// Form1.cs

public partial class Form1 : Form
{
    Viewport viewport;

    public Form1()
    {
        InitializeComponent();

        viewport = new Viewport();
        viewport.Initialize(this.Handle);
        viewport.SetBackgroudColor(System.Drawing.Color.Red);
    }

    protected override void OnPaint(PaintEventArgs e)
    {
        base.OnPaint(e);

        viewport.Update();
    }
}
```

<br/>

- WPF인 경우

```csharp
// MainWindow.xaml.cs

public partial class MainWindow : Window
{
    Viewport viewport;

    public MainWindow()
    {
        InitializeComponent();
        ViewPanel.Loaded += ViewPanel_Loaded;

        LayoutUpdated += MainWindow_LayoutUpdated;
    }

    private void ViewPanel_Loaded(object sender, RoutedEventArgs e)
    {
        // set dimension
        var uc = new System.Windows.Forms.UserControl();
        uc.Width = (int)ViewPanel.ActualWidth;
        uc.Height = (int)ViewPanel.ActualHeight;

        // set handle to viewport
        viewport = new Viewport();
        viewport.Initialize(uc.Handle);
        viewport.SetBackgroudColor(System.Drawing.Color.Red);

        // set viewport to viewpanel content
        var host = new WindowsFormsHost();
        host.Child = uc;
        ViewPanel.Content = host;
    }

    private void MainWindow_LayoutUpdated(object sender, EventArgs e)
    {
        if (viewport != null)
        {
            viewport.Update();
        }
    }
}
```

- 실행 화면

![image](https://github.com/Jay1127/Jay1127.github.io/assets/38006679/72a1b635-ab1e-408a-98cf-b6c24ae21a77){: .align-center}{: width="500"}