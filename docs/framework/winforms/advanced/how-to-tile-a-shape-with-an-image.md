---
title: 如何：使用图像形状中平铺
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- texture brushes [Windows Forms], tiling images with
- images [Windows Forms], filling shapes with
- shapes [Windows Forms], tiling with images
- bitmaps [Windows Forms], filling shapes with
ms.assetid: 6d407891-6e5c-4495-a546-3da5604e9fb8
ms.openlocfilehash: d873ba717fa94852692ce395ef7da30c512aba59
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57719684"
---
# <a name="how-to-tile-a-shape-with-an-image"></a>如何：使用图像形状中平铺
就像可以彼此以涵盖地板放置磁贴，可以将矩形图像彼此放置于填充 （磁贴） 形状。 若要磁贴形状的内部，使用纹理画笔。 当构造<xref:System.Drawing.TextureBrush>对象，将传递给构造函数的自变量之一为<xref:System.Drawing.Image>对象。 纹理画笔用于绘制形状的内部，当填充形状与此图像的重复副本。  
  
 自动换行模式属性的<xref:System.Drawing.TextureBrush>对象将决定如何图像的方向为矩形网格中重复。 您可以进行所有网格中的磁贴具有相同的方向，或者可以进行到下一个网格位置从翻转的图像。 翻转可以水平、 垂直，或两者。 下面的示例演示使用不同类型的翻转平铺。  
  
### <a name="to-tile-an-image"></a>平铺图像  
  
-   此示例使用以下 75 × 75 映像磁贴 200 × 200 的矩形。  
  
 ![磁贴 1](./media/tile1.gif "tile1")  
  
-   下图显示如何使用图像平铺矩形。 请注意，所有磁贴具有相同方向;没有翻转。  
  
 ![磁贴 2](./media/tile2.gif "tile2")  
  
 [!code-csharp[System.Drawing.UsingABrush#31](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingABrush/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.UsingABrush#31](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingABrush/VB/Class1.vb#31)]  
  
### <a name="to-flip-an-image-horizontally-while-tiling"></a>若要水平时平铺翻转图像  
  
-   此示例使用相同 75 × 75 图像以填充 200 × 200 的矩形。 自动换行模式设置为水平翻转图像。 下图显示如何使用图像平铺矩形。 请注意当您从一个磁贴移动到下一个给定行中，水平翻转图像。  
  
 ![磁贴 3](./media/tile3.gif "tile3")  
  
 [!code-csharp[System.Drawing.UsingABrush#32](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingABrush/CS/Class1.cs#32)]
 [!code-vb[System.Drawing.UsingABrush#32](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingABrush/VB/Class1.vb#32)]  
  
### <a name="to-flip-an-image-vertically-while-tiling"></a>若要垂直时平铺翻转图像  
  
-   此示例使用相同 75 × 75 图像以填充 200 × 200 的矩形。 设置环绕模式为垂直翻转图像。  
  
     [!code-csharp[System.Drawing.UsingABrush#33](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingABrush/CS/Class1.cs#33)]
     [!code-vb[System.Drawing.UsingABrush#33](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingABrush/VB/Class1.vb#33)]  
  
### <a name="to-flip-an-image-horizontally-and-vertically-while-tiling"></a>平铺时水平和垂直翻转图像  
  
-   此示例使用相同的 75 × 75 映像磁贴 200 × 200 的矩形。 自动换行模式设置为水平和垂直翻转图像。 下图显示该矩形的映像的平铺。 请注意当您从一个磁贴移动到下一个给定行中，水平翻转图像和当您从一个磁贴移动到下一个给定列中，垂直翻转图像。  
  
 ![磁贴 5](./media/tile5.gif "tile5")  
  
 [!code-csharp[System.Drawing.UsingABrush#34](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingABrush/CS/Class1.cs#34)]
 [!code-vb[System.Drawing.UsingABrush#34](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingABrush/VB/Class1.vb#34)]  
  
## <a name="see-also"></a>请参阅
- [使用画笔填充形状](using-a-brush-to-fill-shapes.md)
