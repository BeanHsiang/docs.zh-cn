---
title: Windows 窗体中鼠标输入的工作原理
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Forms, mouse input
- mouse [Windows Forms], input
ms.assetid: 48fc5240-75a6-44bf-9fce-6aa21b49705a
ms.openlocfilehash: 7817b6a414f313cd2891fe0e124e230643b06e07
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57725319"
---
# <a name="how-mouse-input-works-in-windows-forms"></a>Windows 窗体中鼠标输入的工作原理
接收和处理鼠标输入是每个 Windows 应用程序的一个重要部分。 可以处理应用程序中执行操作的鼠标事件，或使用鼠标位置信息来执行命中测试或其他操作。 此外，你可以更改你的应用程序中的控件处理鼠标输入方式。 本主题介绍这些详细信息，以及如何获取和更改鼠标的系统设置中的鼠标事件。 事件和在其中的鼠标单击事件的顺序引发有关使用鼠标提供的数据详细信息，请参阅[Windows 窗体中的鼠标事件](mouse-events-in-windows-forms.md)。  
  
## <a name="mouse-location-and-hit-testing"></a>鼠标位置和命中测试  
 当用户移动鼠标时，操作系统将鼠标指针移动。 鼠标指针包含一个像素，名为作用点，该操作系统跟踪，并将识别为指针的位置。 当用户移动鼠标或按下鼠标按钮， <xref:System.Windows.Forms.Control> ，其中包含<xref:System.Windows.Forms.Cursor.HotSpot%2A>引发适当的鼠标事件。 你可以获取与当前的鼠标位置<xref:System.Windows.Forms.MouseEventArgs.Location%2A>的属性<xref:System.Windows.Forms.MouseEventArgs>处理鼠标事件时，或通过使用<xref:System.Windows.Forms.Cursor.Position%2A>属性的<xref:System.Windows.Forms.Cursor>类。 你可以随后使用鼠标位置信息来执行命中测试，然后执行一个操作基于鼠标的位置。 命中测试功能内置的 Windows 窗体中的多个控件如<xref:System.Windows.Forms.ListView>， <xref:System.Windows.Forms.TreeView>，<xref:System.Windows.Forms.MonthCalendar>和<xref:System.Windows.Forms.DataGridView>控件。 使用与适当的鼠标事件<xref:System.Windows.Forms.Control.MouseHover>等命中测试，用于确定你的应用程序时应执行特定操作非常有用。  
  
## <a name="mouse-events"></a>鼠标事件  
 响应鼠标输入的主要方法是处理鼠标事件。 下表显示鼠标事件，并说明何时引发它们。  
  
|鼠标事件|描述|  
|-----------------|-----------------|  
|<xref:System.Windows.Forms.Control.Click>|此事件发生时释放鼠标按钮时，通常之前<xref:System.Windows.Forms.Control.MouseUp>事件。 此事件的处理程序接收类型为 <xref:System.EventArgs> 的参数。 处理此事件时仅需要确定何时发生单击。|  
|<xref:System.Windows.Forms.Control.MouseClick>|当用户单击鼠标控件，将发生此事件。 此事件的处理程序接收类型为 <xref:System.Windows.Forms.MouseEventArgs> 的参数。 处理此事件时您需要先单击发生时获取鼠标的有关信息。|  
|<xref:System.Windows.Forms.Control.DoubleClick>|双击该控件时，会发生此事件。 此事件的处理程序接收类型为 <xref:System.EventArgs> 的参数。 处理此事件时只需确定何时发生一次双击。|  
|<xref:System.Windows.Forms.Control.MouseDoubleClick>|当用户双击鼠标控件时发生此事件。 此事件的处理程序接收类型为 <xref:System.Windows.Forms.MouseEventArgs> 的参数。 处理此事件时需要双击发生时获取鼠标的有关信息。|  
|<xref:System.Windows.Forms.Control.MouseDown>|当鼠标指针位于控件上方并且用户按下鼠标按钮时发生此事件。 此事件的处理程序接收类型为 <xref:System.Windows.Forms.MouseEventArgs> 的参数。|  
|<xref:System.Windows.Forms.Control.MouseEnter>|当鼠标指针进入控件，具体取决于控件类型的边框或客户端区域时发生此事件。 此事件的处理程序接收类型为 <xref:System.EventArgs> 的参数。|  
|<xref:System.Windows.Forms.Control.MouseHover>|当鼠标指针停止并停留在控件上时，将发生此事件。 此事件的处理程序接收类型为 <xref:System.EventArgs> 的参数。|  
|<xref:System.Windows.Forms.Control.MouseLeave>|当鼠标指针离开控件，具体取决于控件类型的边框或客户端区域时，会发生此事件。 此事件的处理程序接收类型为 <xref:System.EventArgs> 的参数。|  
|<xref:System.Windows.Forms.Control.MouseMove>|当鼠标指针在控件上移动时发生此事件。 此事件的处理程序接收类型为 <xref:System.Windows.Forms.MouseEventArgs> 的参数。|  
|<xref:System.Windows.Forms.Control.MouseUp>|当鼠标指针位于控件上方并且用户释放鼠标按钮时发生此事件。 此事件的处理程序接收类型为 <xref:System.Windows.Forms.MouseEventArgs> 的参数。|  
|<xref:System.Windows.Forms.Control.MouseWheel>|在控件有焦点并且用户滚动鼠标滚轮时发生此事件。 此事件的处理程序接收类型为 <xref:System.Windows.Forms.MouseEventArgs> 的参数。 可以使用<xref:System.Windows.Forms.MouseEventArgs.Delta%2A>属性的<xref:System.Windows.Forms.MouseEventArgs>以确定鼠标滚动的距离。|  
  
## <a name="changing-mouse-input-and-detecting-system-settings"></a>更改鼠标输入及检测系统设置  
 您可以检测和更改控件通过派生自该控件并使用处理鼠标输入的方式<xref:System.Windows.Forms.Control.GetStyle%2A>和<xref:System.Windows.Forms.Control.SetStyle%2A>方法。 <xref:System.Windows.Forms.Control.SetStyle%2A>方法采用的按位组合<xref:System.Windows.Forms.ControlStyles>值，以确定控件是否将具有标准单击或双击行为，或如果该控件将处理其自己的鼠标处理。 此外，<xref:System.Windows.Forms.SystemInformation>类包含用于描述鼠标的功能并指定鼠标与操作系统交互的方式的属性。 下表总结了这些属性。  
  
|属性|描述|  
|--------------|-----------------|  
|<xref:System.Windows.Forms.SystemInformation.DoubleClickSize%2A>|获取维度，以像素为单位，在其中用户必须单击两次操作系统需要考虑两个区域的单击一次双击。|  
|<xref:System.Windows.Forms.SystemInformation.DoubleClickTime%2A>|获取最大的第一次单击与 operating system to 鼠标操作视为双击第二次单击之间可以经过的毫秒数。|  
|<xref:System.Windows.Forms.SystemInformation.MouseButtons%2A>|获取鼠标上的按钮数。|  
|<xref:System.Windows.Forms.SystemInformation.MouseButtonsSwapped%2A>|获取一个值，该值指示是否已交换鼠标左右按钮的功能。|  
|<xref:System.Windows.Forms.SystemInformation.MouseHoverSize%2A>|获取特定矩形的尺寸（以像素为单位），鼠标指针必须在该矩形范围内停留达到鼠标悬停时间后，才会生成鼠标悬停消息。|  
|<xref:System.Windows.Forms.SystemInformation.MouseHoverTime%2A>|获取一个以毫秒为单位的时间，鼠标指针必须在悬停矩形中停留该时间后，才会生成鼠标悬停消息。|  
|<xref:System.Windows.Forms.SystemInformation.MousePresent%2A>|获取一个值，该值指示是否安装了鼠标。|  
|<xref:System.Windows.Forms.SystemInformation.MouseSpeed%2A>|获取一个值，该值指示当前鼠标的速度，从 1 到 20。|  
|<xref:System.Windows.Forms.SystemInformation.MouseWheelPresent%2A>|获取一个值，该值指示是否安装了带有鼠标轮的鼠标。|  
|<xref:System.Windows.Forms.SystemInformation.MouseWheelScrollDelta%2A>|获取单次鼠标轮旋转增量的增量值的量。|  
|<xref:System.Windows.Forms.SystemInformation.MouseWheelScrollLines%2A>|获取滚动鼠标轮时所滚动过的行数。|  
  
## <a name="see-also"></a>请参阅
- [Windows 窗体应用程序中的鼠标输入](mouse-input-in-a-windows-forms-application.md)
- [Windows 窗体中的鼠标捕获](mouse-capture-in-windows-forms.md)
- [Windows 窗体中的鼠标指针](mouse-pointers-in-windows-forms.md)
