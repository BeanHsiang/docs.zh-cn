---
title: 通过 ImeMode 属性显示亚洲字符
ms.date: 03/30/2017
helpviewer_keywords:
- Asian languages [Windows Forms], displaying with ImeMode
- Chinese characters [Windows Forms], displaying with ImeMode
- IME mode
- Japanese characters [Windows Forms], displaying with ImeMode
- international applications [Windows Forms], character display
- international characters
- Korean characters
- Asian languages
- Input Method Editor (IME), mode
- localization [Windows Forms], character sets
- globalization [Windows Forms], character sets
ms.assetid: c60ae399-0dab-4f07-9dea-6dbfb15ec0ae
ms.openlocfilehash: 25602e1a878443bd54411dfd6481581abebda5c7
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54500510"
---
# <a name="display-of-asian-characters-with-the-imemode-property"></a>通过 ImeMode 属性显示亚洲字符
<xref:System.Windows.Forms.Control.ImeMode%2A>属性用于窗体和控件的输入的法编辑器 (IME) 强制使用特定模式。 IME 是编写中文、日语和朝鲜语脚本的必备组件，因为这些编写系统具有的字符多于常规键盘可编码的字符。 例如，可能想在特定文本框中仅允许使用 ASCII 字符。 在这种情况下可以设置<xref:System.Windows.Forms.Control.ImeMode%2A>属性设置为<xref:System.Windows.Forms.ImeMode>和用户将只能为该特定文本框中输入 ASCII 字符。 默认值<xref:System.Windows.Forms.Control.ImeMode%2A>属性是<xref:System.Windows.Forms.ImeMode>，因此，如果设置窗体的属性，在窗体上的所有控件将都继承该设置。 有关详细信息，请参阅<xref:System.Windows.Forms.Control.ImeMode%2A>) 和<xref:System.Windows.Forms.ImeMode>。  
  
## <a name="see-also"></a>请参阅

- [全球化 Windows 窗体应用程序](globalizing-windows-forms.md)
