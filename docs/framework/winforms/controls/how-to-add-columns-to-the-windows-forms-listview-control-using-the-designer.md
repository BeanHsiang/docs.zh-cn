---
title: 如何：将列添加到使用设计器在 Windows 窗体 ListView 控件
ms.date: 03/30/2017
helpviewer_keywords:
- ListView control [Windows Forms], adding column headers
- columns [Windows Forms], adding to ListView controls
ms.assetid: 5b1a8b4d-587e-479a-95c1-f9b90884f13a
ms.openlocfilehash: 725976e0d4b5903659cc264902890329bd13fcad
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57717279"
---
# <a name="how-to-add-columns-to-the-windows-forms-listview-control-using-the-designer"></a>如何：将列添加到使用设计器在 Windows 窗体 ListView 控件
Windows 窗体<xref:System.Windows.Forms.ListView>控件可以显示多个列的每个列表项中**详细信息**视图。 可以使用列来显示多种类型的每个列表项的相关信息。 例如，文件的列表可以显示文件名、 文件类型、 大小和文件的上次修改的日期。 创建后填充列的信息，请参阅[如何：在具有 Windows 的列中显示子项窗体 ListView 控件](how-to-display-subitems-in-columns-with-the-windows-forms-listview-control.md)。  
  
 下面的过程需要**Windows 应用程序**包含一个窗体，其中包含项目<xref:System.Windows.Forms.ListView>控件。 有关设置此类项目的信息，请参阅[如何：创建 Windows 窗体应用程序项目](/visualstudio/ide/step-1-create-a-windows-forms-application-project)和[如何：将控件添加到 Windows 窗体](how-to-add-controls-to-windows-forms.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。  
  
### <a name="to-add-columns-in-the-designer"></a>若要在设计器中添加列  
  
1.  在中**属性**窗口中，设置控件的<xref:System.Windows.Forms.ListView.View%2A>属性设置为<xref:System.Windows.Forms.View.Details>。  
  
2.  在中**属性**窗口中，单击**省略号**按钮 (![VisualStudioEllipsesButton 屏幕快照](../media/vbellipsesbutton.png "vbEllipsesButton")) 旁边<xref:System.Windows.Forms.ListView.Columns%2A>属性。  
  
     **ColumnHeader 集合编辑器**出现。  
  
3.  使用**添加**按钮以添加新列。 然后，您可以选择列标题并设置其文本 （列的标题）、 文本对齐方式和宽度。  
  
## <a name="see-also"></a>请参阅
- [ListView 控件概述](listview-control-overview-windows-forms.md)
- [如何：添加和删除使用 Windows 窗体 ListView 控件的项](how-to-add-and-remove-items-with-the-windows-forms-listview-control.md)
- [如何：在使用 Windows 窗体 ListView 控件的列中显示子项](how-to-display-subitems-in-columns-with-the-windows-forms-listview-control.md)
- [如何：Windows 窗体 ListView 控件中显示图标](how-to-display-icons-for-the-windows-forms-listview-control.md)
- [如何：将自定义信息添加到 TreeView 或 ListView 控件 （Windows 窗体）](add-custom-information-to-a-treeview-or-listview-control-wf.md)
