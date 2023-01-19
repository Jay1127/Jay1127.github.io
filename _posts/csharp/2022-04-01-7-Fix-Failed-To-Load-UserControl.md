---
layout: single
title: ".NET : 7. 에러메세지 - 도구 상자 항목 ‘UserControl’을 로드하지 못했습니다. 해당 항목은 도구 상자에서 제거됩니다. "
description: 에러메세지 - 도구 상자 항목 ‘UserControl’을 로드하지 못했습니다. 해당 항목은 도구 상자에서 제거됩니다.
categories:
 - CSharp
---

`x64`로 설정한 `Winform`프로젝트에서 `UserControl`을 로드할 경우에 다음과 같은 에러메세지가 발생한다. 원인은 비주얼 스튜디오(2019)가 `x32`버전이므로, 디자이너가 `x64`로 빌드된 컨트롤을 로드하지 못하기 떄문이다.

![image](https://user-images.githubusercontent.com/38006679/161206712-e1747a07-b5ba-421d-8409-19fc7b8ea159.png){: .align-center}

<br/>

플랫폼 대상을 변경할 수 있다면, `x64`로 설정된 프로젝트를 `Any CPU`로 변경하면 컨트롤을 디자이너에 올릴 수 있다.

![image](https://user-images.githubusercontent.com/38006679/161206746-df5a7767-4543-4218-903f-1b5b0d47eab3.png){: .align-center}