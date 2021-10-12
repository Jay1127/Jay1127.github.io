---
layout: single
title: "C++ : 3. windows.h 선언 시, std::min, std::max 함수 컴파일 에러 해결 방법"
categories:
 - Cpp
---

`std::min`, `std::max` 함수를 사용할 때, `windows.h`헤더가 선언된 경우, 컴파일 에러가 발생한다.

```cpp
#include <windows.h>
#include <algorithm>

int main()
{
    auto min = std::min(1, 2);    
}
```

![image](https://user-images.githubusercontent.com/38006679/137044092-0bc1f898-2ed7-4a63-b13b-ad3a9ac2c375.png){: .align-center}

<br/>

에러 발생 원인은 `windows.h`에는 매크로로 `min`, `max`가 이미 정의되어 있기 때문이다.

```cpp
// windows.h에는 이미 정의가 되어 있음.
// 예시코드로 실제 구현과는 다름.
#define min(a,b)            (((a) < (b)) ? (a) : (b))
#define max(a,b)            (((a) > (b)) ? (a) : (b))
```

`#define NOMINMAX`을 선언하면 `min`, `max` 매크로가 정의되는 것을 막을 수 있다.

```cpp
#define NOMINMAX

#include <windows.h>
#include <algorithm>

int main()
{
    auto min = std::min(1, 2);    
}
```