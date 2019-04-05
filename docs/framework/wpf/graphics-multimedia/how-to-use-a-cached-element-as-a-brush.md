---
title: 如何：缓存的元素用作画笔
ms.date: 03/30/2017
helpviewer_keywords:
- BitmapCache [WPF], using
- cached element [WPF], use as a brush
- BitmapCacheBrush [WPF], using
- CacheMode [WPF], using
ms.assetid: d36e944a-866e-4baf-98c4-fd6a75f6fdd0
ms.openlocfilehash: 008bec87390a807ae2b4797af8b86aaf59c92ef5
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57372485"
---
# <a name="how-to-use-a-cached-element-as-a-brush"></a>如何：缓存的元素用作画笔
使用<xref:System.Windows.Media.BitmapCacheBrush>类，以有效地重复使用缓存的元素。 若要缓存的元素，创建的新实例<xref:System.Windows.Media.BitmapCache>类，并将其分配给元素的<xref:System.Windows.UIElement.CacheMode%2A>属性。  
  
## <a name="example"></a>示例  
 下面的代码示例显示如何重复使用缓存的元素。 缓存的元素是<xref:System.Windows.Controls.Image>控件，用于显示大图像。 <xref:System.Windows.Controls.Image>控件通过使用缓存作为位图<xref:System.Windows.Media.BitmapCache>类，并在缓存重新分配到使用<xref:System.Windows.Media.BitmapCacheBrush>。 画笔分配到 25 个按钮的背景以显示有效重用。  
  
 [!code-xaml[System.Windows.Media.BitmapCacheBrush#_BitmapCacheBrushXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/system.windows.media.bitmapcachebrush/cs/window1.xaml#_bitmapcachebrushxaml)]  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Media.BitmapCache>
- <xref:System.Windows.Media.BitmapCacheBrush>
- <xref:System.Windows.UIElement.CacheMode%2A>
- [如何：改善呈现性能，通过缓存元素](how-to-improve-rendering-performance-by-caching-an-element.md)
