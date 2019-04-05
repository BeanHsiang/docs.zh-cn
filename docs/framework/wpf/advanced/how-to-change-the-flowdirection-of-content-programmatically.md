---
title: 如何：以编程方式更改内容的 FlowDirection
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- FlowDirection property [WPF], changing programmatically
- documents [WPF], changing FlowDirection property programmatically
ms.assetid: 02f5a8ba-f8c0-4e5a-84b9-4c5bf12922a2
ms.openlocfilehash: ec159ed0efce8b5514788331e8715a55e7a8a638
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57359323"
---
# <a name="how-to-change-the-flowdirection-of-content-programmatically"></a>如何：以编程方式更改内容的 FlowDirection
此示例演示如何以编程方式更改<xref:System.Windows.FrameworkElement.FlowDirection%2A>属性的<xref:System.Windows.Controls.FlowDocumentReader>。  
  
## <a name="example"></a>示例  
 两个<xref:System.Windows.Controls.Button>元素创建的每个资源表示的可能值之一<xref:System.Windows.FlowDirection>。 单击按钮时，关联的属性值应用于的内容<xref:System.Windows.Controls.FlowDocumentReader>名为`tf1`。  属性值也写入到<xref:System.Windows.Controls.TextBlock>名为`txt1`。  
  
 [!code-xaml[FlowDirectionSnippets#_FlowDirectionXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowDirectionSnippets/CSharp/Window1.xaml#_flowdirectionxaml)]  
  
## <a name="example"></a>示例  
 与上述按钮单击事件处理中C#代码隐藏文件。  
  
 [!code-csharp[FlowDirectionSnippets#_FlowDirection](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowDirectionSnippets/CSharp/Window1.xaml.cs#_flowdirection)]
 [!code-vb[FlowDirectionSnippets#_FlowDirection](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDirectionSnippets/VisualBasic/Window1.xaml.vb#_flowdirection)]
