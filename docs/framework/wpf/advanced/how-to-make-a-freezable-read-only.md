---
title: 如何：使 Freezable 成为只读
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Freezable objects [WPF], making read-only
ms.assetid: 6c544b7d-d3c9-4736-aa90-4b8728234ccb
ms.openlocfilehash: 874724584b44c17ff6c01331295cfa1a60978d54
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57360342"
---
# <a name="how-to-make-a-freezable-read-only"></a>如何：使 Freezable 成为只读
此示例演示如何使<xref:System.Windows.Freezable>只读通过调用其<xref:System.Windows.Freezable.Freeze%2A>方法。  
  
 不能冻结<xref:System.Windows.Freezable>对象是否满足以下条件之一`true`有关对象：  
  
-   它具有经过动画处理或数据绑定属性。  
  
-   它具有由动态资源设置的属性。 有关动态资源的详细信息，请参阅[XAML 资源](xaml-resources.md)。  
  
-   它包含<xref:System.Windows.Freezable>不能冻结的子对象。  
  
 如果这些条件`false`为你<xref:System.Windows.Freezable>对象，并且您不想要对其进行修改，请考虑冻结它来获得性能优势。  
  
## <a name="example"></a>示例  
 下面的示例冻结<xref:System.Windows.Media.SolidColorBrush>，这是一种类型的<xref:System.Windows.Freezable>对象。  
  
 [!code-csharp[freezablesample_procedural#FreezeExample1](~/samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#freezeexample1)]
 [!code-vb[freezablesample_procedural#FreezeExample1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#freezeexample1)]  
  
 有关详细信息<xref:System.Windows.Freezable>对象，请参阅[Freezable 对象概述](freezable-objects-overview.md)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Freezable>
- <xref:System.Windows.Freezable.CanFreeze%2A>
- <xref:System.Windows.Freezable.Freeze%2A>
- [Freezable 对象概述](freezable-objects-overview.md)
- [帮助主题](base-elements-how-to-topics.md)
