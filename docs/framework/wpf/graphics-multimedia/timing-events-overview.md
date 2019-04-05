---
title: 计时事件概述
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- timelines [WPF]
- timing events [WPF]
ms.assetid: 597e3280-0867-4359-a97b-5b2f4149e350
ms.openlocfilehash: 2ce4794c5f0abfc31ae9d6f813bcfd7a9d375611
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57379570"
---
# <a name="timing-events-overview"></a>计时事件概述
本主题介绍如何使用上可用的五个计时事件<xref:System.Windows.Media.Animation.Timeline>和<xref:System.Windows.Media.Animation.Clock>对象。  
  
## <a name="prerequisites"></a>系统必备  
 若要了解本主题，应了解如何创建和使用动画。 若要开始使用动画，请参阅[动画概述](animation-overview.md)。  
  
 有多个方法中的属性进行动画处理[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]:  
  
-   **使用情节提要对象**（标记和代码）：可以使用<xref:System.Windows.Media.Animation.Storyboard>对象排列和分发到一个或多个对象的动画。 有关示例，请参阅[使用情节提要对属性进行动画处理](how-to-animate-a-property-by-using-a-storyboard.md)。  
  
-   **使用本地动画**（仅代码）：您可以将应用<xref:System.Windows.Media.Animation.AnimationTimeline>直接对它们进行动画处理的属性的对象。 有关示例，请参阅[在不使用情节提要的情况下对属性进行动画处理](how-to-animate-a-property-without-using-a-storyboard.md)。  
  
-   **使用时钟**（仅代码）：您可以显式管理时钟创建并自行分发动画时钟。  有关示例，请参阅[通过使用 AnimationClock 对属性进行动画处理](how-to-animate-a-property-by-using-an-animationclock.md)。  
  
 因为您可以使用这些标记和代码中，此概述中的示例使用<xref:System.Windows.Media.Animation.Storyboard>对象。 但是，所介绍的概念适用于其他对属性进行动画处理的方法。  
  
### <a name="what-is-a-clock"></a>是什么时钟？  
 除了描述时间段外，时间线本身并无其他任何作用。 时间线的<xref:System.Windows.Media.Animation.Clock>对象执行实际工作： 它保留为时间线计时相关运行时状态。 在大多数情况下，比如使用情节提要时，会自动为时间线创建时钟。 此外可以创建<xref:System.Windows.Media.Animation.Clock>通过使用显式<xref:System.Windows.Media.Animation.Timeline.CreateClock%2A>方法。 有关详细信息<xref:System.Windows.Media.Animation.Clock>对象，请参阅[动画和计时系统概述](animation-and-timing-system-overview.md)。  
  
## <a name="why-use-events"></a>为什么使用事件？  
 除了一个例外（对齐到上一时钟周期的查找操作），所有交互式计时操作均为异步操作。 无法准确知道它们何时执行。 当存在其他代码依赖于计时操作时，可能会产生问题。 假设你希望停止对矩形进行动画处理的时间线。 在时间线停止后，更改矩形的颜色。  
  
 [!code-csharp[events_procedural#NeedForEventsFragment](~/samples/snippets/csharp/VS_Snippets_Wpf/events_procedural/CSharp/EventExample.cs#needforeventsfragment)]
 [!code-vb[events_procedural#NeedForEventsFragment](~/samples/snippets/visualbasic/VS_Snippets_Wpf/events_procedural/VisualBasic/EventExample.vb#needforeventsfragment)]  
  
 在上一示例中，第二行代码可能会在情节提要停止前执行。 这是因为停止操作是异步操作。 告知时间线或时钟停止将创建各种“停止请求”，但它仅在计时引擎的下一时钟周期才会处理。  
  
 若要在时间线完成后执行命令，请使用计时事件。 在下面的示例中，事件处理程序用于在情节提要停止播放后更改矩形的颜色。  
  
 [!code-csharp[events_procedural#RegisterForStoryboardCurrentStateInvalidatedEvent](~/samples/snippets/csharp/VS_Snippets_Wpf/events_procedural/CSharp/EventExample.cs#registerforstoryboardcurrentstateinvalidatedevent)]
 [!code-vb[events_procedural#RegisterForStoryboardCurrentStateInvalidatedEvent](~/samples/snippets/visualbasic/VS_Snippets_Wpf/events_procedural/VisualBasic/EventExample.vb#registerforstoryboardcurrentstateinvalidatedevent)]  
[!code-csharp[events_procedural#StoryboardCurrentStateInvalidatedEvent2](~/samples/snippets/csharp/VS_Snippets_Wpf/events_procedural/CSharp/EventExample.cs#storyboardcurrentstateinvalidatedevent2)]
[!code-vb[events_procedural#StoryboardCurrentStateInvalidatedEvent2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/events_procedural/VisualBasic/EventExample.vb#storyboardcurrentstateinvalidatedevent2)]  
  
 有关更完整的示例，请参阅[接收通知时在时钟状态更改](how-to-receive-notification-when-clock-state-changes.md)。  
  
## <a name="public-events"></a>公共事件  
 <xref:System.Windows.Media.Animation.Timeline>和<xref:System.Windows.Media.Animation.Clock>类都提供五种计时事件。 下表列出了这些事件及其触发条件。  
  
|事件|触发交互式操作|其他触发器|  
|-----------|--------------------------------------|--------------------|  
|**Completed**|跳过以填充|时钟完成。|  
|**CurrentGlobalSpeedInvalidated**|暂停、恢复、查找、设置速度比、跳过以填充、停止|时钟反转、加速、启动或停止。|  
|**CurrentStateInvalidated**|开始、跳过以填充、停止|时钟开始、停止或填充。|  
|**CurrentTimeInvalidated**|开始、查找、跳过以填充、停止|时钟前进。|  
|**RemoveRequested**|删除||  
  
## <a name="ticking-and-event-consolidation"></a>时钟周期和事件合并  
 当您设置中的对象有动画效果[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]，它是管理动画的计时引擎。 计时引擎跟踪时间进度，并计算每个动画的状态。 它一秒内进行多次计算。 这些计算过程称为“时钟周期”。  
  
 尽管时钟周期频繁发生，但是不同时钟周期之间可能会很多操作。 例如，时间线可能会停止、启动、再次停止，在这种情况下其当前状态将更改三次。 从理论上讲，在一个时钟周期内，可以多次引发事件；但是，计时引擎会合并事件，因此每个事件在每个时钟周期内只能引发一次。  
  
## <a name="registering-for-events"></a>注册事件  
 可以通过两种方法注册计时事件：使用时间线或使用从时间线创建的时钟进行注册。 直接使用时钟注册事件相当简单，不过该方法只能在代码中执行。 可以在标记或代码中使用时间线注册事件。 下一节介绍如何使用时间线注册时钟事件。  
  
<a name="registeringforclockeventswithatimeline"></a>   
## <a name="registering-for-clock-events-with-a-timeline"></a>使用时间线注册时钟事件  
 尽管时间线<xref:System.Windows.Media.Animation.Timeline.Completed>， <xref:System.Windows.Media.Animation.Timeline.CurrentGlobalSpeedInvalidated>， <xref:System.Windows.Media.Animation.Timeline.CurrentStateInvalidated>， <xref:System.Windows.Media.Animation.Timeline.CurrentTimeInvalidated>，并<xref:System.Windows.Media.Animation.Timeline.RemoveRequested>似乎是关联时间线，注册为这些事件实际上将相关联的事件处理程序与事件<xref:System.Windows.Media.Animation.Clock>创建针对时间线。  
  
 当你注册<xref:System.Windows.Media.Animation.Timeline.Completed>时间线上的事件，例如，您实际上在告诉系统注册为<xref:System.Windows.Media.Animation.Clock.Completed>事件的时间线创建每个时钟。 在代码中，您必须注册此事件之前<xref:System.Windows.Media.Animation.Clock>创建为此时间线; 否则，不会收到通知。 发生这种情况中自动[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]; 在之前的事件，分析器自动注册<xref:System.Windows.Media.Animation.Clock>创建。  
  
## <a name="see-also"></a>请参阅
- [动画和计时系统概述](animation-and-timing-system-overview.md)
- [动画概述](animation-overview.md)
- [计时行为概述](timing-behaviors-overview.md)
