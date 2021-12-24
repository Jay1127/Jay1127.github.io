---
layout: single
title: "WPF : 6. RadioButton의 IsChecked프로퍼티와 Enum타입 바인딩하는 법"
categories:
 - WPF
---

- `Enum` 타입

```csharp
public enum FilterType { None, Size, Perent }
```

<div style="line-height : 0.8">
<br/>
</div>

- `Converter` 정의

```csharp
class EnumToBooleanConverter : IValueConverter
{
    public object Convert(object value, Type targetType, 
                          object parameter, CultureInfo culture)
    {
        return value.Equals(parameter);
    }

    public object ConvertBack(object value, Type targetType, 
                              object parameter, CultureInfo culture)
    {
        return value.Equals(true) ? parameter : Binding.DoNothing;
    }
}
```

<div style="line-height : 0.8">
<br/>
</div>

- `xaml` 바인딩

```xml
<RadioButton IsChecked="{Binding FilterOption,    
                         ConverterParameter={x:Static service:FilterType.NONE}, 
                         Converter={StaticResource EnumToBoolean}}" .../>

<RadioButton IsChecked="{Binding FilterOption,    
                         ConverterParameter={x:Static service:FilterType.Size}, 
                         Converter={StaticResource EnumToBoolean}}" .../>

<RadioButton IsChecked="{Binding FilterOption,    
                         ConverterParameter={x:Static service:FilterType.Perent }, 
                         Converter={StaticResource EnumToBoolean}}" .../>
```

<div style="line-height : 0.8">
<br/>
</div>

**참고**

[https://stackoverflow.com/questions/397556/how-to-bind-radiobuttons-to-an-enum](https://stackoverflow.com/questions/397556/how-to-bind-radiobuttons-to-an-enum)