---
layout: single
title: "Math : 6. 좌표축 변환 행렬 유도"
categories:
 - Math
---

## 선형 변환
![image](https://user-images.githubusercontent.com/38006679/159624532-5d47d8a1-d3f7-42e0-add7-72272ae86017.png){: .align-center}


$xy$평면 위에 크기가 $l$ 이고, $x$축과 이루는 각도가 $\alpha$인  벡터 $v$의 각 성분은 다음과 같다.

- $v_x = l⋅cos(\alpha)$
- $v_y = l⋅sin(\alpha)$
- $v_z = 0$

벡터 $v$를 $z$축으로 $\beta$만큼 회전한 벡터 $w$의 각 성분을 구할 수 있다.

- $w_x=l⋅cos(α+β)=l⋅(cosα⋅cosβ - sinα⋅sinβ)=v_x \cdot cosβ - v_y⋅sinβ$
- $w_y=l⋅sin(α+β)=l⋅(cosα⋅sinβ+sinα⋅cosβ)=v_x⋅sinβ+v_y⋅cosβ$
- $w_z=0$

따라서, $z$축 방향으로 $β$만큼 회전한 선형변환 $T(v)$는 다음과 같다.

$$
T(v)=(v_x⋅cosβ - v_y⋅sinβ, \ v_x⋅sinβ+v_y⋅cosβ, \ v_z)
$$

## 행렬 표현 유도

선형 변환을 행렬로 유도하는 과정은 다음과 같다.

1. 먼저, 기저벡터를 정의한다. (3차원 상의 기저벡터는 다음과 같다.)
    - $v_x=(1, 0, 0), v_y=(0, 1, 0), v_z=(0, 0, 1)$


2. 각 기저벡터를 선형변환에 대입한다.
    - $T(v_x)=(1⋅cosβ-0⋅sinβ, 1⋅sinβ-0⋅cosβ, 0)=(cosβ, sinβ, 0)$
    - $T(v_y)=(0⋅cosβ-1⋅sinβ, 0⋅sinβ-1⋅cosβ, 0)=(-sinβ, cosβ, 0)$
    - $T(v_z)=(0⋅cosβ-0⋅sinβ, 0⋅sinβ-0⋅cosβ, 1)=(0, 0, 1)$

3. 변환된 벡터를 확대행렬로 나열하면, 선형변환에 해당하는 행렬을 구할 수 있다. 따라서, $z$축 방향으로 $β$만큼 회전한 변환 행렬은 다음과 같다.

$$
M =\begin{bmatrix} T(v_x) & T(v_y) & T(v_z) \end{bmatrix} = \begin{bmatrix} cosβ & -sinβ & 0 \\ sinβ & cosβ & 0 \\ 0 & 0 & 1 \end{bmatrix}
$$