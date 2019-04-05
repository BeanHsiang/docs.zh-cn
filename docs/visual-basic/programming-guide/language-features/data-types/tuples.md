---
title: 在 Visual Basic 中的元组
ms.date: 04/23/2017
helpviewer_keywords:
- tuples [Visual Basic]
ms.assetid: 3e66cd1b-3432-4e1d-8c37-5ebacae8f53f
ms.openlocfilehash: 146e9c2360cea153d2f487769d5b983516861e8d
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54694719"
---
# <a name="tuples-visual-basic"></a>元组 (Visual Basic)

从 Visual Basic 2017 开始，Visual Basic 语言提供了对元组构成的内置支持创建元组和访问的元素的元组更容易。 元组是具有特定数量和值序列的轻量级数据结构。 时实例化元组，您定义的数量以及每个值 （或元素） 的数据类型。 例如，2 元组 （或对） 具有两个元素。 第一个可能`Boolean`值，而第二个是`String`。 元组，能够轻松存储单个对象中的多个值，因为它们通常用作简便的方法从方法返回多个值。

> [!IMPORTANT]
> 元组支持需要<xref:System.ValueTuple>类型。 如果未安装.NET Framework 4.7，则必须添加 NuGet 包`System.ValueTuple`，即在 NuGet 库上可用。 无此包，您可能会收到编译错误类似于"'ValueTuple(Of,,,) 未定义或导入预定义类型。"

## <a name="instantiating-and-using-a-tuple"></a>实例化并使用元组

您通过封闭它以逗号分隔的值的 im 括号实例化一个元组。 每个这些值然后将成为元组的字段。 下面的代码，如与定义了三次 （或 3 元组）`Date`作为其第一个值，`String`作为其第二，和一个`Boolean`作为其第三个。

[!code-vb[Instantiate](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple1.vb#1)]

默认情况下，元组中每个字段的名称包含字符串的`Item`以及字段的元组中的基于 1 的位置。 对于此 3-元组，`Date`字段是`Item1`，则`String`字段是`Item2`，并`Boolean`字段是`Item3`。 下面的示例显示在上一行代码中实例化的元组字段的值

[!code-vb[Instantiate](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple1.vb#2)]

Visual Basic 元组字段是可读写;已实例化一个元组后，可以修改其值。 下面的示例修改两个元组在上一示例中创建的三个字段，并显示结果。

[!code-vb[Instantiate](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple1.vb#3)]

## <a name="instantiating-and-using-a-named-tuple"></a>实例化和使用命名元组

而不是使用元组的字段的默认名称，可以实例化*命名元组*通过将自己的名称分配给此元组的元素。 可以通过分配名称访问元组的字段*或*按其默认名称。 下面的示例实例化同一个 3 元组，不同之处在于它进行显式命名的第一个字段`EventDate`，第二个`Name`，第三个`IsHoliday`。 然后显示字段值，修改它们，并再次显示字段值。

[!code-vb[Instantiate](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple1.vb#4)]

## <a name="inferred-tuple-element-names"></a>推断元组元素名称

从 Visual Basic 15.3 开始，Visual Basic 可以推断元组元素，则名称不需要显式将其分配。 初始化的变量，一组元组，并且想要为变量的名称相同的元组元素名称时，推断元组名称很有用。 

下面的示例创建`stateInfo`显式包含三个元组命名的元素， `state`， `stateName`，和`capital`。 请注意，在命名元素，元组初始化语句只需将分配已命名的元素具有相同名称的变量的值。

[!code-vb[ExplicitlyNamed](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/named-tuples/program.vb#1)]
 
元素和变量具有相同的名称，因为 Visual Basic 编译器可以推断出的字段的名称，如以下示例所示。

[!code-vb[ExplicitlyNamed](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/named-tuples/program.vb#2)]

若要启用推断元组元素名称，必须定义要在 Visual Basic 项目中使用的 Visual Basic 编译器的版本 (\*.vbproj) 文件： 

```xml 
<PropertyGroup> 
  <LangVersion>15.3</LangVersion> 
</PropertyGroup> 
```

版本号可以是任何版本的 Visual Basic 编译器从 15.3 开始。 而不是硬编码特定编译器版本，您还可以指定"Latest"的值作为`LangVersion`使用 Visual Basic 编译器在系统上安装的最新版本进行编译。

有关详细信息，请参阅[设置的 Visual Basic 语言版本](../../../language-reference/configure-language-version.md)。

在某些情况下，Visual Basic 编译器无法推断元组元素名称从候选名称，并且仅可以使用其默认名称，例如引用元组字段`Item1`， `Item2`，等等。这些问题包括：

- 候选名称是元组成员的名称相同例如`Item3`， `Rest`，或`ToString`。

- 候选名称重复元组中。
 
当字段名称推理失败时，Visual Basic 不会生成编译器错误，也不是在运行时引发的异常。 相反，元组字段必须引用按预定义名称，如`Item1`和`Item2`。 
  
## <a name="tuples-versus-structures"></a>与结构的元组

Visual Basic 元组是值类型之一的实例**System.ValueTuple**泛型类型。 例如，`holiday`在上一示例中定义的元组是的一个实例<xref:System.ValueTuple%603>结构。 它被旨在作为数据的轻量容器。 由于元组的目的是为了更加轻松地使用多个数据项创建一个对象，它缺乏一些自定义结构可能具有的功能。 这些问题包括：

- 自定义成员。 不能定义自己的属性、 方法或事件的元组。

- 验证。 无法验证指派给字段的数据。

- 保持不变。 Visual Basic 元组是可变的。 与此相反，自定义结构允许您控制实例是否为可变或不可变。

如果自定义成员、 属性和字段验证或不可变性很重要，则应使用 Visual Basic[结构](../../../language-reference/statements/structure-statement.md)语句来定义自定义值类型。

Visual Basic 元组的成员来继承其**ValueTuple**类型。 除了其字段，其中包括以下方法：

| 成员 | 描述 |
| ---|---|
| CompareTo | 比较具有相同的元素数的另一个元组的当前元组。 |
| Equals | 确定是否等于另一个元组或对象的当前元组。 |
| GetHashCode | 计算当前实例的哈希代码。 |
| ToString | 返回此元组，其形式的字符串表示形式`(Item1, Item2...)`，其中`Item1`和`Item2`表示元组的字段的值。 |

此外， **ValueTuple**类型可实现<xref:System.Collections.IStructuralComparable>和<xref:System.Collections.IStructuralEquatable>接口，使您可以定义客户比较器。

## <a name="assignment-and-tuples"></a>赋值和元组

Visual Basic 支持具有相同数量的字段的元组类型之间的赋值。 如果以下项之一为 true，则可以转换的字段类型：

- 源和目标字段是属于同一类型。

- 扩大 （或隐式） 转换的源类型，为目标类型定义。 

- `Option Strict` 是`On`，和收缩 （或显式） 转换的源类型，为目标类型定义。 如果源值为目标类型的范围之外，此转换可以引发异常。

对于其他转换，不考虑进行赋值。 让我们看一下元组类型之间允许的赋值类型。

注意以下示例中使用的这些变量：

[!code-vb[Assign](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple3.vb#1)]

前两个变量，`unnamed`和`anonymous`，没有为字段提供语义名称。 其字段名称，则进行默认`Item1`和`Item2`。 两个变量`named`和`differentName`具有语义的字段名称。 请注意，这两个元组具有不同的字段名称。

这四个元组具有相同数量的字段 （称为实参数量），并且这些字段的类型也完全一样。 因此可进行以下赋值：

[!code-vb[Assign](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple3.vb#2)]

请注意，元组的名称未赋值。 字段的赋值顺序遵循字段在元组中的顺序。

最后，请注意，我们可以将分配`named`元组`conversion`元组，即使的第一个字段`named`是`Integer`，和的第一个字段`conversion`是`Long`。 此分配将成功，因为转换`Integer`到`Long`的扩大转换。

[!code-vb[Assign](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple3.vb#3)]

具有不同数量的字段的元组不可赋值：

```vb
' Does not compile.
' VB30311: Value of type '(Integer, Integer, Integer)' cannot be converted
'          to '(Answer As Integer, Message As String)'
var differentShape = (1, 2, 3)
named = differentShape
```

## <a name="tuples-as-method-return-values"></a>作为方法返回值的元组

一种方法可以返回单个值。 通常情况下，不过，您可能希望方法调用返回多个值。 有几种方法来解决此限制：

- 您可以创建自定义类或结构，其属性或字段表示该方法返回的值。 因此是一个重量级解决方案;它需要定义其唯一用途是从方法调用中检索值的自定义类型。

- 可以从方法返回单个值，并返回剩余的值，向它们传递到方法的引用。 这涉及到的实例化变量和风险无意中覆盖通过引用传递的变量的值的开销。

- 可以使用元组，提供了一种轻量型解决方案检索多个返回值。

例如， **TryParse**方法在.NET 返回`Boolean`值，该值指示是否在分析操作成功。 在分析操作的结果中的变量通过引用传递给该方法返回。 通常情况下，调用分析方法如<xref:System.Int32.TryParse%2A?displayProperty=nameWithType>如下所示：

[!code-vb[Return](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple-returns.vb#1)]

我们可以从在分析操作返回一个元组，如果我们换行到调用<xref:System.Int32.TryParse%2A?displayProperty=nameWithType>我们自己的方法中的方法。 在以下示例中，`NumericLibrary.ParseInteger`调用<xref:System.Int32.TryParse%2A?displayProperty=nameWithType>方法，并返回具有两个元素的命名元组。 

[!code-vb[Return](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple-returns.vb#2)]

然后可以调用的方法，如下所示的代码：

[!code-vb[Return](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple-returns.vb#3)]

## <a name="visual-basic-tuples-and-tuples-in-the-net-framework"></a>Visual Basic 元组和.NET Framework 中的元组

Visual Basic 元组是之一的实例**System.ValueTuple**泛型类型，.NET Framework 4.7 中引入的。 .NET Framework 还包括一组泛型**System.Tuple**类。 但是，这些类，与 Visual Basic 元组的不同， **System.ValueTuple**通过多种方式中的泛型类型：

- 元素**元组**类是属性名为`Item1`， `Item2`，依次类推。 在 Visual Basic 元组中， **ValueTuple**元组元素类型是字段。

- 不能将有意义的名称分配到的元素**元组**实例或**ValueTuple**实例。 Visual Basic 可以为分配通信的字段的含义的名称。

- 属性**元组**实例是只读的; 元组是固定不变。 在 Visual Basic 元组中， **ValueTuple**类型，元组字段是可读写; 元组是可变。

- 泛型**元组**类型是引用类型。 使用这些**元组**类型即意味着分配对象。 在热路径中，这可能会对应用程序性能产生明显的影响。 Visual Basic 元组和**ValueTuple**类型是值类型。

中的扩展方法<xref:System.TupleExtensions>类轻松地转换 Visual Basic 元组和.NET 之间**元组**对象。 **ToTuple**方法将 Visual Basic 元组转换为.NET**元组**对象，并且**ToValueTuple**方法将为.NET**元组**为 Visual Basic 元组的对象。

以下示例创建的元组，将其转换为.NET**元组**对象，并将转换回 Visual Basic 元组。 然后，该示例比较了此元组，其原始的一个，以确保它们相等。

[!code-vb[Convert](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple2.vb#1)]

## <a name="see-also"></a>请参阅

- [Visual Basic 语言参考](index.md)
