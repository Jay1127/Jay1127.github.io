---
layout: single
title: "Math : 9. 임의의 축 회전 행렬 표현"
categories:
 - Math
---

벡터 $v$를 임의의 축 $r$로 $θ$만큼 회전한 벡터 $R(v)$는 다음과 같다.

$$
R(v)=cosθ⋅v+(1 -cosθ)⋅(v⋅\hat{r})⋅\hat{r} + (\hat{r} \times v) \cdot sin\theta
$$

벡터의 투영과 외적에 대한 행렬은 다음과 같으므로,

$$
(v⋅\hat{r})⋅\hat{r} = \begin{bmatrix} r_x^2 & r_x r_y & r_x r_z \\ r_x r_y & r_y^2 & r_y r_z \\ r_x r_z & r_y r_z & r_z^2 \end{bmatrix}
$$

$$
\hat{r} \times v = \begin{bmatrix} 0 & -r_z & r_y \\ r_z & 0 & -r_x \\ -r_y & r_x & 0 \end{bmatrix}
$$

이를 대입하면 임의의 축 회전 행렬을 구할 수 있다.

$$
\begin{align*} 
R(v) &= cosθ⋅v+(1 -cosθ)⋅(v⋅\hat{r})⋅\hat{r} + (\hat{r} \times v) \cdot sin\theta \\ \\ &= \begin{bmatrix} cos\theta & 0 & 0 \\ 0 & cos\theta & 0 \\ 0 & 0 & cos\theta\end{bmatrix} + (1 - cos\theta) \begin{bmatrix} r_x^2 & r_x r_y & r_x r_z \\ r_x r_y & r_y^2 & r_y r_z \\ r_x r_z & r_y r_z & r_z^2 \end{bmatrix} + sin\theta \begin{bmatrix} 0 & -r_z & r_y \\ r_z & 0 & -r_x \\ -r_y & r_x & 0 \end{bmatrix} \\ \\ &=\begin{bmatrix} cosθ + (1-cosθ) \cdot r_x^2 & (1-cosθ) \cdot r_x \cdot r_y-sinθ \cdot r_z & (1-cosθ) \cdot r_x \cdot r_z+sinθ \cdot r_y \\ (1-cosθ) \cdot r_x \cdot r_y+sinθ \cdot r_z & cosθ+(1-cosθ) \cdot r_y^2 & (1-cosθ) \cdot r_y \cdot r_z-sinθ \cdot r_x \\  (1-cosθ) \cdot r_x \cdot r_z-sinθ \cdot r_y & (1 -cosθ) \cdot r_y \cdot r_z+sinθ \cdot r_x & cosθ + (1-cosθ) \cdot r_z^2 \end{bmatrix}
\end{align*}
$$