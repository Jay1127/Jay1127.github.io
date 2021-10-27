---
layout: single
title: "C++ : 5. Tesseract API 설치 및 사용법"
categories:
 - Cpp
---

## Tesseract 설치

`vcpkg`를 이용하여 `tesseract` 라이브러리를 설치한다.

```
> vcpkg install tesseract:x64-windows
```

## Tesseract API 사용법

- 다음 코드는 Tesseract API를 호출하여 이미지 내 글자를 인식한다.

```cpp
#define _CRT_SECURE_NO_WARNINGS

#include <iostream>
#include <leptonica/allheaders.h>
#include <tesseract/baseapi.h>

int main()
{
    const char* input_image = "C:/Users/user/Desktop/img.jpg";
    const char* dataPath = "C:/Program Files/Tesseract-OCR/tessdata";

    // tesseract api 설정
    tesseract::TessBaseAPI *api = new tesseract::TessBaseAPI();
    if (api->Init(dataPath, "kor")) {
        return -1;
    }

    // 이미지 설정
    Pix *image = pixRead(input_image);
    api->SetImage(image);
    
    std::string text = api->GetUTF8Text();

    std::cout << text << std::endl;
}
```

<br/>

- 아래 이미지에서 글자를 읽어, 콘솔에 출력하면 깨진 글자가 출력된다.

![image](https://user-images.githubusercontent.com/38006679/139007267-28fc0caa-f013-4bf8-93b2-bc7cbbbb8bdb.png)

![image](https://user-images.githubusercontent.com/38006679/139007287-3e884218-eb20-4b2e-89df-de777197b223.png)

<br/>

- `utf8`로 출력된 글자를 `ansi`로 변환하면, 한글 깨짐 문제를 해결할 수 있다. 변환 코드를 적용하면, `windows.h`와 `tesseract api`가 서로 충돌하여 컴파일 에러가 발생하기 때문에 `NOMINMAX`매크로를 선언한다.

```cpp
#define _CRT_SECURE_NO_WARNINGS
#define NOMINMAX

#include <windows.h>
#include <iostream>
#include <leptonica/allheaders.h>
#include <tesseract/baseapi.h>

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

int main()
{
    const char* input_image = "C:/Users/user/Desktop/img.jpg";
    const char* dataPath = "C:/Program Files/Tesseract-OCR/tessdata";

    // tesseract api 설정
    tesseract::TessBaseAPI *api = new tesseract::TessBaseAPI();
    if (api->Init(dataPath, "kor")) {
        return -1;
    }

    // 이미지 설정
    Pix *image = pixRead(input_image);
    api->SetImage(image);
    
    std::string utf_text = api->GetUTF8Text();
    std::string text = UTF8ToANSI(utf_text.c_str());

    std::cout << text << std::endl;
}
```

<br/>

- 출력 결과

![image](https://user-images.githubusercontent.com/38006679/139007302-f77460fb-b072-4b15-83a4-b612c5229bac.png)

## 참고

[1. utf8을 ansi로 인코딩하는 법(한글 깨짐 문제)](/cpp/1-Encode-Utf8-To-Ansi/)

[3. windows.h 선언 시, std::min, std::max 함수 컴파일 에러 해결 방법](/cpp/3-Conflict-Windows-header-to-std-min-max/)

[4. Tesseract 설치 방법](/cpp/4-Install-Tesseract/)

