# 从模块向 Admin 导航添加菜单项

`INavigationProvider` 接口是每个与处理 admin 导航菜单项相关的任务的入口点。
为了从模块中添加菜单项，你只需要创建一个实现该接口的类。

## 你将构建什么

你将构建一个模块，该模块将在根级别添加一个菜单项和两个子菜单项。
每个菜单项都指向自己的视图。

## 你需要什么

- .NET Core SDK 的当前版本。你可以从这里下载 https://www.microsoft.com/net/download/core。
- 文本编辑器和终端，你可以在其中键入 dotnet 命令。

## 创建一个 Orchard Core CMS 站点和模块

有不同的方法为 Orchard Core 创建站点和模块。你可以在[这里](../../templates/README.md) 了解更多。在本指南中，我们将使用“代码生成模板”。

你可以使用以下命令安装最新发布的模板:

```dotnet new -i OrchardCore.ProjectTemplates::1.0.0-*```

!!! 注意
    要使用模板的开发分支，添加 `--nuget-source https://www.myget.org/F/orchardcore-preview/api/v3/index.json`

创建一个包含站点的空文件夹。打开终端，导航到该文件夹并运行如下操作:

```dotnet new occms -n MySite```

这将在名为 `MySite` 的文件夹中创建一个新的 Orchard Core CMS 站点。
我们现在可以用以下命令创建一个新的模块:

```dotnet new ocmodulecms -n MyModule```

模块是在 `MyModule` 文件夹中创建的。
下一步是通过添加一个项目引用在应用程序中引用模块:

```dotnet add MySite reference MyModule```

我们还需要添加对 `OrchardCore.Admin` 包的引用，以便能够实现所需的接口:

```dotnet add .\MyModule\MyModule.csproj package OrchardCore.Admin --version 1.0.0-*```

!!! 注意
    如果你在使用模板的开发分支，在运行应用程序前执行 ` --source https://www.myget.org/F/orchardcore-preview/api/v3/index.json --version 1.0.0-*`

## 添加我们的控制器和视图

### 添加控制器

在 `.\MyModule\Controllers` 文件夹中创建一个 `DemoNavController.cs` 文件，包含这些内容:

#### DemoNavController.cs

```csharp
using Microsoft.AspNetCore.Mvc;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using OrchardCore.Admin;

namespace MyModule.Controllers
{
    [Admin]
    public class DemoNavController : Controller
    {
        public ActionResult ChildOne()
        {
            return View();
        }

        public ActionResult ChildTwo()
        {
            return View();
        }
    }
}
```

!!! 建议
   `[Admin]` 属性确保控制器使用 Admin 主题，并且用户具有访问该主题的权限。
   另一种实现此行为的方法是将该类命名为 `AdminController`。

### 添加视图

创建一个文件夹 `.\MyModule\Views\DemoNav`，并在其中添加这两个文件:

#### ChildOne.cshtml

```html
<p>View One</p>
```

#### ChildTwo.cshtml

```html
<p>View Two</p>
```

## 添加菜单项 ##

现在只需要添加一个实现 `INavigationProvider` 接口的类。
按照惯例，我们将这些类称为 `AdminMenu.cs`，然后把它放在模块文件夹的根目录下。

#### AdminMenu.cs

```csharp
using System;
using System.Threading.Tasks;
using Microsoft.Extensions.Localization;
using OrchardCore.Navigation;

namespace MyModule
{
    public class AdminMenu : INavigationProvider
    {
        public AdminMenu(IStringLocalizer<AdminMenu> localizer)
        {
            T = localizer;
        }
        
        public IStringLocalizer T { get; set; }

        public Task BuildNavigationAsync(string name, NavigationBuilder builder)
        {
            // We want to add our menus to the "admin" menu only.
            if (!String.Equals(name, "admin", StringComparison.OrdinalIgnoreCase))
            {
                return Task.CompletedTask;
            }

            // Adding our menu items to the builder.
            // The builder represents the full admin menu tree.
            builder
                .Add(T["My Root View"], "after",  rootView => rootView               
                    .Add(T["Child One"],"1", childOne => childOne
                        .Action("ChildOne", "DemoNav", new { area = "MyModule"}))
                    .Add(T["Child Two"], "2", childTwo => childTwo
                        .Action("ChildTwo", "DemoNav", new { area = "MyModule"})));

            return Task.CompletedTask;
        }
    }
}
```

然后你必须在模块的 `Startup.cs` 文件中注册这项服务。

在 `Startup.cs` 文件的顶部，加上这条 `using` 语句:

```csharp
using OrchardCore.Navigation;
```

将这一行添加到 `ConfigureServices()` 方法:

```csharp
services.AddScoped<INavigationProvider, AdminMenu>();
```

## 测试最终的应用程序

在包含两个项目的根目录中运行这条命令:

`dotnet run --project .\MySite\MySite.csproj`

!!! 注意
    如果你在使用模板的开发分支，在运行应用程序前运行 `dotnet restore .\MySite\MySite.csproj --source https://www.myget.org/F/orchardcore-preview/api/v3/index.json`

你的应用程序现在应该正在运行，并包含开放的端口:

```
Now listening on: https://localhost:5001
Now listening on: http://localhost:5000
Application started. Press Ctrl+C to shut down.
```

在浏览器中打开 <https://localhost:5001>

如果还没有设置站点，请选择 __Blank Site__ 作为 recipe，并使用 __SQLite__ 作为数据库。

一旦你的网站准备好了，你应该会看到一个 __The page could not be found.__ 消息，这是 __Blank Site__ recipe 的期望效果。

通过打开 <https://localhost:5001/admin> 进入 Admin 节并登录。

使用左侧菜单转到 __Configuration: Modules__，搜索你的模块 __MyModule__，并启用它。

现在你的模块已启用，你应该会在 admin 看到一个新的条目。
单击新菜单项以呈现我们之前创建的视图。

## 总结

你刚刚学习了如何将菜单项添加到 Admin 导航中。
