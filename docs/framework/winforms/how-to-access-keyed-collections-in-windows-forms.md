---
title: 如何：访问键控集合在 Windows 窗体中
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- keyed collections [Windows Forms]
- collections [Windows Forms], accessing with keys
ms.assetid: b9b79b8b-d9bf-4f8c-b9d6-9578bc3219d3
ms.openlocfilehash: af398e8ac051bfc89c532fe5dc216e9cfbfdc4b9
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57709610"
---
# <a name="how-to-access-keyed-collections-in-windows-forms"></a>如何：访问键控集合在 Windows 窗体中
-   您可以通过键访问单个集合项。 此功能已添加到 Windows 窗体应用程序通常使用的许多集合类。 以下列表显示了一些具有可访问键控的集合的集合类：  
  
-   <xref:System.Windows.Forms.ListView.ListViewItemCollection>  
  
-   <xref:System.Windows.Forms.ListViewItem.ListViewSubItemCollection>  
  
-   <xref:System.Windows.Forms.Control.ControlCollection>  
  
-   <xref:System.Windows.Forms.TabControl.TabPageCollection>  
  
-   <xref:System.Windows.Forms.TreeNodeCollection>  
  
 与集合中的项关联的键通常是项的名称。 以下过程显示如何使用集合类来执行常见任务。  
  
### <a name="to-find-and-give-focus-to-a-nested-control-in-a-control-collection"></a>若要查找并将焦点放到控件集合中的嵌套控件  
  
-   使用<xref:System.Windows.Forms.Control.ControlCollection.Find%2A>和<xref:System.Windows.Forms.Control.Focus%2A>方法，以指定要查找和焦点转至的控件的名称。  
  
     [!code-csharp[System.Windows.Forms.KeyedCollectionsEx#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.KeyedCollectionsEx/CS/Form1.cs#1)]
     [!code-vb[System.Windows.Forms.KeyedCollectionsEx#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.KeyedCollectionsEx/VB/Form1.vb#1)]  
  
### <a name="to-access-an-image-in-an-image-collection"></a>若要访问图像集合中的图像  
  
-   使用<xref:System.Windows.Forms.ImageList.ImageCollection.Item%2A>属性来指定你想要访问的映像的名称。  
  
     [!code-csharp[System.Windows.Forms.KeyedCollectionsEx#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.KeyedCollectionsEx/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.KeyedCollectionsEx#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.KeyedCollectionsEx/VB/Form1.vb#2)]  
  
### <a name="to-set-a-tab-page-as-the-selected-tab"></a>若要为所选的选项卡设置选项卡页  
  
-   使用<xref:System.Windows.Forms.TabControl.SelectedTab%2A>属性和<xref:System.Windows.Forms.TabControl.TabPageCollection.Item%2A>属性来指定要将设置为所选的选项卡上的选项卡页的名称。  
  
     [!code-csharp[System.Windows.Forms.KeyedCollectionsEx#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.KeyedCollectionsEx/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.KeyedCollectionsEx#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.KeyedCollectionsEx/VB/Form1.vb#3)]  
  
## <a name="see-also"></a>请参阅
- [Windows 窗体入门](getting-started-with-windows-forms.md)
- [如何：添加或删除映像使用 Windows 窗体 ImageList 组件](./controls/how-to-add-or-remove-images-with-the-windows-forms-imagelist-component.md)
