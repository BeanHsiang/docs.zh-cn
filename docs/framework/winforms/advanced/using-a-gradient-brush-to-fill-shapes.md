---
title: 使用渐变画笔填充形状
ms.date: 03/30/2017
helpviewer_keywords:
- brushes [Windows Forms], gradient brushes
- gradient brushes
- examples [Windows Forms], gradient brushes
ms.assetid: 2c6037b9-05bd-44c0-a22a-19584b722524
ms.openlocfilehash: 5771aaabd283d71f5fa6934f86a1c24a57f38dca
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57704383"
---
# <a name="using-a-gradient-brush-to-fill-shapes"></a>使用渐变画笔填充形状
可以使用渐变画笔填充形状的渐变的颜色。 例如，可以使用水平渐变来逐渐更改，当您从该形状的左边缘移动到右边缘的颜色填充形状。 设想这样一个矩形是黑色的左边缘 （由红色、 绿色和蓝色分量 0，0，0） 和右边缘，它是红色 （255，0，0 表示）。 如果矩形为 256 像素宽，给定的像素的红色组件将比其左侧的像素的红色组件。 在行中的最左侧像素的颜色分量为 （0，0，0），第二个像素 （1，0，0），第三个像素都有 （2，0，0），依次类推，直到你转到最右边的像素颜色组件 （255，0，0）。 这些内插的颜色值组成的颜色渐变。  
  
 线性渐变更改颜色，当您移动水平、 垂直，或并行到指定的斜线。 路径渐变的内部和路径的边界中移动时更改颜色。 您可以自定义路径渐变来实现各种效果。  
  
 下图显示了使用线性渐变画笔填充矩形和椭圆使用路径渐变画笔填充。  
  
 ![渐变](./media/gradient2.png "gradient2")  
  
## <a name="in-this-section"></a>本节内容  
 [如何：创建线性渐变](how-to-create-a-linear-gradient.md)  
 演示如何创建线性渐变 using<xref:System.Drawing.Drawing2D.LinearGradientBrush>类。  
  
 [如何：创建路径渐变](how-to-create-a-path-gradient.md)  
 介绍如何创建路径渐变 using<xref:System.Drawing.Drawing2D.PathGradientBrush>类。  
  
 [如何：对渐变应用灰度校正](how-to-apply-gamma-correction-to-a-gradient.md)  
 介绍如何使用渐变画笔的灰度校正。  
  
## <a name="reference"></a>参考  
 <xref:System.Drawing.Drawing2D.LinearGradientBrush?displayProperty=nameWithType>  
 包含此类的说明，并提供指向其所有成员。  
  
 <xref:System.Drawing.Drawing2D.PathGradientBrush?displayProperty=nameWithType>  
 包含此类的说明，并提供指向其所有成员。
