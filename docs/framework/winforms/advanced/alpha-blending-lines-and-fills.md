---
title: Alpha 混合线条和填充
ms.date: 03/30/2017
helpviewer_keywords:
- lines [Windows Forms], adding transparency
- examples [Windows Forms], alpha blending
- alpha blending [Windows Forms], using with lines
- alpha blending
- lines [Windows Forms], alpha blending
- fills [Windows Forms], alpha blending
- alpha blending [Windows Forms], using with fills
- shapes [Windows Forms], adding transparency
ms.assetid: 5440f48c-3ac9-44c3-b170-c1c110bdbab8
ms.openlocfilehash: 7a8286fb741effaf668b87e90da04f79d1490de2
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57715992"
---
# <a name="alpha-blending-lines-and-fills"></a>Alpha 混合线条和填充
在[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)]，一种颜色为具有各 8 位 alpha、 红色、 绿色和蓝色的 32 位值。 Alpha 值表示颜色的透明度，向其颜色与背景色混合的范围。 从 0 到 255，其中 0 表示完全透明的颜色，到 255 的 alpha 值范围表示完全不透明的颜色。  
  
 Alpha 值混合处理是由像素值混合处理的数据源和背景颜色数据。 根据以下公式的背景色的对应分量与混合每个给定的源颜色的三个组件 （红色、 绿色、 蓝色）：  
  
 displayColor = sourceColor × alpha / 255 + backgroundColor × (255-alpha) / 255  
  
 例如，假设源颜色中的红色分量为 150，背景颜色中的红色分量为 100。 如果 alpha 值为 200，合成的颜色中红色分量的计算方式如下：  
  
 150 × 200 / 255 + 100 × (255 – 200) / 255 = 139  
  
## <a name="in-this-section"></a>本节内容  
 [如何：绘制不透明和半透明的线条](how-to-draw-opaque-and-semitransparent-lines.md)  
 演示如何绘制 alpha 混合线条。  
  
 [如何：用不透明和半透明的画笔绘制](how-to-draw-with-opaque-and-semitransparent-brushes.md)  
 介绍如何使用画笔的 alpha 混合。  
  
 [如何：使用复合模式控制 Alpha 值混合处理](how-to-use-compositing-mode-to-control-alpha-blending.md)  
 描述如何控制 alpha 混合使用<xref:System.Drawing.Drawing2D.CompositingMode>。  
  
 [如何：使用颜色矩阵在图像中设置 Alpha 值](how-to-use-a-color-matrix-to-set-alpha-values-in-images.md)  
 说明如何使用<xref:System.Drawing.Imaging.ColorMatrix>对象以控制 alpha 值混合处理。
