---
layout: single
title: "Graphics : 2. STL 파일 읽는 방법"
description: STL 파일 읽는 방법
categories:
 - Graphics
---

## 정의

3차원 객체를 색상, 텍스쳐 등의 정보를 제외하고 표면 정보만 삼각형화하여 정의한 파일

## ASCII STL

- ASCII STL파일은 `solid`로 헤더를 정의하며 시작한다.
- 헤더의 `name`은 생략될 수 있지만 `solid` 뒤에 빈칸이 있어야 한다.
- 이후 삼각형 정점 세개와 해당 면의 법선을 반복하여 나열한다.
- ASCII STL파일은 `endsolid`로 끝난다.

```
solid name

facet normal n.x n.y n.z
  outer loop
    vertex v1.x v1.y v1.z
    vertex v2.x v2.y v2.z
    vertex v3.x v3.y v3.z
  endloop
endfacet

endsolid name
```

## Binary STL

- 80개의 문자(80byte)를 가진 헤더로 시작한다.
- 헤더 다음은 4바이트(리틀엔디안(little-endian)으로 표현) 정수로 삼각형 면의 수를 나타낸다.
- 이후는 삼각형 면의 법선과 정점을 나열한다.

```
UINT8[80] – Header
UINT32 – Number of triangles

foreach triangle
  REAL32[3] – Normal vector
  REAL32[3] – Vertex 1
  REAL32[3] – Vertex 2
  REAL32[3] – Vertex 3
  UINT16 – Attribute byte count
end
```

## 소스코드

ASCII STL파일은 문자열을 규칙에 따라서 읽어오고, Binary STL파일은 지정된 바이트만큼 읽어서 값을 가져오면 된다.

[https://github.com/Jay1127/SimpleSTLReader](https://github.com/Jay1127/SimpleSTLReader)

## 참고

[https://en.wikipedia.org/wiki/STL_(file_format)](https://en.wikipedia.org/wiki/STL_(file_format))