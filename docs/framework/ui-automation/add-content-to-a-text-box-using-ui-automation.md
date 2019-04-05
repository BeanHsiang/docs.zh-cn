---
title: 使用 UI 自动化向文本框添加内容
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- adding content to text boxes
- text boxes, adding content
- UI Automation, adding content to text boxes
ms.assetid: 8bdd1a73-1ecb-4a05-a891-a7827ebb767f
ms.openlocfilehash: af9450685452bb25d54a5cd28295092addf6bb20
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2019
ms.locfileid: "57680231"
---
# <a name="add-content-to-a-text-box-using-ui-automation"></a>使用 UI 自动化向文本框添加内容
> [!NOTE]
>  本文档适用于想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空间中定义的托管 <xref:System.Windows.Automation> 类的 .NET Framework 开发人员。 有关最新信息[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]，请参阅[Windows 自动化 API:UI 自动化](https://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 本主题包含代码示例演示如何使用[!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)]单行文本框中插入文本。 另一种方法提供的多行和多格式文本控件其中[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]不适用。 为方便比较，该示例还演示如何使用 Win32 方法来完成相同的结果。  
  
## <a name="example"></a>示例  
 以下示例步骤完成一系列目标应用程序中的文本控件。 每个文本控件进行测试以查看是否<xref:System.Windows.Automation.ValuePattern>对象可以从使用它获取<xref:System.Windows.Automation.AutomationElement.TryGetCurrentPattern%2A>方法。 如果文本控件不支持<xref:System.Windows.Automation.ValuePattern>，则<xref:System.Windows.Automation.ValuePattern.SetValue%2A>方法用于将是用户定义的字符串插入到文本控件。 否则为<xref:System.Windows.Forms.SendKeys.SendWait%2A?displayProperty=nameWithType>使用方法。  
  
 [!code-csharp[InsertText#InsertText](../../../samples/snippets/csharp/VS_Snippets_Wpf/InsertText/CSharp/Window1.xaml.cs#inserttext)]
 [!code-vb[InsertText#InsertText](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/InsertText/VisualBasic/Window1.xaml.vb#inserttext)]  
  
## <a name="see-also"></a>请参阅
- [TextPattern 插入文本示例](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms771478(v=vs.90))
