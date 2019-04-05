---
title: Windows 窗体控件中的属性
ms.date: 03/30/2017
helpviewer_keywords:
- custom controls [Windows Forms], properties overview (using code)
- controls [Windows Forms], properties
- properties [Windows Forms]
ms.assetid: 2785279b-fb57-4937-8f6b-2050e475db6f
ms.openlocfilehash: e531b80cffabb94d2589383936a425b740c9cc07
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57708907"
---
# <a name="properties-in-windows-forms-controls"></a>Windows 窗体控件中的属性
Windows 窗体控件继承许多属性窗体的基类<xref:System.Windows.Forms.Control?displayProperty=nameWithType>。 这些包括属性如下所述<xref:System.Windows.Forms.Control.Font%2A>， <xref:System.Windows.Forms.Control.ForeColor%2A>， <xref:System.Windows.Forms.Control.BackColor%2A>， <xref:System.Windows.Forms.Control.Bounds%2A>， <xref:System.Windows.Forms.Control.ClientRectangle%2A>， <xref:System.Windows.Forms.Control.DisplayRectangle%2A>， <xref:System.Windows.Forms.Control.Enabled%2A>， <xref:System.Windows.Forms.Control.Focused%2A>， <xref:System.Windows.Forms.Control.Height%2A>， <xref:System.Windows.Forms.Control.Width%2A>， <xref:System.Windows.Forms.Control.Visible%2A>， <xref:System.Windows.Forms.Control.AutoSize%2A>，以及许多其他。 有关继承的属性的详细信息，请参阅<xref:System.Windows.Forms.Control?displayProperty=nameWithType>。  
  
 可以在控件中重写继承的属性和定义新属性。  
  
## <a name="in-this-section"></a>本节内容  
 [定义属性](defining-a-property-in-windows-forms-controls.md)  
 演示如何为自定义控件或组件实现属性，以及如何将该属性集成到设计环境中。  
  
 [使用 ShouldSerialize 和 Reset 方法定义默认值](defining-default-values-with-the-shouldserialize-and-reset-methods.md)  
 演示如何为自定义控件或组件定义默认属性值。  
  
 [属性更改事件](property-changed-events.md)  
 介绍如何在属性值发生更改时启用属性更改通知。  
  
 [如何：公开构成控件的属性](how-to-expose-properties-of-constituent-controls.md)  
 演示如何在自定义复合控件中公开构成控件的属性。  
  
 [自定义控件中的方法实现](method-implementation-in-custom-controls.md)  
 介绍如何在自定义控件和组件中实现方法。  
  
## <a name="reference"></a>参考  
 <xref:System.Windows.Forms.UserControl>  
 介绍用于实现复合控件的基类。  
  
 <xref:System.ComponentModel.TypeConverterAttribute>  
 介绍指定的特性<xref:System.ComponentModel.TypeConverter>要用于自定义属性类型。  
  
 <xref:System.ComponentModel.EditorAttribute>  
 介绍指定的特性<xref:System.Drawing.Design.UITypeEditor>要用于自定义属性。  
  
## <a name="related-sections"></a>相关章节  
 [Windows 窗体控件中的特性](attributes-in-windows-forms-controls.md)  
 描述你可以应用到自定义控件和组件的属性或其他成员的特性。  
  
 [组件的设计时特性](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/tk67c2t8(v=vs.120))  
 将列出的元数据特性应用到组件和控件，以便在设计时正确显示在可视化设计器中。  
  
 [扩展设计时支持](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/37899azc(v=vs.120))  
 描述如何实现提供设计时支持的类，例如编辑器和设计器。
