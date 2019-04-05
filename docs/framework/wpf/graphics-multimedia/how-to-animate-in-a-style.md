---
title: 如何在样式 (WPF) 中进行动画处理
ms.date: 03/30/2017
helpviewer_keywords:
- animation [WPF], properties [WPF], within styles
- styles [WPF], animating properties within
ms.assetid: 6a791f3d-6b1f-4972-a2f9-35880bcfd954
ms.openlocfilehash: 5fb18a2d927746c3437ec01d2a19327be373cae3
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57373954"
---
# <a name="how-to-animate-in-a-style"></a>如何在样式中进行动画处理

此示例演示如何在样式中的属性进行动画处理。 时样式中进行动画处理，可以直接针对为其定义样式的框架元素。 若要针对 freezable 对象，您必须"dot 向下"从带样式的元素的属性。

在以下示例中，在样式中定义并应用于多个动画<xref:System.Windows.Controls.Button>。 当用户将鼠标移到按钮上方时，它淡出从不透明为部分透明和后端再次、 重复。 当用户移动鼠标按钮关闭时，它将成为完全不透明。 单击该按钮，将从橙色为白色，并再次更改其背景色。 因为<xref:System.Windows.Media.SolidColorBrush>用于绘制按钮不能直接目标，从按钮的向下对访问<xref:System.Windows.Controls.Control.Background%2A>属性。

## <a name="example"></a>示例

[!code-xaml[timingbehaviors_snip#21](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/StyleStoryboardsExample.xaml#21)]

请注意，当在样式中进行动画处理，可能对不存在的目标对象。 例如，假设您的方式使用<xref:System.Windows.Media.SolidColorBrush>来设置按钮的 background 属性，但在某一时刻样式重写，并且使用设置按钮的背景<xref:System.Windows.Media.LinearGradientBrush>。  尝试进行动画处理<xref:System.Windows.Media.SolidColorBrush>不会引发异常，则动画将以静默方式失败。

有关情节提要目标语法的详细信息，请参阅[情节提要概述](storyboards-overview.md)。 有关动画的详细信息，请参阅[动画概述](animation-overview.md)。 有关样式的详细信息，请参阅[样式和模板化](../controls/styling-and-templating.md)。
