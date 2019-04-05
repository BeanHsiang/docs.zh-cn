---
title: ImageList 组件概述（Windows 窗体）
ms.date: 03/30/2017
f1_keywords:
- ImageList
helpviewer_keywords:
- collection controls [Windows Forms], images
- icon list control
- ImageList component [Windows Forms], about ImageList component
ms.assetid: 7e25d89b-5633-40c1-afc3-82e0e301ffa2
ms.openlocfilehash: 9869e647613ccf009954a5d65445947fbced40e7
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57709838"
---
# <a name="imagelist-component-overview-windows-forms"></a>ImageList 组件概述（Windows 窗体）

Windows 窗体 <xref:System.Windows.Forms.ImageList> 组件用于存储图像，此图像之后可由控件显示。 借助图像列表，你可为图像的单个一致目录编写代码。 例如，只需更改按钮的 <xref:System.Windows.Forms.ButtonBase.ImageIndex%2A> 或 <xref:System.Windows.Forms.ButtonBase.ImageKey%2A> 属性，即可旋转 <xref:System.Windows.Forms.Button> 控件显示的图像。 还可将相同图像列表与多个控件关联。 例如，如果同时使用 <xref:System.Windows.Forms.ListView> 控件和 <xref:System.Windows.Forms.TreeView> 控件来显示相同的文件列表，更改文件在图像列表中的图标将导致新图标显示在这两个视图中。

## <a name="using-imagelist-with-controls"></a>将 ImageList 与控件一起使用

可将图像列表与任何具有 `ImageList` 属性的控件一同使用，如果与 <xref:System.Windows.Forms.ListView> 控件一同使用，则此控件要具有 <xref:System.Windows.Forms.ListView.SmallImageList%2A> 和 <xref:System.Windows.Forms.ListView.LargeImageList%2A> 属性。 可与图像列表关联的控件包括：<xref:System.Windows.Forms.ListView>、<xref:System.Windows.Forms.TreeView>、<xref:System.Windows.Forms.ToolBar>、<xref:System.Windows.Forms.TabControl>、<xref:System.Windows.Forms.Button><xref:System.Windows.Forms.CheckBox>、<xref:System.Windows.Forms.RadioButton> 和 <xref:System.Windows.Forms.Label> 控件。 若要将图像列表与控件关联，请将控件的 `ImageList` 属性设置为 <xref:System.Windows.Forms.ImageList> 组件的名称。

## <a name="key-properties"></a>键属性

<xref:System.Windows.Forms.ImageList> 组件的键属性是 <xref:System.Windows.Forms.ImageList.Images%2A>，其中包含关联控件使用的图片。 可通过相应的索引值或键访问每张单独的图像。 <xref:System.Windows.Forms.ImageList.ColorDepth%2A> 属性确定图像呈现的颜色数。 由 <xref:System.Windows.Forms.ImageList.ImageSize%2A> 属性设置后，图像将以相同大小显示。 较大的图像将调整为合适大小。

## <a name="see-also"></a>请参阅

- <xref:System.Windows.Forms.ImageList>
- [如何：添加或删除映像使用 Windows 窗体 ImageList 组件](how-to-add-or-remove-images-with-the-windows-forms-imagelist-component.md)