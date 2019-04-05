---
title: 基于属性条件查找 UI 自动化元素
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- elements, finding by property conditions
- UI Automation, finding elements by property conditions
ms.assetid: 3acaee5a-6ce8-4c3e-81c8-67e59eb74477
ms.openlocfilehash: 83d3a36d08463cedf46c176208625e76907db2d8
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2019
ms.locfileid: "57675103"
---
# <a name="find-a-ui-automation-element-based-on-a-property-condition"></a>基于属性条件查找 UI 自动化元素
> [!NOTE]
>  本文档适用于想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空间中定义的托管 <xref:System.Windows.Automation> 类的 .NET Framework 开发人员。 有关最新信息[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]，请参阅[Windows 自动化 API:UI 自动化](https://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 本主题包含代码示例演示如何查找中的某个元素[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]基于树的特定属性或属性。  
  
## <a name="example"></a>示例  
 在以下示例中，一系列属性条件，用于标识感兴趣的某些元素 （或元素） 中指定<xref:System.Windows.Automation.AutomationElement>树。 然后执行搜索的所有匹配的元素<xref:System.Windows.Automation.AutomationElement.FindAll%2A>方法，其中包含一系列<xref:System.Windows.Automation.AndCondition>布尔运算以限制匹配的元素数。  
  
> [!NOTE]
>  从搜索时<xref:System.Windows.Automation.AutomationElement.RootElement%2A>，应尝试仅获取直接子级。 对后代的搜索可能循环访问数百个甚至数千个元素，从而可能会导致堆栈溢出。 如果尝试在较低级别上获取特定元素，应该从应用程序窗口或者从较低级别的容器中开始搜索。  
  
 [!code-csharp[InvokePatternApp#1100](../../../samples/snippets/csharp/VS_Snippets_Wpf/InvokePatternApp/CSharp/InvokePatternApp.cs#1100)]
 [!code-vb[InvokePatternApp#1100](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/InvokePatternApp/VisualBasic/Client.vb#1100)]  
  
## <a name="see-also"></a>请参阅
- [InvokePattern 和 ExpandCollapsePattern 菜单项示例](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms771636(v=vs.90))
- [获取 UI 自动化元素](../../../docs/framework/ui-automation/obtaining-ui-automation-elements.md)
- [使用 AutomationID 属性](../../../docs/framework/ui-automation/use-the-automationid-property.md)
