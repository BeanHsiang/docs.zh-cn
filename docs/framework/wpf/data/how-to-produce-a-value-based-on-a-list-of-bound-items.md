---
title: 如何：根据绑定项列表生成值
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data binding [WPF], MultiBinding
- Multibinding [WPF]
ms.assetid: b3d06378-b511-4181-95aa-316d60c9229b
ms.openlocfilehash: 77c832c1460749ced58e7a20af333c5ed9dd1555
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57368120"
---
# <a name="how-to-produce-a-value-based-on-a-list-of-bound-items"></a>如何：根据绑定项列表生成值
<xref:System.Windows.Data.MultiBinding> 可以将绑定目标属性绑定到的源属性列表，然后应用逻辑以生成使用给定的输入值。 此示例演示如何使用<xref:System.Windows.Data.MultiBinding>。  
  
## <a name="example"></a>示例  
 在下面的示例中，`NameListData` 引用包含 `firstName` 和 `lastName` 这两个属性的 `PersonName` 对象的集合。 下面的示例生成<xref:System.Windows.Controls.TextBlock>，显示的第一个和最后一个名称的人员的姓氏第一个。  
  
 [!code-xaml[MultiBinding#Resources1](~/samples/snippets/csharp/VS_Snippets_Wpf/MultiBinding/CSharp/Window1.xaml#resources1)]  
[!code-xaml[MultiBinding#Resources2](~/samples/snippets/csharp/VS_Snippets_Wpf/MultiBinding/CSharp/Window1.xaml#resources2)]  
[!code-xaml[MultiBinding#MultiBindingTextBox2](~/samples/snippets/csharp/VS_Snippets_Wpf/MultiBinding/CSharp/Window1.xaml#multibindingtextbox2)]  
[!code-xaml[MultiBinding#Window](~/samples/snippets/csharp/VS_Snippets_Wpf/MultiBinding/CSharp/Window1.xaml#window)]  
  
 为了了解如何生成姓氏在前的格式，我们来了解一下 `NameConverter` 的实现：  
  
 [!code-csharp[MultiBinding#3](~/samples/snippets/csharp/VS_Snippets_Wpf/MultiBinding/CSharp/NameConverter.cs#3)]
 [!code-vb[MultiBinding#3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MultiBinding/VisualBasic/NameConverter.vb#3)]  
  
 `NameConverter` 实现 <xref:System.Windows.Data.IMultiValueConverter> 接口。 `NameConverter` 从个别绑定获取值并将其存储在值对象数组中。 依据的顺序<xref:System.Windows.Data.Binding>元素出现在<xref:System.Windows.Data.MultiBinding>元素是在其中这些值存储在数组中的顺序。 值<xref:System.Windows.Data.MultiBinding.ConverterParameter%2A>属性引用的参数自变量的<xref:System.Windows.Data.MultiBinding.Converter%2A>方法，后者将执行一个开关参数以确定如何设置名称格式。  
  
## <a name="see-also"></a>请参阅
- [转换已绑定的数据](how-to-convert-bound-data.md)
- [数据绑定概述](data-binding-overview.md)
- [帮助主题](data-binding-how-to-topics.md)
