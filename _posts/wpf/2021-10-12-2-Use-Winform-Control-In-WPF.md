---
layout: single
title: "WPF : 2. WPF에서 Winform Control을 사용하는 법"
categories:
 - WPF
---

## 참조 추가

- WindowsFormsIntegration.dll
- System.Windows.Forms.dll

## 사용법

```xml
<WindowsFormsHost x:Name="host" Grid.Row="1"/>
```

```csharp
public MainWindow()
{
    InitializeComponent();    
    host.Child = new MaskedTextBox();
}
```

## 참고

[https://docs.microsoft.com/ko-kr/dotnet/framework/wpf/advanced/walkthrough-hosting-a-windows-forms-control-in-wpf](https://docs.microsoft.com/ko-kr/dotnet/framework/wpf/advanced/walkthrough-hosting-a-windows-forms-control-in-wpf)