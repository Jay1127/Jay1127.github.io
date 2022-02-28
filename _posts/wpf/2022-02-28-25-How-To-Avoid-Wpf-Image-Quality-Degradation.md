---
layout: single
title: "WPF : 25. Image 품질 저하 방지"
categories:
 - WPF
---

WPF에서 이미지를 컨트롤의 크기에 맞게 조절하면서, 품질이 저하되는 경우가 발생한다. 이 경우 `RenderOptions.BitmapScalingMode`속성을 값을 변경하여, 품질 저하를 방지할 수 있다.

```xml
<Image RenderOptions.BitmapScalingMode="Fant" Source="....."/>
```

<div style="line-height : 0.7">
<br/>
</div>

<div class="notice--info" markdown="1"> 
💡  BitmapScalingMode Enum 참고 
<div style="line-height : 0.3">
<br/>
</div>
[https://docs.microsoft.com/en-us/dotnet/api/system.windows.media.bitmapscalingmode?view=netframework-4.8](https://docs.microsoft.com/en-us/dotnet/api/system.windows.media.bitmapscalingmode?view=netframework-4.8)
</div>
