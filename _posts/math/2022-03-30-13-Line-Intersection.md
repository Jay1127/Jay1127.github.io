---
layout: single
title: "Math : 13. 직선, 선분 교차점 찾기(Line intersection)"
categories:
 - Math
---

## 직선 간 교차점 찾기

![image](https://user-images.githubusercontent.com/38006679/160739925-fd77770e-3ca3-44fa-a19a-de290f5fe5e3.png){: .align-center}

두 직선을 매개변수 방정식으로 정의하면 다음과 같다.

$$
\begin{matrix} Line0 : p + t \cdot \vec{v} \\ Line1 : q + s \cdot \vec{u} \end{matrix}
$$

두 직선의 교차점을 찾는 방법은 $Line0$와 $Line1$를 일치시키는 매개변수 $t$값을 찾으면 된다. (반대로, $s$ 로 찾아도 된다.)

$$
\begin{aligned}
   Line0 \ \ \ &= \ \ \ Line1 \\
   p + t \cdot \vec{v} \ \ \ &= \ \ \ q + s  \cdot \vec{u} \\ t \cdot \vec{v} \ \ \ &= \ \ \ (q-p) + s \cdot \vec{u} \\ t \cdot (\vec{v} \times \vec{u}) \ \ \ &= \ \ \ (q-p) \times \vec{u} + s \cdot \vec{u} \times \vec{u} \ \ \ \ \ \ &(&\because \ \text{양변에 } \vec{u} \text{를 외적}) \\ t \cdot (\vec{v} \times \vec{u}) \ \ \ &= \ \ \ (q-p) \times \vec{u} &(&\because \ \vec{u} \times \vec{u} = 0 ) \\ 
    t \cdot (\vec{v} \times \vec{u}) \cdot (\vec{v} \times \vec{u}) \ \ \ &= \ \ \ (q-p) \times \vec{u} \cdot (\vec{v} \times \vec{u}) &(&\because \ \vec{v} \times \vec{u}\ \text{를 양변에 내적})
   \\
   \  t \ \ \ &= \ \ \ {(q-p) \times \vec{u} \cdot (\vec{v} \times \vec{u}) \over \parallel\vec{v} \times \vec{u}\parallel^{2}   }  &(& \because \ \parallel\vec{v} \times \vec{u}\parallel^{2} \text{로 양변을 나눔})
\end{aligned}
$$

- $\parallel\vec{v} \times \vec{u}\parallel^{2} = 0$ 이면 두 직선은 평행하다.
- 두 직선이 평행하지 않은 경우, $(\vec{v} \times \vec{u}) \cdot (p - q) = 0$ 이면 두 직선은 교차점을 가진다.
- 위 두 조건을 만족하지 않을 때, 두 직선은 꼬인(skew) 위치에 있다.
    - 꼬인 위치인 경우, 찾아낸 매개변수 $t$, $s$로 구한 점은 교차점이 아닌 직선에서 가장 가까운 점이다.

## 소스 코드

```csharp
public Point3D IntersectLine(Line compared)
{
    // Line 0 
    var p = StartPoint;
    var v = Direction.Normalized();

    // Line 1
    var q = compared.StartPoint;
    var u = compared.Direction.Normalized();

    var a = v.Cross(u); // v x u

    var dot_aa = a.Dot(a);	// (v x u) ^ 2

    // 두 직선이 평행
    if(dot_aa == 0)
    {
        return null;
    }
	
    // 두 직선이 꼬인 위치
    if(a.Dot(p-q) != 0) 
    {
        return null;
    }

    var b = (q - p).Cross(u).Dot(a); // (q - p) x u (u x v)
    var t = b / dot_aa;

    return p + t * v;
}
```

## 선분 간 교차점 찾기

선분은 직선 매개변수 방정식에서 매개변수의 값이 `0 ~ 1 범위`에 있는 경우를 말한다. 따라서, 구한 매개변수 $t,s$의 값이 범위 내에 있으면, 해당 교차점이 선분 위에 있는 걸로 판단한다.