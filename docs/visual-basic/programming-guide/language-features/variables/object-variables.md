---
title: Visual Basic 中的对象变量
ms.date: 07/20/2015
helpviewer_keywords:
- object variables [Visual Basic], about object variables
- variables [Visual Basic], object
- objects [Visual Basic], accessing
- object variables [Visual Basic]
ms.assetid: 6169a196-2b13-4ba5-a205-154bc1b87844
ms.openlocfilehash: cc5be13293a89e73d1790e94a99d7936f1711e12
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57352966"
---
# <a name="object-variables-in-visual-basic"></a>Visual Basic 中的对象变量

除了直接存储值，变量还可以引用的对象。 出于相同原因的任何值分配给一个变量可将对象分配给一个变量中：

- 变量名称通常是较短且更易于记住比的方法和属性访问该对象本身所需的完整路径。

- 使用引用的对象的变量是重复通过所必需的方法或属性访问该对象本身相比更高效。

- 你可以为你的代码运行时引用其他对象的变量。

## <a name="making-code-shorter"></a>从而使代码更短

可以使用对象变量来缩短您必须键入的代码。 下面的示例使用的方法和属性的完整路径来访问<xref:System.Windows.Forms.Control>对象。

```vb
' Assume Me is a valid Form, or replace Me with a valid Form.
Me.ActiveForm.ActiveControl.Text = "Test"
Me.ActiveForm.ActiveControl.Location = New Point(100, 100)
Me.ActiveForm.ActiveControl.Show()
```

您可以缩短此代码中，并加快执行，如果控件使用的对象变量。 应该声明对象变量与你想要为其分配的特定类 (`Control`这种情况下)。 一旦将对象分配给变量，可视为它完全相同对待它所引用的对象。 可以设置或检索该对象的属性或使用任何方法。 下面的示例使用对象变量来简化在前面的示例代码。

```vb
Dim ctrlActv As System.Windows.Forms.Control = Me.ActiveForm.ActiveControl
ctrlActv.Text = "Test"
ctrlActv.Location = New Point(100, 100)
ctrlActv.Show()
```

## <a name="see-also"></a>请参阅

- [变量声明](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)
- [如何：加速访问具有长限定路径的对象](../../../../visual-basic/programming-guide/language-features/variables/how-to-speed-up-access-to-an-object-with-a-long-qualification-path.md)
- [对象变量声明](../../../../visual-basic/programming-guide/language-features/variables/object-variable-declaration.md)
- [对象变量赋值](../../../../visual-basic/programming-guide/language-features/variables/object-variable-assignment.md)
- [对象变量值](../../../../visual-basic/programming-guide/language-features/variables/object-variable-values.md)
