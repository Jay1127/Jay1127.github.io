---
layout: single
title: "C++ : 6. 특정 dll이 컴파일된 환경(x86 또는 x64) 알아내는 법(dumpbin)"
categories:
 - Cpp
---

비쥬얼 스튜디오에 포함된 `dumpbin.exe`를 이용하면, 특정 dll파일이 `x86` 또는 `x64`으로 컴파일됬는지 확인할 수 있다. 다음 명령어 입력 시 **`(PE32)`**이 출력되면 `x86`**,** **`(PE32+)`**이 출력되면 `x64`로 컴파일된 파일이다.

```powershell
> .\dumpbin.exe "dll 파일 경로" /Headers | findstr PE
```

<br/>

- 32비트 파일 출력 결과

```powershell
Microsoft (R) COFF/PE Dumper Version 14.00.24234.1
PE signature found
             10B magic # (PE32)
```

<br/>

- 64비트 파일 출력 결과

```powershell
Microsoft (R) COFF/PE Dumper Version 14.00.24234.1
PE signature found
             20B magic # **(PE32+)**
```