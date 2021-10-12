---
layout: single
title: "WPF : 1. 바인딩된 TextBox에 소수점이 입력 안되는 경우 해결 방법"
categories:
 - WPF
---

## **원인**

WPF 4.5에서 `TextBox`의 `Text`프로퍼티에 부동소수타입(double, float)을 바인딩하고, `UpdateSourceTrigger=PropertyChanged`로 설정된 경우, `TextBox`에 소수점('.')을 입력하지 못한다.

```csharp
public class MainViewModel : ViewModelBase
{
    private double decimalValue;
    public double DecimalValue
    {
        get => return decimalValue;
        set => Set(ref decimalValue, value);
    }
}
```

```xml
<TextBox Text="{Binding DecimalValue, UpdateSourceTrigger = PropertyChanged}" ... />
```

## **해결**

`KeepTextBoxDisplaySynchronizedWithTextProperty`속성을 `False`로 지정하면, WPF 4.0 이전의 `TextBox`처럼 동작하도록 설정할 수 있다.

```csharp
// App.xaml.cs
public App()
{ 
    System.Windows.FrameworkCompatibilityPreferences.KeepTextBoxDisplaySynchronizedWithTextProperty = false;
}
```