---
title: AutoSize 属性概述
ms.date: 03/30/2017
helpviewer_keywords:
- sizing [Windows Forms], automatic
- layout [Windows Forms], AutoSize
- automatic sizing
- AutoSizeMode property
ms.assetid: 62fd82a2-9565-4f65-925b-9d1e66dc4e7d
ms.openlocfilehash: 2fc06bef2434e87b7fbd3ec79e7671c4e32b7b3b
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54649825"
---
# <a name="autosize-property-overview"></a>AutoSize 属性概述
<xref:System.Windows.Forms.Control.AutoSize%2A>属性使控件能够更改其大小，如有必要，以获得指定的值<xref:System.Windows.Forms.Control.PreferredSize%2A>属性。 通过设置调整为特定控件的大小调整行为`AutoSizeMode`属性。  
  
## <a name="autosize-behavior"></a>自动调整大小行为  
 某些控件只支持<xref:System.Windows.Forms.Control.AutoSize%2A>属性。 此外，某些控件的支持<xref:System.Windows.Forms.Control.AutoSize%2A>属性还支持`AutoSizeMode`属性。  
  
 <xref:System.Windows.Forms.Control.AutoSize%2A>属性会产生略有不同的行为，具体取决于特定的控件类型和值的`AutoSizeMode`属性，如果存在此属性。 下表介绍了始终正确的行为，并提供每个的简要说明：  
  
|始终正确的行为|描述|  
|--------------------------|-----------------|  
|自动调整大小是运行时功能。|这意味着它永远不会增长或收缩一个控件，然后不再进一步有效。|  
|如果控件更改大小，则其<xref:System.Windows.Forms.Control.Location%2A>属性始终保持不变。|当控件的内容将导致其增长时，该控件的增长向右和向下。 控件不会变得左侧。|  
|<xref:System.Windows.Forms.Control.Dock%2A>并<xref:System.Windows.Forms.Control.Anchor%2A>属性得到遵守<xref:System.Windows.Forms.Control.AutoSize%2A>是`true`。|控件的值<xref:System.Windows.Forms.Control.Location%2A>属性调整为正确的值。<br /><br /> **请注意**<xref:System.Windows.Forms.Label>控制是此规则的例外。 当设置的值的停靠<xref:System.Windows.Forms.Label>控件的<xref:System.Windows.Forms.Control.AutoSize%2A>属性设置为`true`，则<xref:System.Windows.Forms.Label>控件不会拉伸。|  
|控件的<xref:System.Windows.Forms.Control.MaximumSize%2A>并<xref:System.Windows.Forms.Control.MinimumSize%2A>而不考虑的值，则始终遵守属性及其<xref:System.Windows.Forms.Control.AutoSize%2A>属性。|<xref:System.Windows.Forms.Control.MaximumSize%2A>并<xref:System.Windows.Forms.Control.MinimumSize%2A>的属性不会影响<xref:System.Windows.Forms.Control.AutoSize%2A>属性。|  
|没有默认情况下设置最小大小。|这意味着，如果控件设置下收缩<xref:System.Windows.Forms.Control.AutoSize%2A>它未包含任何内容，值和其<xref:System.Windows.Forms.Control.Size%2A>属性为 0，0。 在这种情况下，该控件将缩小为一个点，并不容易看到。|  
|如果控件不实现<xref:System.Windows.Forms.Control.GetPreferredSize%2A>方法，<xref:System.Windows.Forms.Control.GetPreferredSize%2A>方法将返回最后一个值分配给<xref:System.Windows.Forms.Control.Size%2A>属性。|这意味着该设置<xref:System.Windows.Forms.Control.AutoSize%2A>到`true`不会产生影响。|  
|中的控件<xref:System.Windows.Forms.TableLayoutPanel>单元格始终会缩小以适合单元格，直至其<xref:System.Windows.Forms.Control.MinimumSize%2A>为止。|将最大大小设置为强制此大小。 这不是这种情况，单元格时的一部分<xref:System.Windows.Forms.SizeType.AutoSize>行或列。|  
  
## <a name="autosizemode-property"></a>AutoSizeMode 属性  
 `AutoSizeMode`属性提供默认值的更精细地控制<xref:System.Windows.Forms.Control.AutoSize%2A>行为。 `AutoSizeMode`属性指定如何控件本身其内容调整大小。 其内容，例如，可以是文本<xref:System.Windows.Forms.Button>控件或容器的子控件。  
  
 下表显示<xref:System.Windows.Forms.AutoSizeMode>每种设置引起的设置和行为的说明。  
  
|AutoSizeMode 设置|行为|  
|--------------------------|--------------|  
|GrowAndShrink|控件增大或缩小以包含其内容。<br /><br /> <xref:System.Windows.Forms.Control.MinimumSize%2A>并<xref:System.Windows.Forms.Control.MaximumSize%2A>值将起作用，但当前值<xref:System.Windows.Forms.Control.Size%2A>属性将被忽略。<br /><br /> 这是使用控件的行为相同<xref:System.Windows.Forms.Control.AutoSize%2A>属性，但不`AutoSizeMode`属性。|  
|GrowOnly|根据需要尽可能以覆盖其内容，该控件的增长，但它会缩小至小于指定的值及其<xref:System.Windows.Forms.Control.Size%2A>属性。<br /><br /> 这是 `AutoSizeMode` 的默认值。|  
  
## <a name="controls-that-support-the-autosize-property"></a>支持自动调整大小属性的控件  
 下表列出了支持的控件<xref:System.Windows.Forms.Control.AutoSize%2A>和`AutoSizeMode`属性。  
  
|自动调整大小的支持|控件类型|  
|----------------------|------------------|  
|-   <xref:System.Windows.Forms.Control.AutoSize%2A> 支持的属性。<br />-不`AutoSizeMode`属性。|<xref:System.Windows.Forms.CheckBox><br /><br /> <xref:System.Windows.Forms.DomainUpDown><br /><br /> <xref:System.Windows.Forms.Label><br /><br /> <xref:System.Windows.Forms.LinkLabel><br /><br /> <xref:System.Windows.Forms.MaskedTextBox> (<xref:System.Windows.Forms.TextBox> base)<br /><br /> <xref:System.Windows.Forms.NumericUpDown><br /><br /> <xref:System.Windows.Forms.RadioButton><br /><br /> <xref:System.Windows.Forms.TextBox><br /><br /> <xref:System.Windows.Forms.TrackBar>|  
|-   <xref:System.Windows.Forms.Control.AutoSize%2A> 支持的属性。<br />-   `AutoSizeMode` 支持的属性。|<xref:System.Windows.Forms.Button><br /><br /> <xref:System.Windows.Forms.CheckedListBox><br /><br /> <xref:System.Windows.Forms.FlowLayoutPanel><br /><br /> <xref:System.Windows.Forms.Form><br /><br /> <xref:System.Windows.Forms.GroupBox><br /><br /> <xref:System.Windows.Forms.Panel><br /><br /> <xref:System.Windows.Forms.TableLayoutPanel>|  
|-不<xref:System.Windows.Forms.Control.AutoSize%2A>属性。|<xref:System.Windows.Forms.CheckedListBox><br /><br /> <xref:System.Windows.Forms.ComboBox><br /><br /> <xref:System.Windows.Forms.DataGridView><br /><br /> <xref:System.Windows.Forms.DateTimePicker><br /><br /> <xref:System.Windows.Forms.ListBox><br /><br /> <xref:System.Windows.Forms.ListView><br /><br /> <xref:System.Windows.Forms.MaskedTextBox><br /><br /> <xref:System.Windows.Forms.MonthCalendar><br /><br /> <xref:System.Windows.Forms.ProgressBar><br /><br /> <xref:System.Windows.Forms.PropertyGrid><br /><br /> <xref:System.Windows.Forms.RichTextBox><br /><br /> <xref:System.Windows.Forms.SplitContainer><br /><br /> <xref:System.Windows.Forms.TabControl><br /><br /> <xref:System.Windows.Forms.TabPage><br /><br /> <xref:System.Windows.Forms.TreeView><br /><br /> <xref:System.Windows.Forms.WebBrowser><br /><br /> <xref:System.Windows.Forms.ScrollBar>|  
  
## <a name="autosize-in-the-design-environment"></a>在设计环境中自动调整大小  
 下表描述控件的大小调整行为在设计时，值的基础其<xref:System.Windows.Forms.Control.AutoSize%2A>和`AutoSizeMode`属性。  
  
 重写<xref:System.Windows.Forms.Design.ControlDesigner.SelectionRules%2A>属性来确定给定的控件是否处于用户可调整大小状态。 在下表中，"不能"意味着<xref:System.Windows.Forms.Design.SelectionRules.Moveable>仅，"可以"意味着<xref:System.Windows.Forms.Design.SelectionRules.AllSizeable>和<xref:System.Windows.Forms.Design.SelectionRules.Moveable>。  
  
|自动调整大小设置|设计时调整大小操作|  
|-----------------------|---------------------------------|  
|-   <xref:System.Windows.Forms.Control.AutoSize%2A> = `true`<br />-不`AutoSizeMode`属性。|用户不能在设计时，除了以下控件调整控件的大小：<br /><br /> -   <xref:System.Windows.Forms.TextBox><br />-   <xref:System.Windows.Forms.MaskedTextBox><br />-   <xref:System.Windows.Forms.RichTextBox><br />-   <xref:System.Windows.Forms.TrackBar>|  
|-   <xref:System.Windows.Forms.Control.AutoSize%2A> = `true`<br />-   `AutoSizeMode` = <xref:System.Windows.Forms.AutoSizeMode.GrowAndShrink>|用户不能在设计时调整控件的大小。|  
|-   <xref:System.Windows.Forms.Control.AutoSize%2A> = `true`<br />-   `AutoSizeMode` = <xref:System.Windows.Forms.AutoSizeMode.GrowOnly>|用户可以在设计时调整控件的大小。 当<xref:System.Windows.Forms.Control.Size%2A>属性设置，用户可以仅增加该控件的大小。|  
|-   <xref:System.Windows.Forms.Control.AutoSize%2A> = `false`或<xref:System.Windows.Forms.Control.AutoSize%2A>属性被隐藏。|用户可以在设计时调整控件的大小。|  
  
> [!NOTE]
>  若要最大化生产效率，Windows 窗体设计器 shadows<xref:System.Windows.Forms.Control.AutoSize%2A>属性<xref:System.Windows.Forms.Form>类。 在设计时，窗体行为就如同<xref:System.Windows.Forms.Control.AutoSize%2A>属性设置为`false`，无论其实际的设置。 在运行时，进行任何特殊的便利设施，和<xref:System.Windows.Forms.Control.AutoSize%2A>应用属性所指定的属性设置。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.Control.AutoSize%2A>
- <xref:System.Windows.Forms.Control.PreferredSize%2A>
- <xref:System.Windows.Forms.Control.GetPreferredSize%2A>
