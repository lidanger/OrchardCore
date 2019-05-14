# 创建一个模块化 ASP.NET Core 应用程序

## 你将构建什么

你将构建一个由模块组成的应用程序。模块将提供控制器和视图，而布局将由主应用程序项目提供。

## 你需要什么

- .NET Core SDK 的当前版本。你可以在这里下载它 [https://www.microsoft.com/net/download/core](https://www.microsoft.com/net/download/core)。

- 文本编辑器和终端，你可以在其中键入 dotnet 命令。

## 创建一个 Orchard Core 站点和模块

有不同的方法为 Orchard Core 创建站点和模块。你可以在[这里](../../templates/README.md) 了解更多。在本指南中，我们将使用“代码生成模板”。

你可以使用以下命令安装最新发布的模板:

```dotnet new -i OrchardCore.ProjectTemplates::1.0.0-*```

!!! 注意
    要使用模板的开发分支，添加 `--nuget-source https://www.myget.org/F/orchardcore-preview/api/v3/index.json`

创建一个包含站点的空文件夹。打开终端，导航到该文件夹并运行如下操作:

```dotnet new ocmvc -n MySite```

这将在名为 `MySite` 的文件夹中创建一个新的 ASP.NET MVC 应用程序项目。
我们现在可以用以下命令创建一个新的模块:

```dotnet new ocmodulemvc -n MyModule```

模块是在 `MyModule` 文件夹中创建的。
下一步是通过添加一个项目引用在应用程序中引用模块:

```dotnet add MySite reference MyModule```

## 测试最终的应用程序

在包含两个项目的文件夹的根目录中运行以下命令:

`dotnet run --project .\MySite\MySite.csproj`

!!! 注意
    如果你在使用模板的开发分支，在运行应用程序前执行 `dotnet restore .\MySite\MySite.csproj --source https://www.myget.org/F/orchardcore-preview/api/v3/index.json`

你的应用程序现在应该正在运行，并包含开放的端口:

```
Now listening on: https://localhost:5001
Now listening on: http://localhost:5000
Application started. Press Ctrl+C to shut down.
```

在浏览器中打开 <https://localhost:5001/MyModule/Home/Index>
应该会显示 __Hello from MyModule__

> 布局来自主应用程序项目，而控制器、操作和视图来自模块项目。

## 注册自定义路由

默认情况下，模块中的所有路由都建模为 `{area}/{controller}/{action}`，其中 `{area}` 是模块的名称。
我们将在这个模块中更改视图的路径来处理主页。

在 `MyModule` 的 `Startup.cs` 文件中，将这段代码添加到 `Configure()` 方法中。

```csharp
    routes.MapAreaRoute(
        name: "Home",
        areaName: "MyModule",
        template: "",
        defaults: new { controller = "Home", action = "Index" }
    );
```

重新启动应用程序并打开主页，主页应该显示与前一个 url 相同的结果。

## 总结

你刚刚通过一个包含控制器和视图的模块创建了一个 ASP.NET Core 应用程序。
