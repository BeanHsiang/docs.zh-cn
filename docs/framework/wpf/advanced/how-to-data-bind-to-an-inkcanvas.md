---
title: 如何：将数据绑定到 InkCanvas
ms.date: 03/30/2017
helpviewer_keywords:
- InkCanvas [WPF], binding data to
- binding data [WPF], to InkCanvas
ms.assetid: 8d6b4d9e-ea7f-4412-ba83-3feccec5a515
ms.openlocfilehash: 5d3fc0ed7b6176d7bc68bf20af42c311b5563908
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57372940"
---
# <a name="how-to-data-bind-to-an-inkcanvas"></a>如何：将数据绑定到 InkCanvas
## <a name="example"></a>示例  
 下面的示例演示如何将绑定<xref:System.Windows.Controls.InkCanvas.Strokes%2A>的属性<xref:System.Windows.Controls.InkCanvas>到另一个<xref:System.Windows.Controls.InkCanvas>。  
  
 [!code-xaml[InkCanvasBindingSnippet#2](~/samples/snippets/csharp/VS_Snippets_Wpf/InkCanvasBindingSnippet/CS/Window2.xaml#2)]  
  
 下面的示例演示如何将绑定<xref:System.Windows.Controls.InkCanvas.DefaultDrawingAttributes%2A>到数据源的属性。  
  
 [!code-xaml[InkCanvasBindingSnippet#3](~/samples/snippets/csharp/VS_Snippets_Wpf/InkCanvasBindingSnippet/CS/Window2.xaml#3)]  
[!code-xaml[InkCanvasBindingSnippet#4](~/samples/snippets/csharp/VS_Snippets_Wpf/InkCanvasBindingSnippet/CS/Window2.xaml#4)]  
  
 下面的示例声明了两个<xref:System.Windows.Controls.InkCanvas>XAML 中的对象和它们和其他数据源之间建立数据绑定。  第一个<xref:System.Windows.Controls.InkCanvas>，称为`ic`，绑定到两个数据源。  <xref:System.Windows.Controls.InkCanvas.EditingMode%2A>并<xref:System.Windows.Controls.InkCanvas.DefaultDrawingAttributes%2A>上的属性`ic`绑定到<xref:System.Windows.Controls.ListBox>又绑定到 XAML 中定义的数组的对象。  <xref:System.Windows.Controls.InkCanvas.EditingMode%2A>， <xref:System.Windows.Controls.InkCanvas.DefaultDrawingAttributes%2A>，并<xref:System.Windows.Controls.InkCanvas.Strokes%2A>的第二个属性<xref:System.Windows.Controls.InkCanvas>绑定到第一个<xref:System.Windows.Controls.InkCanvas>， `ic`。  
  
 [!code-xaml[InkCanvasBindingSnippet#1](~/samples/snippets/csharp/VS_Snippets_Wpf/InkCanvasBindingSnippet/CS/Window1.xaml#1)]
