---
layout: single
title: "AI : 8. Whisper로 음성을 텍스트로 변환하는 법"
description: Whisper 설치 및 음성 텍스트 변환 방법 정리
date: 2026-05-07 09:00:00 +0900
series_order: 8
categories:
 - AI
---

`Whisper`는 음성 파일을 텍스트로 변환하는 음성 인식 모델이다.

[https://github.com/openai/whisper](https://github.com/openai/whisper)


## 사전 준비

로컬에서 Whisper를 사용하려면 Python과 FFmpeg가 필요하다.

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
```

FFmpeg는 Chocolatey나 Scoop으로 설치할 수 있다.

```powershell
choco install ffmpeg
```

## 설치

로컬에서 실행하려면 `openai-whisper` 패키지를 설치한다.

```powershell
pip install -U openai-whisper
```

## 기본 사용법

기본 형태는 입력 파일 뒤에 필요한 옵션을 붙이는 방식이다.

한국어 음성을 텍스트 파일로 저장하려면 다음과 같이 사용한다.

```powershell
whisper audio.mp3 --model small --language Korean --output_format txt
```

음성을 영어 텍스트로 번역하려면 작업을 `translate`로 바꾼다.

```powershell
whisper audio.mp3 --model small --task translate --output_format txt
```

자막 파일이 필요하면 출력 형식을 `srt` 또는 `vtt`로 바꾸면 된다.

```powershell
whisper audio.mp3 --model small --language Korean --output_format srt
```

`--output_format`을 지정하지 않으면 여러 형식의 파일이 함께 생성된다.

## 로컬 CLI 옵션

Whisper CLI에서 사용할 수 있는 주요 옵션은 다음과 같다.

### 입력과 모델

- `audio`
  변환할 음성 파일을 지정한다. 여러 파일을 한 번에 넘길 수도 있다.
- `--model`
  사용할 Whisper 모델을 지정한다.
  - `tiny`, `base`, `small`, `medium`, `large`, `turbo`
- `--model_dir`
  모델 파일을 저장할 폴더를 지정한다. 비워두면 기본 캐시 폴더를 사용한다.
- `--device`
  실행에 사용할 장치를 지정한다.
  - `cpu`, `cuda`

### 출력

- `--output_dir`, `-o`
  출력 파일을 저장할 폴더를 지정한다.
- `--output_format`, `-f`
  출력 형식을 지정한다.
  - `txt`, `vtt`, `srt`, `tsv`, `json`, `all`
- `--verbose`
  처리 중 진행 상황과 인식된 구간 텍스트를 출력할지 지정한다.

### 변환 작업

- `--task`
  `transcribe` 또는 `translate` 작업을 지정한다.
  `translate`는 음성을 영어 텍스트로 번역한다.
- `--language`
  음성 언어를 지정한다. 지정하지 않으면 언어를 자동으로 감지한다.
- `--initial_prompt`
  음성 인식에 참고할 문맥 힌트를 지정한다.
- `--carry_initial_prompt`
  `initial_prompt`의 문맥 힌트를 뒤쪽 음성 인식에도 계속 사용할지 지정한다.
- `--condition_on_previous_text`
  앞에서 인식한 내용을 다음 구간의 문맥으로 사용할지 지정한다.

### 디코딩

- `--temperature`
  인식 후보를 고를 때 사용할 샘플링 온도를 지정한다.
- `--best_of`
  샘플링 온도가 0보다 클 때 비교할 후보 수를 지정한다.
- `--beam_size`
  샘플링 온도가 0일 때 유지할 문장 후보 수를 지정한다.
- `--patience`
  문장 후보 탐색을 얼마나 더 이어갈지 지정한다.
- `--length_penalty`
  문장 길이에 대한 보정값을 지정한다.
- `--suppress_tokens`
  결과에서 제외할 토큰 번호를 지정한다. 보통 기본값을 사용한다.
- `--fp16`
  반정밀도 연산 사용 여부를 지정한다. GPU에서는 기본적으로 사용하고, CPU에서는 FP32로 처리된다.
- `--temperature_increment_on_fallback`
  인식 결과가 불안정할 때 샘플링 온도를 얼마나 올려 다시 시도할지 지정한다.
- `--compression_ratio_threshold`
  반복 문장이 많다고 판단할 기준값을 지정한다.
- `--logprob_threshold`
  토큰 예측 신뢰도가 낮다고 판단할 기준값을 지정한다.
- `--no_speech_threshold`
  말이 없는 구간으로 판단할 기준값을 지정한다.

### 타임스탬프와 자막

아래 옵션들은 단어 단위 시간 정보나 자막 출력 방식을 조정할 때 사용한다.

- `--word_timestamps`
  단어별 시작 시간과 끝 시간을 추출한다.
- `--prepend_punctuations`
  이미 인식된 여는 괄호나 따옴표를 다음 단어 앞에 붙이도록 지정한다.
- `--append_punctuations`
  이미 인식된 쉼표나 마침표를 이전 단어 뒤에 붙이도록 지정한다.
- `--highlight_words`
  단어별 시간 정보가 있을 때, `srt`, `vtt` 자막에서 현재 발화 중인 단어가 강조되도록 만든다.
- `--max_line_width`
  단어 타임스탬프 기반 자막에서 한 줄의 최대 글자 수를 지정한다.
- `--max_line_count`
  단어 타임스탬프 기반 자막에서 한 구간의 최대 줄 수를 지정한다.
- `--max_words_per_line`
  단어 타임스탬프 기반 자막에서 한 줄의 최대 단어 수를 지정한다.
- `--hallucination_silence_threshold`
  단어별 시간 정보가 있을 때, 잘못 인식된 것으로 보이는 구간 주변의 긴 무음 구간을 건너뛸 기준 초를 지정한다.

### 실행 제어

- `--threads`
  CPU 실행에 사용할 스레드 수를 지정한다.
- `--clip_timestamps`
  처리할 구간의 시작, 끝 시간을 초 단위로 지정한다.

## 예제 코드

다음은 음성 파일을 텍스트 파일로 저장하는 간단한 예제다.

```python
import whisper

model = whisper.load_model("small")

result = model.transcribe(
    "audio.mp3",
    language="Korean",
    task="transcribe",
    fp16=False,
)

with open("audio.txt", "w", encoding="utf-8") as file:
    file.write(result["text"].strip())
```

## 참고

옵션별 동작을 확인하기 위한 간단한 예제는 다음 링크에서 확인할 수 있다.

[https://github.com/Jay1127/WhisperGui](https://github.com/Jay1127/WhisperGui)

![Whisper GUI 실행 화면](/assets/images/whisper-gui.png)
