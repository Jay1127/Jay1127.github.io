---
layout: single
title: "Math : 16. 평면과 직선의 교차점 찾는 법"
categories:
 - Math
---

![image](https://user-images.githubusercontent.com/38006679/160963298-552ddf3f-bafd-4ba7-a7ab-19fac2f4be9c.png){: .align-center}

$$
\begin{aligned}
   Line \ \ &: \ \ p + t \cdot v 
   \\
   Plane \ \  &: \ \ ax +by + cz + d = 0 
\end{aligned}
$$

먼저, 직선과 평면의 교차점 $p'$는 다음과 같다.

$$
p' = (p_x + t \cdot v_x, p_y + t \cdot v_y, p_z + t \cdot v_z)
$$

교차점 $p'$는 평면 위에 존재하므로, 평면의 방정식을 만족한다.

$$
\begin{aligned}
ax +by + cz + d &= 0 
\\ a \cdot (p_x + t \cdot v_x) + b \cdot (p_y + t \cdot v_y) + c \cdot (p_z + t \cdot v_z) + d &= 0 
\\ a \cdot p_x + b \cdot p_y + c \cdot p_z + d + t \cdot (a\cdot v_x + b\cdot v_y + c\cdot v_z) &= 0 
\\ t \cdot (a\cdot v_x + b\cdot v_y + c\cdot v_z) &= -(a \cdot p_x + b \cdot p_y + c \cdot p_z + d) 
\\ \\ 
\therefore t &= {-(a \cdot p_x + b \cdot p_y + c \cdot p_z + d) \over a\cdot v_x + b\cdot v_y + c\cdot v_z} 
\end{aligned}
$$

구한 매개변수 $t$를 직선의 방정식에 대입하면 평면과 직선의 교점을 찾을 수 잇다.