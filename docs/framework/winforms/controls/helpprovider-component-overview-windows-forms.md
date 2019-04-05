---
title: HelpProvider 组件概述（Windows 窗体）
ms.date: 03/30/2017
f1_keywords:
- HelpProvider
helpviewer_keywords:
- HelpProvider component [Windows Forms], about HelpProvider component
- Help [Windows Forms], adding to Windows applications
- F1 Help [Windows Forms], adding to Windows Forms
- dialog boxes [Windows Forms], context-sensitive Help
- Windows Forms, context-sensitive Help
ms.assetid: 6b10c2cc-c577-4cb5-9669-e37b33416af9
ms.openlocfilehash: f9cf0c165c6c64186eff53676c8b1b06f74361fc
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57708374"
---
# <a name="helpprovider-component-overview-windows-forms"></a>HelpProvider 组件概述（Windows 窗体）
Windows 窗体[HelpProvider](helpprovider-component-windows-forms.md)组件用于将 HTML Help 1.x 帮助文件 （.chm 文件，使用 HTML Help Workshop 生成或.htm 文件） 与 Windows 应用程序相关联。 你可以提供多种方式帮助：  
  
-   为 Windows 窗体上控件提供上下文相关帮助。  
  
-   提供特定对话框或出现在对话框中的特定控件的上下文相关帮助。  
  
-   打开帮助文件的特定区域，如表的内容、 索引或搜索功能的主页。  
  
## <a name="using-the-help-provider"></a>使用帮助提供程序  
 添加<xref:System.Windows.Forms.HelpProvider>向 Windows 窗体组件允许要公开的帮助属性的窗体上的其他控件<xref:System.Windows.Forms.HelpProvider>组件。 这使您可以在 Windows 窗体上的控件提供帮助。 可以将帮助文件与相关联<xref:System.Windows.Forms.HelpProvider>组件使用<xref:System.Windows.Forms.HelpProvider.HelpNamespace%2A>属性。 指定通过调用提供的帮助类型<xref:System.Windows.Forms.HelpProvider.SetHelpNavigator%2A>提供的值和<xref:System.Windows.Forms.HelpNavigator>枚举为指定的控件。 你提供的关键字或主题的帮助通过调用<xref:System.Windows.Forms.HelpProvider.SetHelpKeyword%2A>方法。  
  
 （可选） 若要将特定的帮助字符串与另一个控件相关联，请使用<xref:System.Windows.Forms.HelpProvider.SetHelpString%2A>方法。 在用户按 F1 键在控件有焦点时，您将使用此方法的控件相关联的字符串显示弹出窗口中。  
  
 如果<xref:System.Windows.Forms.HelpProvider.HelpNamespace%2A>尚未设置，必须使用<xref:System.Windows.Forms.HelpProvider.SetHelpString%2A>来提供帮助文本。 如果同时设置了<xref:System.Windows.Forms.HelpProvider.HelpNamespace%2A>和帮助字符串，帮助根据<xref:System.Windows.Forms.HelpProvider.HelpNamespace%2A>将优先。  
  
> [!NOTE]
>  您可能会遇到问题时指定的路径中的帮助文件，使用相对路径<xref:System.Windows.Forms.Help.ShowHelp%2A>方法或<xref:System.Windows.Forms.HelpProvider.HelpNamespace%2A>属性的<xref:System.Windows.Forms.HelpProvider>控件。 在这种情况下，请务必使用绝对文件路径来指定帮助文件。  
  
## <a name="see-also"></a>请参阅
- [Windows 窗体应用程序中的帮助系统](../advanced/help-systems-in-windows-forms-applications.md)
