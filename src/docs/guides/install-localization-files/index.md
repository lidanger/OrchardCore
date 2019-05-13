# 安装本地化文件

在本指南中，你将下载并安装社区管理的本地化文件，以本地化 Orchard Core CMS 的管理页面。

## 你需要什么

- .NET Core SDK 的当前版本。你可以从这里下载 [https://www.microsoft.com/net/download/core](https://www.microsoft.com/net/download/core).
- 文本编辑器和终端，你可以在其中键入 dotnet 命令。
- 一个已经运行的 Orchard Core CMS 网站。如果你还没有的话，可以按照这个指南 [创建一个 Orchard Core CMS 网站](../create-cms-application/index.md) 去做。

## 下载本地化文件

本地化文件由社区在 [Crowdin](https://crowdin.com/project/orchard-core) 网站上管理。任何人都可以提供自定义语言或对现有语言进行贡献。

![image](assets/crowdin-languages.jpg)

对于本指南，我们将下载法语。

- 单击 __French__，一个带有所有 `.pot` 文件列表的页面应该会出现。
- 单击页面右上角的 __Download or Upload__ 按钮。
- 选择 __Download__，一个名为 `fr.zip` 的 zip 文件将被你的浏览器下载下来。

![image](assets/crowdin-download.jpg)

## 解压本地化文件

需要将下载的 zip 文件解压到 Orchard Core CMS 网站的 `App_Data/Localization` 文件夹中。

- 在你的网站 `[your_site_root]/App_Data` 下创建一个名为 `Localization` 的文件夹，其中 `your_site_root` 是你网站的位置。
- 将文件 `fr.zip` 解压到 `App_Data/Localization`

结果应该是这样的:

![image](assets/localization-folder.jpg)

## 配置受支持的 cultures

默认情况下，一个新的 Orchard Core CMS 网站将只接受默认的系统 culture。这一步将其配置为接受法语作为替代语言。

- 通过在浏览器中打开 <https://localhost:5001/admin> 打开 Orchard Core CMS 的 Admin 节。
- 在 __Configuration__, __Settings__, __General__ 节单击 __Add or remove supported cultures for the site__。
- 选择 `fr | French` 然后单击 __Add__。
- 单击 __Manage Settings__ 菜单项链接，该链接将重定向到 __General__ 设置页面。
- 单击 __Save__，重新加载站点。

## 启用本地化并测试站点

为了使 Orchard Core CMS 能够使用这些新文件，我们需要启用本地化特性。

- 在 __Modules__ 页面中搜索 __Localization__ 并单击 __Enable__。如果该特性已经启用，则不需要执行任何操作。
- 在当前 url 中添加 `?culture=fr`，链接应该是这样 <https://localhost:44300/blog/OrchardCore.Features/Admin/Features?culture=fr>。

在这一点上，大多数文本应该用法语显示。从现在开始，如果浏览器的默认 culture 配置为法语，那么 Admin 页面将使用我们下载的法语文本翻译显示。`?culture=fr` 只是模拟当前请求应该使用法语作为 UI culture 的一种方法。

![image](assets/localized-french.jpg)

## 总结

你刚刚下载并在 Orchard Core CMS 中启用了一个新的本地化。
