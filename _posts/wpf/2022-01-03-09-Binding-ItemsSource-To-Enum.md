---
layout: single
title: "WPF : 9. ItemsSource에 Enum타입 바인딩하는 법"
description: ItemsSource에 Enum타입 바인딩하는 법
categories:
 - WPF
---

`ItemsSource`속성에 `Enum`타입을 바인딩하여 아래 이미지처럼 나열할 수 있다.

```csharp
public enum ImageExtension
{
    Jpg,
    Png,
    Gif,
    Bmp,
    Ico
}
```

![image](https://user-images.githubusercontent.com/38006679/147892233-756b72fc-1f69-49d6-9a43-e02ae24bfb0c.png){: .align-center}


## ObjectDataProvider를 이용하는 방법

`System.Enum.GetValues`함수는 매개변수로 지정한 `Enum`타입의 목록을 반환한다. 해당 메서드를 `ObjectDataProvider`에 지정하여 `ItemSource`에 바인딩할 수 있다.

- Enum.GetValues

```csharp
// 해당 Enum타입의 목록을 가져옴.
public static Array GetValues(Type enumType);
```

- ObjectDataProvider 정의

```xml
<Window.Resources>
    <ObjectDataProvider x:Key="ItemExtensionType" MethodName="GetValues"
                        ObjectType="{x:Type sys:Enum}">
        <ObjectDataProvider.MethodParameters>
            <x:Type TypeName="local:ItemExtension"/>
        </ObjectDataProvider.MethodParameters>
    </ObjectDataProvider>
</Window.Resources>
```

- ItemsSource 바인딩

```xml
<Grid>
    <ComboBox ItemsSource="{Binding Source={StaticResource ItemExtensionType}}" />
    <ListBox ItemsSource="{Binding Source={StaticResource ItemExtensionType}}" /> 
</Grid>
```

## MarkupExtension을 이용한 방법

매개변수로 받은 `Enum`타입에 대한 목록을 반환하는 `MarkupExtension`을 정의하여 바인딩한다.

- MarkupExtension 정의

```csharp
public class EnumBindingSourceExtension : MarkupExtension
{
    private Type _enumType;
    public Type EnumType
    {
        get { return this._enumType; }
        set
        {
            if (value != this._enumType)
            {
                if (null != value)
                {
                    Type enumType = Nullable.GetUnderlyingType(value) ?? value;
                    if (!enumType.IsEnum)
                        throw new ArgumentException("Type must be for an Enum.");
                }
                this._enumType = value;
            }
        }
    }
    
    public EnumBindingSourceExtension() { }
    
    public EnumBindingSourceExtension(Type enumType)
    {
        this.EnumType = enumType;
    }
    
    public override object ProvideValue(IServiceProvider serviceProvider)
    {
        Array enumValues = Enum.GetValues(EnumType);
        
        return enumValues;
    }
}
```

- ItemsSource 바인딩

```xml
<Grid>
    <ComboBox ItemsSource="{Binding Source={local:EnumBindingSource {x:Type local:ItemExtension}}}"/>
    <ListBox ItemsSource="{Binding Source={local:EnumBindingSource {x:Type local:ItemExtension}}}"/>
</Grid>
```

### 참고

[http://brianlagunas.com/a-better-way-to-data-bind-enums-in-wpf/](http://brianlagunas.com/a-better-way-to-data-bind-enums-in-wpf/)