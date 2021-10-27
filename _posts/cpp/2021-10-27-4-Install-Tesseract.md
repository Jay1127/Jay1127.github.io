---
layout: single
title: "C++ : 4. Tesseract 설치 방법"
categories:
 - Cpp
---

## Tesseract 설치

- [다음 사이트](https://github.com/UB-Mannheim/tesseract/wiki)에서 64비트용 파일을 설치한다.
    - 설치 시 한글 언어팩 선택
    - 설치 후 설치 경로를 환경변수로 설정


## Tesseract 실행

- 샘플 이미지

![image](https://user-images.githubusercontent.com/38006679/139006895-2c90f9c8-7593-45e9-bdea-4bfa131783eb.png)

<br/>

- 커맨드 실행

```css
> tesseract img.jpg stdout -l kor
```

<br/>

- 실행 결과

![image](https://user-images.githubusercontent.com/38006679/139006948-257c5469-614d-4fa7-8918-e395ee5ed3ba.png)