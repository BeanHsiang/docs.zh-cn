---
title: Windows 窗体中的图形和绘制
ms.date: 03/30/2017
helpviewer_keywords:
- graphics [Windows Forms]
- graphics [Windows Forms], using in Windows Forms
- GDI+, using in managed code
- drawing [Windows Forms]
ms.assetid: 362532c5-1a06-4257-bdc8-723461009ede
ms.openlocfilehash: 08f87436ade62bb54295b012a1c24dc177ea9667
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57705413"
---
# <a name="graphics-and-drawing-in-windows-forms"></a>Windows 窗体中的图形和绘制
公共语言运行时使用名为 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 的 Windows 图形设备接口的高级实现 ([!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)]) 。 通过 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)]，你可以创建图形、绘制文本以及将图形图像作为对象进行操作。 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 旨在提供良好性能和易用性。 可以使用 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 来呈现 Windows 窗体和控件上的图形图像。 虽然不能直接在 Web 窗体上使用 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)]，但可通过图像 Web 服务器控件显示图形图像。  
  
 在本节中，你会发现介绍 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 编程基础知识的主题。 本节虽非全面的参考，但涵盖有关 <xref:System.Drawing.Graphics>、<xref:System.Drawing.Pen>、<xref:System.Drawing.Brush> 和 <xref:System.Drawing.Color> 对象的信息，并介绍了如何执行绘制形状、绘制文本或显示图像等任务。 有关详细信息，请参阅[GDI + 参考](/windows/desktop/gdiplus/-gdiplus-class-gdi-reference)。  
  
 若要立即开始，请参阅[图形编程入门](getting-started-with-graphics-programming.md)。 其中包含如何使用代码在 Windows 窗体上绘制线、形状和文本等相关主题。  
  
## <a name="in-this-section"></a>本节内容  
 [图形概述](graphics-overview-windows-forms.md)  
 介绍与与图形相关的托管类。  
  
 [关于 GDI+ 托管代码](about-gdi-managed-code.md)  
 提供有关托管 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 类的信息。  
  
 [使用托管图形类](using-managed-graphics-classes.md)  
 演示如何使用 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 托管类完成各种任务。  
  
## <a name="reference"></a>参考  
 <xref:System.Drawing>  
 提供对 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 基本图形功能的访问权限。  
  
 <xref:System.Drawing.Drawing2D>  
 提供高级二维和矢量图形功能。  
  
 <xref:System.Drawing.Imaging>  
 提供高级 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 图像处理功能。  
  
 <xref:System.Drawing.Text>  
 提供高级 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 板式功能。 此命名空间中的类可用于创建和使用字体集合。  
  
 <xref:System.Drawing.Printing>  
 提供打印功能。  
  
## <a name="related-sections"></a>相关章节  
 [自定义控件的绘制和呈现](../controls/custom-control-painting-and-rendering.md)  
 详细介绍如何为绘制控件提供代码。
