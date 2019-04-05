---
title: 如何：使用 Modifiers 和 GenerateMember 属性
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
f1_keywords:
- Designer_GenerateMember
- Designer_Modifiers
helpviewer_keywords:
- base forms
- inheritance [Windows Forms], forms
- inherited forms [Windows Forms], Windows Forms
- inherited forms
- form inheritance
- Windows Forms, inheritance
ms.assetid: 3381a5e4-e1a3-44e2-a765-a0b758937b85
ms.openlocfilehash: 277d2bdebc1d3b85efb70510b8acd34ed3a91087
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57710792"
---
# <a name="how-to-use-the-modifiers-and-generatemember-properties"></a>如何：使用 Modifiers 和 GenerateMember 属性
当在 Windows 窗体上放置一个组件时，通过在设计环境提供了两个属性：`GenerateMember`和`Modifiers`。 `GenerateMember`属性指定当 Windows 窗体设计器生成的一个组件的成员变量。 `Modifiers`属性是分配给该成员变量的访问修饰符。 如果的值`GenerateMember`属性是`false`，则`Modifiers`属性不起作用。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。  
  
### <a name="to-specify-whether-a-component-is-a-member-of-the-form"></a>若要指定组件是否是窗体的成员  
  
1.  在 Windows 窗体设计器中，打开你的窗体。  
  
2.  打开**工具箱**，并在窗体上将三个<xref:System.Windows.Forms.Button>控件。  
  
3.  设置`GenerateMember`并`Modifiers`每个属性<xref:System.Windows.Forms.Button>根据下表的控件。  
  
    |按钮名称|GenerateMember 值|修饰符值|  
    |-----------------|--------------------------|---------------------|  
    |`button1`|`true`|`private`|  
    |`button2`|`true`|`protected`|  
    |`button3`|`false`|无更改|  
  
4.  生成解决方案。  
  
5.  在“解决方案资源管理器”中，单击“显示所有文件”按钮。  
  
6.  打开**Form1**节点，然后在**代码编辑器**，打开**Form1.Designer.vb**或者**Form1.Designer.cs**文件。 此文件包含 Windows 窗体设计器生成的代码。  
  
7.  找到三个按钮的声明。 下面的代码示例显示了由指定的差异`GenerateMember`和`Modifiers`属性。  
  
     [!code-csharp[System.Windows.Forms.GenerateMember#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.GenerateMember/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.GenerateMember#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.GenerateMember/VB/Form1.vb#3)]  
  
     [!code-csharp[System.Windows.Forms.GenerateMember#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.GenerateMember/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.GenerateMember#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.GenerateMember/VB/Form1.vb#2)]  
  
> [!NOTE]
>  默认情况下，Windows 窗体设计器将分配`private`(`Friend`在 Visual Basic 中) 等容器控件的修饰符<xref:System.Windows.Forms.Panel>。 如果您的群<xref:System.Windows.Forms.UserControl>或<xref:System.Windows.Forms.Form>具有一个容器控件，它不会接受新子级继承的控件和窗体中。 解决方法是更改到基容器控件的修饰符`protected`或`public`。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.Button>
- [Windows 窗体可视化继承](windows-forms-visual-inheritance.md)
- [演练：演示可视化继承](walkthrough-demonstrating-visual-inheritance.md)
- [如何：继承 Windows 窗体](how-to-inherit-windows-forms.md)
