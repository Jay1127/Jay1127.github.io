---
layout: single
title: ".NET : 1. OpenFileDialog형태의 폴더 선택 Dialog 사용하는 법(CommonOpenFileDialog)"
categories:
 - C#
---

폴더를 선택하기 위해 `FolderBrowserDialog`를 사용하면 다음과 같은 창이 뜨게 된다.

![image](https://user-images.githubusercontent.com/38006679/135938493-b75f49e1-dc23-4675-bbd2-13dc21ea42bd.png){: .align-center}



이러한 창 대신에 `OpenFileDialog`형태의 폴더 선택 창을 사용하고 싶다면 `CommonOpenFileDialog`를 사용하면 된다.



### 설치 방법

`CommonOpenFileDialog`를 사용하려면 다음 dll파일이 필요하며, Nuget을 이용해 설치할 수 있다.

- Microsoft.WindowsAPICodePack.dll
- Microsoft.WindowsAPICodePack.Shell.dll

```
Install-Package WindowsAPICodePack-Shell
```



### 사용 방법

```csharp
using (var dialog = new CommonOpenFileDialog())
{
    dialog.IsFolderPicker = true;
    if(dialog.ShowDialog() == CommonFileDialogResult.Ok)
    {
        SelectedFolderPath = dialog.FileName;    
    }
}
```

![image](https://user-images.githubusercontent.com/38006679/135938528-b76b26af-b4ee-4664-ae4f-efb10513c3db.png)