---
layout: single
title: "AI : 11. Whisper와 pyannote 결과를 합치는 법"
description: Whisper 텍스트 결과와 pyannote 화자 구간을 시간 기준으로 합치는 방법 정리
date: 2026-05-13 09:00:00 +0900
series_order: 11
categories:
 - AI
---

Whisper는 음성을 텍스트와 시간 구간으로 변환한다.
pyannote는 같은 음성에서 화자와 시간 구간을 찾는다.

두 결과를 합치려면 시간을 기준으로 맞추면 된다.

```text
Whisper  : 0.0s ~ 3.0s  안녕하세요
pyannote : 0.0s ~ 3.2s  SPEAKER_00

결과     : SPEAKER_00  안녕하세요
```


## 기본 흐름

가장 단순한 방식은 Whisper segment와 가장 많이 겹치는 pyannote 화자 구간을 선택하는 것이다.

```text
Whisper  : 10.0s ~ 14.0s

SPEAKER_00  10.0s ~ 11.0s  1초 겹침
SPEAKER_01  11.0s ~ 14.0s  3초 겹침

선택: SPEAKER_01
```

## 예제 코드

다음 예제는 Whisper 결과와 pyannote 결과를 한 번에 만든 뒤 시간 기준으로 합친다.

```python
import whisper
from pyannote.audio import Pipeline


def overlap_seconds(start_a, end_a, start_b, end_b):
    start = max(start_a, start_b)
    end = min(end_a, end_b)
    return max(0.0, end - start)


def find_speaker(segment, diarization):
    segment_start = segment["start"]
    segment_end = segment["end"]

    best_speaker = "UNKNOWN"
    best_overlap = 0.0

    for turn, speaker in diarization:
        overlap = overlap_seconds(
            segment_start,
            segment_end,
            turn.start,
            turn.end,
        )

        if overlap > best_overlap:
            best_overlap = overlap
            best_speaker = speaker

    return best_speaker


audio_path = "audio.wav"

whisper_model = whisper.load_model("small")
whisper_result = whisper_model.transcribe(audio_path)

pipeline = Pipeline.from_pretrained(
    "pyannote/speaker-diarization-community-1",
    token="HUGGINGFACE_TOKEN",
)

pyannote_result = pipeline(audio_path)
diarization = pyannote_result.exclusive_speaker_diarization

for segment in whisper_result["segments"]:
    speaker = find_speaker(segment, diarization)
    text = segment["text"].strip()
    print(f"{speaker}: {text}")
```

## 결과 형태

출력은 다음과 같은 형태가 된다.

```text
SPEAKER_00: 안녕하세요. 오늘 회의를 시작하겠습니다.
SPEAKER_01: 네, 먼저 진행 상황부터 공유드리겠습니다.
SPEAKER_00: 좋습니다. 그 부분부터 확인해 보죠.
```

## 화자 구간 맞추기

이 방식은 Whisper segment 단위로 화자를 붙인다.
그래서 문장 경계와 화자 전환 지점이 항상 정확히 맞지는 않을 수 있다.

예를 들어 Whisper segment가 화자 전환 지점을 걸쳐 잡히면 다음처럼 보일 수 있다.

```text
SPEAKER_00: 안녕하세요. 오늘 회의를 시작하겠습니다. 네, 먼저 진행
SPEAKER_01: 상황부터 공유드리겠습니다.
```

이 경우 실제로는 `네, 먼저 진행 상황부터 공유드리겠습니다.`가 다음 화자의 발화일 수 있다.

더 세밀하게 맞추려면 Whisper의 단어 타임스탬프를 사용할 수 있다.

```python
whisper_result = whisper_model.transcribe(
    audio_path,
    word_timestamps=True,
)
```

단어 타임스탬프를 사용하면 각 단어의 시간 구간을 기준으로 화자를 찾을 수 있다.

```text
SPEAKER_01: 네,
SPEAKER_01: 먼저
SPEAKER_01: 진행
SPEAKER_01: 상황부터
SPEAKER_01: 공유드리겠습니다
```

다만 단어별 결과를 그대로 출력하면 읽기 어렵기 때문에, 같은 화자가 이어지는 단어를 다시 묶는 후처리가 필요하다.
