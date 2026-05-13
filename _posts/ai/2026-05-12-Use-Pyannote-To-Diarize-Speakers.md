---
layout: single
title: "AI : 10. pyannote로 음성 화자 구분하는 법"
description: pyannote.audio를 사용한 음성 화자 구분 방법 정리
date: 2026-05-12 09:00:00 +0900
series_order: 10
categories:
 - AI
---

`pyannote.audio`는 음성에서 화자 구간을 찾는 라이브러리다.

Whisper가 음성을 텍스트로 바꾼다면, pyannote는 누가 언제 말했는지 구분한다.

[https://github.com/pyannote/pyannote-audio](https://github.com/pyannote/pyannote-audio)


## 사전 준비

이 글에서는 `community-1` 모델을 사용한다.
모델을 내려받으려면 Hugging Face 토큰이 필요하다.

[https://huggingface.co/pyannote/speaker-diarization-community-1](https://huggingface.co/pyannote/speaker-diarization-community-1)

토큰을 로컬에 저장해 두려면 다음 명령으로 로그인한다.

```powershell
hf auth login
```

## 설치

`pyannote.audio` 패키지를 설치한다.

```powershell
pip install pyannote.audio
```

Windows에서 `torchcodec` 오디오 디코딩 오류가 발생하면 shared FFmpeg를 사용하고 있는지 확인한다.

```powershell
where.exe ffmpeg
```

`where.exe ffmpeg`로 확인한 폴더에 `avcodec-*.dll`, `avformat-*.dll`, `avutil-*.dll` 같은 파일이 있어야 한다.
`ffmpeg.exe`만 있다면 shared FFmpeg가 아니다.

## 기본 사용법

기본 형태는 `Pipeline`을 만들고 음성 파일을 넘기는 방식이다.

```python
from pyannote.audio import Pipeline

pipeline = Pipeline.from_pretrained(
    "pyannote/speaker-diarization-community-1",
    token="HUGGINGFACE_TOKEN",
)

output = pipeline("audio.wav")

for turn, speaker in output.speaker_diarization:
    print(f"{turn.start:.1f}s ~ {turn.end:.1f}s: {speaker}")
```

실행 결과는 다음과 같이 화자별 시간 구간으로 나온다.

```text
0.0s ~ 3.2s: SPEAKER_00
3.5s ~ 8.1s: SPEAKER_01
8.4s ~ 12.0s: SPEAKER_00
```

## 주요 옵션

- `num_speakers`
  화자 수를 알고 있을 때 지정한다.
- `min_speakers`
  예상되는 최소 화자 수를 지정한다.
- `max_speakers`
  예상되는 최대 화자 수를 지정한다.

화자 수를 알고 있다면 `num_speakers`를 사용한다.

```python
output = pipeline(
    "audio.wav",
    num_speakers=2,
)
```

정확한 화자 수를 모른다면 `min_speakers`, `max_speakers`로 범위를 지정한다.

```python
output = pipeline(
    "audio.wav",
    min_speakers=2,
    max_speakers=4,
)
```

## 화자 구간 결과

`community-1`의 `output`에서는 두 가지 화자 구간을 확인할 수 있다.

기본 결과인 `speaker_diarization`은 두 화자의 시간이 겹쳐 나올 수 있다.
예를 들면 다음과 같은 형태다.

```text
SPEAKER_00  10.0 ~ 13.0
SPEAKER_01  12.0 ~ 15.0
```

반면 `exclusive_speaker_diarization`은 한 시점에 한 명의 화자만 남도록 정리한 결과다.
같은 구간이라도 다음과 같이 시간이 겹치지 않는다.

```text
SPEAKER_00  10.0 ~ 12.0
SPEAKER_01  12.0 ~ 15.0
```

각 값은 `output`에서 꺼내 사용할 수 있다.

```python
diarization = output.speaker_diarization
exclusive_diarization = output.exclusive_speaker_diarization
```

## Whisper 결과와 함께 사용

Whisper와 pyannote를 함께 사용할 때는 두 결과의 시간을 기준으로 맞춘다.

```text
Whisper  : 0.0s ~ 3.0s  안녕하세요
pyannote : 0.0s ~ 3.2s  SPEAKER_00

결과     : SPEAKER_00  안녕하세요
```

두 결과의 시간이 겹치는 구간을 찾아 텍스트에 화자 이름을 붙이는 방식이다.
