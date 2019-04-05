---
title: Windows 窗体可视化继承
ms.date: 03/30/2017
helpviewer_keywords:
- base forms
- inheritance [Windows Forms], forms
- inherited forms [Windows Forms], Windows Forms
- inheritance
- inherited forms
- form inheritance
- Windows Forms, inheritance
ms.assetid: 857eb737-3602-4d49-bd8b-f70d33ace345
ms.openlocfilehash: e94cdc38b97f95cfe8a8504733298525c25667df
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57705293"
---
# <a name="windows-forms-visual-inheritance"></a>Windows 窗体可视化继承
有时，项目可能需要一个与之前项目中创建的窗体类似的窗体。 或者，可能需要创建一个基本窗体，其中包含某些设置，如随后将再次在项目中使用的水印或某种控件布局，然后每次重复使用时，都需要对该原始窗体模板进行修改。 通过窗体继承，可创建基窗体，然后从其继承并进行修改，同时保留所需的任何原始设置。  
  
 可通过编程方式或使用视觉继承选取器创建派生类窗体。  
  
## <a name="in-this-section"></a>本节内容  
 [如何：继承 Windows 窗体](how-to-inherit-windows-forms.md)  
 提供在代码中创建继承窗体的指导性说明。  
  
 [如何：使用继承选择器对话框继承窗体](how-to-inherit-forms-using-the-inheritance-picker-dialog-box.md)  
 提供使用继承选取器创建继承窗体的指导性说明。  
  
 [修改基窗体的外观的效果](effects-of-modifying-base-form-appearance.md)  
 提供更改基窗体控件及其属性的指导性说明。  
  
 [演练：演示可视化继承](walkthrough-demonstrating-visual-inheritance.md)  
 描述如何创建基 Windows 窗体并将其编译为类库。 可将此类库导入另一个项目，并创建一个从基窗体继承的新窗体。  
  
 [如何：使用 Modifiers 和 GenerateMember 属性](how-to-use-the-modifiers-and-generatemember-properties.md)  
 提供有关如何使用 `GenerateMember` 和 `Modifiers` 属性的指导性说明，Windows 窗体设计器为组件生成成员变量时会涉及这些属性。  
  
## <a name="related-sections"></a>相关章节  
 [继承的基础知识 (Visual Basic)](~/docs/visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)  
 描述如何定义作为其他类的基础的 Visual Basic 类。  
  
 [class](~/docs/csharp/language-reference/keywords/class.md)  
 描述类的 C# 方法，此方法中允许单个继承。  
  
 [Visual Basic 中继承的事件处理程序疑难解答](~/docs/visual-basic/programming-guide/language-features/events/troubleshooting-inherited-event-handlers.md)  
 列出了由继承组件中的事件处理程序引发的常见问题
