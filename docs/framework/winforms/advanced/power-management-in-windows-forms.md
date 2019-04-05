---
title: Windows 窗体中的电源管理
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- battery states
- power states
ms.assetid: ad04a801-5682-4d88-92c5-26eb9cdb209a
ms.openlocfilehash: 77d2096239ec70f98ebfc299f1eda75ad4490be9
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57712417"
---
# <a name="power-management-in-windows-forms"></a>Windows 窗体中的电源管理
在 Windows 操作系统中，Windows 窗体应用程序可以充分利用电源管理功能。 你的应用程序可以监视计算机的电源状态和状态更改发生时执行操作。 例如，如果你的应用程序运行在便携式计算机上，您可能想要计算机的电池电量低于某个级别时禁用你的应用程序中的某些功能。  
  
 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]提供了<xref:Microsoft.Win32.SystemEvents.PowerModeChanged>的电源状态，例如，当用户挂起或恢复操作系统，或 AC 电源状态或电池状态发生更改时变化时，会发生的事件。 <xref:System.Windows.Forms.SystemInformation.PowerStatus%2A>属性的<xref:System.Windows.Forms.SystemInformation>类可以用来查询有关当前状态，如下面的代码示例中所示。  
  
 [!code-csharp[PowerMode#1](~/samples/snippets/csharp/VS_Snippets_Winforms/powermode/cs/form1.cs#1)]
 [!code-vb[PowerMode#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/powermode/vb/form1.vb#1)]  
  
 除了<xref:System.Windows.Forms.BatteryChargeStatus>枚举<xref:System.Windows.Forms.SystemInformation.PowerStatus%2A>属性还包含用于确定电池容量枚举 (<xref:System.Windows.Forms.PowerStatus.BatteryFullLifetime%2A>) 和电池电量百分比 (<xref:System.Windows.Forms.PowerStatus.BatteryLifePercent%2A>， <xref:System.Windows.Forms.PowerStatus.BatteryLifeRemaining%2A>)。  
  
 可以使用<xref:System.Windows.Forms.Application.SetSuspendState%2A>方法的<xref:System.Windows.Forms.Application>使计算机进入休眠状态或暂停模式。 如果`force`参数设置为`false`，操作系统将广播请求挂起的权限的所有应用程序的事件。 如果`disableWakeEvent`参数设置为`true`，操作系统将禁用唤醒的所有事件。  
  
 下面的代码示例演示如何使计算机进入休眠状态。  
  
 [!code-csharp[PowerMode#2](~/samples/snippets/csharp/VS_Snippets_Winforms/powermode/cs/form1.cs#2)]
 [!code-vb[PowerMode#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/powermode/vb/form1.vb#2)]  
  
## <a name="see-also"></a>请参阅
- <xref:Microsoft.Win32.SystemEvents.PowerModeChanged>
- <xref:System.Windows.Forms.SystemInformation.PowerStatus%2A>
- <xref:System.Windows.Forms.Application.SetSuspendState%2A>
- <xref:Microsoft.Win32.SystemEvents.SessionSwitch>
