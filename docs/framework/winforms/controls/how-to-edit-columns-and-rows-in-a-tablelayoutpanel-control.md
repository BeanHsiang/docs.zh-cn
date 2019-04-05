---
title: 如何：编辑 TableLayoutPanel 控件中的行和列
ms.date: 03/30/2017
f1_keywords:
- net.ComponentModel.StyleCollectionEditor
helpviewer_keywords:
- columns [Windows Forms], editing
- TableLayoutPanel control [Windows Forms], editing
- rows [Windows Forms], editing
ms.assetid: c367ed43-40dc-49eb-9e0f-ba70e83dfec0
ms.openlocfilehash: 40129deed1f43480b7bde59ef8a67f4561af5d38
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57724682"
---
# <a name="how-to-edit-columns-and-rows-in-a-tablelayoutpanel-control"></a>如何：编辑 TableLayoutPanel 控件中的行和列
可以使用的集合编辑器<xref:System.Windows.Forms.TableLayoutPanel>控件，调用**列和行样式**对话框中，若要编辑的行和列的控件。  
  
> [!NOTE]
>  如果你想要跨多个行或列的控件，设置`RowSpan`和`ColumnSpan`控件上的属性。 有关详细信息，请参见[演练：使用 TableLayoutPanel 的 Windows 窗体上排列控件](walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)。  
>   
>  如果你想要对齐控件中某一单元，或者如果你想要在单元格中拉伸的控件，使用控件的<xref:System.Windows.Forms.Control.Anchor%2A>属性。 有关详细信息，请参见[演练：使用 TableLayoutPanel 的 Windows 窗体上排列控件](walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)。  
>   
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。  
  
### <a name="to-edit-rows-and-columns"></a>若要编辑行和列  
  
1.  从 <xref:System.Windows.Forms.TableLayoutPanel> “工具箱” **将** 控件拖到你的窗体上。  
  
2.  单击<xref:System.Windows.Forms.TableLayoutPanel>控件的智能标记标志符号 (![智能标记标志符号](./media/vs-winformsmttagglyph.gif "VS_WinFormSmtTagGlyph"))，然后选择**编辑行和列**打开**列和行样式**对话框。 也可以右键单击<xref:System.Windows.Forms.TableLayoutPanel>控件，然后选择**编辑行和列**从快捷菜单。  
  
3.  若要添加或删除列，请选择**列**从**成员类型**下拉列表框。  
  
4.  若要添加或删除的行，请选择**行**从**成员类型**下拉列表框。  
  
5.  单击**外**按钮以将行或列添加到末尾**成员**列表。  
  
6.  单击**插入**按钮在列表中添加行或当前所选的项之前的列。  
  
7.  如果要添加的行或列，选择**大小类型**新行或列。 有关详细信息，请参阅 <xref:System.Windows.Forms.SizeType>。  
  
8.  若要删除的行或列，请单击**删除**按钮以删除当前选定的项中**成员**列表。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.SizeType>
- [TableLayoutPanel 控件](tablelayoutpanel-control-windows-forms.md)
