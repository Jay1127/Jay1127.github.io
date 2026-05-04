---
layout: single
title: "AI : 7. MarkItDown으로 문서를 Markdown으로 변환하는 법"
description: MarkItDown 설치 및 문서 변환 방법 정리
date: 2026-05-04 09:00:00 +0900
series_order: 7
categories:
 - AI
---

`MarkItDown`은 PDF, Word, Excel, PowerPoint, 이미지, 오디오, HTML 같은 파일을 Markdown으로 변환해 주는 Python 도구다.

[https://github.com/microsoft/markitdown](https://github.com/microsoft/markitdown)


## 사전 준비

MarkItDown을 사용하려면 Python 3.10 이상이 필요하다.

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
```

## 설치

대부분의 파일 형식을 한 번에 지원하려면 `[all]` 옵션으로 설치한다.

```powershell
pip install 'markitdown[all]'
```

필요한 형식만 설치할 수도 있다.

```powershell
pip install 'markitdown[pdf,docx,pptx]'
```

## 지원하는 파일 형식

MarkItDown은 다음과 같은 형식을 Markdown으로 변환할 수 있다.

- PDF
- Word
- Excel
- PowerPoint
- 이미지
- 오디오
- HTML
- CSV, JSON, XML
- ZIP
- YouTube URL
- EPUB

## 기본 사용법

입력 파일과 출력 파일을 지정하면 Markdown 파일이 생성된다.

```powershell
markitdown path-to-file.pdf -o document.md
```

출력 파일을 지정하지 않으면 변환 결과를 터미널에서 바로 확인할 수 있다.

```powershell
markitdown path-to-file.pdf
```

## 주요 옵션

자주 쓰는 옵션은 다음과 같다.

- `-o`, `--output`
  변환한 Markdown을 저장할 파일을 지정한다.
- `-x`, `--extension`
  입력 파일의 확장자 힌트를 지정한다.
- `-m`, `--mime-type`
  입력 파일의 MIME 타입 힌트를 지정한다.
- `-c`, `--charset`
  텍스트 파일의 문자 인코딩 힌트를 지정한다.
- `-p`, `--use-plugins`
  설치된 플러그인을 활성화한다.
- `--keep-data-uris`
  data URI를 줄이지 않고 Markdown 안에 유지한다.

예를 들어, 파일 확장자를 직접 지정하려면 다음과 같이 사용한다.

```powershell
markitdown input-file --extension pdf -o document.md
```

이미지를 data URI 형태로 유지하려면 다음과 같이 사용한다.

```powershell
markitdown slides.pptx --keep-data-uris -o slides.md
```

## API 사용

API 사용 방법은 다음과 같다.

```python
from pathlib import Path

from markitdown import MarkItDown, StreamInfo
from openai import OpenAI

md = MarkItDown(
    enable_plugins=True,
    llm_client=OpenAI(),
    llm_model="gpt-4o",
    llm_prompt="이미지를 한국어로 설명해줘.",
)

result = md.convert(
    "path-to-file.pdf",
    stream_info=StreamInfo(
        extension=".pdf",
        mimetype="application/pdf",
    ),
    keep_data_uris=True,
)

Path("document.md").write_text(result.markdown, encoding="utf-8")
```

## 플러그인

MarkItDown은 플러그인을 지원하지만 기본값으로는 비활성화되어 있다.

설치된 플러그인을 확인하려면 다음 명령을 사용한다.

```powershell
markitdown --list-plugins
```

플러그인을 사용해서 변환하려면 `--use-plugins` 옵션을 추가한다.

```powershell
markitdown --use-plugins path-to-file.pdf
```

예를 들어 `markitdown-ocr` 플러그인은 문서 안의 이미지를 비전 모델로 OCR 처리한다.

```powershell
pip install markitdown-ocr openai
```

OCR 플러그인은 플러그인 활성화 외에도 LLM 클라이언트와 비전 모델 설정이 필요하다.

## 참고

MarkItDown은 문서 내용을 판단해서 다시 작성하는 AI 모델은 아니다.  
파일 형식별 파서와 변환기를 사용해 텍스트, 표, 제목, 목록 같은 구조를 Markdown으로 옮긴다.

옵션별 동작을 확인하기 위한 간단한 예제는 다음 링크에서 확인할 수 있다.

[https://github.com/Jay1127/MarkItDownGui](https://github.com/Jay1127/MarkItDownGui)
