---
layout: single
title: ".NET : 4. internal class를 외부 어셈블리에서 사용하는 방법"
categories:
 - CSharp
---

`internal class`는 어셈블리 내에서만 사용할 수 있고, 외부 어셈블리에서는 사용할 수 없다. 만약 외부 어셈블리에서 `internal class`를 사용하고 싶다면, `InternalsVisibleTo`어트리뷰트를 사용하면 된다. `InternalsVisibleTo`어트리뷰트에 `internal class`를 사용할 어셈블리를 지정하면, 해당 어셈블리에서는 `internal class`를 사용할 수 있다.


### 사용 방법

- `internal class`를 정의

```csharp
namespace InternalAssembly
{
    internal class InternalClass
    {
    }
}
```
<br/>

- `AssemblyInfo.cs`파일에 `internal class`를 사용할 외부 어셈블리를 지정

```csharp
[assembly: InternalsVisibleTo("ExternalAssembly")]
```

<br/>

- 지정된 외부 어셈블리에서 `internal class`를 사용

```csharp
using InternalAssembly;

namespace ExternalAssembly
{
    class Program
    {
        static void Main(string[] args)
        {
            var internalObject = new InternalClass();
        }
    }
}
```