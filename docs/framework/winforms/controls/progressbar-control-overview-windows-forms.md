---
title: ProgressBar 控件概述（Windows 窗体）
ms.date: 03/30/2017
f1_keywords:
- ProgressBar
helpviewer_keywords:
- ProgressBar control [Windows Forms], about ProgressBar control
- progress controls [Windows Forms], about progress controls
ms.assetid: a05d9cba-3a6a-4f8f-94b8-8ec12799fb80
ms.openlocfilehash: db0a43534080d630323d8c1c95759fd2dcc04a85
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57707933"
---
# <a name="progressbar-control-overview-windows-forms"></a>ProgressBar 控件概述（Windows 窗体）
> [!IMPORTANT]
>  
  <xref:System.Windows.Forms.ToolStripProgressBar> 控件取代了 <xref:System.Windows.Forms.ProgressBar> 控件并添加了功能；但是，可以选择保留 <xref:System.Windows.Forms.ProgressBar> 控件以实现向后兼容并供将来使用。  
  
 Windows 窗体<xref:System.Windows.Forms.ProgressBar>控件通过显示适当数量的水平栏中排列矩形指示过程的进度。 该过程完成后，填充栏。 进度条通常用于为用户提供的思路很长时间才能等待进程完成;例如，大型文件正在加载时。  
  
> [!NOTE]
>  <xref:System.Windows.Forms.ProgressBar>控件可以只能水平放置在窗体上。  
  
## <a name="key-properties-and-methods"></a>键属性和方法  
 键属性<xref:System.Windows.Forms.ProgressBar>控制是在<xref:System.Windows.Forms.ProgressBar.Value%2A>， <xref:System.Windows.Forms.ProgressBar.Minimum%2A>，和<xref:System.Windows.Forms.ProgressBar.Maximum%2A>。 <xref:System.Windows.Forms.ProgressBar.Minimum%2A>和<xref:System.Windows.Forms.ProgressBar.Maximum%2A>属性设置可以显示进度栏的最大和最小值。 <xref:System.Windows.Forms.ProgressBar.Value%2A>属性表示已完成该操作方面的进度。 通过在控件中显示的栏组成块，因为显示的值<xref:System.Windows.Forms.ProgressBar>控件仅近似于<xref:System.Windows.Forms.ProgressBar.Value%2A>属性的当前值。 基于大小<xref:System.Windows.Forms.ProgressBar>控件，<xref:System.Windows.Forms.ProgressBar.Value%2A>属性确定何时显示下一个块。  
  
 更新当前的进度值的最常见方法是编写代码来设置<xref:System.Windows.Forms.ProgressBar.Value%2A>属性。 在加载大型文件的示例中，可能设置最大值为千字节为单位中的文件的大小。 例如，如果<xref:System.Windows.Forms.ProgressBar.Maximum%2A>属性设置为 100，<xref:System.Windows.Forms.ProgressBar.Minimum%2A>属性设置为 10，和<xref:System.Windows.Forms.ProgressBar.Value%2A>属性设置为 50，将显示 5 个矩形。 这是数目的可以显示的一半。  
  
 但是，还有其他方法来修改显示的值<xref:System.Windows.Forms.ProgressBar>控件，除了设置<xref:System.Windows.Forms.ProgressBar.Value%2A>直接属性。 <xref:System.Windows.Forms.ProgressBar.Step%2A>属性可以用于指定一个值，以递增<xref:System.Windows.Forms.ProgressBar.Value%2A>属性。 然后，调用<xref:System.Windows.Forms.ProgressBar.PerformStep%2A>方法将递增的值。 若要改变的增量值，可以使用<xref:System.Windows.Forms.ProgressBar.Increment%2A>方法并指定具有要递增的值<xref:System.Windows.Forms.ProgressBar.Value%2A>属性。  
  
 以图形方式通知用户有关当前操作的另一个控件是<xref:System.Windows.Forms.StatusBar>控件。  
  
> [!IMPORTANT]
>  <xref:System.Windows.Forms.StatusStrip>并<xref:System.Windows.Forms.ToolStripStatusLabel>控件替换，并将功能添加到<xref:System.Windows.Forms.StatusBar>并<xref:System.Windows.Forms.StatusBarPanel>控制; 但是，<xref:System.Windows.Forms.StatusBar>和<xref:System.Windows.Forms.StatusBarPanel>控件将保留用于向后兼容性并供将来使用，如果你选择。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.ProgressBar>
- [ProgressBar 控件](progressbar-control-windows-forms.md)
