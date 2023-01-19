---
layout: single
title: "WPF : 12. 여러 개의 ResourceDictionary를 한번에 참조하는 법"
description: 여러 개의 ResourceDictionary를 한번에 참조하는 법
categories:
 - WPF
---

![image](https://user-images.githubusercontent.com/38006679/147992188-a5d39bde-e27f-453e-8d95-e098829c1740.png){: .align-center}

여러 개의 `ResourceDictionary`를 외부에서 사용하려면, 다음과 같이 사용할 파일들을 모두 지정해야한다.

```xml
<!-- app.xaml -->
<Application.Resources>
    <ResourceDictionary>
        <ResourceDictionary.MergedDictionaries>
            <ResourceDictionary Source="/SimpleControls;component/Templates/CheckButtonTemplate.xaml"/>
            <ResourceDictionary Source="/SimpleControls;component/Templates/ButtonTemplate.xaml"/>
          
            ...
          
        </ResourceDictionary.MergedDictionaries>
    </ResourceDictionary>
</Application.Resources>
```

만약, 외부 프로젝트에서 일일히 파일을 지정하지 않고, 모든 `ResourceDictionary`를 외부에 한번에 제공하려면, 모든 `ResourceDictionary`를 병합한 하나의 `ResourceDictionary`파일을 작성하면 된다.

```xml
<!-- template.xaml -->
<ResourceDictionary.MergedDictionaries>
    <ResourceDictionary Source="/SimpleControls;component/Templates/CheckButtonTemplate.xaml"/>
    <ResourceDictionary Source="/SimpleControls;component/Templates/ButtonTemplate.xaml"/>
  
    ....
  
</ResourceDictionary.MergedDictionaries>
```

외부 프로젝트에서는 병합된 `ResourceDictionary`파일 하나만 지정하여 사용할 수 있다.

```xml
<!-- app.xaml -->
<Application.Resources>
    <ResourceDictionary>
        <ResourceDictionary.MergedDictionaries>
            <ResourceDictionary Source="/SimpleControls;component/Templates/Template.xaml"/>
        </ResourceDictionary.MergedDictionaries>
    </ResourceDictionary>
</Application.Resources>
```