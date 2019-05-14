# 创建一个 Orchard Core CMS 网站

在本指南中，你将从项目模板开始将 Orchard Core 安装为内容管理系统。

## 你需要什么

- .NET Core SDK 的当前版本。你可以从这里下载 [https://www.microsoft.com/net/download/core](https://www.microsoft.com/net/download/core)。
- 文本编辑器和终端，你可以在其中键入 dotnet 命令。

## 创建项目

有不同的方法为 Orchard Core 创建站点和模块。你可以在[这里](../../templates/README.md)了解更多。在本指南中，我们将使用 “代码生成模板”。

你可以使用以下命令安装最新发布的模板:

```dotnet new -i OrchardCore.ProjectTemplates::1.0.0-*```

!!! 注意
    要使用模板的开发分支，添加 `--nuget-source https://www.myget.org/F/orchardcore-preview/api/v3/index.json`

创建一个包含站点的空文件夹。打开终端，导航到该文件夹并运行如下操作:

```dotnet new occms -n MySite```

这将在名为 `MySite` 的文件夹中创建一个新的 Orchard Core CMS 项目。

## 启动站点

已经通过模板创建了应用程序，但是还没有安装。

执行以下命令运行应用程序:

`dotnet run --project .\MySite\MySite.csproj`

!!! 注意
    如果你在使用模板的开发分支，在运行应用程序前执行 `dotnet restore .\MySite\MySite.csproj --source https://www.myget.org/F/orchardcore-preview/api/v3/index.json`

你的应用程序现在应该正在运行，并包含开放的端口:

```
Now listening on: https://localhost:5001
Now listening on: http://localhost:5000
Application started. Press Ctrl+C to shut down.
```

在浏览器中打开 <https://localhost:5001>，应该会显示安装界面。

为了构建一个具有所有 CMS 特性的网站，都要使用 __Blog__ recipe。recipe 包含一个模块列表和配置 Orchard Core 网站的步骤。

填写表单，选择 __Blog__ recipe，对于数据库选择 __SQLite__。

![image](assets/setup-screen.jpg)

提交表单。几秒钟后，你应该会看到一个博客站点。

![image](assets/blog-home-page.jpg)

为了配置它并开始编写内容，你可以访问 <https://localhost:5001/admin>.

## 总结

你刚刚创建了一个 Orchard Core CMS 支持的博客引擎。
