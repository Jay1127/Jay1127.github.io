---
layout: single
title: "WPF : 10. DataTemplateSelector 사용법"
description: DataTemplateSelector 사용법
categories:
 - WPF
---

아래 이미지의 `DataGrid`는 특정 조건에 따라 `DataGridCell`의 `Template`이 달라진다.

- 1행 1열의 셀은 가운데 정렬된 빨간 텍스트로 렌더링
- 그 외의 셀은 좌측 정렬된 검정 텍스트로 렌더링

이처럼, 조건에 따라서 `Template`을 변경하고 싶다면, `DataTemplateSelctor`를 이용하면 된다.

![image](https://user-images.githubusercontent.com/38006679/147892367-35dbf9b8-ba75-44e7-b064-fabd91ebd1dd.png){: .align-center}

## **DateTemplateSelector 생성**

1행 1번째 열인 경우는 `ConditionalTemplate`을 반환하고, 그 외의 경우는 `BaseTemplate`을 반환한다.

```csharp
public class TemplateSelector : DataTemplateSelector
{
    public DataTemplate ConditionalTemplate { get; set; }
    public DataTemplate BaseTemplate { get; set; }

    public override DataTemplate SelectTemplate(object item, DependencyObject container)
    {
        // 조건 설정
        if(item is Row row)
        {
            if (row.Cells[0].RowIndex == 1 && row.Cells[0].ColIndex == 1)
            {
                return ConditionalTemplate;
            }
            else
            {
                return BaseTemplate;
            }
        }
        
        return base.SelectTemplate(item, container);
    }
}
```

## **DataTemplateSelector 적용**

각 조건에 맞는 `DataTemplate`을 생성하고, 위에 생성한 `DataTemplateSelector`에 지정한다.

```xml
<DataGrid ItemsSource="{Binding Rows}"
          Margin="10,20,0,0"
          Height="100"
          CanUserAddRows="False"
          AutoGenerateColumns="False"
          HeadersVisibility="Column">
    <DataGrid.Resources>
        <!-- 렌더링할 템플릿을 정의-->
        <DataTemplate x:Key="ButtonsTemplate">
            <StackPanel Orientation="Horizontal"
                        HorizontalAlignment="Center">
                <TextBlock Text="{Binding Cells[0].Content}" 
                           Foreground="Red"
                           HorizontalAlignment="Center"/>
            </StackPanel>
        </DataTemplate>
        <DataTemplate x:Key="BaseTemplate">
            <TextBlock Text="{Binding Cells[0].Content}"
                       Margin="1,0,0,0"/>
        </DataTemplate>
    </DataGrid.Resources>
    <DataGrid.Columns>
        <DataGridTemplateColumn Header="TemplateColumn">
          <!-- TemplateSelector 적용-->
            <DataGridTemplateColumn.CellTemplateSelector>
                <local:TemplateSelector BaseTemplate="{StaticResource BaseTemplate}"
                                        ConditionalTemplate="{StaticResource ButtonsTemplate}"/>
            </DataGridTemplateColumn.CellTemplateSelector>
        </DataGridTemplateColumn>
        <DataGridTextColumn Header="TextColumn" 
                            Binding="{Binding Cells[1].Content}"/>
    </DataGrid.Columns>
</DataGrid>
```