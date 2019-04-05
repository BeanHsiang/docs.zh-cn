---
title: ToolStrip 控件概述（Windows 窗体）
ms.date: 03/30/2017
f1_keywords:
- Toolstrip
helpviewer_keywords:
- ToolStrip control [Windows Forms], about ToolStrip control
- toolbars [Windows Forms], what's new in Windows Forms
- toolbars [Windows Forms]
- what's new [Windows Forms], toolbars
ms.assetid: 81d067ed-297c-4dad-90de-1bcac15336ec
ms.openlocfilehash: c701ed6ff155ca507f827874a955b2361a3b2359
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57719372"
---
# <a name="toolstrip-control-overview-windows-forms"></a>ToolStrip 控件概述（Windows 窗体）
Windows 窗体<xref:System.Windows.Forms.ToolStrip>控制和及其关联的类将用户界面元素组合到工具栏、 状态栏和菜单提供一个通用框架。 <xref:System.Windows.Forms.ToolStrip> 控件提供丰富的设计时体验，包括就地激活和编辑、 自定义布局和漂浮，即工具栏共享水平或垂直空间的能力。  
  
 尽管<xref:System.Windows.Forms.ToolStrip>替换，并将功能添加到在上一版本中，控件<xref:System.Windows.Forms.ToolBar>如果需要保留向后兼容性和将来使用。  
  
## <a name="features-of-the-toolstrip-controls"></a>ToolStrip 控件的功能  
 使用<xref:System.Windows.Forms.ToolStrip>控制转移到：  
  
-   在容器中显示常见的用户界面。  
  
-   创建轻松地自定义，支持的常用的工具栏高级用户界面和布局功能，例如使用文本和图像、 下拉按钮和控件停靠、 漂浮、 按钮、 溢出按钮和运行时重新排序<xref:System.Windows.Forms.ToolStrip>项。  
  
-   支持溢出和运行时项重新排序。 溢出功能将项目移动到下拉列表菜单时没有足够的空间来将它们显示在<xref:System.Windows.Forms.ToolStrip>。  
  
-   支持的典型的外观和行为通过常见的呈现模型的操作系统。  
  
-   与处理事件的其他控件相同的方式处理始终对所有容器和包含的项的事件。  
  
-   将项从一个拖<xref:System.Windows.Forms.ToolStrip>到另一个中或在<xref:System.Windows.Forms.ToolStrip>。  
  
-   创建下拉列表控件和用户界面类型编辑器中的高级布局<xref:System.Windows.Forms.ToolStripDropDown>。  
  
 使用<xref:System.Windows.Forms.ToolStripControlHost>类上使用其他控件<xref:System.Windows.Forms.ToolStrip>，并获得<xref:System.Windows.Forms.ToolStrip>为它们的功能。  
  
 可以扩展功能并使用修改的外观和行为<xref:System.Windows.Forms.ToolStripRenderer>， <xref:System.Windows.Forms.ToolStripProfessionalRenderer>，并<xref:System.Windows.Forms.ToolStripManager>连同<xref:System.Windows.Forms.ToolStripRenderMode>和<xref:System.Windows.Forms.ToolStripManagerRenderMode>枚举。  
  
 <xref:System.Windows.Forms.ToolStrip>控件是高度可配置且可扩展的并提供许多属性、 方法和事件，以自定义外观和行为。 以下是一些值得注意的成员：  
  
### <a name="important-toolstrip-members"></a>重要 ToolStrip 成员  
  
|name|描述|  
|----------|-----------------|  
|<xref:System.Windows.Forms.ToolStrip.Dock%2A>|获取或设置父容器的边缘<xref:System.Windows.Forms.ToolStrip>停靠。|  
|<xref:System.Windows.Forms.ToolStrip.AllowItemReorder%2A>|获取或设置一个用于指示是否专门由 <xref:System.Windows.Forms.ToolStrip> 类处理拖放和项重新排序操作的值。|  
|<xref:System.Windows.Forms.ToolStrip.LayoutStyle%2A>|获取或设置一个值，该值指示如何<xref:System.Windows.Forms.ToolStrip>其项的布局。|  
|<xref:System.Windows.Forms.ToolStripItem.Overflow%2A>|获取或设置是否<xref:System.Windows.Forms.ToolStripItem>附加到<xref:System.Windows.Forms.ToolStrip>或<xref:System.Windows.Forms.ToolStripOverflowButton>还是漂浮在两者之间。|  
|<xref:System.Windows.Forms.ToolStrip.IsDropDown%2A>|获取一个值，该值指示是否<xref:System.Windows.Forms.ToolStripItem>下拉列表中显示的其他项列表时<xref:System.Windows.Forms.ToolStripItem>单击。|  
|<xref:System.Windows.Forms.ToolStrip.OverflowButton%2A>|获取 <xref:System.Windows.Forms.ToolStripItem>，它是启用了溢出的 <xref:System.Windows.Forms.ToolStrip> 的“溢出”按钮。|  
|<xref:System.Windows.Forms.ToolStrip.Renderer%2A>|获取或设置<xref:System.Windows.Forms.ToolStripRenderer>用于自定义外观和行为 （外观和感受） <xref:System.Windows.Forms.ToolStrip>。|  
|<xref:System.Windows.Forms.ToolStrip.RenderMode%2A>|获取或设置要应用于的绘制样式<xref:System.Windows.Forms.ToolStrip>。|  
|<xref:System.Windows.Forms.ToolStrip.RendererChanged>|在 <xref:System.Windows.Forms.ToolStrip.Renderer%2A> 属性更改时引发。|  
  
 <xref:System.Windows.Forms.ToolStrip>通过大量的伴生类使用实现控件的灵活性。 下面是最值得注意的一些：  
  
### <a name="important-toolstrip-companion-classes"></a>重要 ToolStrip 伴生类  
  
|name|描述|  
|----------|-----------------|  
|<xref:System.Windows.Forms.MenuStrip>|替换并添加了功能<xref:System.Windows.Forms.MainMenu>类。|  
|<xref:System.Windows.Forms.StatusStrip>|替换并添加了功能<xref:System.Windows.Forms.StatusBar>类。|  
|<xref:System.Windows.Forms.ContextMenuStrip>|替换并添加了功能<xref:System.Windows.Forms.ContextMenu>类。|  
|<xref:System.Windows.Forms.ToolStripItem>|抽象基类，用于管理事件和布局的所有元素的<xref:System.Windows.Forms.ToolStrip>， <xref:System.Windows.Forms.ToolStripControlHost>，或<xref:System.Windows.Forms.ToolStripDropDown>可以包含。|  
|<xref:System.Windows.Forms.ToolStripContainer>|使用窗体以各种方式排列控件的每一侧面板提供容器。|  
|<xref:System.Windows.Forms.ToolStripRenderer>|处理的绘制功能<xref:System.Windows.Forms.ToolStrip>对象。|  
|<xref:System.Windows.Forms.ToolStripProfessionalRenderer>|提供 Microsoft Office 样式外观。|  
|<xref:System.Windows.Forms.ToolStripManager>|控件<xref:System.Windows.Forms.ToolStrip>呈现和漂浮，以及将合并<xref:System.Windows.Forms.MenuStrip>， <xref:System.Windows.Forms.ToolStripDropDownMenu>，和<xref:System.Windows.Forms.ToolStripMenuItem>对象。|  
|<xref:System.Windows.Forms.ToolStripManagerRenderMode>|指定应用到多个的绘制样式 （自定义，Windows XP 或 Microsoft Office Professional）<xref:System.Windows.Forms.ToolStrip>窗体中包含的对象。|  
|<xref:System.Windows.Forms.ToolStripRenderMode>|指定应用于一个的绘制样式 （自定义，Windows XP 或 Microsoft Office Professional）<xref:System.Windows.Forms.ToolStrip>窗体中包含的对象。|  
|<xref:System.Windows.Forms.ToolStripControlHost>|承载其他控件没有专门<xref:System.Windows.Forms.ToolStrip>控件，但要为其<xref:System.Windows.Forms.ToolStrip>功能。|  
|<xref:System.Windows.Forms.ToolStripItemPlacement>|指定是否<xref:System.Windows.Forms.ToolStripItem>是在主要的分布方式<xref:System.Windows.Forms.ToolStrip>，在溢出<xref:System.Windows.Forms.ToolStrip>，或都不。|  
  
 有关详细信息，请参阅[ToolStrip 技术摘要](toolstrip-technology-summary.md)并[ToolStrip 控件体系结构](toolstrip-control-architecture.md)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.ToolStrip>
- <xref:System.Windows.Forms.MenuStrip>
- <xref:System.Windows.Forms.ContextMenuStrip>
- <xref:System.Windows.Forms.StatusStrip>
- <xref:System.Windows.Forms.ToolStripItem>
- <xref:System.Windows.Forms.ToolStripDropDown>
