---
title: 如何：使用系统画笔绘制区域
ms.date: 03/30/2017
helpviewer_keywords:
- system brushes [WPF], painting with
- painting [WPF], with system brushes
- brushes [WPF], painting with system brushes [WPF]
ms.assetid: 5141a763-9235-42cb-a6bb-afc75513eac7
ms.openlocfilehash: 7beaf4370f115a3995c9ca23bb0022bd5b269193
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57364107"
---
# <a name="how-to-paint-an-area-with-a-system-brush"></a>如何：使用系统画笔绘制区域
<xref:System.Windows.SystemColors>类提供了访问系统画笔和颜色，如<xref:System.Windows.SystemColors.ControlBrush%2A>， <xref:System.Windows.SystemColors.ControlBrushKey%2A>，和<xref:System.Windows.SystemColors.DesktopBrush%2A>。 系统画笔是<xref:System.Windows.Media.SolidColorBrush>对象，它使用指定的系统颜色绘制区域。 系统画笔总是生成纯色填充，它不能用于创建渐变。  
  
 可以将系统画笔用作静态资源，也可以用作动态资源。 如果希望在应用程序运行期间画笔自动进行更新（当用户更改系统画笔时），请使用动态资源；否则请使用静态资源。 SystemColors 类包含大量静态属性，这些属性严格遵循命名约定：  
  
-   *\<SystemColor>* Brush  
  
     获取对的静态引用<xref:System.Windows.Media.SolidColorBrush>指定的系统颜色。  
  
-   *\<SystemColor>* BrushKey  
  
     获取到的动态引用<xref:System.Windows.Media.SolidColorBrush>指定的系统颜色。  
  
-   *\<SystemColor>* Color  
  
     获取对的静态引用<xref:System.Windows.Media.Color>指定的系统颜色的结构。  
  
-   *\<SystemColor>* ColorKey  
  
     获取到的动态引用<xref:System.Windows.Media.Color>指定的系统颜色的结构。  
  
 系统颜色是<xref:System.Windows.Media.Color>结构，它可用于配置画笔。 例如，可以创建通过设置使用系统颜色的渐变<xref:System.Windows.Media.GradientStop.Color%2A>的属性<xref:System.Windows.Media.LinearGradientBrush>对象的使用系统颜色的渐变停止点。 有关示例，请参阅[渐变中使用系统颜色](how-to-use-system-colors-in-a-gradient.md)。  
  
## <a name="example"></a>示例  
 以下示例使用动态系统画笔引用来设置按钮的背景。  
  
 [!code-xaml[brushsamples_snip#GraphicsMMDynamicSystemColorDesktopBrushKeyExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/DynamicSystemBrushExample.xaml#graphicsmmdynamicsystemcolordesktopbrushkeyexamplewholepage)]  
  
 下一个示例使用静态系统画笔引用来设置按钮的背景。  
  
 [!code-xaml[brushsamples_snip#GraphicsMMStaticSystemColorDesktopBrushExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/StaticSystemBrushExample.xaml#graphicsmmstaticsystemcolordesktopbrushexamplewholepage)]  
  
 有关演示如何在渐变中使用系统颜色的示例，请参阅[渐变中使用系统颜色](how-to-use-system-colors-in-a-gradient.md)。  
  
## <a name="see-also"></a>请参阅
- [在渐变中使用系统颜色](how-to-use-system-colors-in-a-gradient.md)
- [使用纯色和渐变进行绘制概述](painting-with-solid-colors-and-gradients-overview.md)
