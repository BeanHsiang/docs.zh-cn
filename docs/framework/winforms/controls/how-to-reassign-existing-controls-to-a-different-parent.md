---
title: 如何：重新分配给另一个父现有控件
ms.date: 03/30/2017
helpviewer_keywords:
- container controls [Windows Forms], Windows Forms
- layout [Windows Forms], resizing
- layout [Windows Forms], child controls
ms.assetid: 5a5723ff-34e0-4b6f-a57b-be4ebe35cb34
ms.openlocfilehash: 650d10fd681a55dfb17425111ef9d81726551da9
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57720181"
---
# <a name="how-to-reassign-existing-controls-to-a-different-parent"></a>如何：重新分配给另一个父现有控件
可以将你窗体中的控件分配到新容器控件。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。  
  
### <a name="to-reassign-existing-controls-to-a-different-parent"></a>若要将现有的控件重新分配给不同的父控件  
  
1.  将三个 <xref:System.Windows.Forms.Button> 控件从“工具箱”  拖到窗体上。  
  
     将其相邻放置，但不用对齐它们。  
  
2.  在“工具箱” 中，单击 <xref:System.Windows.Forms.FlowLayoutPanel> 控件图标。  
  
     请勿将该图标拖动到窗体上。  
  
3.  将鼠标指针移至靠近这 3 个 <xref:System.Windows.Forms.Button> 控件。  
  
     指针更改为十字线时就会附上 <xref:System.Windows.Forms.FlowLayoutPanel> 控件图标。  
  
4.  单击并按住鼠标按钮。  
  
5.  拖动鼠标指针以绘制 <xref:System.Windows.Forms.FlowLayoutPanel> 控件的轮廓。  
  
6.  在这三个 <xref:System.Windows.Forms.Button> 控件周围绘制轮廓。  
  
7.  释放鼠标按钮。  
  
     这三种 <xref:System.Windows.Forms.Button> 控件现在插入到 <xref:System.Windows.Forms.FlowLayoutPanel> 控件中。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.FlowLayoutPanel>
- <xref:System.Windows.Forms.TableLayoutPanel>
- [在 Windows 窗体上排列控件](arranging-controls-on-windows-forms.md)
- [演练：使用 TableLayoutPanel 的 Windows 窗体上排列控件](walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)
- [演练：使用对齐线的 Windows 窗体上排列控件](walkthrough-arranging-controls-on-windows-forms-using-snaplines.md)
