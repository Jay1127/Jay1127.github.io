---
layout: single
title: "WPF : 15. LoadingIndicator.WPF 라이브러리 사용법"
categories:
 - WPF
---

- `Nuget`으로 패키지 설치

```
Install-Package LoadingIndicators.WPF -Version 0.0.1
```
<div style="line-height : 0.8">
<br/>
</div>

- `app.xaml`에 리소스 추가

```xml
<Application.Resources>
    <ResourceDictionary>
        <ResourceDictionary.MergedDictionaries>
            <ResourceDictionary Source="pack://application:,,,/LoadingIndicators.WPF;component/Styles/LoadingWave.xaml"/>
            <ResourceDictionary Source="pack://application:,,,/LoadingIndicators.WPF;component/Styles/LoadingThreeDots.xaml"/>
            <ResourceDictionary Source="pack://application:,,,/LoadingIndicators.WPF;component/Styles/LoadingFlipPlane.xaml"/>
            <ResourceDictionary Source="pack://application:,,,/LoadingIndicators.WPF;component/Styles/LoadingPulse.xaml"/>
            <ResourceDictionary Source="pack://application:,,,/LoadingIndicators.WPF;component/Styles/LoadingDoubleBounce.xaml"/>
            <ResourceDictionary Source="pack://application:,,,/LoadingIndicators.WPF;component/Colors.xaml"/>
            <ResourceDictionary Source="pack://application:,,,/LoadingIndicators.WPF;component/Styles.xaml"/>
        </ResourceDictionary.MergedDictionaries>
        </ResourceDictionary>
</Application.Resources>
```

<div style="line-height : 0.8">
<br/>
</div>

- 사용법

```xml
<Window x:Class="WpfApp3.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:WpfApp3"
        xmlns:li="clr-namespace:LoadingIndicators.WPF;assembly=LoadingIndicators.WPF"
        mc:Ignorable="d"
        Title="MainWindow" Height="170" Width="900">

<li:LoadingIndicator Name="ArcsStyle" 
                     SpeedRatio="1" 
                     IsActive="True" 
                     Style="{DynamicResource LoadingIndicatorArcsStyle}" />

<li:LoadingIndicator Name="ArcsRing" 
                     IsActive="True"
                     SpeedRatio="1"
                     Style="{DynamicResource LoadingIndicatorArcsRingStyle}" />

<li:LoadingIndicator Name="DoubleBounce"
                     SpeedRatio="1"
                     IsActive="True" 
                     Style="{DynamicResource LoadingIndicatorDoubleBounceStyle}" />

<li:LoadingIndicator Name="FlipPlane" 
                     SpeedRatio="1"
                     IsActive="True"
                     Style="{DynamicResource LoadingIndicatorFlipPlaneStyle}" />

<li:LoadingIndicator Name="Pulse" 
                     SpeedRatio="1" 
                     IsActive="True"
                     Style="{DynamicResource LoadingIndicatorPulseStyle}" />

<li:LoadingIndicator Name="Ring"
                     SpeedRatio="1"
                     IsActive="True"
                     Style="{DynamicResource LoadingIndicatorRingStyle}" />

<li:LoadingIndicator Name="ThreeDots" 
                     SpeedRatio="1"
                     IsActive="True" 
                     Style="{DynamicResource LoadingIndicatorThreeDotsStyle}" />

<li:LoadingIndicator Name="Wave" 
                     SpeedRatio="1"
                     IsActive="True" 
                     Style="{DynamicResource LoadingIndicatorWaveStyle}" />
```

![image](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ee3f8620-8819-41f0-a18d-35d893aa4abf/image.gif?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220106%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220106T235541Z&X-Amz-Expires=86400&X-Amz-Signature=92f527659de60cc5d342a55d0dbb671fe47ccbb649528331cba3d321e6582421&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22image.gif%22&x-id=GetObject){: .align-center}