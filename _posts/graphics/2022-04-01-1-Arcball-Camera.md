---
layout: single
title: "Graphics : 1. 아크볼 카메라(Arcball Camera)"
description: 아크볼 카메라(Arcball Camera)
categories:
 - Graphics
---

## **개념**

마우스의 위치를 따라 구면좌표계 내 호(arc)를 생성하여, 해당 호가 속한 평면의 법선벡터를 축으로 카메라를 회전시키는 방법

## 구현

**1. 구면좌표계로 변환**

먼저, 아래 그림처럼 마우스로 클릭한 스크린의 좌표를 구면 좌표계의 좌표로 변환해야 한다. 변환시에는 스크린 좌표계와 구면 좌표계의 좌표축이 다른점을 고려해야 한다.

- 스크린 좌표계 : 좌측 상단이 원점이며 X축은 우측으로, Y축은 하단으로 향한다.
- 구면 좌표계 : 화면의 중심이 원점이며, X축은 우축으로, Y축은 상단으로 향한다.

![image](https://user-images.githubusercontent.com/38006679/161180631-79ee3cc0-17c1-4aaa-8f02-3de6ba803da9.png){: .align-center}

```csharp
private Vector3 MapSphereCoordinate(Vector2 screenPt)
{
    Vector3 coord = new Vector3();

    // 타원이 되지않도록 방지
    var diameter = Math.Min(Width, Height);

    // Y축은 좌표축 반대 -1을 곱함
    coord.X = (2 * screenPt.X - diameter) / diameter;
    coord.Y = -(2 * screenPt.Y - diameter) / diameter;

    float length_squared = coord.X * coord.X + coord.Y * coord.Y;

    if (length_squared <= 1.0)
    {
        coord.Z = (float)Math.Sqrt(1.0 - length_squared);
    }
    else
    {        
        coord = Vector3.Normalize(coord);
        coord.Z = 0.0f;                
    }

    return coord;
}
```

<br/>

**2. 회전각도, 회전축 계산**

구면좌표계의 원점, 시작점, 끝점으로 호를 생성한다. 생성된 호가 속하는 평면의 법선 벡터를 회전축으로 하고, 호의 사이각을 회전 각도로 하여 카메라를 회전한다.

![image](https://user-images.githubusercontent.com/38006679/161180675-eb8549f7-072b-42d2-988e-a1b1f7a380c3.png){: .align-center}

```csharp
public void Rotate(Vector2 scrStartPoint, Vector2 srcEndPoint)
{
    Vector3 arcStartPoint = MapSphereCoordinate(scrStartPoint);
    Vector3 arcEndPoint = MapSphereCoordinate(srcEndPoint);

    Vector3 rotateAxis = Vector3.Cross(arcStartPoint, arcEndPoint);
    float angle = Vector3.CalculateAngle(arcStartPoint, arcEndPoint);
    
    var rotation = new Rotation3D(MathUtil.ToDegrees(angle), rotateAxis, Center);
    Rotation *= rotation.Matrix;
}
```

## **소스코드**

[https://github.com/Jay1127/Arcball](https://github.com/Jay1127/Arcball)