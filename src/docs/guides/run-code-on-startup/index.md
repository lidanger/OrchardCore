# 如何在应用程序启动时从模块运行任务

`Startup` 类用于初始化服务和中间件。 
在初始化租户时调用它们。

`OrchardCore.ModulesIModularTenantEvents` 接口提供了一种方法来定义用户代码，这些代码将在第一次命中租户时执行 (临时激活)。

所有租户都是惰性加载的，这意味着当应用程序启动时，不会调用事件处理程序。而是在处理第一个请求时调用它们。

在下面的示例中，类 `MyStartupTaskService` 继承 `ModularTenantEvents` 来实现 `IModularTenantEvents`。

```csharp

using System;
using System.Threading.Tasks;
using Microsoft.Extensions.Logging;
using OrchardCore.Modules;

public class MyStartupTaskService : ModularTenantEvents
{
    private readonly ILogger<MyStartupTaskService> _logger;

    public MyStartupTaskService(ILogger<MyStartupTaskService> logger)
    {
        _logger = logger;
    }

    public override Task ActivatingAsync()
    {
        _logger.LogInfo("A tenant has been activated.");

        return Task.CompletedTask
    }
}
```

然后这个类在模块的 __Startup.cs__ 文件的 `ConfigureServices()` 方法中注册。

```csharp
services.AddScoped<IModularTenantEvents, MyStartupTaskService>();
```

> 注意: `ActivatingAsync` 事件是按照它们的注册顺序调用的，该顺序源自模块依赖关系图。以相反的顺序调用 `ActivatedAsync` 时间。