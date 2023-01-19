---
layout: single
title: ".NET : 9. CefSharp을 AnyCpu로 빌드하는 법"
description: CefSharp을 AnyCpu로 빌드하는 법
categories:
 - CSharp
---

`CefSharp`라이브러리를 `AnyCpu`로 빌드하는 방법은 다음과 같다.

- 프로젝트 파일(.csproj)의 첫번째 `<ProjectGroup>`에 다음과 같이 추가한다.

```xml
<PropertyGroup>
	<CefSharpAnyCpuSupport>true</CefSharpAnyCpuSupport>
.....
</PropertyGroup>
```

- 어플리케이션 로드시 다음과 같이 구현한다.

```csharp
// CefSharp 설정
CefRuntime.SubscribeAnyCpuAssemblyResolver();

var settings = new CefSettings();
settings.RegisterScheme(new CefCustomScheme
{
    SchemeName = CustomProtocolSchemeHandlerFactory.SchemeName,
    SchemeHandlerFactory = new CustomProtocolSchemeHandlerFactory(),
    IsCSPBypassing = true
});
settings.LogSeverity = LogSeverity.Error;
Cef.Initialize(settings, performDependencyCheck: true, browserProcessHandler: null);
```