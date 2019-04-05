---
title: 如何：调整 Windows 窗体标签控件以适应其内容的大小
ms.date: 03/30/2017
helpviewer_keywords:
- captions [Windows Forms], sizing
- sizing controls
- size [Windows Forms], controls
- labels [Windows Forms], sizing to fit contents
- Label control [Windows Forms], sizing to fit contents
ms.assetid: 99648964-63b2-438c-980e-d24103ad602b
ms.openlocfilehash: 5771b232d77e3e5a792b179ebffd3fa0edda7c9b
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57702189"
---
# <a name="how-to-size-a-windows-forms-label-control-to-fit-its-contents"></a>如何：调整 Windows 窗体标签控件以适应其内容的大小
Windows 窗体<xref:System.Windows.Forms.Label>控件可以为单行或多行，它可以为固定大小，或可以自动调整自身大小以容纳其标题。 <xref:System.Windows.Forms.Label.AutoSize%2A>属性可帮助您调整控件大小以适应更大或较小的标题，即如果标题将更改在运行时特别有用的大小。  
  
### <a name="to-make-a-label-control-resize-dynamically-to-fit-its-contents"></a>若要进行动态调整大小以适应其内容的标签控件  
  
1.  设置其<xref:System.Windows.Forms.Label.AutoSize%2A>属性设置为`true`。  
  
 如果<xref:System.Windows.Forms.Label.AutoSize%2A>设置为`false`，在指定的词语<xref:System.Windows.Forms.Label.Text%2A>属性会换行到下一行如果可能，但该控件不会增长。  
  
## <a name="see-also"></a>请参阅
- [如何：使用 Windows 窗体 Label 控件创建访问键](how-to-create-access-keys-with-windows-forms-label-controls.md)
- [Label 控件概述](label-control-overview-windows-forms.md)
- [Label 控件](label-control-windows-forms.md)
