---
title: 如何：演示图板启动后对其进行控制
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Storyboards [WPF], controlling after start
ms.assetid: 040f13f0-69f9-4ab5-be2b-079f4f80c7c0
ms.openlocfilehash: 98eba600f64c8b656e3597b429cc69766f398f7b
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57361052"
---
# <a name="how-to-control-a-storyboard-after-it-starts"></a>如何：演示图板启动后对其进行控制
此示例演示如何使用代码添加到控件<xref:System.Windows.Media.Animation.Storyboard>已开始后。 若要控制在情节提要[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]，使用<xref:System.Windows.Trigger>并<xref:System.Windows.TriggerAction>对象; 有关示例，请参阅[使用事件触发器来控制情节提要启动之后](how-to-use-event-triggers-to-control-a-storyboard-after-it-starts.md)。  
  
 若要启动情节提要，你可以使用其<xref:System.Windows.Media.Animation.Storyboard.Begin%2A>方法，将分发到的属性，它们进行动画处理，然后启动情节提要的情节提要的动画。  
  
 若要使可控制演示图板，应使用<xref:System.Windows.Media.Animation.Storyboard.Begin%2A>方法并指定**true**第二个参数。 然后可以使用情节提要的交互式方法来暂停、 恢复、 查找、 停止、 加快，或降低情节提要，或转到其填充期。 下面是演示图板的交互式方法的列表：  
  
-   <xref:System.Windows.Media.Animation.Storyboard.Pause%2A>：暂停情节提要。  
  
-   <xref:System.Windows.Media.Animation.Storyboard.Resume%2A>：恢复暂停的情节提要。  
  
-   <xref:System.Windows.Media.Animation.Storyboard.SetSpeedRatio%2A>：设置情节提要的交互速度。  
  
-   <xref:System.Windows.Media.Animation.Storyboard.Seek%2A>：查找情节提要的指定位置。  
  
-   <xref:System.Windows.Media.Animation.Storyboard.SeekAlignedToLastTick%2A>：查找到指定位置的情节提要。 与不同<xref:System.Windows.Media.Animation.Storyboard.Seek%2A>在下一时钟周期之前处理方法，此操作。  
  
-   <xref:System.Windows.Media.Animation.Storyboard.SkipToFill%2A>：如果有，请转到其填充期，情节提要。  
  
-   <xref:System.Windows.Media.Animation.Storyboard.Stop%2A>：停止情节提要。  
  
 在以下示例中，多个情节提要方法用于以交互方式控制情节提要。  
  
 **注意：** 若要控制使用触发器和情节提要的示例，请参阅[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]，请参阅[使用事件触发器来控制情节提要启动之后](how-to-use-event-triggers-to-control-a-storyboard-after-it-starts.md)。  
  
## <a name="example"></a>示例  
 [!code-csharp[timingbehaviors_procedural_snip#ControlStoryboardExampleUsingWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_procedural_snip/CSharp/ControlStoryboardExample.cs#controlstoryboardexampleusingwholepage)]
 [!code-vb[timingbehaviors_procedural_snip#ControlStoryboardExampleUsingWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_procedural_snip/visualbasic/controlstoryboardexample.vb#controlstoryboardexampleusingwholepage)]  
  
## <a name="see-also"></a>请参阅
- [在情节提要启动之后使用事件触发器来控制情节提要](how-to-use-event-triggers-to-control-a-storyboard-after-it-starts.md)
