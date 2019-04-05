---
title: 使用 UI 自动化调用控件
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- invoking controls
- UI Automation, invoking controls
- controls, invoking
ms.assetid: 5ee2de3f-256c-43ec-b64c-62ace91f9983
ms.openlocfilehash: 455811b1cf5da6c71225b2c3aaf25d213b3170b1
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2019
ms.locfileid: "57677248"
---
# <a name="invoke-a-control-using-ui-automation"></a>使用 UI 自动化调用控件
> [!NOTE]
>  本文档适用于想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空间中定义的托管 <xref:System.Windows.Automation> 类的 .NET Framework 开发人员。 有关最新信息[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]，请参阅[Windows 自动化 API:UI 自动化](https://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 本主题演示如何执行以下任务：  
  
-   通过遍历目标应用程序 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 树的控件视图，查找与特定属性条件相匹配的控件。  
  
-   为每个控件创建 <xref:System.Windows.Automation.AutomationElement> 。  
  
-   从发现的任何支持 <xref:System.Windows.Automation.InvokePattern> 控件模式的 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 元素中获取 <xref:System.Windows.Automation.InvokePattern> 对象。  
  
-   使用 <xref:System.Windows.Automation.InvokePattern.Invoke%2A> 以从客户端事件处理程序调用该控件。  
  
## <a name="example"></a>示例  
 此示例使用 <xref:System.Windows.Automation.AutomationElement.TryGetCurrentPattern%2A> 类的 <xref:System.Windows.Automation.AutomationElement> 方法来生成 <xref:System.Windows.Automation.InvokePattern> 对象，并通过使用 <xref:System.Windows.Automation.InvokePattern.Invoke%2A> 方法调用控件。  
  
 [!code-csharp[InvokePatternApp#1100](../../../samples/snippets/csharp/VS_Snippets_Wpf/InvokePatternApp/CSharp/InvokePatternApp.cs#1100)]
 [!code-vb[InvokePatternApp#1100](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/InvokePatternApp/VisualBasic/Client.vb#1100)]  
[!code-csharp[InvokePatternApp#1102](../../../samples/snippets/csharp/VS_Snippets_Wpf/InvokePatternApp/CSharp/InvokePatternApp.cs#1102)]
[!code-vb[InvokePatternApp#1102](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/InvokePatternApp/VisualBasic/Client.vb#1102)]  
  
## <a name="see-also"></a>请参阅
- [InvokePattern 和 ExpandCollapsePattern，TogglePattern 示例](https://github.com/Microsoft/WPF-Samples/tree/master/Accessibility/InvokePattern)
