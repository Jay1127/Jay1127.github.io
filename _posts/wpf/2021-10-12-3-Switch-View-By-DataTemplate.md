---
layout: single
title: "WPF : 3. DataTemplate을 사용하여 뷰(UserControl) 스위칭하는 법"
description: DataTemplate을 사용하여 뷰(UserControl) 스위칭하는 법
categories:
 - WPF
---

## **구현**

`DataTemplate`을 이용하면 해당 데이터 타입을 어떻게 표현할지 나타낼 수 있다. 다음 코드는 `ContentControl`의 `Content`프로퍼티에 바인딩된 뷰모델 타입에 따라 `DataTemplate`에 지정된 뷰가 화면에 나타난다.

```xml
<!-- DataTemplate 이용해서 데이터 타입과 해당 타입에 매칭되는 뷰를 지정 -->
<Window.Resources>
    <DataTemplate DataType="{x:Type vm:FirstSettingViewModel}">
        <local:FirstSettingView/>
    </DataTemplate>
    <DataTemplate DataType="{x:Type vm:SecondSettingViewModel}">
        <local:SecondSettingView/>
    </DataTemplate>
</Window.Resources>
<Grid>
    ...
    <!-- 상단 메뉴바를 지정(Listbox에 RadioButton을 나열도 가능.) -->
    <RadioButton Content="{Binding SettingViewModels[0].Title}" 
                 IsChecked="{Binding SettingViewModels[0].IsSelected}" 
                 Command="{Binding SwitchViewCommand}"
                 Style="{StaticResource {x:Type ToggleButton}}" .../>
    <RadioButton Content="{Binding SettingViewModels[1].Title}" 
                 IsChecked="{Binding SettingViewModels[1].IsSelected}" 
                 Command="{Binding SwitchViewCommand}"
                 Style="{StaticResource {x:Type ToggleButton}}" .../>
    
    <!-- 스위칭될 뷰의 영역을 지정 -->
    <!-- CurrentViewModel의 타입에 따라서 표시되는 뷰가 달라짐-->
    <ContentControl Content="{Binding CurrentViewModel}" Grid.Row="1"/>
</Grid>
```

```csharp
class MainViewModel : ViewModelBase
{
    private ObservableCollection<SettingsViewModel> settingViewModels;
    public ObservableCollection<SettingsViewModel> SettingViewModels
    {
        get => settingViewModels;
        set => Set(ref settingViewModels, value);
    }
        
    private SettingsViewModel currentViewModel;
    public SettingsViewModel CurrentViewModel
    {
        get => currentViewModel;
        set => Set(ref currentViewModel, value);
    }

    private ICommand switchViewCommand;
    public ICommand SwitchViewCommand
    {
        get
        {
            if(switchViewCommand == null)
            {
                switchViewCommand = new RelayCommand(() =>
                {
                    CurrentViewModel = SettingViewModels.First(vm => vm.IsSelected);
                });
            }

            return switchViewCommand;
        }
    }

    public MainViewModel()
    {
        SettingViewModels = new ObservableCollection<SettingsViewModel>
        {
            new FirstSettingViewModel(),
            new SecondSettingViewModel()
        };

        CurrentViewModel = SettingViewModels.First();
    }
}
```

## 결과

상단의 버튼을 클릭할 때마다 `DataTemplate`의 뷰로 전환된다.

![image](https://user-images.githubusercontent.com/38006679/136868985-b22111f4-7695-4ec4-9e9e-3e3857ca6b1f.png)

![image](https://user-images.githubusercontent.com/38006679/136869005-d363c3c2-2368-4d4d-9cf0-8e21dd59b5c6.png)