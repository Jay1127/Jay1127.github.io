---
layout: single
title: "AI : 9. faster-whisper로 Whisper를 더 빠르게 실행하는 법"
description: faster-whisper 설치 및 음성 텍스트 변환 방법 정리
date: 2026-05-11 09:00:00 +0900
series_order: 9
categories:
 - AI
---

`faster-whisper`는 CTranslate2 기반으로 Whisper 모델을 실행해 주는 라이브러리다.

[https://github.com/SYSTRAN/faster-whisper](https://github.com/SYSTRAN/faster-whisper)


## 설치

`faster-whisper` 패키지를 설치한다.

```powershell
pip install faster-whisper
```

GPU로 실행하려면 CUDA와 cuDNN 환경이 필요하다.  
GPU 실행 중 DLL 관련 오류가 발생하면 CUDA와 cuDNN DLL이 PATH에 잡혀 있는지 확인한다.

```powershell
where.exe cublas64_12.dll
where.exe cudnn64_9.dll
```

## 주요 옵션

- `compute_type`
  모델을 어떤 계산 방식으로 실행할지 지정한다.
  속도와 메모리 사용량에 영향을 준다.
  - `default`, `float32`, `float16`, `int8`
- `vad_filter`
  음성이 없는 구간을 먼저 제외한 뒤 인식한다.
- `batch_size`
  한 번에 처리할 구간 수를 지정한다.
- `hotwords`
  인식될 가능성이 있는 단어나 문구를 힌트로 전달한다.
  결과를 강제로 바꾸는 기능은 아니다.

## 기본 사용법

기본 형태는 `WhisperModel`을 만들고 `transcribe()`에 음성 파일을 넘기는 방식이다.  
`segments`는 순회할 때 인식 결과가 생성되므로 보통 `for` 문으로 차례대로 처리한다.

```python
from faster_whisper import WhisperModel

model = WhisperModel(
    "small",
    device="cpu",
    compute_type="int8",
)

segments, info = model.transcribe(
    "audio.mp3",
    language="ko",
)

for segment in segments:
    print(f"[{segment.start:.2f}s -> {segment.end:.2f}s] {segment.text}")
```

여러 구간을 배치로 처리하려면 `BatchedInferencePipeline`을 사용한다.  
`batch_size`를 키우면 속도가 빨라질 수 있지만 메모리 사용량도 함께 늘어난다.

```python
from faster_whisper import BatchedInferencePipeline, WhisperModel

model = WhisperModel(
    "small",
    device="cpu",
    compute_type="int8",
)

batched_model = BatchedInferencePipeline(model=model)

segments, info = batched_model.transcribe(
    "audio.mp3",
    batch_size=8,
    language="ko",
)

for segment in segments:
    print(segment.text)
```

## 참고

옵션별 동작을 확인하기 위한 간단한 예제는 다음 링크에서 확인할 수 있다.

[https://github.com/Jay1127/WhisperGui](https://github.com/Jay1127/WhisperGui)


![Whisper GUI 실행 화면](/assets/images/faster-whisper-gui.png)