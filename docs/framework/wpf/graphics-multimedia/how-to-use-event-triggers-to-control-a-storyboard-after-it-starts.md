---
title: 如何：在演示图板启动之后使用事件触发器来控制演示图板
ms.date: 03/30/2017
helpviewer_keywords:
- triggers [WPF], controlling Storyboards
- event triggers [WPF], controlling Storyboards
- Storyboards [WPF], controlling after start
ms.assetid: 3b115594-6a93-4972-b24d-61aa16f1c15f
ms.openlocfilehash: d0b25f56caf3f25b6e649c05ecf1cbe50046dd93
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57362365"
---
# <a name="how-to-use-event-triggers-to-control-a-storyboard-after-it-starts"></a>如何：在演示图板启动之后使用事件触发器来控制演示图板
此示例演示如何控制<xref:System.Windows.Media.Animation.Storyboard>启动后对它。 若要启动<xref:System.Windows.Media.Animation.Storyboard>通过使用[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]，使用<xref:System.Windows.Media.Animation.BeginStoryboard>，这样可以将分发到的对象和属性，它们进行动画处理，然后启动情节提要的动画。 如果您为提供<xref:System.Windows.Media.Animation.BeginStoryboard>通过指定的名称及其<xref:System.Windows.Media.Animation.BeginStoryboard.Name%2A>属性，您使它可控制情节提要。 然后您可以以交互方式控制情节提要启动后。  
  
 使用以下情节提要操作一起使用<xref:System.Windows.EventTrigger>对象来控制情节提要。  
  
-   <xref:System.Windows.Media.Animation.PauseStoryboard>：暂停情节提要。  
  
-   <xref:System.Windows.Media.Animation.ResumeStoryboard>：恢复暂停的情节提要。  
  
-   <xref:System.Windows.Media.Animation.SetStoryboardSpeedRatio>：更改情节提要速度。  
  
-   <xref:System.Windows.Media.Animation.SkipStoryboardToFill>：如果有，请转到其填充期，末尾情节提要。  
  
-   <xref:System.Windows.Media.Animation.StopStoryboard>：停止情节提要。  
  
-   <xref:System.Windows.Media.Animation.RemoveStoryboard>：删除情节提要，释放资源。  
  
## <a name="example"></a>示例  
 以下示例使用可控制情节提要操作来以交互方式控制情节提要。  
  
 **注意：** 若要查看通过使用代码来控制情节提要的示例，请参阅[控制演示图板后它启动使用其交互式方法](how-to-control-a-storyboard-after-it-starts.md)。  
  
 [!code-xaml[timingbehaviors_snip#ControlStoryboardExampleUsingWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/ControlStoryboardExample.xaml#controlstoryboardexampleusingwholepage)]  
  
 有关其他示例，请参阅[动画示例库](https://go.microsoft.com/fwlink/?LinkID=159969)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Media.Animation.ResumeStoryboard>
- <xref:System.Windows.Media.Animation.SetStoryboardSpeedRatio>
- <xref:System.Windows.Media.Animation.SkipStoryboardToFill>
- <xref:System.Windows.Media.Animation.PauseStoryboard>
- <xref:System.Windows.Media.Animation.StopStoryboard>
- <xref:System.Windows.Media.Animation.SeekStoryboard>
- [在情节提要启动后使用其交互式方法对其进行控制](how-to-control-a-storyboard-after-it-starts.md)
- [动画概述](animation-overview.md)
- [演示图板概述](storyboards-overview.md)
