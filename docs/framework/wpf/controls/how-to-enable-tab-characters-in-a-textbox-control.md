---
title: 如何：在 TextBox 控件中启用制表符
ms.date: 03/30/2017
helpviewer_keywords:
- TextBox control [WPF], enabling tab characters
- tab characters [WPF], enabling
ms.assetid: 14b1b064-61f7-4958-be63-88d85b868d03
ms.openlocfilehash: 6d134757c3c08e92e608a7ff868b2f3d28a69b27
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57356541"
---
# <a name="how-to-enable-tab-characters-in-a-textbox-control"></a>如何：在 TextBox 控件中启用制表符
此示例演示如何作为正常输入中启用制表符接受<xref:System.Windows.Controls.TextBox>控件。  
  
## <a name="example"></a>示例  
 若要启用的制表符字符数的接受作为输入<xref:System.Windows.Controls.TextBox>控件，将<xref:System.Windows.Controls.Primitives.TextBoxBase.AcceptsTab%2A>归于**true**。  
  
 [!code-xaml[TextBox_EnablingTab#_AcceptsTab](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBox_EnablingTab/CS/Window1.xaml#_acceptstab)]  
  
## <a name="see-also"></a>请参阅
- [TextBox 概述](textbox-overview.md)
- [RichTextBox 概述](richtextbox-overview.md)
