---
title: 在 Windows 窗体 MenuStrip 控件中合并菜单项
ms.date: 03/30/2017
helpviewer_keywords:
- MenuStrip [Windows Forms], merging
- merging [Windows Forms], general concepts
ms.assetid: 95e113ba-f362-4dda-8a76-6d95ddc45cee
ms.openlocfilehash: 292c299bd15cd62eabd9a13db1abab1ed07fe57e
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57722336"
---
# <a name="merging-menu-items-in-the-windows-forms-menustrip-control"></a>在 Windows 窗体 MenuStrip 控件中合并菜单项
如果有多文档界面 (MDI) 应用程序，您可以合并到父窗体的菜单的菜单项或整个菜单从子窗体。  
  
 本主题介绍与合并菜单项在 MDI 应用程序相关联的基本概念。  
  
## <a name="general-concepts"></a>一般概念  
 合并过程涉及目标和源控件：  
  
-   目标是<xref:System.Windows.Forms.MenuStrip>要在其中合并菜单项 main 的一个或多个 MDI 父窗体上的控件。  
  
-   源是<xref:System.Windows.Forms.MenuStrip>包含你想要合并到目标菜单的菜单项的 MDI 子窗体上的控件。  
  
 <xref:System.Windows.Forms.MenuStrip.MdiWindowListItem%2A>属性标识的下拉列表，则会使用当前 MDI 标题填充父窗体的 MDI 子窗体的菜单项。 例如，您通常列出上当前打开的 MDI 子窗体**窗口**菜单。  
  
 <xref:System.Windows.Forms.ToolStripMenuItem.IsMdiWindowListEntry%2A>属性标识的菜单项来自于<xref:System.Windows.Forms.MenuStrip>MDI 子窗体上。  
  
 您可以手动或自动合并菜单项。 菜单项合并在相同的方式对这两种方法，但合并的激活方式不同，本主题后面的"手动合并"和"自动合并"部分中所述。 在手动和自动合并，每个合并操作将影响下一步的合并操作。  
  
 <xref:System.Windows.Forms.MenuStrip> 合并菜单项从一个移<xref:System.Windows.Forms.ToolStrip>到另一个而不是克隆它们，如同使用<xref:System.Windows.Forms.MainMenu>。  
  
## <a name="mergeaction-values"></a>MergeAction 值  
 在源中的菜单项上设置的合并操作<xref:System.Windows.Forms.MenuStrip>使用<xref:System.Windows.Forms.MergeAction>属性。  
  
 下表描述了可用合并操作的含义和典型用法。  
  
|MergeAction 值|描述|典型用法|  
|-----------------------|-----------------|-----------------|  
|<xref:System.Windows.Forms.MergeAction.Append>|（默认值）将源项添加到目标项的集合的末尾。|激活该程序的某部分时，请将菜单项添加到菜单的末尾。|  
|<xref:System.Windows.Forms.MergeAction.Insert>|将源项添加到目标项的集合，在指定的位置<xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A>源项上设置的属性。|激活该程序的某部分时，请将菜单项添加到中间或菜单的开始位置。<br /><br /> 如果的值<xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A>是相同的两个菜单项，添加按相反的顺序。 设置<xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A>适当地保留原始顺序。|  
|<xref:System.Windows.Forms.MergeAction.Replace>|找到文本匹配项，或使用<xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A>时没有文本匹配项找到，并将源菜单项替换匹配的目标菜单项的值。|将执行不同操作的相同名称的源菜单项替换为目标的菜单项。|  
|<xref:System.Windows.Forms.MergeAction.MatchOnly>|找到文本匹配项，或使用<xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A>时没有文本匹配项找到，然后向目标添加从源下拉列表的所有项的值。|生成菜单结构，该插入或将菜单项添加到子菜单，或删除子菜单的菜单项。 例如，可以将菜单项从 MDI 子窗体添加到 main <xref:System.Windows.Forms.MenuStrip>**另存为**菜单。<br /><br /> <xref:System.Windows.Forms.MergeAction.MatchOnly> 可以导航菜单结构而无需采取任何操作。 它提供了一种方法来评估后续项。|  
|<xref:System.Windows.Forms.MergeAction.Remove>|找到文本匹配项，或使用<xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A>时没有文本匹配项找到，然后从目标中删除项的值。|从目标中删除菜单项<xref:System.Windows.Forms.MenuStrip>。|  
  
## <a name="manual-merging"></a>手动合并  
 仅<xref:System.Windows.Forms.MenuStrip>自动合并参与控件。 若要合并的项的其他控件，如<xref:System.Windows.Forms.ToolStrip>并<xref:System.Windows.Forms.StatusStrip>控件，您必须进行手动合并，通过调用<xref:System.Windows.Forms.ToolStripManager.Merge%2A>和<xref:System.Windows.Forms.ToolStripManager.RevertMerge%2A>根据需要在代码中的方法。  
  
## <a name="automatic-merging"></a>自动合并  
 您可以使用自动合并为 MDI 应用程序通过激活源窗体。 若要使用<xref:System.Windows.Forms.MenuStrip>MDI 应用程序，在设置<xref:System.Windows.Forms.Form.MainMenuStrip%2A>属性设置为目标<xref:System.Windows.Forms.MenuStrip>，以便在源上执行合并操作<xref:System.Windows.Forms.MenuStrip>反映在目标<xref:System.Windows.Forms.MenuStrip>。  
  
 可以触发自动合并通过激活<xref:System.Windows.Forms.MenuStrip>MDI 源上。 在激活时源<xref:System.Windows.Forms.MenuStrip>合并到 MDI 目标。 当新的窗体变为活动状态时，合并是还原最后一个窗体上并触发新的窗体上。 可以通过设置控制此行为<xref:System.Windows.Forms.ToolStripItem.MergeAction%2A>根据需要在每个属性<xref:System.Windows.Forms.ToolStripItem>，并通过设置<xref:System.Windows.Forms.ToolStrip.AllowMerge%2A>上每个属性<xref:System.Windows.Forms.MenuStrip>。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.ToolStripManager>
- <xref:System.Windows.Forms.MenuStrip>
- [MenuStrip 控件](menustrip-control-windows-forms.md)
- [如何：使用 MenuStrip 创建 MDI 窗口列表](how-to-create-an-mdi-window-list-with-menustrip-windows-forms.md)
- [如何：设置自动菜单合并为 MDI 应用程序](how-to-set-up-automatic-menu-merging-for-mdi-applications.md)
