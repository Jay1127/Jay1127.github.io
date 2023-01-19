---
layout: single
title: "Math : 3. 벡터의 외적(Cross Product)"
description: 벡터의 외적(Cross Product)
categories:
 - Math
---

## 정의

![image](https://user-images.githubusercontent.com/38006679/156303588-4a98a60b-fee8-43e9-82cc-19bc8c012c47.png){: .align-center width="300"}


두 벡터 $v,w$의 외적은 3차원 공간에서만 정의되며, 공식은 다음과 같다. (여기서, 벡터 $\hat{n}$은 두 벡터 $v,w$에 수직인 단위 벡터이며, $\parallel v \parallel \cdot \parallel w \parallel sin(\theta)$는 외적의 결과 벡터의 크기를 나타낸다.)

$$
\begin{matrix} u = \ \ v \times w &=& \parallel v \parallel \cdot \parallel w \parallel sin(\theta) \cdot \hat{n} \\ &=& (v_y \cdot w_z - w_y \cdot v_z, v_z \cdot w_x - w_z \cdot v_x,v_x \cdot w_y - w_y \cdot v_x) \end{matrix}
$$

이 때, 벡터 $u$는 벡터 $v,w$와 모두 수직을 이루며, 벡터의 크기는 두 벡터 $v,w$가 이루는 평행사변형의 넓이과 동일하다.

## 방향
![image](https://user-images.githubusercontent.com/38006679/156303611-2bb558b7-736c-4109-a104-a37c57dc7b16.png){: .align-center width="300"}

외적 벡터가 향하는 방향은 오른손으로 해당하는 두 벡터를 감쌀 때 엄지 손가락의 방향이 외적 벡터의 방향과 같다.(오른손 좌표계 기준) 따라서, 외적시 연산 벡터의 순서가 달라지면 방향이 반대가 된다.

$$
a \times b = -(b \times a)
$$

## 평행성

벡터의 외적을 활용하면 두 벡터가 서로 평행한지 판단할 수 있다. 
$sin$함수의 값이 곱해지므로, <U>외적 벡터의 크기가 0이면, 두 벡터($v,w$)는 서로 평행하다.</U> 또한, 벡터 자신을 내적하면 크기의 제곱과 동일하므로, 다음과 같이 외적된 벡터를 스스로 내적한 값을 통해 평행성을 판단할 수 있다.

$$
\text{두 벡터 $v,w$가 서로 평행하면 } (v \times w) \cdot (v \times w) = 0 \text{을 만족한다.}
$$