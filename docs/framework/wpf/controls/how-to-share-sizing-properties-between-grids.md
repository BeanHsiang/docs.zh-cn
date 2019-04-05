---
title: 如何：在网格之间共享大小调整属性
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Grid control [WPF], sharing sizing data of columns
- sizing data in Grid controls [WPF]
- Grid control [WPF], sharing sizing data of rows
ms.assetid: a0535a6f-ff04-4b25-9912-7dd856e11044
ms.openlocfilehash: bd0f812ce9a15628bd0bddf3a88e898311f0a9d3
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57373122"
---
# <a name="how-to-share-sizing-properties-between-grids"></a>如何：在网格之间共享大小调整属性
此示例演示如何共享列的大小调整数据和行之间<xref:System.Windows.Controls.Grid>元素，以使大小调整保持一致。  
  
## <a name="example"></a>示例  
 下面的示例引入了两处<xref:System.Windows.Controls.Grid>元素作为父级的子元素<xref:System.Windows.Controls.DockPanel>。 <xref:System.Windows.Controls.Grid.IsSharedSizeScope%2A>附加属性的<xref:System.Windows.Controls.Grid>的父级上定义<xref:System.Windows.Controls.DockPanel>。  
  
 该示例通过使用两个操作的属性值<xref:System.Windows.Controls.Button>元素; 每个元素表示一个布尔属性值。 当<xref:System.Windows.Controls.Grid.IsSharedSizeScope%2A>属性值设置为`true`，每个列或行成员<xref:System.Windows.Controls.DefinitionBase.SharedSizeGroup%2A>共享大小调整信息，无论行或列的内容。  
  
 [!code-xaml[gridIssharedsizescopeProp#1](~/samples/snippets/csharp/VS_Snippets_Wpf/gridIssharedsizescopeProp/CSharp/Window1.xaml#1)]  
  
 ...  
  
 [!code-xaml[gridIssharedsizescopeProp#2](~/samples/snippets/csharp/VS_Snippets_Wpf/gridIssharedsizescopeProp/CSharp/Window1.xaml#2)]  
  
 下面的代码隐藏示例处理方法，该按钮<xref:System.Windows.Controls.Primitives.ButtonBase.Click>事件引发。 该示例将写入到这些方法调用的结果<xref:System.Windows.Controls.TextBlock>元素使用相关的 get 方法以输出新属性值作为字符串。  
  
 [!code-csharp[gridIssharedsizescopeProp#3](~/samples/snippets/csharp/VS_Snippets_Wpf/gridIssharedsizescopeProp/CSharp/Window1.xaml.cs#3)]
 [!code-vb[gridIssharedsizescopeProp#3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/gridIssharedsizescopeProp/VisualBasic/Window1.xaml.vb#3)]  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Controls.Grid>
- <xref:System.Windows.Controls.Grid.IsSharedSizeScope%2A>
- [面板概述](panels-overview.md)
