---
title: 如何：获取应用程序中的所有 Windows
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- window objects [WPF], getting
ms.assetid: f120f06e-993b-4a97-9657-af0d1986981f
ms.openlocfilehash: 34316f0c6f81b960a8e00131a30b9a237b9ca938
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57378808"
---
# <a name="how-to-get-all-windows-in-an-application"></a>如何：获取应用程序中的所有 Windows
此示例演示如何获取所有<xref:System.Windows.Window>应用程序中的对象。  
  
## <a name="example"></a>示例  
 每个实例化<xref:System.Windows.Window>对象是否可见或不是，自动添加到由管理的窗口中引用的集合<xref:System.Windows.Application>，并公开从<xref:System.Windows.Application.Windows%2A>。  
  
 您可以枚举<xref:System.Windows.Application.Windows%2A>若要获取所有实例化的窗口使用以下代码：  
  
 [!code-csharp[HOWTOWindowManagementSnippets#GetAllWindows](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTOWindowManagementSnippets/CSharp/CustomWindow.xaml.cs#getallwindows)]
 [!code-vb[HOWTOWindowManagementSnippets#GetAllWindows](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTOWindowManagementSnippets/visualbasic/customwindow.xaml.vb#getallwindows)]
