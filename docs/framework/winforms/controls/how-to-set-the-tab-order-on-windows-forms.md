---
title: 如何：设置 Windows 窗体上 tab 键顺序
ms.date: 03/30/2017
f1_keywords:
- TabStop
- TabIndex
helpviewer_keywords:
- tab order [Windows Forms], controls on Windows forms
- Windows Forms controls, setting tab order
- controls [Windows Forms], setting tab order
- Windows Forms, setting tab order
ms.assetid: 71fa8e76-0472-414b-ad3c-0f90166e0ad7
ms.openlocfilehash: 3f566dfb5dbc118c5a6be7f874b5b4857756075a
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57705870"
---
# <a name="how-to-set-the-tab-order-on-windows-forms"></a>如何：设置 Windows 窗体上 tab 键顺序
Tab 键顺序是在其中用户焦点从一个控件移到另一个通过按 TAB 键顺序。 每个窗体具有其自己的 tab 键顺序。 默认情况下，tab 键顺序是在其中创建控件的顺序相同。 Tab 键顺序编号从 0 开始。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。  
  
### <a name="to-set-the-tab-order-of-a-control"></a>若要设置控件的 tab 键顺序  
  
1.  上**视图**菜单上，单击**tab 键顺序**。  
  
     这将激活窗体上的 tab 键顺序选择模式。 一个数字 (表示<xref:System.Windows.Forms.Control.TabIndex%2A>属性) 中的每个控件的左上角显示。  
  
2.  单击控件以建立所需的选项卡顺序。  
  
    > [!NOTE]
    >  大于或等于 0，可以为任何值设置 tab 键顺序中的控件的位置。 重复发生时，计算两个控件的 z 顺序，并为第一个选项卡顶部的控件。 （z 顺序是沿窗体的 z 轴 [深度] 窗体上控件的可视化分层。 Z 顺序确定哪些控件位于其他控件的前面。）Z 顺序的详细信息，请参阅[在 Windows 窗体上的分层对象](how-to-layer-objects-on-windows-forms.md)。  
  
3.  完成后，单击**tab 键顺序**上**视图**菜单，再次将 tab 键顺序模式。  
  
    > [!NOTE]
    >  无法获取焦点的控件，以及已禁用且不可见控件不具有<xref:System.Windows.Forms.Control.TabIndex%2A>属性并且将不包含在 tab 键顺序中。 当用户按 TAB 键，将跳过这些控件。  
  
 或者，可以在属性窗口中使用设置 tab 键顺序<xref:System.Windows.Forms.Control.TabIndex%2A>属性。 <xref:System.Windows.Forms.Control.TabIndex%2A>控件的属性确定其定位的 tab 键顺序。 默认情况下，具有第一个控件绘制<xref:System.Windows.Forms.Control.TabIndex%2A>值为 0，第二个<xref:System.Windows.Forms.Control.TabIndex%2A>为 1，依此类推。  
  
 此外，默认情况下，<xref:System.Windows.Forms.GroupBox>控件具有其自己<xref:System.Windows.Forms.Control.TabIndex%2A>值，该值是一个整数。 一个<xref:System.Windows.Forms.GroupBox>控件本身不能在运行时具有焦点。 因此，在每个控件<xref:System.Windows.Forms.GroupBox>具有其自己的十进制<xref:System.Windows.Forms.Control.TabIndex%2A>值，从.0 开始。 当然，作为<xref:System.Windows.Forms.Control.TabIndex%2A>的<xref:System.Windows.Forms.GroupBox>递增控件时，将相应递增中它的控件。 如果您更改<xref:System.Windows.Forms.Control.TabIndex%2A>介于 5 和 6，<xref:System.Windows.Forms.Control.TabIndex%2A>其组中的第一个控件的值将自动更改为 6.0 中，依次类推。  
  
 最后，任何窗体上的多个控件可以跳过的 tab 键顺序。 通常情况下，连续按 tab 键在运行的时选择每个控件的 tab 键顺序。 通过关闭<xref:System.Windows.Forms.Control.TabStop%2A>属性，可以使窗体的 tab 键顺序通过传递控件。  
  
#### <a name="to-remove-a-control-from-the-tab-order"></a>若要从 tab 键顺序中移除控件  
  
1.  设置控件的<xref:System.Windows.Forms.Control.TabStop%2A>属性设置为`false`属性窗口中。  
  
     一个控件<xref:System.Windows.Forms.Control.TabStop%2A>属性已设置为`false`仍保持其 tab 键顺序中的位置，即使控件循环使用 TAB 键时，将跳过该控件。  
  
    > [!NOTE]
    >  单选按钮组具有一个选项卡在运行时停止。 选定的按钮 (即，具有按钮及其<xref:System.Windows.Forms.RadioButton.Checked%2A>属性设置为`true`) 具有其<xref:System.Windows.Forms.Control.TabStop%2A>属性自动设置为`true`，而其他按钮都有其<xref:System.Windows.Forms.Control.TabStop%2A>属性设置为`false`。 有关分组的详细信息<xref:System.Windows.Forms.RadioButton>控件，请参阅[分组 Windows 窗体 RadioButton 控件按功能](how-to-group-windows-forms-radiobutton-controls-to-function-as-a-set.md)。  
  
## <a name="see-also"></a>请参阅
- [Windows 窗体控件](index.md)
- [在 Windows 窗体上排列控件](arranging-controls-on-windows-forms.md)
- [在 Windows 窗体上使用的控件](controls-to-use-on-windows-forms.md)
- [按功能列出的 Windows 窗体控件](windows-forms-controls-by-function.md)
