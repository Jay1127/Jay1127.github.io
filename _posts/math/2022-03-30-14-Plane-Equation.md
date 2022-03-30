---
layout: single
title: "Math : 14. 평면의 방정식(Plane equation)"
categories:
 - Math
---

![image](https://user-images.githubusercontent.com/38006679/160733039-caa01373-52b1-4d51-acf2-a68be8028a0b.png){: .align-center}

<br/>
평면의 방정식은 평면 위의 한 점 $P'$와 평면에 수직인 벡터 $n$(법선 벡터)로 정의할 수 있다.

<br/>
먼저, 평면 위의 임의의 점을 $P$라 하면, $P'$에서 $P$로 지나는 벡터 $v$는 다음과 같다.

$$
v = P - P' = (x - x \ ', y - y \ ', z - z \ ')
$$

법선 벡터 $n$은 평면 위의 모든 벡터와 수직을 이루므로 벡터 $n$과 벡터 $v$의 내적 값은 0이다.

$$
n \cdot v = 0
$$

위 식을 전개하면 평면의 방정식을 구할 수 있다.

$$
\begin{aligned} (a,b,c) \cdot (x - x \ ', y - y \ ', z - z \ ') \ \ \   &= \ \ \ 0 \\  a(x - x \ ') + b(y - y \ ') + c(z - z \ ') \ \ \ &= \ \ \ 0 \\ ax + by + cz -(ax' + by' + cz') \ \ \ &= \ \ \ 0 \\ ax + by + cz + d \ \ \ &= \ \ \ 0 \end{aligned}
$$