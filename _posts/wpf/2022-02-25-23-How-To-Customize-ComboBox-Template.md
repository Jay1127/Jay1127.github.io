---
layout: single
title: "WPF : 23. ComboBox 커스터마이징(Template)"
description: ComboBox 커스터마이징(Template)
categories:
 - WPF
---

## ComboBox Template 정의

`Combobox`의 `Template`은 다음과 같은 컨틀로 구성되며, 각 컨트롤의 `Template`을 변경하여 외형을 커스터마이징한다.

- 선택된 아이템 표시 영역(`ContentPresenter`)
- 드롭다운 버튼(`ToggleButton`)
- 드롭다운 메뉴(`Popup`)

```xml
<!-- 드롭다운 버튼 외형 변경 -->
<Style TargetType="{x:Type ToggleButton}">
    <Setter Property="Template">
        <Setter.Value>
            <ControlTemplate TargetType="{x:Type ToggleButton}">
                <Grid>
                    <Border BorderBrush="{Binding BorderBrush, RelativeSource={RelativeSource TemplatedParent}}"
                            BorderThickness="{Binding BorderThickness, RelativeSource={RelativeSource TemplatedParent}}"
                            Background="White">
                        <ContentPresenter FlowDirection="RightToLeft"
                                          VerticalAlignment="Center"
                                          Margin="0,0,3,0"
                                          Content="▼" />
                    </Border>
                </Grid>
                <ControlTemplate.Triggers>
                    <Trigger Property="IsMouseOver"
                             Value="True">
                        <Setter Property="BorderBrush"
                                Value="Blue" />
                    </Trigger>
                </ControlTemplate.Triggers>
            </ControlTemplate>
        </Setter.Value>
    </Setter>
</Style>

<!-- 콤보박스 아이템 외형 변경 -->
<Style TargetType="{x:Type ComboBoxItem}">
    <Setter Property="Template">
        <Setter.Value>
            <ControlTemplate TargetType="{x:Type ComboBoxItem}">
                <Border Padding="5,2,2,2"
                        Background="White"
                        x:Name="ComboBoxItem_Border">
                    <ContentPresenter />
                </Border>
                <ControlTemplate.Triggers>
                    <Trigger Property="IsMouseOver"
                             Value="True">
                        <Setter TargetName="ComboBoxItem_Border"
                                Property="Background"
                                Value="SkyBlue" />
                    </Trigger>
                </ControlTemplate.Triggers>
            </ControlTemplate>
        </Setter.Value>
    </Setter>
</Style>


<Style TargetType="{x:Type ComboBox}">
    <Setter Property="BorderBrush"
            Value="Black" />
    <Setter Property="BorderThickness"
            Value="1" />
    <Setter Property="MinWidth"
            Value="120" />
    <Setter Property="MinHeight"
            Value="20" />
    <Setter Property="Template">
        <Setter.Value>
            <ControlTemplate TargetType="{x:Type ComboBox}">
                <Grid>
                    <!-- 드롭다운 버튼 -->
                    <ToggleButton IsChecked="{Binding IsDropDownOpen, Mode=TwoWay, RelativeSource={RelativeSource TemplatedParent}}"
                                  Content="▼" />

                    <!-- 선택된 아이템 표시 -->
                    <ContentPresenter IsHitTestVisible="False"
                                      Content="{TemplateBinding SelectionBoxItem}"
                                      ContentTemplate="{TemplateBinding SelectionBoxItemTemplate}"
                                      ContentTemplateSelector="{TemplateBinding ItemTemplateSelector}"
                                      VerticalAlignment="Center"
                                      Margin="5,0,0,0" />

                    <!-- 드롭다운 메뉴 -->
                    <Popup IsOpen="{TemplateBinding IsDropDownOpen}"
                           Placement="Bottom"
                           PopupAnimation="Slide">
                        <Grid Width="{TemplateBinding ActualWidth}"
                              MaxHeight="{TemplateBinding MaxDropDownHeight}"
                              Background="White">
                            <Border BorderBrush="Black"
                                    BorderThickness="1,0,1,1">
                                <ScrollViewer>
                                    <ItemsPresenter KeyboardNavigation.DirectionalNavigation="Contained" />
                                </ScrollViewer>
                            </Border>
                        </Grid>
                    </Popup>
                </Grid>
            </ControlTemplate>
        </Setter.Value>
    </Setter>
</Style>
```


![image](https://user-images.githubusercontent.com/38006679/155627792-36a7fdde-7316-4cd9-add7-4f9c1883c93a.png){: .align-center}
