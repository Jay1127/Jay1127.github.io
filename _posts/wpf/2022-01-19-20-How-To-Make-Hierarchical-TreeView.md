---
layout: single
title: "WPF : 20. 계층구조 트리뷰(Hierarchical TreeView)"
description: 계층구조 트리뷰(Hierarchical TreeView)
categories:
 - WPF
---

### 클래스 정의

`TreeView`에 바인딩할 클래스를 계층구조 형태로 만든다.

```csharp
public class Folder
{
    public string Name { get; set; }
    public List<Folder> SubFolders { get; set;} // 계층구조
}

public class MainViewModel
{
    public ObservableCollection<Folder> FolderTree { get; set; }
  	...
}
```

### TreeView 정의

`ItemTemplate`를 `HierarchicalDataTemplate`로 지정하고 바인딩한다.

```xml
<TreeView ItemsSource="{Binding FolderTree}">
    <TreeView.ItemTemplate>
    	<HierarchicalDataTemplate ItemsSource="{Binding SubFolders}">
        	<TextBlock Text="{Binding Name}" Width="200"/>
        </HierarchicalDataTemplate>
	</TreeView.ItemTemplate>
</TreeView>
```