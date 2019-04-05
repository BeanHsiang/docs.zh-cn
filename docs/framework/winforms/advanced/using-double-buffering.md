---
title: 使用双缓冲
ms.date: 03/30/2017
helpviewer_keywords:
- graphics [Windows Forms], double buffering
- double buffering
- flicker [Windows Forms], reducing in Windows Forms
- buffering [Windows Forms], double buffering
ms.assetid: dc484e33-7101-4e4b-ada5-d3c96155fbcd
ms.openlocfilehash: ac6c9b7f2cc1fea86a75eaaf4a2dde1ea60e4f40
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57716267"
---
# <a name="using-double-buffering"></a>使用双缓冲
可以使用双缓冲的图形以包含复杂画图操作在应用程序中减少闪烁。 .NET Framework 包含的双缓冲的内置支持，也可以管理并手动呈现图形。  
  
## <a name="in-this-section"></a>本节内容  
 [双缓冲的图形](double-buffered-graphics.md)  
 引入了双缓冲的概念，并概述了.NET Framework 支持。  
  
 [如何：减少对窗体和控件使用双缓冲图形闪烁](how-to-reduce-graphics-flicker-with-double-buffering-for-forms-and-controls.md)  
 演示如何使用默认双缓冲支持.NET Framework 中。  
  
 [如何：手动管理缓冲的图形](how-to-manually-manage-buffered-graphics.md)  
 演示如何管理应用程序中的双缓冲。  
  
 [如何：手动呈现缓冲的图形](how-to-manually-render-buffered-graphics.md)  
 演示如何呈现双缓冲的图形。  
  
## <a name="reference"></a>参考  
 <xref:System.Windows.Forms.Control.SetStyle%2A> ,  
 启用双缓冲的控制方法。  
  
 <xref:System.Drawing.BufferedGraphicsContext> ,  
 提供用于创建图形缓冲区的方法。  
  
 <xref:System.Drawing.BufferedGraphicsManager>  
 提供对缓冲的图形上下文为应用程序域的访问。
