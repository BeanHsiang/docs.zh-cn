---
title: Windows 窗体安全
ms.date: 03/30/2017
helpviewer_keywords:
- designer access security [Windows Forms]
- permissions [Windows Forms], Windows Forms
- Windows Forms, security
- security [Windows Forms]
- access control [Windows Forms], Windows Forms
- security policy [Windows Forms], Windows Forms
ms.assetid: 932d438a-5285-46d8-a958-8c93d0ad6cae
ms.openlocfilehash: f64d5ef2e9bb0e977b4c007e8c5109ac0c331a84
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57709544"
---
# <a name="windows-forms-security"></a>Windows 窗体安全
Windows 窗体的功能是基于代码的 （安全级别设置为代码，而不考虑运行代码的用户） 的安全模型。 其中不包括任何可能已在您的计算机系统中的安全架构。 其中可能包括那些在浏览器 （如基于区域的安全在 Internet Explorer 中可用） 或操作系统 （例如基于凭据的 Windows NT 的安全性）。  
  
## <a name="in-this-section"></a>本节内容  
 [Windows 窗体中的安全性概述](security-in-windows-forms-overview.md)  
 简要介绍了.NET Framework 安全模型并要确保你的应用程序中的 Windows 窗体所需的基本步骤的安全。  
  
 [在 Windows 窗体中提高文件和数据访问的安全性](more-secure-file-and-data-access-in-windows-forms.md)  
 介绍如何访问文件和不完全受信任环境中的数据。  
  
 [Windows 窗体中更加安全的打印](more-secure-printing-in-windows-forms.md)  
 介绍如何访问部分信任的环境中的打印功能。  
  
 [Windows 窗体中额外的安全注意事项](additional-security-considerations-in-windows-forms.md)  
 介绍使用剪贴板，并调用非托管代码在部分信任的环境中执行窗口操作。  
  
## <a name="related-sections"></a>相关章节  
 [默认安全策略](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/03kwzyfc(v=vs.100))  
 列出了授予完全信任、 本地 Intranet 和 Internet 权限集的默认权限。  
  
 [常规安全策略管理](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ed5htz45(v=vs.100))  
 提供有关管理的.NET Framework 安全策略和提升权限的信息。  
  
 [危险权限和策略管理](../misc/dangerous-permissions-and-policy-administration.md)  
 讨论一些可能允许绕过安全系统的.net Framework 权限。  
  
 [安全编码准则](../../standard/security/secure-coding-guidelines.md)  
 这些主题介绍用于安全地编写针对.NET Framework 代码的最佳做法的链接。  
  
 [请求权限](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/yd267cce(v=vs.100))  
 介绍如何使用属性告知运行时知道你的代码需要运行哪些权限。  
  
 [安全性的基础概念](../../standard/security/key-security-concepts.md)  
 链接到介绍代码安全性的基本方面的主题。  
  
 [代码访问安全性基础知识](../misc/code-access-security-basics.md)  
 讨论使用运行时安全策略的.NET Framework 的基础知识。  
  
 [确定何时修改安全策略](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/xky659fc(v=vs.100))  
 介绍如何确定您的应用程序需要从默认的安全策略发生偏离。  
  
 [部署安全性策略](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/13wcxx6y(v=vs.100))  
 讨论用于部署的安全策略更改的最佳方式。
