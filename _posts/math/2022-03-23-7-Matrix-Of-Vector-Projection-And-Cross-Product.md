---
layout: single
title: "Math : 7.  벡터의 투영과 외적의 변환 행렬 표현"
categories:
 - Math
---

## 벡터의 투영 행렬 표현

벡터 $v$를 단위 벡터인 $w$에 투영한 벡터는 다음과 같다.

- $v_{proj}=(v⋅w)⋅w=(v_x⋅w_x+v_y⋅w_y+v_z⋅w_z)⋅(w_x,w_y,w_z)$

각 기저 벡터를 대입하여, 벡터 $v$를 $v_{proj}$로 변환하는 변환 행렬을 구할 수 있다.

- $T(a_x)=(1⋅w_x+0⋅w_y+0⋅w_z)⋅(w_x,w_y,w_z)=(w_x^2,\ w_x⋅w_y,\ w_x⋅w_z)$
- $T(a_y)=(0⋅w_x+1⋅w_y+0⋅w_z)⋅(w_x,w_y,w_z)=(w_x⋅w_y,\ w_y^2,\ w_y⋅w_z)$
- $T(a_z)=(0⋅w_x+0⋅w_y+1⋅w_z)⋅(w_x,w_y,w_z)=(w_x⋅w_z,\ w_y⋅w_z,\ w_z^2)$

$$
M =\begin{bmatrix} T(v_x) & T(v_y) & T(v_z) \end{bmatrix} = \begin{bmatrix} w_x^2 & w_x⋅ w_y & w_x⋅ w_z \\ w_x ⋅w_y & w_y^2 & w_y⋅ w_z \\ w_x ⋅ w_z & w_y ⋅ w_z & w_z^2 \end{bmatrix}
$$

## 벡터의 외적 행렬 표현

벡터 $v,w$를 외적한 벡터는 다음과 같다.

- $v_{cross}=v \times w=(v_y⋅w_z-w_y⋅v_z, v_z⋅w_x-w_z⋅v_x, v_x⋅w_y-w_x⋅v_y)$

각 기저 벡터를 대입하여, 벡터 $v$를 $v_{cross}$ 로 변환하는 행렬을 구할 수 있다.

- $T(a_x)=(0⋅w_z-w_y⋅0, 0⋅w_x-w_z⋅1, 1⋅w_y-w_x⋅0)=(0, -w_z, w_y)$
- $T(a_y)=(1⋅w_z-w_y⋅0, 0⋅w_x-w_z⋅0, 0⋅w_y-w_x⋅1)=(w_z, 0, -w_x)$
- $T(a_z)=(0⋅w_z-w_y⋅1, 1⋅w_x-w_z⋅0, 0⋅w_y-w_x⋅0)=(-w_y, w_x, 0)$

$$
M =\begin{bmatrix} T(v_x) & T(v_y) & T(v_z) \end{bmatrix} = \begin{bmatrix} 0 & w_z & -w_y \\ -w_z & 0 & w_x \\ w_y & -w_x & 0 \end{bmatrix}
$$