---
title: 如何：实现 PriorityBinding
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data binding [WPF], PriorityBinding class
ms.assetid: d63b65ab-b3e9-4322-9aa8-1450f8d89532
ms.openlocfilehash: cf21041a7f3d5b75803378cf05768ee6f1008fdd
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57354591"
---
# <a name="how-to-implement-prioritybinding"></a>如何：实现 PriorityBinding
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中 <xref:System.Windows.Data.PriorityBinding> 的工作方式是指定一个绑定列表。 列表中的绑定按优先级从高到低排序。 对最高优先级绑定进行处理时，如果成功返回一个值，就不再需要处理列表中的其他绑定。 在最高优先级绑定需要长时间计算的情况下，则会使用已成功返回值的下一个优先级最高的绑定，直到优先级更高的绑定成功返回值为止。  
  
## <a name="example"></a>示例  
 为了演示 <xref:System.Windows.Data.PriorityBinding> 的工作方式，我们创建了 `AsyncDataSource` 对象，该对象具有三个属性：`FastDP`、`SlowerDP` 和 `SlowestDP`。  
  
 `FastDP` 的 Get 访问器返回数据成员 `_fastDP` 的值。  
  
 `SlowerDP` 的 Get 访问器等待 3 秒后返回数据成员 `_slowerDP` 的值。  
  
 `SlowestDP` 的 Get 访问器等待 5 秒后返回数据成员 `_slowestDP` 的值。  
  
> [!NOTE]
>  此示例仅供演示。 [!INCLUDE[TLA#tla_net](../../../../includes/tlasharptla-net-md.md)] 准则不建议将比字段设置更慢的操作定义为属性。 有关详细信息，请参阅[选择属性和方法](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms229054(v=vs.100))。  
  
 [!code-csharp[PriorityBinding#1](~/samples/snippets/csharp/VS_Snippets_Wpf/PriorityBinding/CSharp/Window1.xaml.cs#1)]
 [!code-vb[PriorityBinding#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PriorityBinding/VisualBasic/AsyncDataSource.vb#1)]  
  
 <xref:System.Windows.Controls.TextBlock.Text%2A> 属性使用 <xref:System.Windows.Data.PriorityBinding> 绑定到上述 `AsyncDS`:  
  
 [!code-xaml[PriorityBinding#2](~/samples/snippets/csharp/VS_Snippets_Wpf/PriorityBinding/CSharp/Window1.xaml#2)]  
  
 绑定引擎在处理 <xref:System.Windows.Data.Binding> 对象时，会从已绑定到 `SlowestDP` 属性的第一个 <xref:System.Windows.Data.Binding> 开始。 处理此 <xref:System.Windows.Data.Binding> 时并未成功返回值，因为它正处于 5 秒的睡眠状态，因此会开始处理下一个 <xref:System.Windows.Data.Binding> 元素。 该 <xref:System.Windows.Data.Binding> 也没有成功返回值，因为它正处于 3 秒的睡眠状态。 绑定引擎随后会转至下一个 <xref:System.Windows.Data.Binding> 元素，该元素已绑定到 `FastDP` 属性。 该 <xref:System.Windows.Data.Binding> 会返回值“Fast Value”。 于是 <xref:System.Windows.Controls.TextBlock> 会显示值“Fast Value”。  
  
 3 秒后，`SlowerDP` 属性返回了值“Slower Value”。 于是 <xref:System.Windows.Controls.TextBlock> 会显示值“Slower Value”。  
  
 5 秒后，`SlowestDP` 属性返回了值“Slowest Value”。 该绑定第一个列出，因此具有最高优先级。 于是 <xref:System.Windows.Controls.TextBlock> 会显示值“Slowest Value”。  
  
 请参阅 <xref:System.Windows.Data.PriorityBinding>，了解“何为成功的绑定返回值” 相关信息。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Data.Binding.IsAsync%2A?displayProperty=nameWithType>
- [数据绑定概述](data-binding-overview.md)
- [帮助主题](data-binding-how-to-topics.md)
