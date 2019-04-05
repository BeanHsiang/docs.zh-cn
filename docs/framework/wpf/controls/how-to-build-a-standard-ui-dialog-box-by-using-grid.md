---
title: 如何：使用 Grid 来构建标准的 UI 对话框
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- dialog boxes [WPF], creating
- Grid control [WPF], creating [WPF], dialog box
ms.assetid: d6ac3d51-844b-4d29-96d8-81a696a7b960
ms.openlocfilehash: 57edaa173b85bc06c6859b08d3edec281e1b8942
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57372850"
---
# <a name="how-to-build-a-standard-ui-dialog-box-by-using-grid"></a>如何：使用 Grid 来构建标准的 UI 对话框
此示例演示如何创建标准[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]对话框中，通过使用<xref:System.Windows.Controls.Grid>元素。  
  
## <a name="example"></a>示例  
 下面的示例创建像那样的对话框**运行**中的对话框[!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)]操作系统。  
  
 此示例将创建<xref:System.Windows.Controls.Grid>，并使用<xref:System.Windows.Controls.ColumnDefinition>和<xref:System.Windows.Controls.RowDefinition>类来定义五个列和四个行。  
  
 该示例然后添加并将置于<xref:System.Windows.Controls.Image>， `RunIcon.png`，用于表示在对话框中找到的映像。 图像被置于中第一列和行的<xref:System.Windows.Controls.Grid>（左上角）。  
  
 接下来，该示例将添加<xref:System.Windows.Controls.TextBlock>跨越第一行的剩余列的第一列的元素。 它将添加另一个<xref:System.Windows.Controls.TextBlock>元素来表示第一列中的第二个行**打开**文本框。 一个<xref:System.Windows.Controls.TextBlock>如下所示，它表示数据输入区域。  
  
 最后，该示例将添加三个<xref:System.Windows.Controls.Button>针对最后一行的元素，后者表示**确定**，**取消**，并且**浏览**事件。  
  
 [!code-csharp[GridRunDialog#1](~/samples/snippets/csharp/VS_Snippets_Wpf/GridRunDialog/CSharp/window1.xaml.cs#1)]
 [!code-vb[GridRunDialog#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/GridRunDialog/VisualBasic/grid_vb.vb#1)]  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Controls.Grid>
- <xref:System.Windows.GridUnitType>
- [面板概述](panels-overview.md)
- [帮助主题](grid-how-to-topics.md)
