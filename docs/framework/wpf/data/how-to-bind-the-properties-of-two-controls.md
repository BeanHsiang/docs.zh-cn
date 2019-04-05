---
title: 如何：绑定两个控件的属性
ms.date: 03/30/2017
helpviewer_keywords:
- data binding [WPF], binding properties of two controls
- binding properties of two controls [WPF]
- controls [WPF], binding properties of
ms.assetid: 06318fac-6afd-4c7d-a277-6d7ef50f47bc
ms.openlocfilehash: f3355969d0f12f0f3ed9b49bdb7efa6913c5e4c4
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57372095"
---
# <a name="how-to-bind-the-properties-of-two-controls"></a>如何：绑定两个控件的属性
此示例演示如何使用 <xref:System.Windows.Data.Binding.ElementName%2A> 属性将一个实例化控件的属性绑定到另一个。  
  
## <a name="example"></a>示例  
 下面的示例演示如何将 <xref:System.Windows.Controls.Canvas> 的 <xref:System.Windows.Controls.Panel.Background%2A> 属性绑定到<xref:System.Windows.Controls.ComboBox> 的 <xref:System.Windows.Controls.Primitives.Selector.SelectedItem%2A>.<xref:System.Windows.Controls.ContentControl.Content%2A> 属性： 属性的<xref:System.Windows.Controls.ComboBox>:  
  
 [!code-xaml[BindDptoDp#1](~/samples/snippets/csharp/VS_Snippets_Wpf/BindDPtoDP/CS/Window1.xaml#1)]  
  
 当此示例呈现时，应如下所示：  
  
 ![具有绿色背景的画布](./media/databindingbindingdpssample.PNG "DataBindingBindingDPsSample")  
  
 **注意** 绑定目标属性（在此示例中为 <xref:System.Windows.Controls.Panel.Background%2A> 属性）必须是依赖项属性。 有关详细信息，请参阅[数据绑定概述](data-binding-overview.md)。  
  
## <a name="see-also"></a>请参阅
- [指定绑定源](how-to-specify-the-binding-source.md)
- [帮助主题](data-binding-how-to-topics.md)
