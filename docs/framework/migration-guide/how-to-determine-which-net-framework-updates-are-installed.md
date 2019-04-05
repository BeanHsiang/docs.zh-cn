---
title: 如何：确定安装了哪些 .NET Framework 安全更新和修补程序
description: 了解如何确定计算机上安装了哪些 .NET Framework 安全更新和修补程序。
ms.date: 11/27/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- updates, determining for .NET Framework
- .NET Framework, determining updates
ms.assetid: 53c7b5f7-d47a-402a-b194-7244a696a88b
author: mairaw
ms.author: mairaw
ms.openlocfilehash: e11b2588471e95b4e47fd0efaf41757430b9bb39
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54604179"
---
# <a name="how-to-determine-which-net-framework-security-updates-and-hotfixes-are-installed"></a>如何：确定安装了哪些 .NET Framework 安全更新和修补程序

本文介绍如何找出计算机上安装了哪些 .NET Framework 安全更新和修补程序。

> [!NOTE]
> 本文中介绍的所有方法均需要具有管理权限的帐户。

## <a name="to-find-installed-updates-using-the-registry"></a>使用注册表找到已安装的更新

安装在计算机上的各个版本 .NET Framework 的已安装安全更新和修补程序都列在 Windows 注册表中。 可以使用注册表编辑器 (regedit.exe) 程序查看此信息。

1. 打开程序 **regedit.exe**。 在 Windows 8 和更高版本中，右键单击“开始”![Windows 徽标](../get-started/media/windowskeyboardlogo.png "Windowskeyboardlogo")，然后选择“运行”。 在“打开”对话框中，输入“regedit.exe”并选择“确定”。

2. 在注册表编辑器中，打开以下子项：

     `HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Updates`

     已安装的更新在标识适用的 .NET Framework 版本的子项下方列出。 每个更新均由知识库 (KB) 编号进行标识。

在注册表编辑器中，.NET Framework 版本和每个版本已安装的更新都保存在不同的子项中。 有关检测已安装版本号的信息，请参阅[如何：确定已安装的 .NET Framework 版本](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)。

## <a name="to-find-installed-updates-by-querying-the-registry-in-code"></a>通过在代码中查询注册表找到已安装的更新

以下示例以编程方式确定已安装在计算机上的 .NET Framework 安全更新和修补程序：

[!code-csharp[ListUpdates](../../../samples/snippets/csharp/VS_Snippets_CLR/listupdates/cs/program.cs)]
[!code-vb[ListUpdates](../../../samples/snippets/visualbasic/VS_Snippets_CLR/listupdates/vb/program.vb)]

该示例生成类似下面内容的输出：

```console
Microsoft .NET Framework 4 Client Profile
  KB2468871
  KB2468871v2
  KB2478063
  KB2533523
  KB2544514
  KB2600211
  KB2600217
Microsoft .NET Framework 4 Extended
  KB2468871
  KB2468871v2
  KB2478063
  KB2533523
  KB2544514
  KB2600211
  KB2600217
```

## <a name="to-find-installed-updates-by-querying-the-registry-in-powershell"></a>在 PowerShell 中查询注册表找到已安装的更新

以下示例介绍如何使用 PowerShell 确定已安装在计算机上的 .NET Framework 安全更新和修补程序：

```powershell
$DotNetVersions = Get-ChildItem HKLM:\SOFTWARE\WOW6432Node\Microsoft\Updates | Where-Object {$_.name -like
 "*.NET Framework*"}

ForEach($Version in $DotNetVersions){
    
   $Updates = Get-ChildItem $Version.PSPath
    $Version.PSChildName
    ForEach ($Update in $Updates){
       $Update.PSChildName
       }
}
```

该示例生成类似下面内容的输出：

```console
Microsoft .NET Framework 4 Client Profile
KB2468871
KB2468871v2
KB2478063
KB2533523
KB2544514
KB2600211
KB2600217
Microsoft .NET Framework 4 Extended
KB2468871
KB2468871v2
KB2478063
KB2533523
KB2544514
KB2600211
KB2600217
```

## <a name="see-also"></a>请参阅

- [如何：确定已安装的 .NET Framework 版本](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)
- [安装面向开发者的 .NET Framework](../../../docs/framework/install/guide-for-developers.md)
- [版本和依赖关系](../../../docs/framework/migration-guide/versions-and-dependencies.md)
