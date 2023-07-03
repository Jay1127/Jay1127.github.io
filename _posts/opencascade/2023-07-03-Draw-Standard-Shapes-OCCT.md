---
layout: single
title: "OCCT : 3. 모델 그리기(Built-in)"
description: OCCT 모델 그리기
categories:
 - opencascade
---

```cpp
void DrawShapes_Viewport::DrawLine()
{
    // make geometry data
    gp_Pnt startPt(0, 0, 0);
    gp_Pnt endPt(100, 100, 100);
    Handle(Geom_Line) line = GC_MakeLine(startPt, endPt);

    // make presentable object using geometry data
    Handle(AIS_Line) shape = new AIS_Line(line);

    // display presentable object
    _aisContext()->Display(shape, false);
}

void DrawShapes_Viewport::DrawCyliner()
{
    gp_Ax2 dir = gp::XOY();
    TopoDS_Shape box = BRepPrimAPI_MakeCylinder(dir, 100.0, 200.0);

    Handle(AIS_Shape) shape = new AIS_Shape(box);
    shape->SetDisplayMode(1);

    _aisContext()->Display(shape, false);
}
```

![image](https://github.com/Jay1127/Jay1127.github.io/assets/38006679/541ef422-bd5c-44a4-a65c-c39d1f79a5c7){: .align-center}

![image](https://github.com/Jay1127/Jay1127.github.io/assets/38006679/78343475-d729-4d62-934a-0c9ae3b4a093){: .align-center}