---
layout: single
title: ".NET : 6. Nuget Package 만드는 법"
categories:
 - CSharp
tags: 
 - CSharp
---

## 사전 작업

- [사이트](https://www.nuget.org/downloads)에 접속하여 `nuget.exe CLI`를 설치한다.

![image](https://user-images.githubusercontent.com/38006679/136137518-7e735480-4e3e-497c-bd0a-305cf7e6a64c.png){: .align-center}

## 패키지 생성

- `nuget package` 생성할 프로젝트

```csharp
using System;

namespace Jay.NugetTestLib
{
    public class Logger
    {
        public void Log(string text)
        {
            Console.WriteLine($"{text}");
        }
    }
}
```
<br/>
- `프로젝트 → 속성 → 어셈블리 정보` 또는 `AssemblyInfo.cs`에서 메타데이터를 입력한다.

![image](https://user-images.githubusercontent.com/38006679/136137549-d4be2d31-e769-4162-b7d9-c7f2cde0a750.png){: .align-center}

<br/>
- 프로젝트 파일(`.csproj`)이 있는 폴더로 이동하여 `nuget spec`명령어 입력하면, `.nuspec`파일이 생성된다.

```powershell
nuget spec
```
<br/>

<div class="notice--info" markdown="1"> 
💡 생성된 `.nuspec`파일에 값이 `$...$`로 감싸진 경우(`$id$,$version$`), 패키지 생성시 미리 설정한 어셈블리 정보로 대체된다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<package>
  <metadata>
    <id>$id$</id>
    <version>$version$</version>
    <title>$title$</title>
    <authors>$author$</authors>
    <owners>$author$</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <license type="expression">MIT</license>
    <projectUrl>http://project_url_here_or_delete_this_line/</projectUrl>
    <iconUrl>http://icon_url_here_or_delete_this_line/</iconUrl>
    <description>$description$</description>
    <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
    <copyright>Copyright 2020</copyright>
    <tags>Tag1 Tag2</tags>
  </metadata>
</package>
```
</div>

<br/>
- `nuget pack`명령어를 입력하면, `.nuspec`파일과 프로젝트 정보를 바탕으로 `.nupkg`파일을 생성한다.

```powershell
nuget pack
```

<br/>
<div class="notice--info" markdown="1"> 

💡 `nuget package explorer`로 생성된 `.nupkg`파일 정보를 확인할 수 있다.

![image](https://user-images.githubusercontent.com/38006679/136144510-d8a7664d-6de8-4654-bb7d-352a278ba267.png){: .align-center}

</div>


## 패키지 등록

- 다음 사이트에 [https://www.nuget.org](https://www.nuget.org) 회원가입 후 로그인한다.
- 프로필에 API Keys로 이동하여, API Key를 생성한 후 복사한다.

![image](https://user-images.githubusercontent.com/38006679/136144577-7a99640c-21f2-45d6-9b21-070b19b6f2bb.png){: .align-center}

- `nuget package explorer`에서 `File → Publish`를 선택한다. 다음 창에 `API Key`를 입력하고, `Publish`버튼을 누르면 패키지가 등록된다.

![image](https://user-images.githubusercontent.com/38006679/136144609-65d9fecc-a7ad-459f-a6cc-f2f6894af5c3.png){: .align-center}

## 패키지 사용

- 비쥬얼 스튜디오의 `패키지 관리자 콘솔`에서 등록된 패키지를 설치하여, 사용할 수 있다.

```powershell
Install-Package Jay.NugetTestLib -Version 1.0.0
```

```csharp
namespace NugetTestConsole
{
    class Program
    {
        static void Main(string[] args)
        {
            var logger = new Jay.NugetTestLib.Logger();
            logger.Log("nuget is Loaded");
        }
    }
}
```

![image](https://user-images.githubusercontent.com/38006679/136144623-52826066-9e96-4d02-a62d-763670ebb6c3.png){: .align-center}