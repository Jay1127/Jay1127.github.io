---
layout: single
title: ".NET : 5. 동일한 네임스페이스.클래스명을 가지는 경우 구분하는 법"
categories:
 - C#
---

Lib1, Lib2 어셈블리에 `동일한 네임스페이스.클래스명`을 가진 클래스가 존재한다.

```csharp
// Lib1, Lib2 Assembly
namespace Lib
{
    public class Class1
    {
    }
}
```

<br/>

외부 어셈블리에서 Lib1, Lib2클래스를 모두 참조한 경우, Lib.Class1클래스를 구분할 수 없기 때문에 에러가 발생한다.

```csharp
namespace ConsoleApp
{
    class program
    {
        static void Main(string[] args)
        {
            // 에러 발생
            Console.WriteLine(new Lib.Class1());
        }
    }
}
```
<br/>
두 프로젝트를 구분하기 위해서 각 어셈블리에 `별칭`을 지정한다.

![image](https://user-images.githubusercontent.com/38006679/136136851-cf0c435d-583e-4e90-b098-0844a9a653e1.png){: .align-center}

<br/>
`extern alias`를 이용해서 `별칭`을 선언하면 각 프로젝트를 구분할 수 있다.

```csharp
namespace ConsoleApp
{
    extern alias Lib1;
    extern alias Lib2;
  
    class program
    {
        static void Main(string[] args)
        {
            Console.WriteLine(new Lib1.Lib.Class1());
            Console.WriteLine(new Lib2.Lib.Class1());
        }
    }
}
```