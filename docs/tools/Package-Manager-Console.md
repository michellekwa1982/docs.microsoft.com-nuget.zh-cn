---
title: NuGet 程序包管理器控制台指南
description: 使用 Visual Studio 中的 NuGet 程序包管理器控制台，用于处理包的说明。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/23/2018
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 06c525cab2dac61c92c4596533173f1d93493d9a
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817653"
---
# <a name="package-manager-console"></a>程序包管理器控制台

NuGet Package Manager Console 内置于 Visual Studio 在 Windows 2012 和更高版本。 （不包含在 Visual Studio 用于 Mac 或 Visual Studio Code。）

控制台，你可以使用[NuGet PowerShell 命令](../tools/powershell-reference.md)若要查找，安装、 卸载和更新 NuGet 程序包。 使用控制台是在包管理器 UI 不提供了如何执行操作的情况下必需的。 若要使用`nuget.exe`命令在控制台中，请参阅[使用控制台中的 CLI nuget.exe](#using-the-nugetexe-cli-in-the-console)。

例如，查找和安装的包，可使用三个简单步骤：

1. 在 Visual Studio 中，打开项目/解决方案并打开控制台使用**工具 > NuGet 包管理器 > 程序包管理器控制台**命令。

1. 查找你想要安装的程序包。 如果你已经知道此，请跳到步骤 3。

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. 运行安装命令：

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> 在控制台中可用的所有操作也都可以与[NuGet CLI](../tools/nuget-exe-cli-reference.md)。 但是，控制台命令在 Visual Studio 和已保存的项目/解决方案的上下文中运行，并且通常完成多个其等效的 CLI 命令。 例如，安装通过控制台的包将引用添加到项目而 CLI 命令不运行。 为此，通常在 Visual Studio 中工作的开发人员喜欢使用 CLI 到控制台。

> [!Tip]
> 许多控制台操作取决于使用已知的路径名称在 Visual Studio 中打开解决方案。 如果你有未保存的解决方案或没有解决方案，您可以看到此错误，"是未打开或保存解决方案。 请确保你已打开并保存解决方案。" 这表示控制台无法确定解决方案的文件夹。 保存未保存的解决方案，或创建和保存解决方案，如果你还没有打开，应纠正该错误。

## <a name="opening-the-console-and-console-controls"></a>打开的控制台和控制台控件

1. 打开 Visual Studio 中使用控制台**工具 > NuGet 包管理器 > 程序包管理器控制台**命令。 在控制台中，可以排列和定位你的喜好的 Visual Studio 窗口 (请参阅[自定义 Visual Studio 中的窗口布局](/visualstudio/ide/customizing-window-layouts-in-visual-studio))。

1. 默认情况下，控制台命令运行针对特定的包源和项目中控件的窗口的顶部设置：

    ![对包源和项目程序包管理器控制台控制](media/PackageManagerConsoleControls1.png)

1. 选择一个不同的包源和/或项目更改这些默认设置的后续命令。 覆盖而无需更改默认设置，这些设置的大多数命令支持`-Source`和`-ProjectName`选项。

1. 若要管理的包源，选择齿轮图标。 这是一个指向快捷方式**工具 > 选项 > NuGet 包管理器 > 程序包源**对话框上所述[包管理器 UI](package-manager-ui.md#package-sources)页。 此外，右侧为项目选择器控件清除控制台的内容：

    ![程序包管理器控制台设置和清除控件](media/PackageManagerConsoleControls2.png)

1. 最右边的按钮中断长时间运行的命令。 例如，运行`Get-Package -ListAvailable -PageSize 500`列出上默认源 （如 nuget.org)，可能需要几分钟时间运行的前 500 包。

    ![程序包管理器控制台停止控件](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a>安装的包

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

请参阅[安装包](../tools/ps-ref-install-package.md)。

在控制台中安装的包执行相同的步骤，如所述[安装包时，会发生什么情况](../consume-packages/ways-to-install-a-package.md#what-happens-when-a-package-is-installed)，添加了以下内容：

- 控制台显示在其窗口并默示协议适用的许可条款。 如果你不同意这些条款，你应立即卸载程序包。
- 此外对包的引用添加到项目文件，并出现在**解决方案资源管理器**下**引用**节点，您必须先保存该项目才能直接看到项目文件中的更改。

## <a name="uninstalling-a-package"></a>卸载包

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

请参阅[卸载包](../tools/ps-ref-uninstall-package.md)。 使用[Get 包](../tools/ps-ref-get-package.md)查看当前安装在默认项目中，如果你需要查找标识符的所有包。

卸载程序包执行下列操作：

- 将对包从项目 （和正在使用的任何管理格式） 的引用。 引用不再显示在**解决方案资源管理器**。 (你可能需要重新生成该项目才能看到它从删除**Bin**文件夹。)
- 反转对所做任何更改`app.config`或`web.config`时已安装了包。
- 如果没有剩余的包使用这些依赖关系，依赖以前安装中删除项。

## <a name="updating-a-package"></a>更新程序包

```ps
# Checks if there are newer versions available for any installed packages
Get-Package -updates

# Updates a specific package using its identifier, in this case jQuery
Update-Package jQuery

# Update all packages in the project named MyProject (as it appears in Solution Explorer)
Update-Package -ProjectName MyProject

# Update all packages in the solution
Update-Package
```

请参阅[Get 包](../tools/ps-ref-get-package.md)和[更新包](../tools/ps-ref-update-package.md)

## <a name="finding-a-package"></a>查找包

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```

请参阅[查找包](../tools/ps-ref-find-package.md)。 在 Visual Studio 2013 和更早版本，使用[Get 包](../tools/ps-ref-get-package.md)相反。

## <a name="availability-of-the-console"></a>控制台可用性

在 Visual Studio 2017，NuGet 和 NuGet 包管理器将自动安装时选择任何。提供与.NET 相关的工作负荷;你就可以还单独安装它，通过检查**各个组件 > 代码工具 > NuGet 包管理器**在 Visual Studio 2017 安装程序中的选项。

此外，如果你缺少 NuGet 包管理器在 Visual Studio 2015 及更早版本，请检查**工具 > 扩展和更新...** 和搜索 NuGet 包管理器扩展。 如果你无法使用 Visual Studio 中的扩展安装程序，你可以下载直接从扩展[ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html)。

程序包管理器控制台不是当前适用于 Visual Studio for mac。 等效命令，但是，这些功能通过[NuGet CLI](nuget-exe-CLI-reference.md)。 适用于 Mac 的 visual Studio 也用于管理 NuGet 包存在一些 UI。 请参阅[中你的项目包括 NuGet 包](/visualstudio/mac/nuget-walkthrough)。

程序包管理器控制台不包括 Visual Studio 代码。

## <a name="extending-the-package-manager-console"></a>扩展包管理器控制台

某些包安装新的控制台的命令。 例如，`MvcScaffolding`创建等命令`Scaffold`下面所示，这将生成 ASP.NET MVC 控制器和视图：

![安装和使用 MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a>设置 NuGet PowerShell 配置文件

PowerShell 配置文件，可以提供常用的命令，只要你使用 PowerShell。 NuGet 支持通常在以下位置找到 NuGet 特定配置文件：

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

若要查找配置文件，请键入`$profile`在控制台中：

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

有关更多详细信息，请参阅[Windows PowerShell 配置文件](https://technet.microsoft.com/library/bb613488.aspx)。

## <a name="using-the-nugetexe-cli-in-the-console"></a>使用 nuget.exe CLI 在控制台中

若要使[ `nuget.exe` CLI](nuget-exe-cli-reference.md)可用在程序包管理器控制台中，安装[NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/)从控制台的包：

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
