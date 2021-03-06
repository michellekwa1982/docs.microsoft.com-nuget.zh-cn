---
title: 通过 dotnet CLI 使用 NuGet 包的介绍性指南
description: 有关如何在 .NET Core 项目中安装并使用 NuGet 包的演练教程。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 2fac013de5457f26bbbaeff37209316daedcdbb0
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2018
ms.locfileid: "34816938"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a>快速入门：使用 dotnet CLI 安装并使用包

NuGet 包包含其他开发人员提供的在项目中使用的可重用代码。 请参阅[什么是 NuGet？](../What-is-NuGet.md)，了解背景信息。 使用如本文所述的适用于常用 [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) 包的 `dotnet add package` 命令将包安装到 .NET Core 项目中。

安装完成后，请引用具有 `using <namespace>` 的代码中的包，其中 \<namespace\> 特定于正在使用的包。 然后，可以使用包的 API。

> [!Tip]
> **nuget.org 入门**：浏览 nuget.org 是 .NET 开发人员通常在自己的应用程序中查找可重用组件的方式。 你可以直接搜索 nuget.org 或根据本文中的介绍，在 Visual Studio 中查找和安装包。

## <a name="prerequisites"></a>系统必备

- [.NET Core SDK](https://www.microsoft.com/net/download/)，提供 `dotnet` 命令行工具。

## <a name="create-a-project"></a>创建项目

可以将 NuGet 包安装到某种类型的 .NET 项目。 在本演练中，如下所示创建一个简单的 .NET Core 控制台项目：

1. 为项目创建文件夹。

1. 请使用以下命令创建项目：

    ```cli
    dotnet new console
    ```

1. 使用 `dotnet run` 来测试已正确创建的应用。

## <a name="add-the-newtonsoftjson-nuget-package"></a>添加 Newtonsoft.Json Nuget 包

1. 运行以下命令安装 `Newtonsoft.json` 包：

    ```cli
    dotnet add package Newtonsoft.Json
    ```

2. 该命令完成后，打开 `.csproj` 文件以查看所添加的引用：

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="10.0.3" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>在应用中使用 Newtonsoft.Json API

1. 打开 `Program.cs` 文件，然后在文件的顶部添加以下行：

    ```cs
    using Newtonsoft.Json;
    ```

1. 在 `class Program` 行的前面添加以下代码：

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. 使用以下代码替换 `Main` 函数：

    ```cs
    static void Main(string[] args)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@nuget.org",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };

        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        Console.WriteLine(json);
    }
    ```

1. 使用 `dotnet run` 命令生成并运行应用。 输出应是 `Account` 对象在代码中的 JSON 表示形式：

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="related-articles"></a>相关文章

- [包使用的概述和工作流](../consume-packages/overview-and-workflow.md)
- [查找和选择包](../consume-packages/finding-and-choosing-packages.md)
- [安装包的方式](../consume-packages/ways-to-install-a-package.md)
- [配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md)
