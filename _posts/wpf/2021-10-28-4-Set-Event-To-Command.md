---
layout: single
title: "WPF : 4. Event를 Command로 설정하는 법"
categories:
 - WPF
---

WPF 컨트롤은 모든 이벤트에 대한 `Command`를 가지고 있지 않다. 특정 이벤트에 대해 `Command`를 사용하고 싶다면, `InvokeCommandAction`을 이용하면 된다.

<div style="line-height : 0.8">
<br/>
</div>

- Nuget을 이용해서 패키지 다운로드

```coffeescript
Install-Package Expression.Blend.Sdk
```

<div style="line-height : 0.8">
<br/>
</div>

- 사용법

```xml
<Window ...
        xmlns:i = "http://schemas.microsoft.com/expression/2010/interactivity" 
        ... />   

<Button>
	<i:Interaction.Triggers>
    	<i:EventTrigger EventName="PreviewMouseDown">
        	<i:InvokeCommandAction Command="{Binding OpenCommand}"/>
    	</i:EventTrigger>
	</i:Interaction.Triggers>
</Button>
```