---
layout: single
title: "WPF : 13. ListBoxItem의 CheckBox와 Selection 연동하는 법"
description: ListBoxItem의 CheckBox와 Selection 연동하는 법
categories:
 - WPF
---

아래 이미지처럼 `ListBoxItem`의 `CheckBox`를 선택한 경우, `ListBoxItem`은 동시에 선택되지 않는다.

```xml
<ListBox ItemsSource="{Binding Items}">
    <ListBox.ItemTemplate>
        <DataTemplate>
            <CheckBox Content="{Binding .}"/>
        </DataTemplate>
    </ListBox.ItemTemplate>
</ListBox>
```

![_2020_05_06_16_58_58_863](https://user-images.githubusercontent.com/38006679/148853549-bc0eaa3a-5ab2-4a59-a61f-16297f1b05c9.gif){: .align-center}


### 해결 방법

`CheckBox`를 선택한 경우, 상위에 있는 `ListBoxItem`을 찾아 동시에 선택해주는 `Attached Property`를 생성한다.

```csharp
public class SelectionService
{
    public static readonly DependencyProperty UseSyncSelectionProperty =
        DependencyProperty.RegisterAttached("UseSyncSelection", typeof(bool), typeof(SelectionService),
            new PropertyMetadata(false, new PropertyChangedCallback(OnUseSyncSelectionChanged)));

    public static bool GetUseSyncSelection(DependencyObject obj)
    {
        return (bool)obj.GetValue(UseSyncSelectionProperty);
    }

    public static void SetUseSyncSelection(DependencyObject obj, bool value)
    {
        obj.SetValue(UseSyncSelectionProperty, value);
    }

    private static void OnUseSyncSelectionChanged(DependencyObject d, DependencyPropertyChangedEventArgs e)
    {
        var control = d as ButtonBase;
				var useSync = (bool)e.NewValue;

        if (useSync)
        {
            control.Click += OnChildButtonClicked;
        }
        else
        {
            control.Click -= OnChildButtonClicked;
        }
    }

    private static void OnChildButtonClicked(object sender, RoutedEventArgs e)
    {
        var parent = sender as DependencyObject;
        var ancestors = new List<DependencyObject>();

        // 클릭된 컨트롤의 상위 부모 찾기
        while (parent != null)
        {
            if (parent is Selector)
                break;

            parent = VisualTreeHelper.GetParent(parent);
            ancestors.Add(parent);
        }

        // Selector에서 선택된 위치 찾기
        if (parent != null)
        {
            var selector = (Selector)parent;

            for (int i = 0; i < selector.Items.Count; i++)
            {
                var item = selector.ItemContainerGenerator.ContainerFromIndex(i);

                if (ancestors.Contains(item))
                {
                    selector.SelectedIndex = i;
                    break;
                }
            }
        }
    }
}
```

```xml
<StackPanel Margin="20,125,0,0"
            HorizontalAlignment="Left"
            VerticalAlignment="Top"
            Grid.Row="1"
            Orientation="Horizontal">
    <Label Content="Selector Sync Service" />
    <CheckBox Name="UseSyncCheckBox"
              VerticalAlignment="Center"/>
</StackPanel>
<ListBox ItemsSource="{Binding Items}"
         Grid.Row="1"
         Width="137"
         Height="100"
         HorizontalAlignment="Left"
         VerticalAlignment="Top"
         Margin="24,153,0,0">
    <ListBox.ItemTemplate>
        <DataTemplate>                    
            <CheckBox Content="{Binding .}"
                      wht:SelectorSyncService.UseSyncSelection="{Binding IsChecked, ElementName=UseSyncCheckBox}" />
        </DataTemplate>
    </ListBox.ItemTemplate>
</ListBox>
```

`CheckBox`가 선택되면 `ListBoxItem`도 동시에 선택되는 것을 확인할 수 있다.

![_2020_05_06_16_59_41_973](https://user-images.githubusercontent.com/38006679/148853586-2b0bfd8f-1aac-45b2-bcd4-b4b396b62cbd.gif){: .align-center}