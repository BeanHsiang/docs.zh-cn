---
title: 如何：创建缩略图图像
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- thumbnail images [Windows Forms], creating
- images [Windows Forms], creating thumbnails
ms.assetid: e956242a-1e5b-4217-a3cf-5f3fb45d00ba
ms.openlocfilehash: 3ed1fb6a9a7fc8e7ded6ae0e124ca7dcbf0f3c98
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57716954"
---
# <a name="how-to-create-thumbnail-images"></a>如何：创建缩略图图像
缩略图是映像的小版本。 您可以通过调用创建缩略图<xref:System.Drawing.Image.GetThumbnailImage%2A>方法的<xref:System.Drawing.Image>对象。  
  
## <a name="example"></a>示例  
 下面的示例构造<xref:System.Drawing.Image>JPG 文件中的对象。 原始图像的宽度为 640 像素，高度为 479 像素。 代码将创建具有 100 个像素的宽度和高度为 100 像素的缩略图。  
  
 下图显示的缩略图。  
  
 ![缩略图](./media/thumbnail1.png "Thumbnail1")  
  
> [!NOTE]
>  在此示例中，回调方法，声明，但从未使用。 这支持所有版本的 GDI +。  
  
 [!code-csharp[System.Drawing.WorkingWithImages#71](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/CS/Class1.cs#71)]
 [!code-vb[System.Drawing.WorkingWithImages#71](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/VB/Class1.vb#71)]  
  
## <a name="compiling-the-code"></a>编译代码  
 前面的示例专用于 Windows 窗体，它需要 <xref:System.Windows.Forms.PaintEventArgs> `e`，后者是 <xref:System.Windows.Forms.Control.Paint> 事件处理程序的参数。 若要运行该示例，请按照下列步骤：  
  
1.  创建新的 Windows 窗体应用程序。  
  
2.  将示例代码添加到窗体。  
  
3.  创建窗体的一个处理程序<xref:System.Windows.Forms.Control.Paint>事件  
  
4.  在中<xref:System.Windows.Forms.Control.Paint>处理程序，请调用`GetThumbnail`方法并传入`e`为<xref:System.Windows.Forms.PaintEventArgs>。  
  
5.  找到你想要的缩略图图像文件。  
  
6.  在`GetThumbnail`方法中，指定的路径和文件到你的映像的名称。  
  
7.  按 F5 以运行该示例。  
  
     100 的 100 缩略图显示在窗体。  
  
## <a name="see-also"></a>请参阅
- [图像、位图和图元文件](images-bitmaps-and-metafiles.md)
- [使用图像、位图、图标和图元文件](working-with-images-bitmaps-icons-and-metafiles.md)
