---
layout: single
title: "Math : 4. 스칼라 삼중곱(Scalar triple product)"
categories:
 - Math
---

## 정의

스칼라 삼중곱은 두 벡터를 외적해서 나온 벡터에 다른 벡터를 내적하면 스칼라가 나오는 연산을 말한다.

$$
a \cdot (b \times c)
$$

## 성질

![image](https://user-images.githubusercontent.com/38006679/157789466-88f222f5-f860-4699-9d57-a68e70cd7cfb.png){: .align-center}


- 해당 연산으로 나오는 스칼라 값은 세 개의 벡터가 이루는 평행육면체의 부피와 같다.

$$
\begin{matrix} V &=& h \cdot \text{평행사변형 넓이} \\ &=& \parallel a \parallel \cdot \ cos(\alpha) \ \cdot \parallel (b \times c) \parallel \\ &=& \parallel a \parallel \cdot \parallel (b \times c) \parallel \cdot \ cos(\alpha) \\ &=& \parallel a \cdot (b \times c) \parallel \end{matrix}
$$

- 세 개의 벡터가 이루는 평행육면체의 형상은 항상 같기 때문에 부피도 항상 동일하다. 따라서 곱하는 순서에 상관없이 항상 같은 값이 나온다.

$$
a \cdot (b \times c) = b \cdot (c \times a) = c \cdot (a \times b)
$$