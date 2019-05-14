# 代码生成模板

Orchard Core 模板使用 `dotnet new` 模板配置从命令 shell 创建新网站、主题和模块。

有关 `dotnet new` 的更多信息，请访问 <https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-new>

## 安装 Orchard CMS 模板

安装了 .NET Core SDK 之后，键入以下命令来安装创建 Orchard Core web 应用程序的模板:

```CMD
dotnet new -i OrchardCore.ProjectTemplates::1.0.0-beta3-*
```

这将使用 Orchard Core 的最稳定版本。为了使用 Orchard Core 的最新 `dev` 分支，可以使用以下命令:

```CMD
dotnet new -i OrchardCore.ProjectTemplates::1.0.0-beta3-* --nuget-source https://www.myget.org/F/orchardcore-preview/api/v3/index.json  
```

## 创建一个新网站

### 在命令 Shell 中 (自动方式)

#### 生成一个 Orchard Cms Web 应用程序

```CMD
dotnet new occms  
```
上面的命令将使用默认选项。

你可以将以下 CLI 参数传递给启动选项

```CMD
Orchard Core Cms Web App (C#)
Author: Orchard Project
Options:
  -lo|--logger           Configures the logger component.
                             nlog       - Configures NLog as the logger component.
                             serilog    - Configures Serilog as the logger component.
                             none       - Do not use a logger.
                         Default: nlog

  -ov|--orchard-version  Specifies which version of Orchard Core packages to use.
                         string - Optional
                         Default: 1.0.0-beta3
```

使用以下命令可以忽略日志记录:

```CMD
dotnet new occms --logger none
```

#### 生成一个模块化的 ASP.NET MVC Core Web 应用程序

```CMD
dotnet new ocmvc  
```

### 在 Visual Studio 中 (手动方式)

启动 Visual Studio，通过创建一个新 ASP.NET Core Web 应用程序来创建一个新解决方案文件 (`.sln`):

![image](../assets/images/templates/orchard-screencast-1.gif)

现在我们创建了一个新的 Web 应用程序，我们需要添加适当的依赖项，这样这个新 Web 应用程序可以当成 Orchard Core 应用程序。

参见 [Adding Orchard Core Nuget Feed](#adding-orchard-core-nuget-feed)

![image](../assets/images/templates/orchard-screencast-2.gif)

最后，我们需要在我们的 `Startup.cs` 文件中注册 Orchard CMS 服务，像这样:

```C#
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Hosting;
using Microsoft.AspNetCore.Http;
using Microsoft.Extensions.DependencyInjection;

namespace MyNewWebsite
{
    public class Startup
    {
        // This method gets called by the runtime. Use this method to add services to the container.
        // For more information on how to configure your application, visit https://go.microsoft.com/fwlink/?LinkID=398940
        public void ConfigureServices(IServiceCollection services)
        {
            services.AddOrchardCms();
        }

        // This method gets called by the runtime. Use this method to configure the HTTP request pipeline.
        public void Configure(IApplicationBuilder app, IHostingEnvironment env)
        {
            if (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
            }

            app.UseOrchardCore();
        }
    }
}
```

## 创建一个新 CMS 模块

### 在命令 Shell 中创建新模块 (自动方式)

#### 模块命令

```CMD
dotnet new ocmodulecms -n ModuleName.OrchardCore

dotnet new ocmodulecms -n ModuleName.OrchardCore --PartName TestPart

dotnet new ocmodulecms -n ModuleName.OrchardCore --PartName TestPart --AddPart true
```

### 在 Visual Studio 中创建新模块 (手动方式)

打开 Visual Studio，打开 Orchard Core 解决方案文件 (`.sln`)，选择 `OrchardCore.Modules` 文件夹，右键单击并选择 "add --> new project"，创建一个新 .NET Standard 类库:

![image](../assets/images/templates/38450533-6c0fbc98-39ed-11e8-91a5-d26a1105b91a.png)

为了将这个新类库标记为 Orchard 模块，我们现在需要引用 `OrchardCore.Module.Targets` Nuget 包。

参见 [adding Orchard Core Nuget Feed](#adding-orchard-core-nuget-feed)。

每一个 `*.Targets` Nuget 包用于将类库标记为特定的 Orchard Core 功能。`OrchardCore.Module.Targets` 是我们目前感兴趣的。我们通过将 `OrchardCore.Module.Targets` 添加位依赖把我们的新类库标记为一个模块。为此，你需要右键单击 `MyModule.OrchardCore` 项目并选择 "Manage Nuget Packages" 选项。要在 Nuget Package Manager 中找到包，你需要检查 "include prerelease" ，并确保你有我们之前选择的 Orchard Core 源。找到它之后，单击 Version: Latest prerelease x.x.x.x 旁边右侧面板上的 Install 按钮

![image](../assets/images/templates/38450558-f4b83098-39ed-11e8-93c7-0fd9e5112dff.png)

一旦完成，你的新模块将如下所示:

![image](../assets/images/templates/38450628-31c8e2b0-39ef-11e8-9de7-c15f0c6544c5.png)

为了让 Orchard Core 识别这个模块，现在需要一个 `Manifest.cs` 文件。下面是这个文件的一个例子:

```C#
using OrchardCore.Modules.Manifest;

[assembly: Module(
    Name = "TemplateModule.OrchardCore",
    Author = "The Orchard Team",
    Website = "http://orchardproject.net",
    Version = "0.0.1",
    Description = "Template module."
)]

```

要启动这个模块，我们现在需要添加一个 `Startup.cs` 文件到我们的新模块。以这个文件为例:  
[`OrchardCore.Templates.Cms.Module/Startup.cs`](https://github.com/OrchardCMS/OrchardCore/tree/dev/src/Templates/OrchardCore.ProjectTemplates/content/OrchardCore.Templates.Cms.Module/Startup.cs)

为了将我们的新模块添加为我们网站模块的一部分，最后一步是在 `OrchardCore.Cms.Web` 项目将它添加为引用。在此之后，你应该为开始构建自定义模块做好了一切准备。你可以参考我们的 [template module](https://github.com/OrchardCMS/OrchardCore/tree/dev/src/Templates/OrchardCore.ProjectTemplates/content/OrchardCore.Templates.Cms.Module/) 来了解正常情况下基本需要什么。

## 创建一个新主题

### 在命令 Shell 中创建新主题 (自动方式)

#### 主题命令

`dotnet new octheme -n "ThemeName.OrchardCore"`

### 在 Visual Studio 中创建新主题 (手动方式)

应该与模块的过程相同，但相反我们需要引用 `OrchardCore.Theme.Targets`，而且 `Manifest.cs` 文件略有不同:

```C#
using OrchardCore.DisplayManagement.Manifest;

[assembly: Theme(
    Name = "TemplateTheme.OrchardCore",
    Author = "The Orchard Team",
    Website = "https://orchardproject.net",
    Version = "0.0.1",
    Description = "The TemplateTheme."
)]
```

## 添加 Orchard Core Nuget 源

为了能够使用来自 Visual Studio 的 __dev__ 源，打开 Nuget Package Manager --> Package Manager Settings 下的 Tools 菜单。源 url 是 <https://www.myget.org/F/orchardcore-preview/api/v3/index.json>

![image](../assets/images/templates/38450422-63670f1c-39eb-11e8-9c14-0743f0a4da42.png)
