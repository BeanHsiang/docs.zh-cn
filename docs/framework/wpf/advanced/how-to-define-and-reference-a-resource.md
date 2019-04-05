---
title: 如何：定义和引用资源
ms.date: 03/30/2017
helpviewer_keywords:
- resources [WPF], defining
- defining resources [WPF]
- resources [WPF], referencing
- referencing resources [WPF]
ms.assetid: b86b876b-0a10-489b-9a5d-581ea9b32406
ms.openlocfilehash: 80be1460906100072e6263c967c213df7968c705
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57492057"
---
# <a name="how-to-define-and-reference-a-resource"></a>如何：定义和引用资源

此示例演示如何定义资源，通过使用中的一个属性引用该[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]。

## <a name="example"></a>示例

下面的示例定义两种类型的资源：<xref:System.Windows.Media.SolidColorBrush>资源和多个<xref:System.Windows.Style>资源。 <xref:System.Windows.Media.SolidColorBrush>资源`MyBrush`用于提供多个属性的值，每个需要<xref:System.Windows.Media.Brush>键入值。 <xref:System.Windows.Style>资源`PageBackground`，`TitleText`和`Label`每个目标特定控件类型。 样式时设置的各种不同的属性上的目标控件，该样式资源引用的资源键，用于设置<xref:System.Windows.FrameworkElement.Style%2A>属性中定义的多个特定的控件元素[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]。

第一个属性的 setter 中注意`Label`样式也引用`MyBrush`前面定义的资源。 这是一种常用技术，但请务必记住，资源是分析，并输入到的资源字典中，系统将提供的顺序。 如果使用的字典中找到的顺序也请求资源[StaticResource 标记扩展](staticresource-markup-extension.md)另一个资源中引用它们。 请确保你引用的任何资源比然后请求该资源所在的资源集合中之前定义。 如果有必要，您可以解决资源引用的严格的创建顺序通过使用[DynamicResource 标记扩展](dynamicresource-markup-extension.md)相反，引用在运行时的资源，但应注意，此 DynamicResource方法对性能产生影响。 有关详细信息，请参阅[XAML 资源](xaml-resources.md)。

[!code-xaml[FEResource#XAML](~/samples/snippets/csharp/VS_Snippets_Wpf/FEResource/CS/default.xaml#xaml)]

## <a name="see-also"></a>请参阅

- [XAML 资源](xaml-resources.md)
- [样式设置和模板化](../controls/styling-and-templating.md)
