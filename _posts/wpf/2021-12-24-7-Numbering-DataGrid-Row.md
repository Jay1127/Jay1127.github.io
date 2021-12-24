---
layout: single
title: "WPF : 7. DataGrid의 Row번호 매기는 법"
categories:
 - WPF
---

- Converter

```csharp
class RowNumberConverter : IMultiValueConverter
{
    public object Convert(object[] values, Type targetType, object parameter, CultureInfo culture)
    {
        var row = values[0] as RowData;
        var rowList = values[1] as ObservableCollection<RowData>;

        return rowList.IndexOf(row).ToString();
    }

    public object[] ConvertBack(object value, Type[] targetTypes, object parameter, CultureInfo culture)
    {
        throw new NotImplementedException();
    }
}
```

<div style="line-height : 0.8">
<br/>
</div>


- Row Header에 표시

```xml
<DataGrid.RowHeaderTemplate>
    <DataTemplate>
        <TextBlock>
            <TextBlock>
                <TextBlock.Text>
                    <MultiBinding Converter="{StaticResource rowNumberConverter}">
                        <Binding RelativeSource="{RelativeSource AncestorType={x:Type DataGridRow}}" Path="Item"/>
                        <Binding RelativeSource="{RelativeSource AncestorType={x:Type DataGrid}}" Path="ItemsSource"/>
                    </MultiBinding>
                </TextBlock.Text>
                </TextBlock>
        </TextBlock>
    </DataTemplate>
</DataGrid.RowHeaderTemplate>
```

![image](https://user-images.githubusercontent.com/38006679/147320892-a4920a48-5e5f-4e3a-a2a9-e19ffdb2cccb.png){: .align-center}


<div style="line-height : 0.8">
<br/>
</div>

- Column에 표시

```xml
<DataGridTextColumn Header="Index">
    <DataGridTextColumn.Binding>
        <MultiBinding Converter="{StaticResource rowNumberConverter}">
            <Binding />
            <Binding RelativeSource="{RelativeSource AncestorType={x:Type DataGrid}}" 
                     Path="ItemsSource"/>
        </MultiBinding>
    </DataGridTextColumn.Binding>
</DataGridTextColumn>
```

![image](https://user-images.githubusercontent.com/38006679/147320904-e1c59328-8951-4a32-bf10-8b1cf279a9f3.png){: .align-center}