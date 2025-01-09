---
layout: single
title: "WPF : 36. 엑셀에서 DataGrid에 셀 붙여넣기"
description: Paste excel to datagrid in wpf
categories:
 - WPF
---

`DataGrid`는 붙여넣기가 기본적으로 지원되지 않기 때문에 다음과 같이 해결할 수 있다.

- 클립보드에서 붙여넣을 데이터를 분류
- 바인딩된 열(column)에 해당하는 속성(property)정보를 가져와 업데이트

<br/>

```csharp
public class DataGridPasteBehavior : Behavior<DataGrid>
{
    protected override void OnAttached()
    {
        base.OnAttached();

        CommandBinding PasteCommandBinding = new CommandBinding(
            ApplicationCommands.Paste,
            PasteCommandExecuted,
            PasteCommandCanExecute);
        AssociatedObject.CommandBindings.Add(PasteCommandBinding);
    }

    protected override void OnDetaching()
    {
        base.OnDetaching();
    }

    private void PasteCommandExecuted(object target, ExecutedRoutedEventArgs e)
    {
        try
        {
            var dataGrid = target as DataGrid;

            var rowDatas = Clipboard.GetText().Split(new[] { "\r\n", "\n" }, StringSplitOptions.RemoveEmptyEntries);
            int selectedRowIndex = dataGrid.Items.IndexOf(dataGrid.CurrentItem);
            int selectedColIndex = dataGrid.Columns.IndexOf(dataGrid.CurrentColumn);

            for (int i = 0; i < rowDatas.Length; i++)
            {
                string[] columns = rowDatas[i].Split('\t');

                for (int j = 0; j < columns.Length; j++)
                {
                    var cell = columns[j];
                    var rowData = dataGrid.Items[selectedRowIndex + i];
                    var column = dataGrid.Columns[selectedColIndex + j];

                    if (column is DataGridTextColumn textColumn)
                    {
                        var binding = textColumn.Binding as System.Windows.Data.Binding;
                        var propertyName = binding?.Path.Path;

                        if (!string.IsNullOrEmpty(propertyName))
                        {
                            var propertyInfo = rowData.GetType().GetProperty(propertyName);
                            var convertedValue = Convert.ChangeType(cell, propertyInfo.PropertyType);
                            propertyInfo.SetValue(rowData, convertedValue, null);
                        }
                    }
                }
            }
        }
        catch (Exception ex)
        {
        }
    }

    private void PasteCommandCanExecute(object target, CanExecuteRoutedEventArgs e)
    {
        var dataGrid = target as DataGrid;
        e.CanExecute = dataGrid.CurrentCell != null;
        e.Handled = true;
    }
}
```