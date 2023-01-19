---
layout: single
title: "WPF : 27. ToggleButton 클릭하여 Popup 호출하는 법"
description: ToggleButton 클릭하여 Popup 호출하는 법
categories:
 - WPF
---

- `ToggleButton`의 `IsChecked`속성과 `Popup`의 `IsOpen`속성을 바인딩하여, `ToggleButton`을 클릭하면 `Popup`을 열도록 한다.
- `StayOpen=False`로 지정하여 `Popup` 외부 영역을 클릭하면 닫히도록 한다.

```xml
<Grid>
    <ToggleButton x:Name="ExpandBtn" 
                  Content="Expand" 
                  HorizontalAlignment="Center" 
                  VerticalAlignment="Top"
                  Height="30"
                  Width="100"
                  Margin="0,30,0,0"/>

    <Popup x:Name="popup"
           IsOpen="{Binding ElementName=ExpandBtn, Path=IsChecked}"
           StaysOpen="False"
           PlacementTarget="{Binding ElementName=ExpandBtn}"
           Placement="Bottom"
           HorizontalOffset="-12"
           PopupAnimation = "Slide">
						...
    </Popup>
</Grid>
```

<br/>

- 하지만, `Popup`이 열린 상태에서 `ToggleButton`을 클릭하면, `Popup`이 닫히지 않고 다시 열리는 문제가 발생한다. `StaysOpen`속성을 `ToggleButton`위에 마우스가 있는지 여부에 따라 변경해주면, 다시 열리는 문제를 해결할 수 있다.

```xml
<Grid>
    <ToggleButton x:Name="ExpandBtn" 
                  Content="Expand" 
                  HorizontalAlignment="Center" 
                  VerticalAlignment="Top"
                  Height="30"
                  Width="100"
                  Margin="0,30,0,0"/>

    <Popup x:Name="popup"
           IsOpen="{Binding ElementName=ExpandBtn, Path=IsChecked}"
		   StaysOpen="{Binding ElementName=ExpandBtn, Path=IsMouseOver}"
           PlacementTarget="{Binding ElementName=ExpandBtn}"
           Placement="Bottom"
           HorizontalOffset="-12"
           PopupAnimation = "Slide">
						...
    </Popup>
</Grid>
```