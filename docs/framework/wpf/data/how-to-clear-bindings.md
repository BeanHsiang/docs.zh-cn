---
title: 如何：清除绑定
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- bindings [WPF], clearing
- clearing bindings [WPF]
- data binding [WPF], clearing bindings
ms.assetid: 73962a93-32a9-4bcd-9240-bcfbb239093a
ms.openlocfilehash: 8bffc34864a2bf929bcbed09f16eac282e1ba2a5
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57360210"
---
# <a name="how-to-clear-bindings"></a>如何：清除绑定
此示例演示如何从对象中清除绑定。  
  
## <a name="example"></a>示例  
 若要从对象中某一个属性清除绑定，可以调用 <xref:System.Windows.Data.BindingOperations.ClearBinding%2A>，如以下示例所示。 以下示例将从 mytext（<xref:System.Windows.Controls.TextBlock> 对象）的 <xref:System.Windows.Controls.TextBlock.TextProperty> 删除绑定。  
  
 [!code-csharp[CodeOnlyBinding#ClearBinding](~/samples/snippets/csharp/VS_Snippets_Wpf/CodeOnlyBinding/CSharp/binding.cs#clearbinding)]
 [!code-vb[CodeOnlyBinding#ClearBinding](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CodeOnlyBinding/VisualBasic/App.vb#clearbinding)]  
  
 清除绑定会移除绑定，这样依赖属性的值会更改为过去尚未绑定时的值。 此值可以是默认值、继承值或来自数据模板绑定的值。  
  
 若要清除一个对象的所有可操作属性的绑定，请使用 <xref:System.Windows.Data.BindingOperations.ClearAllBindings%2A>。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Data.BindingOperations>
- [数据绑定概述](data-binding-overview.md)
- [帮助主题](data-binding-how-to-topics.md)
