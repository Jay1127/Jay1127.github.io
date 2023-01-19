---
layout: single
title: "Math : 10. 벡터의 내적을 통한 각도 구하기(0~360 또는 -180~180도)"
description: 벡터의 내적을 통한 각도 구하기(0~360 또는 -180~180도)
categories:
 - Math
---

벡터의 내적을 이용한 두 벡터의 사이각은 다음과 같다.

$$
\theta = arccos({v_1⋅v_2 \over \parallel v_1 \parallel ⋅ \parallel v_2 \parallel})
$$

<br/>
$arccos$으로 구한 각도는 0 ~ 180°내 존재하므로 아래 그림처럼 방향이 달라도 같은 각도로 표현된다.

![image](https://user-images.githubusercontent.com/38006679/160726219-e4fc4729-ab50-41aa-b587-e256d3409593.png){: .align-center}

<br/>

일반적으로, 3차원 상에서 두 벡터를 외적한 벡터와 글로벌 $z$축의 방향성을 비교하여, 각도 표현 방법을 변경할 수 있다. 즉, 두 벡터를 외적한 벡터를 $w$라하면, 다음과 같이 $w.z$값이 양수, 음수인지에 따라 각도 표현 방법을 다르게 할 수 있다.

- $0$° $\sim$ $360$°로 표현

$$
\theta = \begin{cases} \ \ \ \ \ \ \theta &\text{if } w.z \geq 0 \\ \ 360-\theta &\text{if } w.z < 0 \end{cases}
$$

- -$180$° $\sim$ $180$°로 표현

$$
\theta = \begin{cases} \ \ \ \ \theta &\text{if } w.z \geq 0 \\ \ -\theta &\text{if } w.z < 0 \end{cases}
$$