---
layout: single
title: "WPF : 11. 외부 프로젝트의 ResourceDictionary 참조하는 법"
categories:
 - WPF
---

`SimpleControls.Samples`프로젝트에서 외부 프로젝트인 `SimpleControls`의 `ResourceDictionary`를 참조하려고 한다.

![image](https://user-images.githubusercontent.com/38006679/147992188-a5d39bde-e27f-453e-8d95-e098829c1740.png){: .align-center}

### 참조 방법

```xml
<ResourceDictionary Source="/참조하는 프로젝트명;component/상대 경로(폴더)/참조할 리소스 파일"/>
```

### 예시

```xml
<!-- app.xaml -->
<Application.Resources>
    <ResourceDictionary>
        <ResourceDictionary.MergedDictionaries>
            <ResourceDictionary Source="/SimpleControls;component/Templates/CheckButtonTemplate.xaml"/>
        </ResourceDictionary.MergedDictionaries>
    </ResourceDictionary>
</Application.Resources>
```