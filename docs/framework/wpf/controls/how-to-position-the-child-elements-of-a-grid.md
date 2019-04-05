---
title: 如何：定位网格的子元素
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Grid control [WPF], positioning child elements
ms.assetid: 27b3ba9b-ad32-44e2-bcab-a79d573a463c
ms.openlocfilehash: 90115bc6192a33f4c27eaa75ebfe6a7c9d1458e5
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57369170"
---
# <a name="how-to-position-the-child-elements-of-a-grid"></a>如何：定位网格的子元素
此示例演示如何使用 get 和 set 方法上定义的<xref:System.Windows.Controls.Grid>来定位子元素。  
  
## <a name="example"></a>示例  
 下面的示例定义一个父级<xref:System.Windows.Controls.Grid>元素 (`grid1`)，有三个列和三个行。 子<xref:System.Windows.Shapes.Rectangle>元素 (`rect1`) 添加到<xref:System.Windows.Controls.Grid>中的列位置零，行位置零。 <xref:System.Windows.Controls.Button> 元素表示方法可以调用以进行重新定位<xref:System.Windows.Shapes.Rectangle>元素内的<xref:System.Windows.Controls.Grid>。 当用户单击按钮时，激活相关的方法。  
  
 [!code-xaml[gridGetSetMethods](~/samples/snippets/csharp/VS_Snippets_Wpf/gridGetSetMethods/CSharp/Window1.xaml)]  
  
 下面的代码隐藏示例处理方法，该按钮<xref:System.Windows.Controls.Primitives.ButtonBase.Click>事件引发。 该示例将写入到这些方法调用<xref:System.Windows.Controls.TextBlock>元素使用相关的 get 方法以输出新属性值作为字符串。  
  
 [!code-csharp[gridGetSetMethods#2](~/samples/snippets/csharp/VS_Snippets_Wpf/gridGetSetMethods/CSharp/Window1.xaml.cs#2)]
 [!code-vb[gridGetSetMethods#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/gridGetSetMethods/VisualBasic/Window1.xaml.vb#2)]  
 下面是最终的结果 ！
 
 ![屏幕快照描述了具有两个列的 WPF 用户界面、 右侧有一个 3x3 网格和左侧具有按钮的网格行和列之间移动一个有色的矩形](././media/grid-methods-sample.png) 
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Controls.Grid>
- [面板概述](panels-overview.md)
