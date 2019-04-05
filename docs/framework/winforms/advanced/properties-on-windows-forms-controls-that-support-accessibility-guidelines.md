---
title: 支持辅助功能准则的 Windows 窗体控件上的属性
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Forms, accessibility properties of controls
- accessibility [Windows Forms], Windows Forms control properties
ms.assetid: ad3567a6-313b-4708-9e15-f487a831f049
ms.openlocfilehash: eee7499373809538355227633ab9a1a66aedb9ed
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57716395"
---
# <a name="properties-on-windows-forms-controls-that-support-accessibility-guidelines"></a>支持辅助功能准则的 Windows 窗体控件上的属性
标准 Windows 窗体的工具箱上的控件支持许多辅助功能准则，包括公开键盘焦点和屏幕元素。  
  
## <a name="planning-ahead-for-accessibility"></a>提前规划可访问性  
 可以使用控件的属性，以支持其他可访问性准则下, 表中所示。 此外，您应使用菜单来访问程序功能。  
  
|控件属性|有关辅助功能注意事项|  
|----------------------|--------------------------------------|  
|AccessibleDescription|说明报告给屏幕阅读器等辅助工具。 辅助工具是专用的程序和设备，用于帮助残障人士更加有效地使用计算机。|  
|AccessibleName|将报告给辅助工具的名称。|  
|AccessibleRole|介绍如何使用用户界面中的元素。|  
|TabIndex|创建一个通过窗体的合理的导航路径。 务必没有内部函数的标签，如文本框中，必须按 tab 键顺序紧跟及其关联的标签的控件。|  
|Text|使用"&"字符来创建访问键。 使用访问密钥是提供有案可稽的键盘访问功能的一部分。|  
|字号|如果字体大小不是可调整的则应将它设为 10 磅或更大。 一旦设置窗体的字体大小，此后添加到窗体的所有控件将都具有相同的大小。|  
|前景色|如果此属性设置为默认值，则将在窗体上使用用户的颜色首选项。|  
|背景色|如果此属性设置为默认值，则将在窗体上使用用户的颜色首选项。|  
|BackgroundImage|将此属性为空，以使文本更具可读性。|  
  
## <a name="see-also"></a>请参阅
- [演练：创建可访问的基于 Windows 的应用程序](walkthrough-creating-an-accessible-windows-based-application.md)
