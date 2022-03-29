---
layout: single
title: "Math : 8.  임의의 축 회전 공식 유도(로드리게스 회전 공식)"
categories:
 - Math
---

![image](https://user-images.githubusercontent.com/38006679/160548406-49943858-f436-4eb9-b9f7-864e91d53cec.png){: .align-center}

벡터 $v$를 임의의 벡터 $r$을 회전축으로 $θ$만큼 회전한 벡터 $R(v)$를 구하는 방법은 다음과 같다.

먼저, 벡터 $v$는 회전축 $r$에 투영시킨 벡터 $v_{\parallel}$와 두 벡터를 잇는 벡터 $v_{\bot}$로 나눠서 표현한다.

- $v_{\parallel} = (v \cdot \hat{r}) \cdot \hat{r}$
- $v_{\bot} = v - v_{\parallel}$
- $v= v_{\parallel} + v_{\bot}$

<br/>

다음으로, 벡터 $v_{\bot}$를 벡터 $r$을 회전축으로 $θ$만큼 회전한 벡터를 $R(v_{\bot})$로 정의하면, $R(v)$를 다음과 같이 나타낼 수 있다.

- $R(v)= v_{\parallel} + R(v_{\bot})$

![image](https://user-images.githubusercontent.com/38006679/160548444-32e62d44-288d-423e-b576-3d5539455ae1.png){: .align-center}

<br/>

$R(v_{\bot})$를 구하기 위해서 두 벡터 $\hat{r}, v$를 외적한 벡터 $w$를 이용한다.

- $w= \hat{r} \times v$
- $\parallel w \parallel = \parallel \hat{r} \parallel \cdot \parallel v \parallel \cdot sin(\alpha) = \parallel v \parallel \cdot sin(\alpha) = \parallel v_{\bot} \parallel$ ($α$는 두 벡터의 사이각)

![image](https://user-images.githubusercontent.com/38006679/160548488-63fb6e7c-871d-4f2b-a709-2f3a2a1285a1.png){: .align-center}

벡터 $w$는 두 벡터 $\hat{r}, \ v$로 만들어지는 평면의 법선벡터이므로, 해당 평면 위 벡터인 $v_{\bot}$도 벡터 $w$와 수직을 이룬다. 따라서, 벡터 $R(v_{\bot})$를 두 벡터 $w,v_{\bot}$를 축으로 표현할 수 있다.

$$
\begin{align*}  R(v_{\bot}) \ \ \ &= \ \ \ \parallel R(v_{\bot}) \parallel ⋅ \ cos(\theta) ⋅ \hat{v}_{\bot} + \parallel R(v{\bot}) \parallel ⋅ \ sin(\theta)⋅ \hat{w} \\ \ \ \ &= \ \ \  \parallel v_{\bot} \parallel ⋅ \ cos(\theta) ⋅ \hat{v}_{\bot} + \parallel v{\bot} \parallel ⋅ \ sin(\theta)⋅\hat{w} \\ \ \ \ &= \ \ \  \parallel v_{\bot} \parallel ⋅ \ cos(\theta) ⋅ \frac{v_{\bot}}{\parallel v_{\bot} \parallel} + \parallel v_{\bot} \parallel ⋅ \ sin(\theta)⋅ \frac{w}{\parallel w \parallel} \\ \ \ \ &= \ \ \  v_{\bot} ⋅ \ cos(\theta) + \parallel v_{\bot} \parallel ⋅ \ sin(\theta)⋅ \frac{w}{\parallel v_{\bot} \parallel} \\ \ \ \ &= \ \ \  v_{\bot} ⋅ \ cos(\theta) + w ⋅ \ sin(\theta)
\end{align*}
$$

위에서 구한 $R(v_{\bot})$값을 대입하면, 벡터 $R(v)$를 구할 수 있다.

$$
\begin{align*}  R(v) \ \ \ &= \ \ \ v_{\parallel} + R(v_{\bot}) \\ \ \ \ &= \ \ \ v_{\parallel} + v_{\bot} ⋅ cos(\theta) + w ⋅ sin(\theta) \\ \ \ \ &= \ \ \ v_{\parallel} + (v - v_{\parallel})⋅ cos(\theta) + (\hat{r} \times v) ⋅ sin(\theta) \\ \ \ \ &= \ \ \ cos(\theta) ⋅ v + (1 - cos(\theta)) ⋅ v_{\parallel} + (\hat{r} \times v) ⋅ sin(\theta) \\ \ \ \ &= \ \ \ cos(\theta) ⋅ v + (1 - cos(\theta)) ⋅ (v \cdot \hat{r}) \cdot r + (\hat{r} \times v) ⋅ sin(\theta) 
\end{align*}
$$

즉, 공간상 임의의 벡터 $v$를 임의의 벡터 $r$을 회전축으로 $θ$만큼 회전했을 때, 만들어지는 벡터 $v_r$은 다음과 같다.

$$
v_r = cos(\theta) ⋅ v + (1 - cos(\theta)) ⋅ (v \cdot \hat{r}) \cdot r + (\hat{r} \times v) ⋅ sin(\theta)
$$