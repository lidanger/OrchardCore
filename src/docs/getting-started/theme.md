# Orchard Core 主题入门指南

在本文中，我们将通过将 Orchard Core 主题添加到现有的[以前创建的](README) Orchard Core CMS 应用程序中来创建它。

## 创建一个 Orchard Core 主题

- 安装[代码生成模板](../../Templates/README) 
- 创建一个名为你的主题 (Ex: `MyTheme.OrchardCore`) 的文件夹并打开它
- 执行命令 `dotnet new octheme`
- 从主 Orchard Core CMS Web 应用程序中添加对主题的引用

缩略图也可以通过添加 `wwwwroot` 文件夹中的 `Theme.png` 来创建。

![image](assets/MyTheme.png)

主题的属性可在 __Manifest.cs__ 文件中更改:

```csharp
using OrchardCore.DisplayManagement.Manifest;

[assembly: Theme(
    Name = "MyTheme",
    Author = "My name",
    Website = "https://mywebsite.net",
    Version = "0.0.1",
    Description = "My Orchard Core Theme description."
)]
```

主题应该在 `Active themes` 管理页面中可用，并且可以设置为默认主题。
