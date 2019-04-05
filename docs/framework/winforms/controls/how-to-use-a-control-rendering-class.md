---
title: 如何：使用控件呈现类
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- professional appearance [Windows Forms], rendering Windows Forms controls
- visual themes [Windows Forms], applying to Windows Forms controls
- visual styles [Windows Forms], rendering Windows Forms controls
ms.assetid: c0125e34-cd74-4c35-818c-3e40f462b0a3
ms.openlocfilehash: d9da43b1686f416cf2149cef07665b0a726c3b0c
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57723148"
---
# <a name="how-to-use-a-control-rendering-class"></a>如何：使用控件呈现类
此示例演示如何使用<xref:System.Windows.Forms.ComboBoxRenderer>类呈现的下拉箭头的组合框控件。 此示例由<xref:System.Windows.Forms.Control.OnPaint%2A>简单的自定义控件的方法。 <xref:System.Windows.Forms.ComboBoxRenderer.IsSupported%2A?displayProperty=nameWithType>属性用于确定是否在应用程序窗口的工作区中启用了可视样式。 如果视觉样式已处于活动状态，则<xref:System.Windows.Forms.ComboBoxRenderer.DrawDropDownButton%2A?displayProperty=nameWithType>方法将呈现的下拉箭头以视觉样式; 否则为<xref:System.Windows.Forms.ControlPaint.DrawComboButton%2A?displayProperty=nameWithType>方法将呈现中的经典 Windows 样式的下拉箭头。  
  
## <a name="example"></a>示例  
 [!code-cpp[System.Windows.Forms_ControlRenderer#10](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms_ControlRenderer/cpp/form1.cpp#10)]
 [!code-csharp[System.Windows.Forms_ControlRenderer#10](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms_ControlRenderer/CS/form1.cs#10)]
 [!code-vb[System.Windows.Forms_ControlRenderer#10](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms_ControlRenderer/VB/form1.vb#10)]  
  
## <a name="compiling-the-code"></a>编译代码  
 此示例需要：  
  
-   自定义控件派生自<xref:System.Windows.Forms.Control>类。  
  
-   一个<xref:System.Windows.Forms.Form>承载自定义控件。  
  
-   对引用<xref:System?displayProperty=nameWithType>， <xref:System.Drawing?displayProperty=nameWithType>， <xref:System.Windows.Forms?displayProperty=nameWithType>，和<xref:System.Windows.Forms.VisualStyles?displayProperty=nameWithType>命名空间。  
  
## <a name="see-also"></a>请参阅
- [使用视觉样式呈现控件](rendering-controls-with-visual-styles.md)
