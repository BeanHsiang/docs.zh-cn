---
title: 定义与 .NET Framework XAML 服务一起使用的自定义类型
ms.date: 03/30/2017
helpviewer_keywords:
- defining custom types [XAML Services]
ms.assetid: c2667cbd-2f46-4a7f-9dfc-53696e35e8e4
ms.openlocfilehash: fa341b7df32823c653df25ddb0dabcb4658b72b5
ms.sourcegitcommit: 5c1abeec15fbddcc7dbaa729fabc1f1f29f12045
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2019
ms.locfileid: "58042627"
---
# <a name="defining-custom-types-for-use-with-net-framework-xaml-services"></a>定义与 .NET Framework XAML 服务一起使用的自定义类型
当您定义了业务对象的自定义类型或不在特定框架上具有依赖项的类型时，有的 XAML 可以按照某些最佳实践。 如果您遵循这些实践，.NET Framework XAML 服务及其 XAML 读取器和 XAML 编写器可以发现你的类型的 XAML 特征，并为其适当 XAML 节点流使用的 XAML 类型系统中的表示形式。 本主题介绍类型定义、 成员定义和 CLR 类型或成员的特性化最佳的实践。  
  
## <a name="constructor-patterns-and-type-definitions-for-xaml"></a>构造函数模式和 XAML 的类型定义  
 若要实例化成对象元素在 XAML 中，自定义类必须满足以下要求：  
  
-   自定义类必须是公共的并且必须公开默认 （无参数） 公共构造函数。 （有关结构注释，请参阅下节内容。）  
  
-   自定义类不得为嵌套的类。 额外的完整名称路径中的"dot"使类命名空间划分不明确的并且会干扰其他 XAML 功能，例如附加属性。  
  
 如果为对象元素，可以实例化一个对象，所创建的对象可以填充属性元素将该对象作为其基础类型的任何属性的形式。  
  
 如果启用了值转换器，仍可以为不符合这些条件的类型提供对象值。 有关详细信息，请参阅[Type Converters and Markup Extensions for XAML](type-converters-and-markup-extensions-for-xaml.md)。  
  
### <a name="structures"></a>结构  
 结构永远是能够在 XAML 中，通过 CLR 定义构造的。 这是因为 CLR 编译器隐式创建一个结构的默认构造函数。 此构造函数初始化为其默认值的所有属性值。  
  
 在某些情况下，一种结构的默认构造行为是不可取。 这可能是因为结构旨在填补值和函数在概念上作为联合。 作为一个联合，所含的值可能具有互斥的解释，并因此，其属性都是不可设置。 此类结构的 WPF 词汇中的一个示例是<xref:System.Windows.GridLength>。 此类结构应实现类型转换器，以便可以通过创建不同的解释或模式的结构值的字符串约定属性形式表示的值。 结构还应通过非默认构造函数对代码构造公开类似的行为。  
  
### <a name="interfaces"></a>接口  
 接口可以用作基础类型的成员。 XAML 类型系统检查可分配的列表，并且期望作为值提供的对象可以分配给的接口。 不存在的接口必须存在方式作为 XAML 类型，只要相关的可分配类型支持 XAML 构造要求概念。  
  
### <a name="factory-methods"></a>工厂方法  
 工厂方法是 XAML 2009 功能。 他们修改 XAML 原则对象必须具有默认构造函数。 本主题中未记录的工厂方法。 请参阅[X:factorymethod 指令](x-factorymethod-directive.md)。  
  
## <a name="enumerations"></a>枚举  
 枚举具有 XAML 的本机类型转换行为。 在 XAML 中指定的枚举常量名解析对基础的枚举类型，并返回到 XAML 对象编写器的枚举值。  
  
 XAML 与枚举支持标志样式使用<xref:System.FlagsAttribute>应用。 有关详细信息，请参阅[XAML 语法详述](../wpf/advanced/xaml-syntax-in-detail.md)。 ([XAML 语法详述](../wpf/advanced/xaml-syntax-in-detail.md)专为 WPF 受众，但该主题中的信息的大多数都是适用于不是特定于特定实现框架的 XAML。)  
  
## <a name="member-definitions"></a>成员定义  
 类型可以定义 XAML 用法的成员。 它是可以定义是 XAML 可用，即使该特定类型不是 XAML 可用的成员的类型。 这是因为 CLR 继承。 只要某种类型的继承成员支持 XAML 用法作为一个类型，并且该成员的基础类型支持 XAML 用法或具有本机的 XAML 语法，该成员是 XAML 可用。  
  
### <a name="properties"></a>Properties  
 如果定义为公共 CLR 属性使用典型的 CLR 属性`get`和`set`访问器模式和相应语言的建立关键词，XAML 类型系统可以提供具有适当的信息的成员作为属性进行报告<xref:System.Xaml.XamlMember>属性，如<xref:System.Xaml.XamlMember.IsReadPublic%2A>和<xref:System.Xaml.XamlMember.IsWritePublic%2A>。  
  
 特定的属性可以通过应用启用文本语法<xref:System.ComponentModel.TypeConverterAttribute>。 有关详细信息，请参阅[Type Converters and Markup Extensions for XAML](type-converters-and-markup-extensions-for-xaml.md)。  
  
 在没有文本语法或本机的 XAML 转换，并且没有进一步中间环节，例如标记扩展用法，属性的类型 (<xref:System.Xaml.XamlMember.TargetType%2A>中 XAML 类型系统) 必须能够返回到 XAML 对象编写器实例，方法是将 target 作为 CLR 类型的类型。  
  
 如果使用 XAML 2009 [X:reference 标记扩展](x-reference-markup-extension.md)可用于提供值，如果不满足前述注意事项; 但是，这是多个类型定义问题之外的使用情况问题。  
  
### <a name="events"></a>事件  
 如果为公共 CLR 事件定义事件，XAML 类型系统可以将事件报告为成员，同时<xref:System.Xaml.XamlMember.IsEvent%2A>作为`true`。 连接事件处理程序不是.NET Framework XAML 服务功能; 的作用域内此功能由特定框架和实现。  
  
### <a name="methods"></a>方法  
 方法的内联代码不是默认 XAML 功能。 在大多数情况下不直接引用方法成员从 XAML，并在 XAML 中的方法的角色是仅为特定 XAML 模式提供支持。 [X:factorymethod 指令](x-factorymethod-directive.md)是一个例外。  
  
### <a name="fields"></a>字段  
 CLR 设计原则不鼓励使用非静态字段。 对于静态字段，您可以访问静态字段值只能通过[X:static 标记扩展](x-static-markup-extension.md); 在这种情况下不执行任何特殊 CLR 定义公开的字段中[x： 静态](x-static-markup-extension.md)用法。  
  
## <a name="attachable-members"></a>可附加成员  
 可附加成员上定义的类型的取值函数方法模式通过向 XAML 公开。 定义类型本身不需要为 XAML 可用作对象。 实际上，一种常见模式是声明其角色是一个服务类来拥有可附加成员和实现相关的行为，但是不提供用户界面表示形式如任何其他函数。 为以下部分中，将占位符*PropertyName*表示可附加成员的名称。 该名称中必须是有效[XamlName 语法](xamlname-grammar.md)。  
  
 请务必谨慎的这些模式和类型的其他方法之间的名称冲突。 如果存在匹配的模式之一的成员，它可以被解释为可附加成员用法路径由 XAML 处理器即使这不是您的意图。  
  
#### <a name="the-getpropertyname-accessor"></a>GetPropertyName 访问器  
 `Get` PropertyName 访问器的签名必须是：  
  
 `public static object Get` PropertyName `(object` `target` `)`  
  
-   `target` 对象在实现中可以指定为更具体的类型。 可以使用此范围限定在可附加成员; 的使用情况你预期的作用域之外的使用情况将引发无效强制转换异常，然后显示 XAML 分析错误的。 参数名称`target`不是必需的但名为`target`大多数实现约定。  
  
-   返回值在实现中可以指定为更具体的类型。  
  
 若要支持<xref:System.ComponentModel.TypeConverter>应用的可附加成员的特性用法的已启用的文本语法<xref:System.ComponentModel.TypeConverterAttribute>到`Get` *PropertyName*访问器。 将应用于`get`而不是`set`可能看起来直观; 但是，此约定可支持这一概念的只读的可附加成员进行序列化的这是在设计器的情况下很有用。  
  
#### <a name="the-setpropertyname-accessor"></a>SetPropertyName 访问器  
 为集签名*PropertyName*访问器必须是：  
  
 `public static void Set` PropertyName `(object`  `target` `, object`  `value` `)`  
  
-   `target`上一节中所述，可以在实现中，使用相同的逻辑和后果更具体的类型为指定对象。  
  
-   `value` 对象在实现中可以指定为更具体的类型。  
  
 请记住，此方法的值是从 XAML 用法，通常以特性形式的输入。 从属性窗体必须针对文本语法，值转换器支持，并且特性上`Get` *PropertyName*访问器。  
  
### <a name="attachable-member-stores"></a>可附加成员存储  
 访问器方法通常是不足够，以提供一种方式将可附加成员的值放入对象关系图，或用于检索对象图的值并正确地将它们序列化。 若要提供此功能，`target`上一个取值函数签名中的对象必须能够存储值。 应与该成员是可附加到目标的可附加成员不在成员列表中的可附加成员原则一致的存储机制。 .NET framework XAML 服务提供了实现的一种技术，可附加成员存储通过 Api<xref:System.Xaml.IAttachedPropertyStore>和<xref:System.Xaml.AttachablePropertyServices>。 <xref:System.Xaml.IAttachedPropertyStore> XAML 编写器用于发现存储实现，并应是类型上实现`target`的访问器。 静态<xref:System.Xaml.AttachablePropertyServices>Api 的访问器，在正文中使用和通过的可附加成员是指其<xref:System.Xaml.AttachableMemberIdentifier>。  
  
## <a name="xaml-related-clr-attributes"></a>与 XAML 相关 CLR 特性  
 属性类型、 成员和程序集正确设置到报表到.NET Framework XAML 服务 XAML 类型系统信息的顺序至关重要。 如果你想用于直接基于.NET Framework XAML 服务 XAML 读取器和 XAML 编写器的 XAML 系统类型，或如果你定义或使用基于这些 XAML 读取器和 XAML 编写器的 XAML 利用框架，这是相关。  
  
 适用于自定义类型的 XAML 支持的每个与 XAML 相关的属性的列表，请参阅[XAML-Related CLR 特性自定义类型和库的](xaml-related-clr-attributes-for-custom-types-and-libraries.md)。  
  
## <a name="usage"></a>用法  
 使用自定义类型需要标记作者必须映射包含自定义类型的程序集和 CLR 命名空间的前缀。 本主题中不记录此过程。  
  
## <a name="access-level"></a>访问级别  
 XAML 提供了一种加载和实例化类型具有`internal`访问级别。 此功能，以便用户代码可以定义其自己的类型，然后实例化也是相同的用户代码作用域的一部分的标记从这些类提供。  
  
 WPF 中的示例是每当用户的代码定义<xref:System.Windows.Controls.UserControl>目的是作为一种方式重构 UI 行为，但不是可能通过声明的支持类暗示任何可能的扩展机制的一部分`public`访问级别。 此类<xref:System.Windows.Controls.UserControl>可以使用声明`internal`如果支持代码编译到同一程序集从其其引用为 XAML 类型访问。  
  
 应用程序，在完全信任下加载 XAML 并使用<xref:System.Xaml.XamlObjectWriter>，类加载`internal`访问级别始终处于启用状态。  
  
 对于在部分信任下加载 XAML 的应用，可以通过使用控制访问级别特征<xref:System.Xaml.Permissions.XamlAccessLevel>API。 此外，延迟机制 （如 WPF 模板系统） 必须能够将传播任何访问级别权限，并保留它们的最终运行的时计算中;这通过传递内部处理<xref:System.Xaml.Permissions.XamlAccessLevel>信息。  
  
### <a name="wpf-implementation"></a>WPF 实现  
 WPF XAML 使用部分信任访问模型，如果在部分信任下加载 BAML，则访问权限仅限于<xref:System.Xaml.Permissions.XamlAccessLevel.AssemblyAccessTo%2A>是 BAML 源的程序集。 对于延迟，WPF 使用<xref:System.Xaml.IXamlObjectWriterFactory.GetParentSettings%2A?displayProperty=nameWithType>作为传递的访问级别信息的机制。  
  
 在 WPF XAML 术语中，*内部类型*是由同一程序集，它还包括引用的 XAML 定义的类型。 这种类型可以映射 XAML 命名空间的有意省略了该程序集 = 一部分的映射，例如， `xmlns:local="clr-namespace:WPFApplication1"`。  如果 BAML 将引用的内部类型和类型具有`internal`访问级别，这将生成`GeneratedInternalTypeHelper`程序集的类。 如果你想要避免`GeneratedInternalTypeHelper`，则必须使用`public`访问级别，或必须分解为单独的程序集相关的类，并将该程序集依赖。  
  
## <a name="see-also"></a>请参阅
- [自定义类型和库的 XAML 相关 CLR 特性](xaml-related-clr-attributes-for-custom-types-and-libraries.md)
- [XAML 服务](index.md)
