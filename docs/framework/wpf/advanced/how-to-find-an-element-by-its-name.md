---
title: 如何：按名称查找元素
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- elements [WPF], finding by name
ms.assetid: cfa7cf35-8aa2-4060-9454-872ed4af3f0e
ms.openlocfilehash: 7405f9ba8db5d4db0ce35ca250f13e456685f39b
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57351035"
---
# <a name="how-to-find-an-element-by-its-name"></a>如何：按名称查找元素
此示例介绍了如何使用<xref:System.Windows.FrameworkElement.FindName%2A>方法以按查找元素及其<xref:System.Windows.FrameworkElement.Name%2A>值。  
  
## <a name="example"></a>示例  
 在此示例中，要查找特定元素由其名称的方法编写为一个按钮的事件处理程序。 `stackPanel` 是<xref:System.Windows.FrameworkElement.Name%2A>的根<xref:System.Windows.FrameworkElement>要搜索和示例方法然后以可视方式指示找到的元素的强制转换为<xref:System.Windows.Controls.TextBlock>并更改其中一个<xref:System.Windows.Controls.TextBlock>可见[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]属性。  
  
 [!code-csharp[FEFindName#Find](~/samples/snippets/csharp/VS_Snippets_Wpf/FEFindName/CSharp/default.xaml.cs#find)]
 [!code-vb[FEFindName#Find](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FEFindName/VisualBasic/default.xaml.vb#find)]
