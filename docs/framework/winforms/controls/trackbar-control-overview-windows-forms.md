---
title: TrackBar 控件概述（Windows 窗体）
ms.date: 03/30/2017
f1_keywords:
- TrackBar
helpviewer_keywords:
- sliders [Windows Forms], about sliders
- TrackBar control [Windows Forms], about TrackBar control
- slider controls [Windows Forms], about slider controls
ms.assetid: 95910ecb-8a4c-4776-89fa-206c89ed6973
ms.openlocfilehash: 74a8feba14b7e2186fb64729cb915e53132805d5
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57707009"
---
# <a name="trackbar-control-overview-windows-forms"></a>TrackBar 控件概述（Windows 窗体）
Windows 窗体<xref:System.Windows.Forms.TrackBar>控件 （有时也称为"滑块"控件） 用于浏览大量的信息或用于直观地调整数字设置。 <xref:System.Windows.Forms.TrackBar>控件具有两个部分： thumb，也称为滑块，将和刻度线。 滚动块是可调整的一部分。 其位置对应于<xref:System.Windows.Forms.TrackBar.Value%2A>属性。 刻度线是按固定间隔分布的可视指示符。 指定并可以水平或垂直对齐的增量移动跟踪条。 例如，可能会使用跟踪条以控制光标闪烁速率或鼠标的速度的系统。  
  
## <a name="key-properties"></a>键属性  
 键属性<xref:System.Windows.Forms.TrackBar>控制是在<xref:System.Windows.Forms.TrackBar.Value%2A>， <xref:System.Windows.Forms.TrackBar.TickFrequency%2A>， <xref:System.Windows.Forms.TrackBar.Minimum%2A>，和<xref:System.Windows.Forms.TrackBar.Maximum%2A>。 <xref:System.Windows.Forms.TrackBar.TickFrequency%2A> 为刻度间隔。 <xref:System.Windows.Forms.TrackBar.Minimum%2A> 和<xref:System.Windows.Forms.TrackBar.Maximum%2A>是可以表示跟踪条的最小和最大值。  
  
 其他两个重要属性是<xref:System.Windows.Forms.TrackBar.SmallChange%2A>和<xref:System.Windows.Forms.TrackBar.LargeChange%2A>。 值<xref:System.Windows.Forms.TrackBar.SmallChange%2A>属性是滚动块移动到具有左或向右箭头键按下的响应中的位置数。 值<xref:System.Windows.Forms.TrackBar.LargeChange%2A>属性是 thumb 响应具有 PAGE UP 或 PAGE DOWN 键按下，移动或以响应鼠标单击跟踪条上滚动块的任何一侧上的位置数。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.TrackBar>
- [TrackBar 控件](trackbar-control-windows-forms.md)
