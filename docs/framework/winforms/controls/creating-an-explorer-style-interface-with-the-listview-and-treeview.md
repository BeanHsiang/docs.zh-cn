---
title: 演练：创建带有 ListView 和 TreeView 控件使用设计器的资源管理器样式界面
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Explorer-style applications [Windows Forms], walkthroughs
- TreeView control [Windows Forms], ListView controls used with
- ListView control [Windows Forms], TreeView controls used with
- Explorer-style applications
- TreeView control [Windows Forms], using for explorer-style interface
- ListView control [Windows Forms], explorer style interface
- ListView control [Windows Forms], explorer-style interface
ms.assetid: 9e5e7721-19e2-4890-b273-a43589fe99ff
ms.openlocfilehash: a849eae086c3507bbaf7050afd2e0496ab5a970e
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57716976"
---
# <a name="walkthrough-creating-an-explorer-style-interface-with-the-listview-and-treeview-controls-using-the-designer"></a>演练：创建带有 ListView 和 TreeView 控件使用设计器的资源管理器样式界面
Visual Studio 的优势之一是时间的能够在较短中创建具有专业外观的 Windows 窗体应用程序。 一种常见方案使用创建用户界面 (UI)<xref:System.Windows.Forms.ListView>和<xref:System.Windows.Forms.TreeView>类似于 Windows 操作系统的 Windows 资源管理器功能的控件。 Windows 资源管理器中显示用户的计算机上的文件和文件夹的层次结构。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。  
  
### <a name="to-create-the-form-containing-a-listview-and-treeview-control"></a>若要创建包含 ListView 和 TreeView 控件的窗体  
  
1.  在 **“文件”** 菜单上，指向 **“新建”**，然后单击 **“项目”**。  
  
2.  在中**新的项目**对话框框中，执行以下操作：  
  
    1.  在类别中，选择**Visual Basic**或**Visual C#**。  
  
    2.  在模板列表中，选择**Windows 窗体应用程序**。  
  
3.  单击 **“确定”**。 创建一个新的 Windows 窗体项目。  
  
4.  添加<xref:System.Windows.Forms.SplitContainer>向窗体控件，并设置其<xref:System.Windows.Forms.SplitContainer.Dock%2A>属性设置为<xref:System.Windows.Forms.DockStyle.Fill>。  
  
5.  添加<xref:System.Windows.Forms.ImageList>名为`imageList1`到窗体，使用属性窗口添加两个映像： 一个文件夹图像和文档图像，按该顺序。  
  
6.  添加<xref:System.Windows.Forms.TreeView>名为控件`treeview1`窗体，并将其置于的左侧<xref:System.Windows.Forms.SplitContainer>控件。 在属性窗口中`treeView1`执行以下操作：  
  
    1.  将 <xref:System.Windows.Forms.Control.Dock%2A> 属性设置为 <xref:System.Windows.Forms.DockStyle.Fill>。  
  
    2.  将 <xref:System.Windows.Forms.TreeView.ImageList%2A> 属性设置为 `imagelist1.`  
  
7.  添加<xref:System.Windows.Forms.ListView>名为控件`listView1`窗体，并将其置于的右侧<xref:System.Windows.Forms.SplitContainer>控件。 在属性窗口中`listview1`执行以下操作：  
  
    1.  将 <xref:System.Windows.Forms.Control.Dock%2A> 属性设置为 <xref:System.Windows.Forms.DockStyle.Fill>。  
  
    2.  将 <xref:System.Windows.Forms.ListView.View%2A> 属性设置为 <xref:System.Windows.Forms.View.Details>。  
  
    3.  通过单击省略号打开 ColumnHeader 集合编辑器 (![VisualStudioEllipsesButton 屏幕快照](../media/vbellipsesbutton.png "vbEllipsesButton")) 中<xref:System.Windows.Forms.ListView.Columns%2A>属性 **。** 添加三个列，并设置其<xref:System.Windows.Forms.ColumnHeader.Text%2A>属性设置为`Name`， `Type`，和`Last Modified`分别。 单击“确定”关闭对话框。  
  
    4.  将 <xref:System.Windows.Forms.ListView.SmallImageList%2A> 属性设置为 `imageList1.`  
  
8.  实现代码来填充<xref:System.Windows.Forms.TreeView>节点和子节点。 添加到此代码`Form1`类。  
  
     [!code-csharp[System.Windows.Forms.ExplorerStyleInterface#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/CS/Form1.cs#1)]
     [!code-vb[System.Windows.Forms.ExplorerStyleInterface#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/VB/Form1.vb#1)]  
  
9. 由于前面的代码使用 System.IO 命名空间，添加相应的使用或导入窗体顶部的语句。  
  
     [!code-csharp[System.Windows.Forms.ExplorerStyleInterface#4](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/CS/Form1.cs#4)]
     [!code-vb[System.Windows.Forms.ExplorerStyleInterface#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/VB/Form1.vb#4)]  
  
10. 从上一步中窗体的构造函数调用设置方法或<xref:System.Windows.Forms.Form.Load>事件处理方法。 将此代码添加到窗体构造函数。  
  
     [!code-csharp[System.Windows.Forms.ExplorerStyleInterface#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.ExplorerStyleInterface#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/VB/Form1.vb#2)]  
  
11. 处理<xref:System.Windows.Forms.TreeView.NodeMouseClick>事件`treeview1` **，** 并实现代码来填充`listview1`单击节点时的节点的内容。 添加到此代码`Form1`类。  
  
     [!code-csharp[System.Windows.Forms.ExplorerStyleInterface#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.ExplorerStyleInterface#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/VB/Form1.vb#3)]  
  
     如果使用的 C#，请确保你有<xref:System.Windows.Forms.TreeView.NodeMouseClick>事件与其事件处理方法关联。 将此代码添加到窗体构造函数。  
  
     [!code-csharp[System.Windows.Forms.ExplorerStyleInterface#5](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/CS/Form1.cs#5)]  
  
## <a name="testing-the-application"></a>测试应用程序  
 现在可以测试窗体，以确保其行为符合预期。  
  
#### <a name="to-test-the-form"></a>若要测试窗体  
  
-   按 F5 运行该应用程序。  
  
     你将看到一个拆分窗体，其中包含<xref:System.Windows.Forms.TreeView>控件，用于左侧和右侧，显示你的项目目录和一个<xref:System.Windows.Forms.ListView>包含三列右侧的控件。 您可以遍历<xref:System.Windows.Forms.TreeView>通过选择目录节点和<xref:System.Windows.Forms.ListView>填充与所选目录的内容。  
  
## <a name="next-steps"></a>后续步骤  
 此应用程序提供的一种方法可以使用示例<xref:System.Windows.Forms.TreeView>和<xref:System.Windows.Forms.ListView>一起控制。 有关这些控件的详细信息，请参阅以下主题：  
  
-   [如何：将自定义信息添加到 TreeView 或 ListView 控件 （Windows 窗体）](add-custom-information-to-a-treeview-or-listview-control-wf.md)  
  
-   [如何：向 ListView 控件添加搜索功能](how-to-add-search-capabilities-to-a-listview-control.md)  
  
-   [如何：将快捷菜单附加到 TreeView 节点](how-to-attach-a-shortcut-menu-to-a-treeview-node.md)  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.ListView>
- <xref:System.Windows.Forms.TreeView>
- [ListView 控件](listview-control-windows-forms.md)
- [如何：添加和删除节点使用 Windows 窗体 TreeView 控件](how-to-add-and-remove-nodes-with-the-windows-forms-treeview-control.md)
- [如何：添加和删除使用 Windows 窗体 ListView 控件的项](how-to-add-and-remove-items-with-the-windows-forms-listview-control.md)
- [如何：将列添加到 Windows 窗体 ListView 控件](how-to-add-columns-to-the-windows-forms-listview-control.md)
