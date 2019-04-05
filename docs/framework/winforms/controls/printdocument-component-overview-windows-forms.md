---
title: PrintDocument 组件概述（Windows 窗体）
ms.date: 03/30/2017
f1_keywords:
- PrintDocument
helpviewer_keywords:
- PrintDocument component [Windows Forms], about PrintDocument component
- printing [Windows Forms], PrintDocument component
ms.assetid: b59b4b60-dce5-42ca-8421-3a54a2f7bab0
ms.openlocfilehash: c35c60b651dd3becfeca0f07788efab9d1619117
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57715858"
---
# <a name="printdocument-component-overview-windows-forms"></a>PrintDocument 组件概述（Windows 窗体）
Windows 窗体 [PrintDocument](printdocument-component-windows-forms.md) 组件用于设置属性，这些属性描述在基于 Windows 的应用程序中要打印什么内容以及打印文档的能力。 此组件可与 [PrintDialog](printdialog-component-windows-forms.md) 组件一起使用，控制文档打印的各个方面。  
  
## <a name="working-with-the-printdocument-component"></a>使用 PrintDocument 组件  
 涉及的主要方案的两个<xref:System.Drawing.Printing.PrintDocument>组件是：  
  
-   简单的打印作业，如打印单个文本文件。 在这种情况下将添加<xref:System.Drawing.Printing.PrintDocument>组件向 Windows 窗体，然后添加打印文件的编程逻辑<xref:System.Drawing.Printing.PrintDocument.PrintPage>事件处理程序。 编程逻辑应以使用<xref:System.Drawing.Printing.PrintDocument.Print%2A>方法打印文档。 此方法将发送<xref:System.Drawing.Graphics>中包含的对象<xref:System.Drawing.Printing.PrintPageEventArgs.Graphics%2A>属性的<xref:System.Drawing.Printing.PrintPageEventArgs>类到打印机。 有关演示如何打印文本文档中使用的示例<xref:System.Drawing.Printing.PrintDocument>组件，请参阅[如何：打印 Windows 窗体中的多页文本文件](../advanced/how-to-print-a-multi-page-text-file-in-windows-forms.md)。  
  
-   更复杂的打印作业，如想要重新使用已编写的打印逻辑的情况。 在这种情况中将派生中的新组件<xref:System.Drawing.Printing.PrintDocument>组件和重写 (请参阅[重写](~/docs/visual-basic/language-reference/modifiers/overrides.md)适用于 Visual Basic 或[重写](~/docs/csharp/language-reference/keywords/override.md)的C#)<xref:System.Drawing.Printing.PrintDocument.PrintPage>事件。  
  
 添加到窗体时<xref:System.Drawing.Printing.PrintDocument>组件在 Windows 窗体设计器底部的任务栏中显示。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Drawing.Graphics>
- <xref:System.Drawing.Printing.PrintDocument>
- [Windows 窗体打印支持](../advanced/windows-forms-print-support.md)
- [PrintDocument 组件](printdocument-component-windows-forms.md)
