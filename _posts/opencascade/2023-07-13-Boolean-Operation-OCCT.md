---
layout: single
title: "OCCT : 6. Boolean Operation(Union, Difference, Intersection)"
description: OCCT Boolean Operation(Union, Difference, Intersection), opencascade, occt
categories:
 - opencascade
---

![image](https://github.com/Jay1127/Jay1127.github.io/assets/38006679/90706926-9837-4eeb-b1d5-e3d21e09e768){: .align-center}{: width="700"}

### Union(BRepAlgoAPI_Fuse)

```cpp
gp_Pnt corner1 = gp_Pnt(0, 0, 0);
gp_Pnt corner2 = gp_Pnt(1000, 100, 100);
TopoDS_Shape box1 = BRepPrimAPI_MakeBox(corner1, corner2);

gp_Pnt corner3 = gp_Pnt(450, -500, 50);
gp_Pnt corner4 = gp_Pnt(550, 500, 150);
TopoDS_Shape box2 = BRepPrimAPI_MakeBox(corner3, corner4);

TopoDS_Shape fuse = BRepAlgoAPI_Fuse(box1, box2);
```

![image](https://github.com/Jay1127/Jay1127.github.io/assets/38006679/385110a5-6101-4711-834c-67329187eee5){: .align-center}{: width="700"}

### Difference(BRepAlgoAPI_Cut)

```cpp
gp_Pnt corner1 = gp_Pnt(0, 0, 0);
gp_Pnt corner2 = gp_Pnt(1000, 100, 100);
TopoDS_Shape box1 = BRepPrimAPI_MakeBox(corner1, corner2);

gp_Pnt corner3 = gp_Pnt(450, -500, 50);
gp_Pnt corner4 = gp_Pnt(550, 500, 150);
TopoDS_Shape box2 = BRepPrimAPI_MakeBox(corner3, corner4);

TopoDS_Shape cut = BRepAlgoAPI_Cut(box1, box2);
```

![image](https://github.com/Jay1127/Jay1127.github.io/assets/38006679/b48773d2-8703-4e0c-9332-1504614497a2){: .align-center}{: width="700"}

### Intersection(BRepAlgoAPI_Common)

```cpp
gp_Pnt corner1 = gp_Pnt(0, 0, 0);
gp_Pnt corner2 = gp_Pnt(1000, 100, 100);
TopoDS_Shape box1 = BRepPrimAPI_MakeBox(corner1, corner2);

gp_Pnt corner3 = gp_Pnt(450, -500, 50);
gp_Pnt corner4 = gp_Pnt(550, 500, 150);
TopoDS_Shape box2 = BRepPrimAPI_MakeBox(corner3, corner4);

TopoDS_Shape common = BRepAlgoAPI_Common(box1, box2);
```

![image](https://github.com/Jay1127/Jay1127.github.io/assets/38006679/474b743b-83ac-45a8-9668-e0c7ecf8eb56){: .align-center}{: width="700"}