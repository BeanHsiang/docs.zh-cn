---
title: 如何：管理在 Windows 窗体的 ToolStrip 溢出
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ToolStrip control [Windows Forms], managing overflow
- toolbars [Windows Forms], managing overflow
- examples [Windows Forms], toolbars
- CanOverflow property
ms.assetid: fa10e0ad-4cbf-4c0d-9082-359c2f855d4e
ms.openlocfilehash: 53f610a728925d454a8833a49e705818f027aec5
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57707269"
---
# <a name="how-to-manage-toolstrip-overflow-in-windows-forms"></a>如何：管理在 Windows 窗体的 ToolStrip 溢出

当上的所有项<xref:System.Windows.Forms.ToolStrip>控件不适合分配的空间，则可以在启用溢出功能<xref:System.Windows.Forms.ToolStrip>，并确定特定的溢出行为<xref:System.Windows.Forms.ToolStripItem>s。

添加时<xref:System.Windows.Forms.ToolStripItem>需要更多的空间比已分配到的 s<xref:System.Windows.Forms.ToolStrip>给定窗体的当前大小<xref:System.Windows.Forms.ToolStripOverflowButton>上将自动显示<xref:System.Windows.Forms.ToolStrip>。 <xref:System.Windows.Forms.ToolStripOverflowButton>出现，并启用了溢出的项移到下拉列表溢出菜单。 这使您可以自定义和确定优先级如何在<xref:System.Windows.Forms.ToolStrip>项未能正确地调整到不同的窗体的大小。 当它们发生溢出时，使用时，还可以更改项的外观<xref:System.Windows.Forms.ToolStripItem.Placement%2A>并<xref:System.Windows.Forms.ToolStripOverflow.DisplayedItems%2A?displayProperty=nameWithType>属性和<xref:System.Windows.Forms.ToolStrip.LayoutCompleted>事件。 如果更放大窗体在设计时或运行的时， <xref:System.Windows.Forms.ToolStripItem>s 可以显示在主<xref:System.Windows.Forms.ToolStrip>和<xref:System.Windows.Forms.ToolStripOverflowButton>直到减小窗体的大小可能甚至会消失。

## <a name="to-enable-overflow-on-a-toolstrip-control"></a>若要启用溢出的 ToolStrip 控件

- 絋粄<xref:System.Windows.Forms.ToolStrip.CanOverflow%2A>属性未设置为`false`为<xref:System.Windows.Forms.ToolStrip>。 默认值为 `True`。

     当<xref:System.Windows.Forms.ToolStrip.CanOverflow%2A>是`True`（默认值），<xref:System.Windows.Forms.ToolStripItem>发送到下拉列表溢出菜单时的内容<xref:System.Windows.Forms.ToolStripItem>超出的水平宽度<xref:System.Windows.Forms.ToolStrip>或高度的垂直<xref:System.Windows.Forms.ToolStrip>。

## <a name="to-specify-overflow-behavior-of-a-specific-toolstripitem"></a>若要指定特定 ToolStripItem 溢出行为

- 设置<xref:System.Windows.Forms.ToolStripItem.Overflow%2A>属性的<xref:System.Windows.Forms.ToolStripItem>到所需的值。 可能的值为`Always`， `Never`，和`AsNeeded`。 默认值为 `AsNeeded`。

    ```vb
    toolStripTextBox1.Overflow = _
    System.Windows.Forms.ToolStripItemOverflow.Never
    ```

    ```csharp
    toolStripTextBox1.Overflow = _
    System.Windows.Forms.ToolStripItemOverflow.Never;
    ```

## <a name="see-also"></a>请参阅

- <xref:System.Windows.Forms.ToolStrip>
- <xref:System.Windows.Forms.ToolStripOverflowButton>
- <xref:System.Windows.Forms.ToolStripItem.Overflow%2A>
- <xref:System.Windows.Forms.ToolStrip.CanOverflow%2A>
- [ToolStrip 控件概述](toolstrip-control-overview-windows-forms.md)
- [ToolStrip 控件体系结构](toolstrip-control-architecture.md)
- [ToolStrip 技术摘要](toolstrip-technology-summary.md)
