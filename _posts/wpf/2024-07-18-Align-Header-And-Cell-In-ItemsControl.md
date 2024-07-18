---
layout: single
title: "WPF : 32. ItemsControl의 헤더,셀 라인 맞추는 법(Grid.IsSharedSizeScope)"
description: ItemsControl의 헤더,셀 라인 맞추는 법, Grid.IsSharedSizeScope, Align Header And Cell In ItemsControl, SharedSizeGroup
categories:
 - WPF
---

`ItemsControl`을 이용해서 헤더+셀형식으로 테이블을 만든 경우, 헤더부분과 셀부분이 크기를 공유하지 않아 테이블이 어긋나 보이는 경우가 있다.

![image](https://github.com/user-attachments/assets/1b07a74d-510d-41c3-bb45-dce890ee3518){: .align-center}{: width="500"}

![image](https://github.com/user-attachments/assets/1f7dfc92-e322-4aca-998b-edf6d09f9c16){: .align-center}{: width="500"}

 <br/>

다음과 같이 `ItemsControl`에 `Grid.IsSharedSizeScope="True"`로 설정하고, 공유하려는 헤더,셀 그리드의 `SharedSizeGroup`속성에 동일한 값을 지정하면, 해당 헤더와 셀의 크기가 공유되서 어긋나지 않는다.

```xml
<ItemsControl Grid.IsSharedSizeScope="True"
              HorizontalAlignment="Center"
              VerticalAlignment="Center"
              ItemsSource="{Binding Items}">
    <ItemsControl.ItemsPanel>
        <ItemsPanelTemplate>
            <StackPanel Orientation="Horizontal" />
        </ItemsPanelTemplate>
    </ItemsControl.ItemsPanel>
    <ItemsControl.Template>
        <ControlTemplate TargetType="{x:Type ItemsControl}">
            <Grid>
                <Grid.ColumnDefinitions>
                    <ColumnDefinition Width="100" />
                    <ColumnDefinition />
                </Grid.ColumnDefinitions>
                <Grid.RowDefinitions>
                    <RowDefinition Height="35" />
                    <RowDefinition MinHeight="35"
                                   Height="auto"
                                   SharedSizeGroup="shared" />
                </Grid.RowDefinitions>

                <Label Content="Header1"
                       Background="LightGreen"
                       BorderBrush="Black"
                       BorderThickness="1" />
                <Label Content="Header2"
                       Background="LightGreen"
                       BorderBrush="Black"
                       BorderThickness="1,0,1,1"
                       Grid.Row="1" />

                <ItemsPresenter Grid.Column="1"
                                Grid.RowSpan="2" />
            </Grid>
        </ControlTemplate>
    </ItemsControl.Template>
    <ItemsControl.ItemTemplate>
        <DataTemplate>
            <Grid Width="50">
                <Grid.RowDefinitions>
                    <RowDefinition Height="35" />
                    <RowDefinition SharedSizeGroup="shared" />
                </Grid.RowDefinitions>
                <TextBox Text="{Binding X1}"
                         BorderBrush="Black"
                         BorderThickness="1"
                         Grid.Row="0" />
                <TextBox Text="{Binding X2}"
                         TextWrapping="Wrap"
                         BorderBrush="Black"
                         BorderThickness="1,0,1,1"
                         Grid.Row="1" />
            </Grid>
        </DataTemplate>
    </ItemsControl.ItemTemplate>
</ItemsControl>
```

 <br/>

![image](https://github.com/user-attachments/assets/61f52f81-f5e3-4361-acb2-b2670f46ada5){: .align-center}{: width="500"}