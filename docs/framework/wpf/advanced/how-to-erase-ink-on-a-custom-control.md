---
title: 如何：清除自定义控件上的墨迹
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- custom controls [WPF], erasing ink on
- ink [WPF], erasing on custom control
ms.assetid: d88c50f9-b4d8-4962-a28b-67d6a15a5fe0
ms.openlocfilehash: 60e2af64cb0c5b313f4f1201cab70da6a88f61e7
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57365888"
---
# <a name="how-to-erase-ink-on-a-custom-control"></a>如何：清除自定义控件上的墨迹
<xref:System.Windows.Ink.IncrementalStrokeHitTester>确定当前绘制的笔画是否与另一个笔画相交。  对于创建控件，使用户擦除笔划的部分，这很有用，方式用户可以在<xref:System.Windows.Controls.InkCanvas>时<xref:System.Windows.Controls.InkCanvas.EditingMode%2A>设置为<xref:System.Windows.Controls.InkCanvasEditingMode.EraseByPoint>。  
  
## <a name="example"></a>示例  
 以下示例创建自定义控件，使用户能够擦除部分笔画。  此示例创建包含手写内容时进行初始化的控件。  若要创建收集墨迹的控件，请参阅[创建墨迹输入控件](creating-an-ink-input-control.md)。  
  
 [!code-csharp[HowToEraseInk#1](~/samples/snippets/csharp/VS_Snippets_Wpf/HowToEraseInk/CSharp/InkEraser.cs#1)]
 [!code-vb[HowToEraseInk#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HowToEraseInk/VisualBasic/InkEraser.vb#1)]
