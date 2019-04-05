---
title: C# 委托 - C# 语言介绍
description: 了解包含 C# 委托的晚期绑定
ms.date: 08/10/2016
ms.assetid: 3cc27357-3ac2-43a1-aad0-86a77b88f884
ms.openlocfilehash: 2744f774392ef021974535de535b063264ae9a54
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53151273"
---
# <a name="delegates"></a>委托

***委托类型***表示对具有特定参数列表和返回类型的方法的引用。 通过委托，可以将方法视为可分配给变量并可作为参数传递的实体。 委托类似于其他一些语言中的函数指针概念，但与函数指针不同的是，委托不仅面向对象，还类型安全。

下面的示例声明并使用 `Function` 委托类型。

[!code-csharp[DelegateExample](../../../samples/snippets/csharp/tour/delegates/Program.cs#L3-L37)]

`Function` 委托类型实例可以引用需要使用 `double` 自变量并返回 `double` 值的方法。 `Apply` 方法将给定的函数应用于 `double[]` 的元素，从而返回包含结果的 `double[]`。 在 `Main` 方法中，`Apply` 用于向 `double[]` 应用三个不同的函数。

委托可以引用静态方法（如上面示例中的 `Square` 或 `Math.Sin`）或实例方法（如上面示例中的 `m.Multiply`）。 引用实例方法的委托还会引用特定对象，通过委托调用实例方法时，该对象会变成调用中的 `this`。

还可以使用匿名函数创建委托，这些函数是便捷创建的“内联方法”。 匿名函数可以查看周围方法的局部变量。 因此，可以更轻松地编写上面的乘数示例，而无需使用 Multiplier 类：

[!code-csharp[LambdaExample](../../../samples/snippets/csharp/tour/delegates/Program.cs#L44-L44)]

委托的一个有趣且有用的属性是，它不知道也不关心所引用的方法的类；只关心引用的方法是否具有与委托相同的参数和返回类型。

>[!div class="step-by-step"]
>[上一页](enums.md)
>[下一页](attributes.md)