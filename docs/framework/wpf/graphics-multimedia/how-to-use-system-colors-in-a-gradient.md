---
title: 如何：在渐变中使用系统颜色
ms.date: 03/30/2017
helpviewer_keywords:
- gradients [WPF], system colors in
- system colors in gradients [WPF]
ms.assetid: 11942e7e-6300-4b50-8ed1-f50e8d20e7d2
ms.openlocfilehash: 3148a5901ccf64194717e26664ab8b9cbd57db2a
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57365953"
---
# <a name="how-to-use-system-colors-in-a-gradient"></a>如何：在渐变中使用系统颜色
若要在渐变中使用系统颜色，请使用 *\<SystemColor >* 颜色和 *\<SystemColor >* ColorKey 静态属性<xref:System.Windows.SystemColors>类来获取对颜色，引用其中 *\<SystemColor >* 是所需的系统颜色的名称。 使用 *\<SystemColor >* ColorKey 属性时想要创建的动态引用，随着系统主题变化而自动更新。 否则，请使用 *\<SystemColor >* Color 属性。  
  
## <a name="example"></a>示例  
 以下示例使用动态系统颜色资源创建渐变。  
  
 [!code-xaml[brushsamples_snip#GraphicsMMDynamicSystemColorGradientExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/DynamicSystemColorExample.xaml#graphicsmmdynamicsystemcolorgradientexamplewholepage)]  
  
 下一个示例使用静态系统颜色资源创建渐变。  
  
 [!code-xaml[brushsamples_snip#GraphicsMMStaticSystemColorGradientExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/StaticSystemColorExample.xaml#graphicsmmstaticsystemcolorgradientexamplewholepage)]  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.SystemColors>
- [使用系统画笔绘制区域](how-to-paint-an-area-with-a-system-brush.md)
- [使用纯色和渐变进行绘制概述](painting-with-solid-colors-and-gradients-overview.md)
