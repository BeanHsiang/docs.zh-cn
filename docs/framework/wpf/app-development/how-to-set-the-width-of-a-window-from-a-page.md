---
title: 如何：设置页面窗口宽度
ms.date: 03/30/2017
helpviewer_keywords:
- width of windows [WPF], setting from a page
- windows [WPF], setting width from a page
- pages [WPF], setting window width from
ms.assetid: 31601c92-7889-472a-b07e-bf675ad21c92
ms.openlocfilehash: fee6d4c9ae9dae03e81cc4be56576763cb59958b
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57379349"
---
# <a name="how-to-set-the-width-of-a-window-from-a-page"></a>如何：设置页面窗口宽度
此示例说明了如何设置从窗口的宽度<xref:System.Windows.Controls.Page>。  
  
## <a name="example"></a>示例  
 一个<xref:System.Windows.Controls.Page>通过设置可设置及其主机窗口的宽度<xref:System.Windows.Controls.Page.WindowWidth%2A>。 此属性允许<xref:System.Windows.Controls.Page>以不显式了解承载它的窗口的类型。  
  
> [!NOTE]
>  若要设置的窗口使用宽度<xref:System.Windows.Controls.Page.WindowWidth%2A>、<xref:System.Windows.Controls.Page>必须是一个窗口的子级。  
  
 [!code-xaml[HOWTONavigationSnippets#SetPageWindowWidthXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTONavigationSnippets/CSharp/SetWindowWidthPage.xaml#setpagewindowwidthxaml)]
