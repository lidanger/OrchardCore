# Getting started with Orchard Core as a NuGet package

在本文中，我们将看到使用 Orchard Core 提供的 NuGet 包创建 CMS Web 应用程序是多么容易。

你可以在这里找到 Chris Payne 最初的博客文章:  
<http://ideliverable.com/blog/getting-started-with-orchard-core-as-a-nuget-package>

## 创建一个 Orchard Core CMS 应用程序

在 Visual Studio 中，创建一个新的空 .NET Core web 应用程序。例: `Cms.Web`。

如果你想使用 `dev` 包，添加这个 OrchardCore-preview MyGet url 到你的 NuGet 源:  
<https://www.myget.org/F/orchardcore-preview/api/v3/index.json>

右键单击项目，然后单击 `Manage NuGet packages...`。
在 `Browse` 选项卡中，搜索 `OrchardCore.Application.Cms.Targets` 并 `Install` 包。

打开 `Startup.cs` 并修改 `ConfigureServices` 方法，添加这一行:

```csharp
services.AddOrchardCms();
```

在 `Configure` 方法中，替换这个代码块:

```csharp
app.Run(async (context) =>
{
    await context.Response.WriteAsync("Hello World!");
});
```

使用这一行:

```csharp
app.UseOrchardCore();
```

添加一个 `wwwroot` 文件夹到你的项目

## Setup your application

启动你的应用程序 (Ctrl+F5)。将显示安装界面。

输入关于网站的所需资料:

- The name of the site. Ex: `Orchard Core`.
- The theme recipe to use. Ex: `Agency`.
- The timezone of the site. Ex: `(+01:00) Europe/Paris`.
- The Sql provider to use. Ex: `SqLite`.
- The name of the admin user. Ex: `admin`.
- The email of the admin. Ex: `foo@bar.com`
- The password and the password confirmation.

提交表单，你的站点几秒钟后就会生成。

然后，你可以使用 `/admin` url 访问 admin。享受它。
