---
title: 受保护的友元 (Visual Basic)
ms.date: 05/10/2018
helpviewer_keywords:
- Protected Friend keyword [Visual Basic]
- Protected Friend keyword [Visual Basic], syntax
ms.openlocfilehash: 1858411e5543448e6d822c97b6e5c18da4a6c11e
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54639596"
---
# <a name="protected-friend-visual-basic"></a>受保护的友元 (Visual Basic)

`Protected Friend` 关键字组合是一种成员访问修饰符。 它授予这两[友元](friend.md)访问权限和[受保护](protected.md)上声明的元素，因此它们可从同一程序集，从其自身的类，以及从派生类中的任意位置访问的访问。 您可以指定`Protected Friend`只能在类; 的成员上不能应用`Protected Friend`为结构成员的因为结构不能被继承。

> [!NOTE]
> 在 Visual Studio 中，选择上的 F1 帮助`protected friend`提供有关可以帮助[受保护](protected.md)或[友元](friend.md)。 IDE 选取单个令牌在光标，而不是组合词。

## <a name="rules"></a>规则

- **声明上下文。** 可以使用`Protected Friend`仅在类级别。 这意味着声明上下文`Protected`元素必须是类，且不能为源文件、 命名空间、 接口、 模块、 结构或过程。 


## <a name="see-also"></a>请参阅

- [Public](../../../visual-basic/language-reference/modifiers/public.md)
- [Protected](../../../visual-basic/language-reference/modifiers/protected.md)
- [Friend](friend.md)
- [Private](../../../visual-basic/language-reference/modifiers/private.md)
- [Private Protected](./private-protected.md)
- [在 Visual Basic 中的访问级别](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)
- [过程](../../../visual-basic/programming-guide/language-features/procedures/index.md)
- [结构](../../../visual-basic/programming-guide/language-features/data-types/structures.md)
- [对象和类](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)
