---
title: 使用图形容器
ms.date: 03/30/2017
helpviewer_keywords:
- graphics [Windows Forms], using containers
- graphics containers
- examples [Windows Forms], graphics containers
ms.assetid: 74632f91-cefa-4f51-ab7c-f9ac91942caf
ms.openlocfilehash: cfad7254057a31ea8268784cd4b6849850f3e2aa
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57704458"
---
# <a name="using-graphics-containers"></a>使用图形容器
一个<xref:System.Drawing.Graphics>对象提供的方法，如<xref:System.Drawing.Graphics.DrawLine%2A>， <xref:System.Drawing.Graphics.DrawImage%2A>，和<xref:System.Drawing.Graphics.DrawString%2A>用于显示矢量图像、 光栅图像和文本。 一个<xref:System.Drawing.Graphics>对象还具有影响的质量和方向绘制的项的多个属性。 例如，平滑的模式属性确定是否抗锯齿应用于直线和曲线和世界变换属性影响的位置和旋转绘制的项。  
  
 一个<xref:System.Drawing.Graphics>对象是与特定显示设备相关联。 当你使用<xref:System.Drawing.Graphics>对象中要在窗口中，绘制<xref:System.Drawing.Graphics>对象也是与该特定窗口相关联。  
  
 一个<xref:System.Drawing.Graphics>对象可以被认为是作为容器因为它包含一组影响绘图的属性和链接到特定于设备的信息。 可以创建第二个容器中的现有<xref:System.Drawing.Graphics>对象通过调用<xref:System.Drawing.Graphics.BeginContainer%2A>方法的<xref:System.Drawing.Graphics>对象。  
  
## <a name="in-this-section"></a>本节内容  
 [管理图形对象的状态](managing-the-state-of-a-graphics-object.md)  
 介绍如何管理质量设置、 剪辑区域和转换的<xref:System.Drawing.Graphics>对象。  
  
 [使用嵌套的图形容器](using-nested-graphics-containers.md)  
 演示如何使用容器来控制的状态<xref:System.Drawing.Graphics>对象。
