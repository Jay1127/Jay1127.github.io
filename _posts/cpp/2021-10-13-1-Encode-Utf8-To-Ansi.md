---
layout: single
title: "C++ : 1. utf8을 ansi로 인코딩하는 법(한글 깨짐 문제)"
categories:
 - Cpp
---

`utf8`에서 한글이 깨져나오는 경우 `ansi`로 변환하면 제대로 된 출력 결과를 얻을 수 있다.

```cpp
#include <OleAuto.h>

char* UTF8ToANSI(const char *pszCode)
{
    BSTR    bstrWide;
    char*   pszAnsi;
    int     nLength;

    // Get nLength of the Wide Char buffer
    nLength = MultiByteToWideChar(CP_UTF8, 0, pszCode, strlen(pszCode) + 1,
        NULL, NULL);
    bstrWide = SysAllocStringLen(NULL, nLength);

    // Change UTF-8 to Unicode (UTF-16)
    MultiByteToWideChar(CP_UTF8, 0, pszCode, strlen(pszCode) + 1, bstrWide, nLength);

    // Get nLength of the multi byte buffer
    nLength = WideCharToMultiByte(CP_ACP, 0, bstrWide, -1, NULL, 0, NULL, NULL);
    pszAnsi = new char[nLength];

    // Change from unicode to mult byte
    WideCharToMultiByte(CP_ACP, 0, bstrWide, -1, pszAnsi, nLength, NULL, NULL);
    SysFreeString(bstrWide);

    return pszAnsi;
}
```