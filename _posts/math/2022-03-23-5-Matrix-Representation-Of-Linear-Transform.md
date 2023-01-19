---
layout: single
title: "Math : 5. 선형 변환의 행렬 표현"
description: 선형 변환의 행렬 표현
categories:
 - Math
---

$n$차원의 벡터공간 $V$를 $m$차원의 벡터공간 $W$로 변환하는 선형변환 $T$는 다음과 같다.

$$
T : R^n→R^m
$$

벡터 공간 $V$의 임의의 벡터 $v$는 해당 벡터 공간의 기저 벡터($v_1.v_2,v_3,…v_n$)들의 선형 조합으로 나타낼 수 있다.

$$
v=c_1⋅v_1+ c_2⋅v_2+ c_3⋅v_3+…+ c_n⋅v_n=(c_1, c_2, c_3, …, c_n )= \begin{bmatrix} c_1 \\ c_2 \\ ... \\ c_n \end{bmatrix}
$$

이 벡터를 선형변환 $T$에 대입하면 다음과 같다.

$$
\begin{matrix} T(v) &=& T(c_1⋅v_1+ c_2⋅v_2+ c_3⋅v_3+…+ c_n⋅v_n) \\ &=& T(c_1⋅v_1 )+T(c_2⋅v_2 )+T(c_3⋅v_3 )+…+(c_n⋅v_n ) \\ &=& c_1⋅T(v_1)+ c_2⋅T(v_2)+ c_3⋅T(v_3)+…+ c_n⋅T(v_n) \end{matrix}
$$

결국, 선형 변환 $T(v_1), T(v_2), …, T(v_n)$의 값은 벡터 공간 $W$에 속하게 되므로, 벡터 공간 $W$의 기저 벡터들의 선형 조합으로 표현할 수 있다.

$$
T(v_i)=a_{(1,i)}⋅w_1+a_{(2,i)}⋅w_2+…+a_{(m,i)}⋅w_m=(a_{(1,i)} ,a_{(2,i)},…,a_{(m,i)})= \begin{bmatrix} a_{(1,i)} \\ a_{(2,i)} \\ ... \\ a_{(m,i)} \end{bmatrix}
$$

해당 식을 벡터 $v$에 대한 선형변환 $T(v)$에 대입하여 정리하면 다음과 같다.

$$
\begin{matrix} T(v) &=& c_1⋅T(v_1)+ c_2⋅T(v_2)+ c_3⋅T(v_3)+…+ c_n⋅T(v_n) \\ \\ &=& c_1 ⋅ \begin{bmatrix} a_{(1,1)} \\ a_{(2,1)} \\ ... \\ a_{(m,1)} \end{bmatrix} + c_2 ⋅ \begin{bmatrix} a_{(1,2)} \\ a_{(2,2)} \\ ... \\ a_{(m,2)} \end{bmatrix} + c_3 ⋅ \begin{bmatrix} a_{(1,3)} \\ a_{(2,3)} \\ ... \\ a_{(m,3)} \end{bmatrix} + ... + c_n ⋅ \begin{bmatrix} a_{(1,n)} \\ a_{(2,n)} \\ ... \\ a_{(m,n)} \end{bmatrix}\\ \\ &=& \begin{bmatrix} a_{(1,1)} & a_{(1,2)} & ... & a_{(1,n)} \\ a_{(2,1)} & a_{(2,2)} & ... & a_{(2,n)} \\ ... & ... & ... & ... \\ a_{(m,1)} & a_{(m,2)} & ... & a_{(m,n)} \end{bmatrix} \begin{bmatrix} c_1 \\ c_2 \\ ... \\ c_n \end{bmatrix} \\ \\ &=& \begin{bmatrix} \ [T(v_1)] & [T(v_2)] & ... & [T(v_n)] \ \end{bmatrix} \times v \\ \\ &=& M \times v \end{matrix}
$$

이제, 선형변환 $T$에 대한 행렬 $M$만 알고 있으면, 벡터 공간 $V$에 있는 임의의 벡터($v$)를 벡터공간 $W$의 벡터로 변환할 수 있다. 여기서, 행렬 $M$을 구하려면, 벡터 공간 $V$의 각 기저 벡터에 선형 변환 $T$를 적용한 벡터를 구하고, 해당 벡터들을 나열하면 된다.