---
title: 如何：实现属性更改通知
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- notifications of change [WPF]
- data binding [WPF], property change notifications
- change notifications [WPF]
- properties [WPF], change notifications
ms.assetid: 30b59d9e-8c3a-4349-aa82-4be837e841cf
ms.openlocfilehash: 93a291b6dd35f9cc13c3c6f88aca5dc376b8bc1b
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57352745"
---
# <a name="how-to-implement-property-change-notification"></a>如何：实现属性更改通知
若要支持 <xref:System.Windows.Data.BindingMode.OneWay> 或 <xref:System.Windows.Data.BindingMode.TwoWay> 绑定，从而使你的绑定目标属性自动反映绑定源的动态更改 （例如，当用户编辑表单时自动更新预览面板），你的类需要提供相应的属性更改通知。 此示例演示如何创建一个类以实现<xref:System.ComponentModel.INotifyPropertyChanged>。  
  
## <a name="example"></a>示例  
 若要实现 <xref:System.ComponentModel.INotifyPropertyChanged>，则需要声明 <xref:System.ComponentModel.INotifyPropertyChanged.PropertyChanged> 事件并创建 `OnPropertyChanged` 方法。 然后，对于每个需要更改通知的属性，只要属性更新就调用 `OnPropertyChanged`。  
  
 [!code-csharp[SimpleBinding#PersonClass](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleBinding/CSharp/Person.cs#personclass)]
 [!code-vb[SimpleBinding#PersonClass](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleBinding/VisualBasic/Person.vb#personclass)]  
  
 若要查看有关如何使用 `Person` 类来支持 <xref:System.Windows.Data.BindingMode.TwoWay> 绑定的示例，请参阅[控制文本框文本更新源的时间](how-to-control-when-the-textbox-text-updates-the-source.md)。  
  
## <a name="see-also"></a>请参阅
- [绑定源概述](binding-sources-overview.md)
- [数据绑定概述](data-binding-overview.md)
- [帮助主题](data-binding-how-to-topics.md)
