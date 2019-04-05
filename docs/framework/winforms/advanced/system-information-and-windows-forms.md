---
title: 系统信息和 Windows 窗体
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- domain names [Windows Forms], retrieving
- SystemInformation class [Windows Forms]
- user names [Windows Forms], retrieving
- system information [Windows Forms]
ms.assetid: 30cf43a3-8cb2-4ff3-862b-6c34576616a8
ms.openlocfilehash: d8efb783fcb5bcbe9c4ee99bc784e27a1aebb0cf
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57707659"
---
# <a name="system-information-and-windows-forms"></a>系统信息和 Windows 窗体
有时有必要收集有关你的应用程序运行才能在你的代码中进行决策的计算机的信息。 例如，可能有一个函数，则仅当连接到特定网络域; 适用在这种情况下需要一种方法来确定域并禁用函数，如果域不存在。  
  
 Windows 窗体应用程序可以使用<xref:System.Windows.Forms.SystemInformation>类来确定在运行时执行大量有关计算机的操作。 下面的示例演示了如何使用<xref:System.Windows.Forms.SystemInformation>类来检索<xref:System.Windows.Forms.SystemInformation.UserName%2A>和<xref:System.Windows.Forms.SystemInformation.UserDomainName%2A>:  
  
```vb  
Dim User As String = Windows.Forms.SystemInformation.UserName  
Dim Domain As String = Windows.Forms.SystemInformation.UserDomainName  
  
MessageBox.Show("Good morning " & User & ". You are connected to " _  
& Domain)  
```  
  
```csharp  
string User = SystemInformation.UserName;  
string Domain = SystemInformation.UserDomainName;  
  
MessageBox.Show("Good morning " + User + ". You are connected to " _  
+ Domain)  
```  
  
 所有成员<xref:System.Windows.Forms.SystemInformation>类是只读的不能修改用户的设置。 有 100 多个类的成员，从监视器连接到计算机的数目上的所有内容返回信息 (<xref:System.Windows.Forms.SystemInformation.MonitorCount%2A>) 到 Windows 资源管理器中的图标的间距 (<xref:System.Windows.Forms.SystemInformation.IconHorizontalSpacing%2A>和<xref:System.Windows.Forms.SystemInformation.IconVerticalSpacing%2A>)。  
  
 一些更有用的成员<xref:System.Windows.Forms.SystemInformation>类包含<xref:System.Windows.Forms.SystemInformation.ComputerName%2A>， <xref:System.Windows.Forms.SystemInformation.DbcsEnabled%2A>， <xref:System.Windows.Forms.SystemInformation.PowerStatus%2A>，和<xref:System.Windows.Forms.SystemInformation.TerminalServerSession%2A>。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.SystemInformation>
- [Windows 窗体中的电源管理](power-management-in-windows-forms.md)
