---
layout: single
title: "Math : 2. 벡터의 내적(Dot Product)"
description: 벡터의 내적(Dot Product)
categories:
 - Math
---

## 정의

![image](https://user-images.githubusercontent.com/38006679/156297365-7db30fad-e600-4821-aecd-b4c3bb286cc0.png){: .align-center width="300"}


3차원 상의 두 벡터 $v=(v_x, v_y, v_z),\ w=(w_x, w_y, w_z)$의 내적 공식은 다음과 같다. ($\parallel v \parallel$는 벡터 $v$의 크기, $\theta$는 두 벡터의 사이각)

$$
\begin{matrix} v \cdot w &=& \parallel v \parallel \cdot \parallel w \parallel \cdot \ cos(\theta) \\ &=& v_x \cdot w_x + v_y \cdot w_y + v_z \cdot w_z \end{matrix}
$$

## 사이각

내적을 이용하면 두 벡터 사이의 사이각을 알아낼 수 있다.

$$
\begin{matrix} cos(\theta) = {v \cdot w \over \parallel v \parallel \cdot \parallel w \parallel} = {v_x \cdot w_x + v_y \cdot w_y + v_z \cdot w_z \over \parallel v \parallel \cdot \parallel w \parallel} \\ \\ \theta = arccos({v_x \cdot w_x + v_y \cdot w_y + v_z \cdot w_z \over \parallel v \parallel \cdot \parallel w \parallel}) \end{matrix}
$$

- 내적을 통해 알아낸 사이각은 $0 \sim 180^\circ$ 범위에 존재한다.($arccos$)
- $v \cdot w > 0$ 이면 사이각은 $90^\circ$보다 작다.(예각)
- $v \cdot w < 0$ 이면 사이각은 $90^\circ$보다 크다.(둔각)
- $v \cdot w = 0$ 이면 두 벡터는 수직이다.
- $\left\vert v \cdot w \right\vert  = 1$이면 두 벡터는 평행하다.

## 길이

벡터를 자신을 내적하면 벡터의 길이의 제곱값을 구할 수 있다.

$$
v \cdot v = v_x^2 + v_y^2 + v_z^2 = |v|^2
$$

## 투영

![image](https://user-images.githubusercontent.com/38006679/156297524-d9035e29-6b4b-4c87-9b54-ecfb06a10d3e.png){: .align-center width="300"}

투영된 벡터를 구하기 위해서는 벡터 $w$의 단위 벡터에 투영된 벡터의 크기를 곱하면 된다.

- 투영된 벡터의 크기는 다음과 같다.

$$
\parallel v_{projection} \parallel = \ \parallel v \parallel \cdot cos(\theta) = \ \parallel v \parallel \cdot {v \cdot w \over \parallel v \parallel \cdot \parallel w \parallel} = \ { v \cdot w \over \parallel w \parallel }
$$

- 계산한 투영된 벡터의 크기와 벡터 $w$의 단위 벡터를 곱하여 투영된 벡터를 구한다.

$$
v_{projection} = \ \parallel v_{projection} \parallel \cdot \hat{w} = ({ v \cdot w \over \parallel w \parallel }) \cdot {w \over \parallel w \parallel} =({ v \cdot w \over {\parallel w \parallel}^2 }) \cdot w
$$

- 만약, 투영된 벡터의 크기가 단위벡터인 경우 투영된 벡터는 다음과 같다.

$$
v_{projection} = (v \cdot \hat{w}) \cdot \hat{w}
$$