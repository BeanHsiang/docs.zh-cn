---
title: 编码和 Windows 窗体全球化
ms.date: 03/30/2017
helpviewer_keywords:
- ListView control [Windows Forms], lack of Unicode support
- DateTimePicker control [Windows Forms], lack of Unicode support
- TrackBar control [Windows Forms], lack of Unicode support
- ImageList component [Windows Forms], lack of Unicode support
- Unicode [Windows Forms]
- ToolBar control [Windows Forms], lack of Unicode support
- international applications [Windows Forms], character display
- StatusBar control [Windows Forms], lack of Unicode support
- MonthCalendar control [Windows Forms], lack of Unicode support
- international characters
- TabControl control [Windows Forms], lack of Unicode support
- Windows Forms, encoding
- TreeView control [Windows Forms], lack of Unicode support
- ProgressBar control [Windows Forms], Unicode-enabled forms
- localization [Windows Forms], character sets
- globalization [Windows Forms], character sets
ms.assetid: 22e8965d-a712-42b3-8167-3ee346bd70f9
ms.openlocfilehash: 3a9d891fe898cf691a5f0d36e6360c2a73fb199d
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54629223"
---
# <a name="encoding-and-windows-forms-globalization"></a>编码和 Windows 窗体全球化
Windows 窗体应用程序完全支持 Unicode，这意味着每个字符都用唯一编号表示，无论何种平台、程序或语音都是如此。 有关 Unicode 的详细信息，请参阅[Unicode 联盟网站](https://www.unicode.org)。  
  
## <a name="benefits-of-unicode"></a>Unicode 的优点  
 启用 Unicode 的窗体的优点包括，能够处理仅限 Unicode（例如印地语）的脚本。 此外，还可以在单个窗体上使用多种语言。 以 Unicode 格式，所有字符都是两个字节长，所以不需要执行任何特殊操作来表示双字节字符。 还可以编写可在所有平台上工作的单个代码集。 这是从早期版本的 Visual Basic 中，您不得不编写针对不同平台，例如 Windows NT 不同的代码更改和[!INCLUDE[win98](../../../../includes/win98-md.md)]。  
  
 但是，某些控件不支持在 [!INCLUDE[win98](../../../../includes/win98-md.md)] 和 Windows Millennium Edition 中启用 Unicode。 全部继承自公共控件的这些控件将使用 Windows 代码页（例如 [!INCLUDE[vcpransi](../../../../includes/vcpransi-md.md)]）处理数据。 这些控件包括：<xref:System.Windows.Forms.TabControl>、<xref:System.Windows.Forms.ListView>、<xref:System.Windows.Forms.TreeView>、<xref:System.Windows.Forms.DateTimePicker>、<xref:System.Windows.Forms.MonthCalendar>、<xref:System.Windows.Forms.TrackBar>、<xref:System.Windows.Forms.ProgressBar>、<xref:System.Windows.Forms.ImageList>、<xref:System.Windows.Forms.ToolBar> 和 <xref:System.Windows.Forms.StatusBar>。 因此，不能在列出的平台上的这些控件中显示 Unicode 数据。 例如，不能在英语版 [!INCLUDE[win98](../../../../includes/win98-md.md)] 操作系统上显示日语字符。  
  
 对于 <xref:System.Windows.Forms.ToolBar> 和 <xref:System.Windows.Forms.StatusBar> 控件具有 Unicode 意识的替代项，可使用 <xref:System.Windows.Forms.ToolStrip> 和 <xref:System.Windows.Forms.StatusStrip> 控件替换这些旧控件。 要想维护应用程序中各可视化元素之间的外观和感觉，可使用用于呈现菜单的 <xref:System.Windows.Forms.MenuStrip> 控件代替 <xref:System.Windows.Forms.MainMenu>。 正如 <xref:System.Windows.Forms.ToolStrip> 和 <xref:System.Windows.Forms.StatusStrip> 一样，<xref:System.Windows.Forms.MenuStrip> 还可以处理和显示 Unicode 字符。  
  
## <a name="see-also"></a>请参阅

- [全球化 Windows 窗体应用程序](globalizing-windows-forms.md)
