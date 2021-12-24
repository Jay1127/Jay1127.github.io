---
layout: single
title: "WPF : 8. DataGridColumn의 Visibility 바인딩하는 방법"
categories:
 - WPF
---

## 초기 구현

![image](https://user-images.githubusercontent.com/38006679/147324565-1925cb0f-a586-49f6-951c-821297573ee7.png)

<div style="line-height : 0.8">
<br/>
</div>

`DataGridColumn`의 `Visibility`속성을 직접 바인딩해서 첫번째 열을 숨긴다.

```xml
<DataGrid>
    <DataGrid.Columns>
        <DataGridTextColumn Header="First" 
                            Visibility="{Binding IsFirstColumnVisible}"/>
        <DataGridTextColumn Header="Second"/>
    </DataGrid.Columns>
</DataGrid>
```

```csharp
public partial class MainWindow : Window
{
    public Visibility IsFirstColumnVisible { get; set; }

    public MainWindow()
    {
        InitializeComponent();
        DataContext = this;

        IsFirstColumnVisible = Visibility.Hidden; // 숨기기
    }
}
```

<div style="line-height : 0.8">
<br/>
</div>

첫번째 열이 사라지지 않고 다음과 같은 에러가 발생한다.

```
System.Windows.Data Error: 2 : Cannot find governing FrameworkElement or FrameworkContentElement for target element. BindingExpression:Path=IsFirstColumnVisible; DataItem=null; target element is 'DataGridTextColumn' (HashCode=21800467); target property is 'Visibility' (type 'Visibility')
```

<div style="line-height : 0.8">
<br/>
</div>

## 해결 방법

`DataGridColumn`은 `DataGrid`의 `Visual Tree`에 있지 않으므로 `DataGrid`의 `DataContext`를 상속하지 않는다. 또한 `Visual Tree`에 놓여있지 않으면, `RelativeSource`를 이용해서 상위 타입을 찾는 방법도 사용할 수 없다. 해결 방법은 `Freezable`객체는 `Visual Tree`에 있지 않아도, `DataContext`를 상속받기 때문에, `Freezable`객체를 이용하면 된다.

<div style="line-height : 0.8">
<br/>
</div>

먼저. `Freezable`클래스를 상속받은 후 의존속성(Data)생성한다.

```csharp
public class BindingProxy : Freezable
{
    public static readonly DependencyProperty DataProperty =
        DependencyProperty.Register("Data", typeof(object), typeof(BindingProxy));

    public object Data
    {
        get { return GetValue(DataProperty); }
        set { SetValue(DataProperty, value); }
    }

    protected override Freezable CreateInstanceCore()
    {
        return new BindingProxy();
    }
}
```

다음으로, `DataGrid`의 `DataContext`를 상속받는 `Freezable`인스턴스를 리소스에 추가하고, `DataGridColumn`의 `Visibility`속성과 바인딩한다.

```xml
<DataGrid>
    <DataGrid.Resources>
        <local:BindingProxy x:Key="FirstColumnProxy" Data="{Binding IsFirstColumnVisible}"/>
    </DataGrid.Resources>
    <DataGrid.Columns>
        <DataGridTextColumn Header="First" 
                            Visibility="{Binding Data, Source={StaticResource FirstColumnProxy}}"/>
        <DataGridTextColumn Header="Second"/>
    </DataGrid.Columns>
</DataGrid>
```

`DataGrid`의 첫번째 열이 사라진 걸 확인할 수 있다.

![image](https://user-images.githubusercontent.com/38006679/147324626-f2ce52ef-0d6e-482b-88f6-1f89690c33c7.png)

## 참고

[https://stackoverflow.com/questions/22073740/binding-visibility-for-datagridcolumn-in-wpf/22074985#22074985](https://stackoverflow.com/questions/22073740/binding-visibility-for-datagridcolumn-in-wpf/22074985#22074985)