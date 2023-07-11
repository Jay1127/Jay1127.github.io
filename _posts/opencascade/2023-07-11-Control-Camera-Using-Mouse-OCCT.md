---
layout: single
title: "OCCT : 5. 마우스를 이용해 카메라 조작하는 법(이동, 회전, 줌인/아웃)"
description: 마우스를 이용해 카메라 조작하는 법(이동, 회전, 줌인/아웃), opencascade, occt
categories:
 - opencascade
---

`V3d_View`에서 제공하는 카메라 이동, 회전, 줌인/아웃 함수에 마우스 위치를 매개 변수로 넘겨준다.

```cpp
// Viewport.cpp
void CameraController_Viewport::Pan(int deltaX, int deltaY)
{
    _view()->Pan(deltaX, deltaY);
}

void CameraController_Viewport::Rotate(int x, int y)
{
    _view()->Rotation(x, y);
}

void CameraController_Viewport::Zoom(int x, int y, double delta)
{
    int width, height;
    _view()->Window()->Size(width, height);

    int x1 = x + width * delta / 10000.0;
    int y1 = y + height * delta / 10000.0;
    
    _view()->StartZoomAtPoint(x, y);
    _view()->ZoomAtPoint(x, y, x1, y1);
}

void CameraController_Viewport::StartRotation(int x, int y)
{
    _view()->StartRotation(x, y);
}
```

<br/>

WPF에서 마우스 관련 이벤트를 구현하여, 마우스 위치를 찾는다. 해당 위치를 Viewport의 함수에 넘기면, 마우스에 따라 카메라가 조작된다.

```csharp
// MainWindow.xaml.cs

int mousePosX;
int mousePosY;
bool isDragging = false;

private void Viewport_MouseUp(object sender, System.Windows.Forms.MouseEventArgs e)
{
    isDragging = false;
}

private void Viewport_MouseDown(object sender, System.Windows.Forms.MouseEventArgs e)
{
    isDragging = true;

    mousePosX = e.X;
    mousePosY = e.Y;

    if(e.Button == System.Windows.Forms.MouseButtons.Right)
    {
        // set rotation start position
        viewport.StartRotation(e.X, e.Y);
    }
}

private void Viewport_MouseWheel(object sender, System.Windows.Forms.MouseEventArgs e)
{
    viewport.Zoom(e.X, e.Y, e.Delta);
}

private void Viewport_MouseMove(object sender, System.Windows.Forms.MouseEventArgs e)
{
    if(isDragging is false)
    {
        return;
    }

    if (e.Button == System.Windows.Forms.MouseButtons.Left)
    {
        var deltaX = e.X - mousePosX;
        var deltaY = mousePosY - e.Y;
        viewport.Pan(deltaX, deltaY);
    }
    else if (e.Button == System.Windows.Forms.MouseButtons.Right)
    {
        viewport.Rotate(e.X, e.Y);
    }

    mousePosX = e.X;
    mousePosY = e.Y;
    //viewport.MoveTo(e.X, e.Y);
}
```

![Animation](https://github.com/Jay1127/Jay1127.github.io/assets/38006679/5adc7e82-47ff-4cbd-992a-94474ae26762){: .align-center}{: width="700"}
