---
title: F#风格指南
description: 了解良好的五个原则F#代码。
ms.date: 12/10/2018
ms.openlocfilehash: 9f47257626e04b09b546de2ae315d48d791678be
ms.sourcegitcommit: 3b9b7ae6771712337d40374d2fef6b25b0d53df6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/04/2019
ms.locfileid: "54030264"
---
# <a name="f-style-guide"></a>F#风格指南

以下文章介绍了格式设置准则F#代码和主题的指南的语言功能以及应如何使用它们。

本指南已被表述基于使用的F#在大型基本代码与多样化的程序员。 本指南通常可以成功地使用F#和挫折时随时间变化的程序要求最小化。

## <a name="five-principles-of-good-f-code"></a>良好的五个原则F#代码

请记住您编写任何时间的以下原则F#代码，尤其是在会随时间变化的系统。 在以后的文章的指南的每个片段源自以下五个点。

1. **好F#代码是简洁、 富有表现力的且可组合**

    F#具有许多功能，使您能够表达更少的代码行中的操作并重用一般功能。 F#核心库还包含许多有用的类型和函数用于处理数据的通用集合。 您自己的函数和中的组合F#核心库 （或其他库） 是惯用的例程的一部分F#编程。 作为一般规则，如果可以快速解决问题更少的代码中，行中其他开发人员 （或将来自助） 将感激。 此外强烈建议你使用如 FSharp.Core，库[vast.NET 库](../../../api/index.md)的F#上，运行或上的第三方包[NuGet](https://www.nuget.org/)时需要执行非常重要的任务。

2. **好F#代码进行互操作**

    互操作可能需要多个窗体，包括使用不同的语言代码。 其他调用方与互操作的代码的边界是关键部分，以得到正确结果，即使调用方也是在F#。 编写时F#，您应始终认为有关其他代码将调用您要编写的包括如果用户将这样做类似的另一种语言的代码C#。 [ F#组件设计准则](component-design-guidelines.md)介绍了详细的互操作性。

3. **好F#的代码使对象编程的使用，不 object 方向**

    F#在.NET 中，已使用的对象进行编程的完全支持包括[类](../language-reference/classes.md)，[接口](../language-reference/interfaces.md)，[访问修饰符](../language-reference/access-control.md)，[抽象类](../language-reference/abstract-classes.md)，依次类推。 对于更复杂的功能代码，例如必须是上下文感知的函数对象可以轻松地封装函数不能的方式的上下文信息。 等功能[可选参数](../language-reference/members/methods.md#optional-arguments)和小心使用[重载](../language-reference/members/methods.md#overloaded-methods)可以使用此功能的更轻松地进行调用方。

4. **好F#也不公开的变化情况下执行代码**

    它是公开的若要编写高性能代码，则必须使用变化。 它是计算机的工作原理，别忘了。 此类代码通常是容易出错且难以得到正确结果。 避免公开给调用方的变化。 相反，[生成隐藏的变化基于实现的功能接口](conventions.md#performance)性能至关重要。

5. **好F#代码是可工具化**

    工具是非常宝贵的工作大型代码库，也可以编写F#代码，以便可以使用更有效地使用F#语言工具。 一个示例确保你不要过度使用无点的样式的编程，以便可以使用调试器来检查中间值。 另一个示例使用[XML 文档注释](../language-reference/xml-documentation.md)描述构造，以便在编辑器中的工具提示可以在调用站点上显示这些注释。 始终考虑如何在代码将读取、 导航、 调试，并由其工具能够与其他编程人员操作。

## <a name="next-steps"></a>后续步骤

[ F#代码格式设置准则](formatting.md)指南提供有关如何设置代码格式，以便轻松阅读。

[ F#编码约定](conventions.md)提供的指南F#编程习语可帮助更大的长期维护F#代码库。

[ F#组件设计准则](component-design-guidelines.md)提供创作指南F#组件，例如库。
