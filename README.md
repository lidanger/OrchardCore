# Orchard Core 

Orchard Core 包括两个不同的项目:

- __Orchard Core 框架__: 一个用于在 ASP.NET Core 上构建模块化、多租户应用程序的框架。
- __Orchard Core CMS__: 建立在 Orchard Core 框架之上的 Web 内容管理系统 (CMS)。

[![Join the chat at https://gitter.im/OrchardCMS/OrchardCore](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/OrchardCMS/OrchardCore?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
[![BSD-3-Clause License](https://img.shields.io/badge/license-BSD--3--Clause-blue.svg)](LICENSE.txt)
[![Documentation](https://readthedocs.org/projects/orchardcore/badge/)](https://orchardcore.readthedocs.io/en/latest/)
[![Crowdin](https://d322cqt584bo4o.cloudfront.net/orchard-core/localized.svg)](https://crowdin.com/project/orchard-core)


## 构建状态

Stable (master): 

[![Build Status](https://api.travis-ci.org/OrchardCMS/OrchardCore.svg?branch=master)](https://travis-ci.org/OrchardCMS/OrchardCore/branches)
[![Build status](https://img.shields.io/appveyor/ci/alexbocharov/orchardcore/master.svg?label=appveyor&style=flat-square)](https://ci.appveyor.com/project/alexbocharov/orchardcore/branch/master)
[![NuGet](https://img.shields.io/nuget/v/OrchardCore.Application.Cms.Targets.svg)](https://www.nuget.org/packages/OrchardCore.Application.Cms.Targets)

Nightly (dev): 

[![Build Status](https://api.travis-ci.org/OrchardCMS/OrchardCore.svg?branch=dev)](https://travis-ci.org/OrchardCMS/OrchardCore/branches)
[![Build status](https://img.shields.io/appveyor/ci/alexbocharov/orchardcore/dev.svg?label=appveyor&style=flat-square)](https://ci.appveyor.com/project/alexbocharov/orchardcore/branch/dev)
[![MyGet](https://img.shields.io/myget/orchardcore-preview/vpre/OrchardCore.Application.Cms.Targets.svg)](https://myget.org/feed/orchardcore-preview/package/nuget/OrchardCore.Application.Cms.Targets)

## 项目状态

### Beta 3

软件已经足够完成外部测试——也就是说，由开发此软件的组织或社区之外的小组进行测试。Beta 版软件通常功能齐全，但可能有已知的限制或缺陷。Beta 版本要么是封闭的 (私有的)，并仅限于特定的一组用户，要么是向公众开放的。

这里是更详细的 [路线图](https://github.com/OrchardCMS/OrchardCore/wiki/Roadmap)。

## 入门指南

- 使用命令 `git clone https://github.com/OrchardCMS/OrchardCore.git` Clone 出存储库并检出 `dev` 分支。 

### 命令行

- 安装来自这个页面 https://www.microsoft.com/net/download/core 的最新版本 (当前版本) .NET Core 运行时和 SDK。
- 导航到 `D:\OrchardCore\src\OrchardCore.Cms.Web` 或任何可以在管理员模式的命令行中打开的文件夹。
- 调用 `dotnet run`。
- 然后在你的浏览器中打开 URL `http://localhost:5000`。

### Visual Studio

- 从 https://www.visualstudio.com/downloads/ 下载 Visual Studio 2017 或 2019 (任何版本) 
- 打开 `OrchardCore.sln` 然后等待 Visual Studio 恢复所有 Nuget 包
- 确保 `OrchardCore.Cms.Web` 是一个启动项目，并运行它

### Docker

- Run `docker run --name orchardcms orchardproject/orchardcore-cms-linux:latest`

Docker 镜像和参数可以在 https://hub.docker.com/u/orchardproject/ 找到

### 文档

文档可以在这里浏览: [https://orchardcore.readthedocs.io/en/dev/](https://orchardcore.readthedocs.io/en/dev/)
