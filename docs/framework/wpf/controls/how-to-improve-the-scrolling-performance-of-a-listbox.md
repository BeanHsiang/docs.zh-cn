---
title: 如何：提高 ListBox 的滚动性能
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ListBox control [WPF], reusing item containers
- ListBox control [WPF], improving scrolling performance
ms.assetid: 1e2bf8f3-c8ce-47f7-a400-a7fe11d1a848
ms.openlocfilehash: a9d1ca1d8ac2ef830984408f3052eb0ed0987c5d
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57364548"
---
# <a name="how-to-improve-the-scrolling-performance-of-a-listbox"></a>如何：提高 ListBox 的滚动性能
如果<xref:System.Windows.Controls.ListBox>包含多个项，当用户滚动时，用户界面响应可能会很慢<xref:System.Windows.Controls.ListBox>通过使用鼠标滚轮或拖动滚动条的滚动块。 您可以提高的性能<xref:System.Windows.Controls.ListBox>通过设置在用户滚动时`VirtualizingStackPanel.VirtualizationMode`附加属性设置为<xref:System.Windows.Controls.VirtualizationMode.Recycling?displayProperty=nameWithType>。  
  
## <a name="example"></a>示例  
  
## <a name="description"></a>描述  
下面的示例创建<xref:System.Windows.Controls.ListBox>，并设置`VirtualizingStackPanel.VirtualizationMode`附加属性设置为<xref:System.Windows.Controls.VirtualizationMode.Recycling?displayProperty=nameWithType>若要在滚动期间提高性能。  
  
## <a name="code"></a>代码  
 [!code-xaml[RecycleItemContainerShippets#VirtualizationMode](~/samples/snippets/csharp/VS_Snippets_Wpf/RecycleItemContainerShippets/CSharp/Window1.xaml#virtualizationmode)]  
  
 下面的示例显示了前面的示例使用的数据。  
  
 [!code-csharp[RecycleItemContainerShippets#ListBoxData](~/samples/snippets/csharp/VS_Snippets_Wpf/RecycleItemContainerShippets/CSharp/Window1.xaml.cs#listboxdata)]
 [!code-vb[RecycleItemContainerShippets#ListBoxData](~/samples/snippets/visualbasic/VS_Snippets_Wpf/RecycleItemContainerShippets/visualbasic/window1.xaml.vb#listboxdata)]
