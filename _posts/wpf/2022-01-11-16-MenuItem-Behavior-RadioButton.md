---
layout: single
title: "WPF : 16. MenuItem을 RadioButton처럼 동작시키는 법"
categories:
 - WPF
---

`IsCheckable`프로퍼티를 `True`로 설정한 경우, `MenuItem`은 `CheckBox`처럼 여러 개를 선택할 수 있다. 만약 `MenuItem`을 `RadioButton`처럼 한 개만 선택하려면, 다음과 같은 `Behavior`를 구현해주면 된다.

## Behaivor 구현
특정 `MenuItem`이 선택되면, 이미 선택됐던 찾아 `MenuItem`을 선택 해제하도록 구현한다.

```csharp
public class MenuItemMutableCheckBehavior : Behavior<MenuItem>
{
    protected override void OnAttached()
    {
        base.OnAttached();

        AssociatedObject.Loaded += OnMenuItemLoaded;
    }

    protected override void OnDetaching()
    {
        base.OnDetaching();

        AssociatedObject.Unloaded -= OnMenuItemLoaded;

        foreach(var item in FindCheckableItems())
        {
            item.Click -= OnMenuItemClicked;
        }
    }

    private void OnMenuItemLoaded(object sender, System.Windows.RoutedEventArgs e)
    {
        foreach (var item in FindCheckableItems())
        {
            item.Click -= OnMenuItemClicked;
            item.Click += OnMenuItemClicked;
        }
    }

    private void OnMenuItemClicked(object sender, System.Windows.RoutedEventArgs e)
    {
        var menuItem = sender as MenuItem;

        if (!menuItem.IsChecked)
        {
            menuItem.IsChecked = true;
            return;
        }

        var unCheckedItems = FindCheckableItems().Where(item => item != menuItem);
        foreach (var item in unCheckedItems)
        {
            item.IsChecked = false;
        }
    }

    private List<MenuItem> FindCheckableItems()
    {
        return AssociatedObject.Items
                               .OfType<MenuItem>()
                               .Where(item => item.IsCheckable)
                               .ToList();
    }
}
```

## Behaivor 적용

```xml
<Menu>
	<!-- 다중 선택 허용 -->
    <MenuItem Header="Default Check">
        <MenuItem Header="Check1"
                  IsCheckable="True" />
        <MenuItem Header="Check2"
                  IsCheckable="True" />
        <MenuItem Header="Check3"
                  IsCheckable="True" />
    </MenuItem>

	<!-- 하나의 선택만 허용 -->
    <MenuItem Header="Mutable Check">
        <i:Interaction.Behaviors>
            <wht:MenuItemMutableCheckBehavior />
        </i:Interaction.Behaviors>
        <MenuItem Header="Check1"
                  IsCheckable="True"
                  IsChecked="True" />
        <MenuItem Header="Check2"
                  IsCheckable="True" />
        <MenuItem Header="Check3"
                  IsCheckable="True" />
    </MenuItem>
</Menu>
```

![_2020_08_27_17_52_11_66](https://user-images.githubusercontent.com/38006679/148854625-da52aaaf-9aa7-4a01-b4ef-d51199d13d25.gif){: .align-center}
