---
title: 如何：实现依赖项属性
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- dependency properties [WPF], backing properties with
- properties [WPF], backing with dependency properties
ms.assetid: 855fd6d7-19ac-493c-bf5e-2f40b57cdc92
ms.openlocfilehash: 8ee944c521b7e4ec75394c821e8bd509dd4eca74
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57374409"
---
# <a name="how-to-implement-a-dependency-property"></a>如何：实现依赖项属性
此示例演示如何重新[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)]具有属性<xref:System.Windows.DependencyProperty>字段，从而定义依赖项属性。 定义自己的属性并需要其支持 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 功能的诸多方面（包括样式、数据绑定、继承、动画和默认值）时，应将其作为依赖属性实现。  
  
## <a name="example"></a>示例  
 下面的示例第一次注册依赖属性通过调用<xref:System.Windows.DependencyProperty.Register%2A>方法。 用于存储名称，并且必须依赖项属性的特征的标识符字段的名称<xref:System.Windows.DependencyProperty.Name%2A>作为的一部分为依赖属性选择了<xref:System.Windows.DependencyProperty.Register%2A>调用中，文字字符串由追加`Property`。 例如，如果你注册具有的依赖关系属性<xref:System.Windows.DependencyProperty.Name%2A>的`Location`，则定义的依赖项属性标识符字段必须命名为`LocationProperty`。  
  
 在此示例中，依赖项属性的名称并将其[!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)]访问器已`State`; 标识符字段`StateProperty`; 属性的类型是<xref:System.Boolean>; 注册依赖属性的类型是`MyStateControl`。  
  
 如果不遵循此命名模式，则设计器可能无法正确地报告属性，而且属性系统样式应用程序的某些方面可能不会以预期的方式工作。  
  
 还可为依赖属性指定默认元数据。 此示例将 `State` 依赖属性的默认值注册为 `false`。  
  
 [!code-csharp[PropertySystemEsoterics#MyStateControl](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertySystemEsoterics/CSharp/SDKSampleLibrary/class1.cs#mystatecontrol)]
 [!code-vb[PropertySystemEsoterics#MyStateControl](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertySystemEsoterics/visualbasic/sdksamplelibrary/class1.vb#mystatecontrol)]  
  
 若要深入了解实现依赖属性而非仅使用私有字段支持 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 属性的原因及其实现方式，请参阅[依赖属性概述](dependency-properties-overview.md)。  
  
## <a name="see-also"></a>请参阅
- [依赖项属性概述](dependency-properties-overview.md)
- [帮助主题](properties-how-to-topics.md)
