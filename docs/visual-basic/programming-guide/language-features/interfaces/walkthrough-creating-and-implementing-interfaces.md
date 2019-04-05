---
title: 创建和实现接口 (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- interfaces [Visual Basic], walkthroughs
- interfaces [Visual Basic], testing
- interface implementation [Visual Basic], walkthrough
- interfaces [Visual Basic], creating
ms.assetid: ded82af2-9f52-4232-98ef-fe458180f112
ms.openlocfilehash: 7a5694826e0fff82aceb8ad18f75f96f308e724c
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54680382"
---
# <a name="walkthrough-creating-and-implementing-interfaces-visual-basic"></a>演练：创建和实现接口 (Visual Basic)

接口描述特征的属性、 方法和事件，但保留最多结构或类的实现详细信息。  
  
 本演练演示如何声明和实现接口。  
  
> [!NOTE]
>  本演练不提供有关如何创建用户界面的信息。  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
## <a name="to-define-an-interface"></a>若要定义一个接口
  
1.  打开一个新的 Visual Basic Windows 应用程序项目。  
  
2.  将新模块添加到项目中，通过单击**添加模块**上**项目**菜单。  
  
3.  命名新模块`Module1.vb`然后单击**添加**。 显示新的模块的代码。  
  
4.  定义一个名为的接口`TestInterface`内`Module1`通过键入`Interface TestInterface`之间`Module`和`End Module`语句，并按 ENTER。 **代码编辑器**缩进`Interface`关键字，并将添加`End Interface`语句以形成一个代码块。  
  
5.  通过将下面的代码之间定义属性、 方法和事件接口`Interface`和`End Interface`语句：  
  
     [!code-vb[VbVbalrOOP#98](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#98)]
  
## <a name="implementation"></a>实现

 你可能会发现用于声明接口成员的语法不同于用来声明类成员的语法。 这一区别反映了这一事实，接口不能包含实现代码。  
  
### <a name="to-implement-the-interface"></a>若要实现接口
  
1.  添加名为的类`ImplementationClass`通过将添加到下面的语句`Module1`后面`End Interface`语句之前`End Module`语句，并按 ENTER:  
  
     [!code-vb[VbVbalrOOP#99](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#99)]
  
     如果你正在使用集成的开发环境**代码编辑器**提供一条匹配`End Class`语句时按 ENTER。  
  
2.  添加以下`Implements`语句`ImplementationClass`，命名的类接口实现：  
  
     [!code-vb[VbVbalrOOP#100](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#100)]
  
     当分别列出了在类或结构的顶部的其他项的`Implements`语句指示类或结构实现的接口。  
  
     如果你正在使用集成的开发环境**代码编辑器**实现所需的类成员`TestInterface`时按 enter 键，并且你可以跳过下一步。  
  
3.  如果不使用集成的开发环境中，则必须实现该接口的所有成员`MyInterface`。 将以下代码添加到`ImplementationClass`来实现`Event1`， `Method1`，和`Prop1`:  
  
     [!code-vb[VbVbalrOOP#101](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#101)]
  
     `Implements`语句命名的接口和实现的接口成员。  
  
4.  完成的定义`Prop1`通过将私有字段添加到存储的属性值的类中：  
  
     [!code-vb[VbVbalrOOP#102](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#102)]
  
     返回的值`pval`从属性 get 访问器。  
  
     [!code-vb[VbVbalrOOP#103](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#103)]
  
     值设置`pval`在属性 set 访问器。  
  
     [!code-vb[VbVbalrOOP#104](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#104)]
  
5.  完成的定义`Method1`通过添加以下代码。  
  
     [!code-vb[VbVbalrOOP#105](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#105)]
  
### <a name="to-test-the-implementation-of-the-interface"></a>若要测试接口的实现
  
1.  右键单击你的项目中的启动窗体**解决方案资源管理器**，然后单击**查看代码**。 编辑器会显示启动窗体的类。 默认情况下，启动窗体称为`Form1`。  
  
2.  添加以下`testInstance`字段改为`Form1`类：  
  
     [!code-vb[VbVbalrOOP#120](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#120)]
  
     通过声明`testInstance`作为`WithEvents`，则`Form1`类可以处理其事件。  
  
3.  添加到以下事件处理程序`Form1`类来处理引发的事件`testInstance`:  
  
     [!code-vb[VbVbalrOOP#106](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#106)]
  
4.  添加一个名为子例程`Test`到`Form1`类，以测试实现类：  
  
     [!code-vb[VbVbalrOOP#107](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#107)]
  
     `Test`过程将创建实现的类的实例`MyInterface`，将分配到该实例`testInstance`字段中，设置属性，并通过界面运行某个方法。  
  
5.  添加代码以调用`Test`过程从`Form1 Load`启动窗体的过程：  
  
     [!code-vb[VbVbalrOOP#108](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#108)]
  
6.  运行`Test`过程通过按 F5。 显示消息"Prop1 已设置为 9"。 之后，单击确定，显示"Method1 X 参数是 5"的消息。 单击确定，并显示"事件处理程序捕获到事件"的消息。  
  
## <a name="see-also"></a>请参阅

- [Implements 语句](../../../../visual-basic/language-reference/statements/implements-statement.md)
- [接口](../../../../visual-basic/programming-guide/language-features/interfaces/index.md)
- [Interface 语句](../../../../visual-basic/language-reference/statements/interface-statement.md)
- [Event 语句](../../../../visual-basic/language-reference/statements/event-statement.md)
