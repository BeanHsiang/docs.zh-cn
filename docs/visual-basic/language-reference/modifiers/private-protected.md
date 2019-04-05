---
title: 专用受保护 (Visual Basic)
ms.date: 05/10/2018
helpviewer_keywords:
- Private Protected keyword [Visual Basic]
- Private Protected keyword [Visual Basic], syntax
ms.openlocfilehash: fea43558ac0fe8181f2786b69f2621346d446b2e
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57376385"
---
# <a name="private-protected-visual-basic"></a>专用受保护 (Visual Basic)

`Private Protected` 关键字组合是一种成员访问修饰符。 一个`Private Protected`成员是由其包含的类中的所有成员以及派生自包含类的类型可访问，但仅当它们位于其包含程序集。

您可以指定`Private Protected`只能在类; 的成员上不能应用`Private Protected`为结构成员的因为结构不能被继承。

`Private Protected`由 Visual Basic 15.5 和更高版本提供支持访问修饰符。 若要使用它，您可以将以下元素添加到 Visual Basic 项目 (\*.vbproj) 文件。 只要 Visual Basic 15.5 或更高版本在系统上安装的因为它允许您充分利用所有最新版本的 Visual Basic 编译器支持的语言功能：

```xml
<PropertyGroup>
   <LangVersion>latest</LangVersion>
</PropertyGroup>
```

有关详细信息请参阅[设置的 Visual Basic 语言版本](../../language-reference/configure-language-version.md)。

> [!NOTE]
> 在 Visual Studio 中，选择上的 F1 帮助`private protected`提供有关可以帮助[专用](private.md)或[保护](protected.md)。 IDE 选取单个令牌在光标，而不是组合词。

## <a name="rules"></a>规则

- **声明上下文。** 可以使用`Private Protected`仅在类级别。 这意味着声明上下文`Protected`元素必须是类，且不能为源文件、 命名空间、 接口、 模块、 结构或过程。

## <a name="behavior"></a>行为

- **访问级别。** 在类中的所有代码可以都访问它的元素。 中的任何类都派生自的基类并且包含在同一程序集代码可以访问所有`Private Protected`元素的基类。 但是中的任何类都派生自的基类和其他程序集中包含的代码无法访问的基类`Private Protected`元素。

- **访问修饰符。** 指定的访问级别的关键字称为*访问修饰符*。 访问修饰符的比较，请参阅[访问 Visual Basic 中的级别](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)。


  `Private Protected` 修饰符可用于下面的上下文中：

- [Class 语句](../../../visual-basic/language-reference/statements/class-statement.md)的嵌套类

- [Const 语句](../../../visual-basic/language-reference/statements/const-statement.md)

- [Declare 语句](../../../visual-basic/language-reference/statements/declare-statement.md)

- [Delegate 语句](../../../visual-basic/language-reference/statements/delegate-statement.md)委托的嵌套类中

- [Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md)

- [Enum 语句](../../../visual-basic/language-reference/statements/enum-statement.md)枚举的嵌套类中

- [Event 语句](../../../visual-basic/language-reference/statements/event-statement.md)

- [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)

- [Interface 语句](../../../visual-basic/language-reference/statements/interface-statement.md)接口的嵌套类中

- [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)

- [结构语句](../../../visual-basic/language-reference/statements/structure-statement.md)结构的嵌套类中

- [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)

## <a name="see-also"></a>请参阅

- [Public](../../../visual-basic/language-reference/modifiers/public.md)
- [Protected](../../../visual-basic/language-reference/modifiers/protected.md)
- [Friend](friend.md)
- [Private](../../../visual-basic/language-reference/modifiers/private.md)
- [Protected Friend](./protected-friend.md)
- [在 Visual Basic 中的访问级别](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)
- [过程](../../../visual-basic/programming-guide/language-features/procedures/index.md)
- [结构](../../../visual-basic/programming-guide/language-features/data-types/structures.md)
- [对象和类](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)
