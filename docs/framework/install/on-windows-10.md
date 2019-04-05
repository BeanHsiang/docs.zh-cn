---
title: 在 Windows 10 上安装 .NET Framework
description: 了解如何在 Windows 10 或 Windows Server 2016 上安装 .NET Framework。
author: rlander
ms.author: mairaw
ms.date: 04/10/2018
ms.custom: updateeachrelease
ms.openlocfilehash: db5c6a45db299d716b2fdd115086e0dbc5952a59
ms.sourcegitcommit: e39d93d358974b9ed4541cedf4e25c0101015c3c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/29/2019
ms.locfileid: "55204296"
---
# <a name="install-the-net-framework-on-windows-10-and-windows-server-2016-and-later"></a>在 Windows 10 和 Windows Server 2016 及更高版本上安装 .NET Framework

在 Windows 上运行许多应用程序需要 .NET Framework。 本文中的相关说明可帮助你安装所需的 .NET Framework 版本。 [.NET Framework 4.7.2](https://dotnet.microsoft.com/download/dotnet-framework-runtime/net472) 是可用的最新版本。

在尝试运行应用程序后，你可能转到了此页并在计算机上看到一个对话框，如下所示：

![无法启动此应用程序](./media/this-application-could-not-be-started.png)

## <a name="net-framework-472"></a>.NET Framework 4.7.2

.NET Framework 4.7.2 随附：

* [Windows 10 2018 年 10 月更新](https://support.microsoft.com/help/4028685/windows-10-get-the-update)

* [Windows 10 2018 年 4 月更新](https://www.microsoft.com/software-download/windows10)

* Windows Server 2019

* Windows Server 版本 1809

* Windows Server 版本 1803

> [!div class="button"]
> [下载 .NET Framework 4.7.2](https://dotnet.microsoft.com/download/dotnet-framework-runtime/net472)

[.NET Framework 4.7.2](https://dotnet.microsoft.com/download/dotnet-framework-runtime/net472) 可用于运行针对 .NET Framework 4.0 到 4.7.1 生成的应用程序。

[.NET Framework 4.7.2](https://dotnet.microsoft.com/download/dotnet-framework-runtime/net472) 可安装于：

* Windows 10 秋季创意者更新（版本 1709）
* Windows 10 创意者更新（版本 1703）
* Windows 10 周年更新（版本 1607）
* Windows Server 版本 1709
* Windows 2016 Server

以下系统不支持 .NET Framework 4.7.2：

* Windows 10 1507
* Windows 10 1511

如果正在使用 Windows 10 1507 或 1511，且想要安装 .NET Framework 4.7.2，首先需要升级到较新的 Windows 10 版本。

## <a name="net-framework-462"></a>.NET Framework 4.6.2

[.NET Framework 4.6.2](https://www.microsoft.com/en-us/download/details.aspx?id=53345) 是 Windows 10 1507 和 1511 上支持的最新 .NET Framework 版本。

.NET Framework 4.6.2 支持针对 .NET Framework 4.0 到 4.6.2 生成的应用。

## <a name="net-framework-35"></a>.NET Framework 3.5

请按照说明操作，[在 Windows 10 上安装 .NET Framework 3.5](dotnet-35-windows-10.md)。

.NET Framework 3.5 支持针对 .NET Framework 1.0 到 3.5 生成的应用。

## <a name="additional-information"></a>其他信息

.NET Framework 4.x 版本是早期版本的就地更新版。 这意味着：

- 计算机上只能安装一个版本的 .NET Framework 4.x。

- 如果计算机上已安装更高版本，则不能安装 .NET Framework 的早期版本。

- .NET Framework 4.x 版本可用于运行针对 .NET Framework 4.0 到该版本生成的应用程序。 例如，.NET Framework 4.7 可用于运行针对 .NET Framework 4.0-4.7 生成的应用程序。 最新版本（即 .NET Framework 4.7.2）可用于运行使用从 .NET Framework 4.0 开始的 .NET Framework 的所有版本生成的应用程序。

如需可供下载的 .NET Framework 所有版本的列表，请参阅 [.NET 下载](https://www.microsoft.com/net/download?utm_source=ms-docs&utm_medium=referral)页。

## <a name="help"></a>帮助

如果无法确定已安装 .NET Framework 的正确版本，可以[联系 Microsoft 获取帮助](mailto:dotnet-install-help@service.microsoft.com?subject=Install-Help)。

## <a name="see-also"></a>请参阅

- [.NET 下载](https://www.microsoft.com/net/download?utm_source=ms-docs&utm_medium=referral)
- [安装和卸载 .NET Framework 受阻疑难解答](troubleshoot-blocked-installations-and-uninstallations.md)
- [安装面向开发者的 .NET Framework](guide-for-developers.md)
