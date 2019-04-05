---
title: 使用 UI 自动化遍历文本
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- UI Automation, traversing text
- text, traversing
- traversing text
ms.assetid: 3ddb3b7b-1d6b-4dba-8678-5a68e868aadb
ms.openlocfilehash: 11f1b189d16d572ac1661e2b175f15ecae2f039f
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2019
ms.locfileid: "57678197"
---
# <a name="traverse-text-using-ui-automation"></a>使用 UI 自动化遍历文本
> [!NOTE]
>  本文档适用于想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空间中定义的托管 <xref:System.Windows.Automation> 类的 .NET Framework 开发人员。 有关最新信息[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]，请参阅[Windows 自动化 API:UI 自动化](https://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 本主题演示如何使用 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 按 <xref:System.Windows.Automation.Text.TextUnit> 增量来遍历文档的文本内容。  
  
## <a name="example"></a>示例  
 下面的代码示例演示如何遍历 UI 自动化文本提供程序的内容。 <xref:System.Windows.Automation.Text.TextPatternRange.Move%2A> 方法将移动 <xref:System.Windows.Automation.Text.TextPatternRangeEndpoint.Start> 和 <xref:System.Windows.Automation.Text.TextPatternRangeEndpoint.End> 的 <xref:System.Windows.Automation.Text.TextPatternRange>终结点。 此文本范围通常是一个退化范围，表示文本的插入点。  
  
> [!NOTE]
>  由于只有基于文本的嵌入对象被视为文本流的一部分，因此图像等嵌入对象将不会影响 `Move` 或其返回值。  
  
[!code-csharp[FindText#StartApp](../../../samples/snippets/csharp/VS_Snippets_Wpf/FindText/CSharp/SearchWindow.cs#startapp)]
[!code-vb[FindText#StartApp](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FindText/VisualBasic/SearchWindow.vb#startapp)]  
[!code-csharp[FindText#FindTextProvider](../../../samples/snippets/csharp/VS_Snippets_Wpf/FindText/CSharp/SearchWindow.cs#findtextprovider)]
[!code-vb[FindText#FindTextProvider](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FindText/VisualBasic/SearchWindow.vb#findtextprovider)]  
[!code-csharp[FindText#Navigate](../../../samples/snippets/csharp/VS_Snippets_Wpf/FindText/CSharp/SearchWindow.cs#navigate)]
[!code-vb[FindText#Navigate](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FindText/VisualBasic/SearchWindow.vb#navigate)]  
  
 如果控件不支持给定的 <xref:System.Windows.Automation.Text.TextUnit> ，则使用 <xref:System.Windows.Automation.Text.TextUnit> 的所有方法都将推迟到下一个支持的最大 <xref:System.Windows.Automation.Text.TextUnit> 。  
  
## <a name="see-also"></a>请参阅
- [UI 自动化 TextPattern 概述](../../../docs/framework/ui-automation/ui-automation-textpattern-overview.md)
- [使用 UI 自动化向文本框添加内容](../../../docs/framework/ui-automation/add-content-to-a-text-box-using-ui-automation.md)
- [使用 UI 自动化查找和突出显示文本](../../../docs/framework/ui-automation/find-and-highlight-text-using-ui-automation.md)
- [UI 自动化控件模式概述](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)
- [客户端的 UI 自动化控件模式](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)
