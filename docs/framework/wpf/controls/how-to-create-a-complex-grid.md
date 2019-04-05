---
title: 如何创建复杂网格
description: 有关如何使用网格控件来创建布局的示例，看起来像每月的日历。
ms.date: 03/30/2017
helpviewer_keywords:
- calendar [WPF], creating
- monthly calendar [WPF], creating
- Grid control [WPF], creating [WPF], complex grid
ms.assetid: 4ce3040a-a156-4364-9596-98ca1eca5550
ms.openlocfilehash: dd17dfeea85e2b404f7a284f93faceec63145b1f
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57355008"
---
# <a name="how-to-create-a-complex-grid"></a>如何创建复杂网格

此示例演示如何使用<xref:System.Windows.Controls.Grid>控件来创建布局看起来像每月的日历。

## <a name="example"></a>示例

下面的示例通过定义八个行和八个列<xref:System.Windows.Controls.RowDefinition>和<xref:System.Windows.Controls.ColumnDefinition>类。 它使用<xref:System.Windows.Controls.Grid.ColumnSpan%2A?displayProperty=nameWithType>并<xref:System.Windows.Controls.Grid.RowSpan%2A?displayProperty=nameWithType>一起使用的附加属性，<xref:System.Windows.Shapes.Rectangle>填充各种列和行的背景的元素。 这种设计是可能的因为多个元素可以存在于每个单元格中<xref:System.Windows.Controls.Grid>的主要区别<xref:System.Windows.Controls.Grid>和<xref:System.Windows.Documents.Table>。

该示例使用垂直渐变来<xref:System.Windows.Shapes.Shape.Fill%2A>列和行，以改进的可视化展示和日历的可读性。 样式<xref:System.Windows.Controls.TextBlock>元素表示的日期和星期数。 <xref:System.Windows.Controls.TextBlock> 元素绝对定位在其单元格内使用<xref:System.Windows.FrameworkElement.Margin%2A>属性和应用程序的样式中定义的对齐方式属性。

[!code-xaml[GridComplex#1](~/samples/snippets/csharp/VS_Snippets_Wpf/GridComplex/CS/default.xaml#1)]

下图显示了生成的控件，可自定义日历：

![生成的控件的屏幕截图](././media/how-to-create-a-complex-grid/wpf-manual-calendar.png)

## <a name="see-also"></a>请参阅

- <xref:System.Windows.Controls.Grid?displayProperty=nameWithType>
- <xref:System.Windows.Documents.TableCell?displayProperty=nameWithType>
- [使用纯色和渐变进行绘制概述](../graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)
- [面板概述](panels-overview.md)
- [表概述](../advanced/table-overview.md)