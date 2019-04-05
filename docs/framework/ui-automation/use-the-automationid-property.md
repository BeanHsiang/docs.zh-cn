---
title: 使用 AutomationID 属性
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- AutomationId property
- UI Automation, AutomationId property
- properties, AutomationId
ms.assetid: a24e807b-d7c3-4e93-ac48-80094c4e1c90
ms.openlocfilehash: 88e703d6cee608676be541961614403cf34a53c7
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2019
ms.locfileid: "57674830"
---
# <a name="use-the-automationid-property"></a>使用 AutomationID 属性
> [!NOTE]
>  本文档适用于想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空间中定义的托管 <xref:System.Windows.Automation> 类的 .NET Framework 开发人员。 有关最新信息[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]，请参阅[Windows 自动化 API:UI 自动化](https://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 本主题包含一些方案和代码示例，这些方案和代码示例演示如何以及在何时能够使用 <xref:System.Windows.Automation.AutomationElement.AutomationIdProperty> 在 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 树中找到元素。  
  
 <xref:System.Windows.Automation.AutomationElement.AutomationIdProperty> 唯一地将 UI 自动化元素从其同级中标识出来。 有关与控件标识相关的属性标识符的详细信息，请参阅 [UI Automation Properties Overview](../../../docs/framework/ui-automation/ui-automation-properties-overview.md)。  
  
> [!NOTE]
>  <xref:System.Windows.Automation.AutomationElement.AutomationIdProperty> 不保证标识在整个树中的唯一性；它通常需要容器和范围信息才有用。 例如，一个应用程序可能包含具有多个顶级菜单项的菜单控件，而这些顶级菜单项又具有多个子菜单项。 这些二级菜单项通过常规架构（如“Item1”、“Item2”，依此类推）进行标识，允许对顶级菜单项中的子菜单项使用重复的标识符。  
  
## <a name="scenarios"></a>方案  
 已确定有三个主要的 UI 自动化客户端应用程序方案需要使用 <xref:System.Windows.Automation.AutomationElement.AutomationIdProperty> 才能在搜索元素时获得准确一致的结果。  
  
> [!NOTE]
>  控件视图中（除顶级应用程序窗口外）的所有 UI 自动化元素、派生自没有 ID 或 x:Uid 的<xref:System.Windows.Automation.AutomationElement.AutomationIdProperty> 控件的 UI 自动化元素以及派生自没有控件 ID 的 [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)] 控件的 UI 自动化元素都支持 [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)] 。  
  
#### <a name="use-a-unique-and-discoverable-automationid-to-locate-a-specific-element-in-the-ui-automation-tree"></a>使用唯一且可发现的 AutomationID 在 UI 自动化树中查找特定元素  
  
-   使用 [!INCLUDE[TLA#tla_uispy](../../../includes/tlasharptla-uispy-md.md)] 等工具来报告关注的 <xref:System.Windows.Automation.AutomationElement.AutomationIdProperty> 元素的 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 。 然后，可以将此值复制并粘贴到客户端应用程序（如测试脚本）中，以便随后进行自动化测试。 此方法减少并简化了在运行时标识和查找元素所需的代码。  
  
> [!CAUTION]
>  通常，你应当尝试只获取 <xref:System.Windows.Automation.AutomationElement.RootElement%2A>的直接子项。 对后代的搜索可能循环访问数百个甚至数千个元素，这可能导致堆栈溢出。 如果尝试在较低级别上获取特定元素，应该从应用程序窗口或者从较低级别的容器中开始搜索。  
  
 [!code-csharp[UIAAutomationID_snip#100](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAAutomationID_snip/CSharp/FindByAutomationID.xaml.cs#100)]
 [!code-vb[UIAAutomationID_snip#100](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAAutomationID_snip/VisualBasic/FindByAutomationID.xaml.vb#100)]  
  
#### <a name="use-a-persistent-path-to-return-to-a-previously-identified-automationelement"></a>使用持久的路径返回到之前标识的 AutomationElement  
  
-   客户端应用程序（从简单的测试脚本到强大的录制和播放实用程序）可能需要访问当前未实例化并因此不存在于 UI 自动化树中的元素（如打开文件对话框或菜单项）。 仅可以通过重现 （或"播放"） 一系列通过 UI 自动化属性，例如 AutomationID、 控件模式和事件侦听器使用的 UI 操作的特定实例化这些元素。
  
 [!code-csharp[UIAAutomationID_snip#UIAWorkerThread](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAAutomationID_snip/CSharp/FindByAutomationID.xaml.cs#uiaworkerthread)]
 [!code-vb[UIAAutomationID_snip#UIAWorkerThread](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAAutomationID_snip/VisualBasic/FindByAutomationID.xaml.vb#uiaworkerthread)]  
[!code-csharp[UIAAutomationID_snip#Playback](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAAutomationID_snip/CSharp/FindByAutomationID.xaml.cs#playback)]
[!code-vb[UIAAutomationID_snip#Playback](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAAutomationID_snip/VisualBasic/FindByAutomationID.xaml.vb#playback)]  
  
#### <a name="use-a-relative-path-to-return-to-a-previously-identified-automationelement"></a>使用相对路径返回到之前标识的 AutomationElement  
  
-   在某些情况下，由于只能保证 AutomationID 在同级项之间唯一，因此 UI 自动化树中的多个元素可能具有相同的 AutomationID 属性值。 对于这些情况，可以基于父项（必要情况下使用其祖父项）来唯一地标识元素。 例如，开发人员可能提供一个包含多个菜单项（其中每个菜单项又包含多个子菜单项）的菜单栏，其中的子项是用连续的 AutomationID（如“Item1”、“Item2”，依此类推）标识的。 然后，可以通过其 AutomationID 以及其父项（必要情况下使用其祖父项）的 AutomationID 来唯一地标识每个菜单项。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Automation.AutomationElement.AutomationIdProperty>
- [UI 自动化树概述](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)
- [基于属性条件查找 UI 自动化元素](../../../docs/framework/ui-automation/find-a-ui-automation-element-based-on-a-property-condition.md)
