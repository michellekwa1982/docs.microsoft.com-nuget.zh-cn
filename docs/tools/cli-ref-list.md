---
title: NuGet CLI 列表命令
description: 对于 nuget.exe 列出命令的引用
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b0f144d8abbba7388fe39cd113e4eeddccbca2c6
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818433"
---
# <a name="list-command-nuget-cli"></a>(NuGet CLI) 中的列表命令

**适用于：** 包消耗、 发布&bullet;**受支持的版本：** 所有

显示从给定的源的包的列表。 如果未不指定任何源，在全局配置文件中，定义所有源`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`，使用。 如果`NuGet.Config`然后指定任何源`list`使用默认的源 (nuget.org)。

## <a name="usage"></a>用法

```cli
nuget list [search terms] [options]
```

其中可选的搜索词将筛选显示的列表。 搜索条款将应用到的包、 标记和包说明的名称，就像它们在 nuget.org 上使用它们时。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| AllVersions | 列出所有版本的包。 默认情况下，显示仅最新的包版本。 |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`使用 (Mac/Linux)。|
| ForceEnglishOutput | *（3.5 +)* 强制 nuget.exe 运行使用固定的、 基于英语的区域性。 |
| 帮助 | 显示的帮助命令的信息。 |
| IncludeDelisted | *（3.2 +)* 显示未列出的程序包。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| 预发行版 | 在列表中包含预发行程序包。 |
| 源 | 指定要搜索的程序包源的列表。 |
| 详细级别 | 指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
