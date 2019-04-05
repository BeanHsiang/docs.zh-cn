---
title: 如何：在不更改时间线速度的情况下更改时钟速度
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- speed of Clock [WPF], changing
- clocks [WPF], changing speed of
ms.assetid: 72f36dd0-f085-445d-8589-19a83fe74f5e
ms.openlocfilehash: 19e6874b9b472cb4a5f716677f99af03f2b73b10
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57358270"
---
# <a name="how-to-change-the-speed-of-a-clock-without-changing-the-speed-of-its-timeline"></a>如何：在不更改时间线速度的情况下更改时钟速度
一个<xref:System.Windows.Media.Animation.ClockController>对象的<xref:System.Windows.Media.Animation.ClockController.SpeedRatio%2A>属性使您能够更改的速度<xref:System.Windows.Media.Animation.Clock>而不会改变<xref:System.Windows.Media.Animation.Timeline.SpeedRatio%2A>的时钟的<xref:System.Windows.Media.Animation.Timeline>。 在以下示例中，<xref:System.Windows.Media.Animation.ClockController>用于以交互方式修改<xref:System.Windows.Media.Animation.ClockController.SpeedRatio%2A>的时钟。 <xref:System.Windows.Media.Animation.Clock.CurrentGlobalSpeedInvalidated>事件和时钟<xref:System.Windows.Media.Animation.Clock.CurrentGlobalSpeed%2A>属性用于显示时钟的当前全局速度每次其交互式<xref:System.Windows.Media.Animation.ClockController.SpeedRatio%2A>发生更改。  
  
## <a name="example"></a>示例  
 [!code-csharp[timingbehaviors_procedural_snip#GraphicsMMClockControllerSpeedRatioExample](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_procedural_snip/CSharp/ClockControllerSpeedRatioExample.cs#graphicsmmclockcontrollerspeedratioexample)]
 [!code-vb[timingbehaviors_procedural_snip#GraphicsMMClockControllerSpeedRatioExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_procedural_snip/visualbasic/clockcontrollerspeedratioexample.vb#graphicsmmclockcontrollerspeedratioexample)]
