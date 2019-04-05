---
title: 如何：为依赖项属性添加所有者类型
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- classes [WPF], adding as owners of dependency properties
- dependency properties [WPF], adding classes as owners of
ms.assetid: edcce050-0576-4edb-a31a-3f909637b452
ms.openlocfilehash: 03ffec87c98c88452aa8fde89c64646eaf48a8da
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57369586"
---
# <a name="how-to-add-an-owner-type-for-a-dependency-property"></a>如何：为依赖项属性添加所有者类型
此示例演示如何将类添加为所有者为不同类型注册依赖属性。 通过执行此操作，请[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)][!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]读取器和属性系统都能够识别此类为附加属性的所有者。 （可选） 将添加为所有者可以选择添加类以提供特定于类型的元数据。  
  
 在以下示例中，`StateProperty`通过注册一个属性`MyStateControl`类。 该类`UnrelatedStateControl`将自身添加为所有者`StateProperty`使用<xref:System.Windows.DependencyProperty.AddOwner%2A>方法，特别使用它位于添加类型上允许进行新的依赖项属性的元数据的签名。 请注意，应提供[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)]中所示的示例类似的属性的访问器[实现依赖属性](how-to-implement-a-dependency-property.md)示例中，以及重新公开要添加的类上的依赖项属性标识符作为所有者。  
  
 未使用包装，依赖项属性仍将从以编程方式访问使用的角度来看有效<xref:System.Windows.DependencyObject.GetValue%2A>或<xref:System.Windows.DependencyObject.SetValue%2A>。 但你通常想要使用此属性系统行为的并行[!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)]属性包装器。 这些包装更加轻松地以编程方式设置依赖项属性，使其可以将设置为属性[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]属性。  
  
 若要了解如何重写默认元数据，请参阅[重写依赖属性的元数据](how-to-override-metadata-for-a-dependency-property.md)。  
  
## <a name="example"></a>示例  
 [!code-csharp[PropertySystemEsoterics#MyStateControl](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertySystemEsoterics/CSharp/SDKSampleLibrary/class1.cs#mystatecontrol)]
 [!code-vb[PropertySystemEsoterics#MyStateControl](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertySystemEsoterics/visualbasic/sdksamplelibrary/class1.vb#mystatecontrol)]  
[!code-csharp[PropertySystemEsoterics#UnrelatedStateControl](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertySystemEsoterics/CSharp/SDKSampleLibrary/class1.cs#unrelatedstatecontrol)]
[!code-vb[PropertySystemEsoterics#UnrelatedStateControl](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertySystemEsoterics/visualbasic/sdksamplelibrary/class1.vb#unrelatedstatecontrol)]  
  
## <a name="see-also"></a>请参阅
- [自定义依赖属性](custom-dependency-properties.md)
- [依赖项属性概述](dependency-properties-overview.md)
