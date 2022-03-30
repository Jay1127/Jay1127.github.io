---
layout: single
title: "Math : 12. 두 직선의 위치 관계"
categories:
 - Math
---

## 직선 간 위치 관계

![image](https://user-images.githubusercontent.com/38006679/160733348-af529e5b-b2f2-4839-8bbb-4d55e9254886.png){: .align-center}

3차원 상의 두 직선 간의 생길 수 있는 위치 관계는 다음과 같다.

- 두 직선이 `평행(parallel)` (ex : $\overline{AB}$, $\overline{CD}$)
- 두 직선이 `교차(intersect)` (ex : $\overline{AB}$, $\overline{AD}$)
    - 두 직선이 평행하지 않을 때, 두 직선을 이루는 **4개의 점이 한 평면에 있으면** 두 직선은 교차한다.
- 두 직선이 평행, 교차하지 않는 `꼬인 위치(skew)` (ex :$\overline{AB}$, $\overline{DD_{1}}$)
    - 두 직선이 평행하지 않을 때, 두 직선을 이루는 **4개의 점이 한 평면에 있지 않으면** 두 직선은 꼬인 위치에 있다.
    

## 판단 방법

3차원 상의 두 직선 $LineA$, $LineB$ 가 존재하는 경우

$$
\begin{aligned} Line A : p + t \cdot \vec{v} \\ LineB : q + s \cdot \vec{u} \end{aligned}
$$

- 두 직선이 `평행`한 경우 다음 조건을 만족한다.

$$
(\vec{v} \times \vec{u}) \cdot (\vec{v} \times \vec{u}) = 0
$$

- 평행하지 않은 두 직선이, 다음 조건을 만족하면 두 직선은 `교차`한다.

$$
(\vec{v} \times \vec{u}) \cdot (p - q) = 0
$$

- 위 두 조건을 만족하지 않는 경우, 두 직선은 `꼬인 위치`에 있다.

## 참고

[https://en.wikipedia.org/wiki/Skew_lines](https://en.wikipedia.org/wiki/Skew_lines)

[https://math.stackexchange.com/questions/697124/how-to-determine-if-two-lines-in-3d-intersect](https://math.stackexchange.com/questions/697124/how-to-determine-if-two-lines-in-3d-intersect)