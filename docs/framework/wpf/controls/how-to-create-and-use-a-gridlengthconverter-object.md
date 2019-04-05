---
title: 如何：创建和使用 GridLengthConverter 对象
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Grid control [WPF], creating [WPF], GridLengthConverter objects
ms.assetid: 5ab75911-e36a-4825-80e4-081c57e8e182
ms.openlocfilehash: 0455d91eff820e5c087af20207ece1313f6f3a39
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57352251"
---
# <a name="how-to-create-and-use-a-gridlengthconverter-object"></a>如何：创建和使用 GridLengthConverter 对象
## <a name="example"></a>示例  
 下面的示例演示如何创建和使用的实例<xref:System.Windows.GridLengthConverter>。 该示例定义一个名为的自定义方法`changeCol`，哪些阶段<xref:System.Windows.Controls.ListBoxItem>到<xref:System.Windows.GridLengthConverter>用于将转换<xref:System.Windows.Controls.ContentControl.Content%2A>的<xref:System.Windows.Controls.ListBoxItem>的实例<xref:System.Windows.GridLength>。 转换后的值然后返回作为值传递<xref:System.Windows.Controls.ColumnDefinition.Width%2A>属性的<xref:System.Windows.Controls.ColumnDefinition>元素。  
  
 该示例还定义第二个自定义方法，称为`changeColVal`。 此自定义方法将转换<xref:System.Windows.Controls.Primitives.RangeBase.Value%2A>的<xref:System.Windows.Controls.Slider>到<xref:System.String>，然后将值改回<xref:System.Windows.Controls.ColumnDefinition>作为<xref:System.Windows.Controls.ColumnDefinition.Width%2A>的元素。  
  
 请注意，单独[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]文件定义的内容<xref:System.Windows.Controls.ListBoxItem>。  
  
 [!code-csharp[gridlengthConverterGrid#1](~/samples/snippets/csharp/VS_Snippets_Wpf/gridlengthConverterGrid/CSharp/Window1.xaml.cs#1)]
 [!code-vb[gridlengthConverterGrid#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/gridlengthConverterGrid/VisualBasic/Window1.xaml.vb#1)]  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.GridLengthConverter>
- <xref:System.Windows.GridLength>
