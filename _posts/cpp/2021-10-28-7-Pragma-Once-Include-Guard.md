---
layout: single
title: "C++ : 7. 헤더 중복 포함(include) 방지(#include guard, #program once)"
categories:
 - Cpp
---

## #include guard

헤더 파일이 중복해서 포함되면 컴파일 에러가 발생하므로, `#include guard`를 추가해서 이를 방지할 수 있다.

```cpp
// 첫번째 include할 때는 MATH_H가 없으므로, MATH_H를 정의하고 헤더 파일 내용을 include함.
// 그 다음 include할 떄는 MATH_H가 이미 정의됐으므로, 헤더 파일 내용을 무시함.
#ifndef MATH_H
#define MATH_H

// 헤더 파일 내용

#endif
```

## #pragma once

`#pragma once`를 선언하면, `#include guard`와 동일하게 동작한다.

`#include guard`를 사용하는 것보다 덜 번거롭지만, C++표준이 아니므로 컴파일러가 지원하지 않을 수 있다.

```cpp
#pragma once

// 헤더 파일 내용
```