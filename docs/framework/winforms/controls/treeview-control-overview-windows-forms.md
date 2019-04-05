---
title: TreeView 控件概述（Windows 窗体）
ms.date: 03/30/2017
f1_keywords:
- TreeView
helpviewer_keywords:
- TreeView control [Windows Forms], about TreeView control
ms.assetid: 0ece823a-9508-478a-bbdb-7d7c3bae51d5
ms.openlocfilehash: 046713745e7de18cefe5b4883af73034af2cfb31
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57711996"
---
# <a name="treeview-control-overview-windows-forms"></a>TreeView 控件概述（Windows 窗体）

使用 Windows 窗体 <xref:System.Windows.Forms.TreeView> 控件，可以为用户显示节点层次结构，就像在 Windows 操作系统的 Windows 资源管理器功能的左窗格中显示文件和文件夹一样。 在树视图中的每个节点可能包含其他节点，称为*子节点*。 以按展开或折叠的方式显示父节点或包含子节点的节点。 还可以通过将树视图的 <xref:System.Windows.Forms.TreeView.CheckBoxes%2A> 属性设置为 `true` 来显示在节点旁边带有复选框的树视图。 然后，通过将节点的 <xref:System.Windows.Forms.TreeNode.Checked%2A> 属性设置为 `true` 或 `false`，可以采用编程方式来选中或清除节点。

## <a name="key-properties"></a>键属性

<xref:System.Windows.Forms.TreeView> 控件的键属性包括 <xref:System.Windows.Forms.TreeView.Nodes%2A> 和 <xref:System.Windows.Forms.TreeView.SelectedNode%2A>。 <xref:System.Windows.Forms.TreeView.Nodes%2A> 属性包括树视图中的顶级节点列表。 <xref:System.Windows.Forms.TreeView.SelectedNode%2A> 属性设置当前选中的节点。 你可以在节点旁边显示图标。 该控件使用在树视图的 <xref:System.Windows.Forms.TreeView.ImageList%2A> 属性中命名的 <xref:System.Windows.Forms.ImageList> 中的图像。 
  <xref:System.Windows.Forms.TreeView.ImageIndex%2A> 属性可以设置树视图中节点的默认图像。 有关显示图像的详细信息，请参阅[如何：设置 Windows 窗体 TreeView 控件的图标](how-to-set-icons-for-the-windows-forms-treeview-control.md)。 如果使用 Visual Studio 2005，则可以使用的标准映像的大型库可以访问<xref:System.Windows.Forms.TreeView>控件。

## <a name="see-also"></a>请参阅

- <xref:System.Windows.Forms.TreeView>
- [TreeView 控件](treeview-control-windows-forms.md)
- [如何：设置 Windows 窗体 TreeView 控件的图标](how-to-set-icons-for-the-windows-forms-treeview-control.md)
- [如何：添加和删除节点使用 Windows 窗体 TreeView 控件](how-to-add-and-remove-nodes-with-the-windows-forms-treeview-control.md)
- [如何：循环访问 Windows 窗体 TreeView 控件的所有节点](how-to-iterate-through-all-nodes-of-a-windows-forms-treeview-control.md)
- [如何：确定被单击的 TreeView 节点](how-to-determine-which-treeview-node-was-clicked-windows-forms.md)
- [如何：将自定义信息添加到 TreeView 或 ListView 控件 （Windows 窗体）](add-custom-information-to-a-treeview-or-listview-control-wf.md)