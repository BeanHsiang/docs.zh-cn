---
title: 自定义控件的绘制和呈现
ms.date: 03/30/2017
helpviewer_keywords:
- custom controls [Windows Forms], rendering
- custom controls [Windows Forms], painting
- user controls [Windows Forms], painting
ms.assetid: a09dbf76-0966-4cbf-a66a-2083ba98e068
ms.openlocfilehash: ec9002ffa4a7e2c82f59d52344764a01afe4c568
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57722134"
---
# <a name="custom-control-painting-and-rendering"></a>自定义控件的绘制和呈现
自定义绘制的控件是可轻松在.NET Framework 的许多复杂任务之一。 在创作时自定义控件，有许多种有关控件的图形外观。 如果创作继承的控件`Control`，必须提供代码，使您的控件来呈现其图形表示形式。 如果通过继承创建用户控件`UserControl`，继承或从一个 Windows 窗体控件，可以忽略在标准的图形表示形式，并提供你自己的图形代码。 如果你想要提供的构成控件的自定义呈现`UserControl`创作，你的选项变得更为有限，但仍允许范围广泛的控件和应用程序的图形化可能性。  
  
## <a name="in-this-section"></a>本节内容  
 [呈现 Windows 窗体控件](rendering-a-windows-forms-control.md)  
 演示如何编写显示一个控件的逻辑。  
  
 [用户绘制的控件](user-drawn-controls.md)  
 概述在编写和重写为您的控件的呈现代码中所涉及的步骤。  
  
 [构成控件](constituent-controls.md)  
 介绍如何在你的用户控件和窗体中实现的构成控件的自定义呈现代码。  
  
 [如何：使控件在运行时不可见](how-to-make-your-control-invisible-at-run-time.md)  
 演示如何使用<xref:System.Windows.Forms.Control.Visible%2A>隐藏和显示控件的属性。  
  
 [如何：使控件拥有透明背景](how-to-give-your-control-a-transparent-background.md)  
 演示如何使用<xref:System.Windows.Forms.Control.SetStyle%2A>方法来创建不透明、 透明或部分透明的背景颜色。  
  
 [使用视觉样式呈现控件](rendering-controls-with-visual-styles.md)  
 演示如何呈现支持它们的操作系统中使用视觉样式的控件。  
  
## <a name="reference"></a>参考  
 <xref:System.Windows.Forms.Control>  
 对此类进行描述，并提供指向其所有成员的链接。  
  
 <xref:System.Windows.Forms.UserControl>  
 对此类进行描述，并提供指向其所有成员的链接。  
  
 <xref:System.Windows.Forms.Control.OnPaint%2A>  
 介绍了此方法。  
  
## <a name="related-sections"></a>相关章节  
 [如何：创建用于绘制图形对象](../advanced/how-to-create-graphics-objects-for-drawing.md)  
 引入了[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)]从 Visual Studio 角度来看，并提供链接的详细信息的图形功能。  
  
 [各种自定义控件](varieties-of-custom-controls.md)  
 描述可以创作自定义控件的类型。
