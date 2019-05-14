# Orchard Core

Orchard Core 是对 [ASP.NET Core](https://docs.microsoft.com/aspnet/core/) 上的 [Orchard CMS](https://github.com/OrchardCMS/Orchard) 的重新开发。 

Orchard Core 包括两个不同的目标:

- **Orchard Core 框架**: 一个用于在 ASP.NET Core 上构建**模块化**、**多租户**应用程序的框架。
- **Orchard Core CMS**: 建立在 Orchard Core 框架之上的 Web 内容管理系统 (CMS).

重要的是要注意框架和 CMS 之间的区别。一些希望开发 SaaS 应用程序的开发人员只对模块化框架感兴趣。其他想要构建可管理网站的人将关注 CMS 并构建模块来增强他们的网站或整个生态系统。

[![Join the chat at https://gitter.im/OrchardCMS/OrchardCore](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/OrchardCMS/OrchardCore?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
[![BSD-3-Clause License](https://img.shields.io/badge/license-BSD--3--Clause-blue.svg)](https://github.com/OrchardCMS/OrchardCore/blob/master/LICENSE)
[![Documentation](https://readthedocs.org/projects/orchardcore/badge/)](https://orchardcore.readthedocs.io/en/latest/)
[![Crowdin](https://d322cqt584bo4o.cloudfront.net/orchard-core/localized.svg)](https://crowdin.com/project/orchard-core)

## 使用 Orchard Core 框架构建软件即服务 (SaaS) 解决方案

理解 Orchard Core 框架独立于 nuget.org 上的 CMS 是非常重要的。我们在 <https://github.com/OrchardCMS/OrchardCore.Samples> 上创建了一些示例应用程序，它们将指导你如何使用 Orchard Core 框架构建**模块化**和**多租户**应用程序，而不使用任何 CMS 的特定功能。

我们的目标之一是支持托管应用程序的基于社区的生态系统，这些应用程序可以通过模块 (如电子商务系统、博客引擎等) 进行扩展。Orchard Core 框架支持模块化环境，允许不同的团队处理应用程序的不同部分，并使组件可以跨项目重用。

## 使用 Orchard Core CMS 构建网站

Orchard Core CMS 是 Orchard CMS 在 ASP.NET Core 上的完整重写。它并不只是简单移植，因为我们希望大幅度提高性能，并尽可能地与 ASP.NET Core 的开发模型保持一致。

- **性能**。这可能是开始使用 Orchard Core CMS 时最明显的变化。这对于 CMS 来说是非常快的。速度如此之快，以至于我们甚至不关心如何处理输出缓存模块。为了让你了解一下，如果没有缓存 Orchard Core CMS，其速度大约是以前版本的 20 倍。

- **可移植**。现在可以在 Windows、Linux 和 macOS 上开发和部署 Orchard Core CMS。我们也有 Docker 镜像准备使用。

- **文档数据库**抽象。Orchard Core CMS 仍然需要一个关系数据库，并且兼容 SQL Server、MySQL、PostgreSQL 和 SQLite，但是现在它使用了一个文档抽象 (YesSql)，它提供了一个文档数据库 API 来存储和查询文档。对于 CMS 系统来说，这是一种更好的方法，可以显著提高性能。

- **NuGet 包**。模块和主题现在以 NuGet 包形式共享。使用 Orchard Core CMS 创建一个新网站实际上非常简单，只需从 NuGet gallery 中引用一个元包即可。它还意味着更新到一个较新的版本只需要更新这个包的版本号。

- **实时预览**。当编辑内容项时，你现在可以实时看到它在站点上的样子，甚至在保存内容之前也是如此。它也适用于模板，你可以浏览任何页面，在键入模板时检查更改对模板的影响。

- **支撑 Liquid 模板**。编辑器可以安全地使用 Liquid 模板语言更改 HTML 模板。之所以选择它，是因为它有很好的文档 (Jekyll, Shopify，…) 和安全性。

- **自定义查询**。我们希望为开发人员提供一种尽可能简单地访问所有数据的方法。我们创建了一个模块，该模块允许你创建自定义的 ad-hoc SQL 和 Lucene 查询，这些查询可以被重用来显示自定义内容，或者作为 API 端点公开。你可以使用它来创建有效的查询，或者将数据公开给 SPA 应用程序。

- **部署计划**。部署计划是可以包含构建网站的内容和元数据的脚本。现在可以包含二进制文件，例如，甚至可以使用它们将站点从临时场所远程部署到生产环境。它们也可以是 NuGet 包的一部分，使你可以发布预定义的网站。

- **可伸缩性**。因为 Orchard Core 是一个多租户系统，你可以通过一个部署来托管任意数量的网站。然后，一台典型的云计算机可以并行地承载数千个站点，包括数据库、内容、主题和用户隔离。

- **工作流**。创建内容审批工作流、对 webhook 做出反应、在提交表单时采取行动，以及你希望通过用户友好的 UI 实现的任何其他流程。

- **GraphQL**。我们提供了一个非常灵活的 GraphQL API，这样任何经过授权的外部应用程序都可以重用你的内容，比如 SPA 应用程序或静态站点生成器。

### 不同的网站构建策略

Orchard Core CMS 支持所有主要站点建设策略:

- **Full CMS**。在这种模式下，网站使用主题和模板来呈现内容，目标是很少或根本没有定制开发。

- **Decoupled CMS**。除了内容管理后端之外，站点一开始是空白的。你可以使用 Razor 页面或 MVC 操作创建所需的所有模板，并通过内容服务访问内容。

- **Headless CMS**。站点只管理内容，你可以创建一个单独的应用程序，该应用程序将使用 GraphQL 或 REST Api 获取托管内容。

## 状态

最新发布的 Orchard Core 版本是 `1.0.0-beta3`。
发布说明可以在 <https://github.com/OrchardCMS/OrchardCore/releases/tag/1.0.0-beta3> 找到

软件已经足够完成外部测试——也就是说，由开发软件的组织或社区之外的小组进行测试。Beta 版软件通常功能齐全，但可能有已知的限制或缺陷。Beta 版本要么是封闭的(私有的)，并且仅限于特定的一组用户，要么是向公众开放的。

这里是更详细的[路线图](https://github.com/OrchardCMS/OrchardCore/wiki/Roadmap).

## 入门指南

- 使用命令 `git clone https://github.com/OrchardCMS/OrchardCore.git` 克隆存储库，并检出 `master` 分支来获取最新版本，或者检出 `dev` 分支来获取 cutting-edge 版本。

- 观看展示 Orchard Core 的 ASP.NET Community Standup 视频: <https://www.youtube.com/watch?v=HeDjv3blBjQ&t=2246s&list=PL1rZQsJPBU2StolNg0aqvQswETPcYnNKL&index=24> 

- 跟随 <https://github.com/OrchardCMS/OrchardCore.Samples> 上的示例，该示例将指导你如何构建**模块化**和**多租户**应用程序

- 跟随 [Training Demo Module](https://github.com/Lombiq/Orchard-Training-Demo-Module) 中的教程学习如何开发 Orchard Core 模块。

### 命令行

- 安装来自这个页面 <https://www.microsoft.com/net/download/core> 的 .NET Core SDK 的最新版本 
- 调用 `dotnet build`。
- 下一步，导航到 `D:\OrchardCore\src\OrchardCore.Cms.Web` 或任何你可以打开管理员模式命令行的文件夹。
- 调用 `dotnet run`。
- 然后在你的浏览器中打开 URL `http://localhost:5000`。

你还可以阅读[代码生成模板文档](Templates/README)，从预定义的模板创建新应用程序。

### Visual Studio 2017

- 从 <https://www.visualstudio.com/downloads/> 下载 Visual Studio 2017 (任何版本)。
- 打开 `OrchardCore.sln` 然后等待 Visual Studio 恢复所有 Nuget 包。
- 确保 `OrchardCore.Cms.Web` 是启动项目，并运行它。
- 可以选择安装 [Lombiq Orchard Visual Studio Extension](https://marketplace.visualstudio.com/items?itemName=LombiqVisualStudioExtension.LombiqOrchardVisualStudioExtension)，向 Visual Studio 添加一些有用的实用程序，比如错误日志监视程序或依赖注入器。

### 贡献代码

我们目前遵循这些[工程指南](https://github.com/OrchardCMS/OrchardCore/wiki/Engineering-Guidelines)。
