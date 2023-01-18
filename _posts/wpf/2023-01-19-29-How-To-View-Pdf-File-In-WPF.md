---
layout: single
title: "WPF : 29. PDF 파일 보는법(PDF Viewer)"
categories:
 - WPF
---

## WebBrowser

`WebBrowser`를 이용해서 PDF문서를 볼 수 있다. 하지만 `WebBrowser`는 IE기반이기 떄문에, PDF파일을 보려면, IE에서 PDF파일을 보게 해주는 플러그인(Acrobat Reader…)을 설치해야만 한다.

```xml
<WebBrowser x:Name="pdfViewer"/>
```

```csharp
var path = $@"C:\Users\user\Desktop\테스트문서.pdf";
var uri = System.Web.HttpUtility.UrlDecode(path);
pdfViewer.Navigate(new Uri(uri));
```

![image](https://user-images.githubusercontent.com/38006679/213319060-d6853c2e-4ae0-41ba-868f-2111d2c23cf5.png)

## CefSharp

`CefSharp`라이브러리를 이용하면 별도의 플러그인 설치 없이 PDF파일을 볼 수 있다.

```csharp
<wpf:ChromiumWebBrowser x:Name="pdfViewer"/>
```

```csharp
var path = $@"C:\Users\user\Desktop\테스트문서.pdf";
pdfViewer.Address = path;
```

```csharp
// app.xaml
// 어플리케이션 시작 시 설정
var settings = new CefSettings();
settings.RegisterScheme(new CefCustomScheme
{
    SchemeName = CustomProtocolSchemeHandlerFactory.SchemeName,
    SchemeHandlerFactory = new CustomProtocolSchemeHandlerFactory(),
    IsCSPBypassing = true
});
settings.LogSeverity = LogSeverity.Error;
Cef.Initialize(settings)
```

```csharp
public class CustomProtocolSchemeHandlerFactory : ISchemeHandlerFactory
{
    public const string SchemeName = "local";

    public IResourceHandler Create(IBrowser browser, IFrame frame, string schemeName, IRequest request)
    {
        return new LocalSchemeHandler();
    }
}
public class LocalSchemeHandler : ResourceHandler
{
    public override CefReturnValue ProcessRequestAsync(IRequest request, ICallback callback)
    {
        var uri = new Uri(request.Url);
        var file = uri.AbsolutePath;

        Task.Run(() =>
        {
            using (callback)
            {
                if (!File.Exists(file))
                {
                    callback.Cancel();
                    return;
                }

                byte[] bytes = File.ReadAllBytes(file);

                var stream = new MemoryStream(bytes);
                if (stream == null)
                {
                    callback.Cancel();
                }
                else
                {
                    stream.Position = 0;
                    ResponseLength = stream.Length;

                    var fileExtension = System.IO.Path.GetExtension(file);
                    MimeType = GetMimeType(fileExtension);
                    StatusCode = (int)HttpStatusCode.OK;
                    Stream = stream;

                    callback.Continue();
                }
            }
        });

        return CefReturnValue.Continue;
    }
}
```