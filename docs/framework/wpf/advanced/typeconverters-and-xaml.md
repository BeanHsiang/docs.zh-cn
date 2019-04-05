---
title: TypeConverters 和 XAML
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [WPF], TypeConverter class
ms.assetid: f6313e4d-e89d-497d-ac87-b43511a1ae4b
ms.openlocfilehash: 7f42bb6e4333fcb5e83ee4b95e404230424b317f
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57352706"
---
# <a name="typeconverters-and-xaml"></a>TypeConverters 和 XAML
本主题介绍将从字符串进行的类型转换作为常规 XAML 语言功能的用途。 在.NET Framework 中，<xref:System.ComponentModel.TypeConverter>类作为某种特定用途可以用作 XAML 特性用法中的属性值的托管自定义类的实现的一部分。 如果您编写的自定义类，并且你希望类用作 XAML 可设置属性值的实例，您可能需要应用<xref:System.ComponentModel.TypeConverterAttribute>到类，编写自定义<xref:System.ComponentModel.TypeConverter>类，或两者。  
  

  
## <a name="type-conversion-concepts"></a>类型转换概念  
  
### <a name="xaml-and-string-values"></a>XAML 和字符串值  
 在 XAML 文件中设置特性值时，该值的初始类型是纯文本形式的字符串。 如甚至其他基元<xref:System.Double>最初是为 XAML 处理器的文本字符串。  
  
 XAML 处理器需要两条信息来处理特性值。 第一条信息是所设置的属性的值类型。 定义特性值以及在 XAML 中进行处理的任何字符串都必须最终转换或解析为该类型的值。 如果值是 XAML 分析器可理解的基元（如数值），则会尝试直接转换字符串。 如果值是枚举，则字符串用于检查是否存在与该枚举中的命名常量匹配的名称。 如果值既不是分析器可理解的基元，也不是枚举，则所讨论的类型必须能够基于转换后的字符串提供类型的实例或值。 可通过指示类型转换器类达到此目的。 类型转换器实际上是提供其他类的值的帮助器类，可用于的 XAML 方案和 .NET 代码中的代码调用。  
  
### <a name="using-existing-type-conversion-behavior-in-xaml"></a>在 XAML 中使用现有的类型转换行为  
 你可能已经在基础应用程序 XAML 中使用了类型转换行为，只是你还不知道，具体取决于你对基础 XAML 概念的熟悉程度。 例如，WPF 定义成百上千个采用类型的值的属性<xref:System.Windows.Point>。 一个<xref:System.Windows.Point>是描述二维坐标空间中中的坐标的值，它实际上只是具有两个重要属性：<xref:System.Windows.Point.X%2A>和<xref:System.Windows.Point.Y%2A>。 如果在 XAML 中指定一个点，将其指定为分隔符 （通常为逗号） 的字符串之间<xref:System.Windows.Point.X%2A>和<xref:System.Windows.Point.Y%2A>你提供的值。 例如：`<LinearGradientBrush StartPoint="0,0" EndPoint="1,1"/>`。  
  
 即使这种简单的<xref:System.Windows.Point>，而其简单的用法在 XAML 中涉及的类型转换器。 在这种情况下，这是类<xref:System.Windows.PointConverter>。  
  
 类型转换器<xref:System.Windows.Point>采用的所有属性的标记用法定义在类级别简化<xref:System.Windows.Point>。 如果没有类型转换器，那么对于前面显示的同一示例，将需要更冗长的标记，如下所示：  

```xaml
<LinearGradientBrush>
  <LinearGradientBrush.StartPoint>
    <Point X="0" Y="0"/>
  </LinearGradientBrush.StartPoint>
  <LinearGradientBrush.EndPoint>
    <Point X="1" Y="1"/>
  </LinearGradientBrush.EndPoint>
</LinearGradientBrush>
 ```
  
 使用类型转换字符串或使用更复杂的等效语法通常是编码风格的选择。 XAML 工具工作流也可能会影响值的设置方式。 某些 XAML 工具可能会生成最复杂的标记窗体，以便更容易往返于设计器视图或其自身的序列化机制。  
  
 现有的类型转换器可以通常会发现 WPF 和.NET Framework 类型通过检查类 （或属性） 的应用是否存在<xref:System.ComponentModel.TypeConverterAttribute>。 此属性将对支持类型转换器转换类型的值的类进行命名，用于 XAML 或其他可能的用途。  
  
### <a name="type-converters-and-markup-extensions"></a>类型转换器和标记扩展  
 标记扩展和类型转换器根据 XAML 处理器行为及其应用场景来实现正交角色。 尽管上下文可用于标记扩展用途，但通常不会在标记扩展实现中检查属性的类型转换行为（其中标记扩展提供了一个值）。 换言之，即使标记扩展返回一个文本字符串作为其 `ProvideValue` 输出，该字符串上应用于特定属性或属性值类型的类型转换行为也不会被调用。通常，标记扩展的目的是在不调用任何类型转换器的情况下，处理字符串和返回对象。  
  
 需要标记扩展而不是类型转换器的一种常见情况是使对已存在的对象进行引用。 无状态类型转换器最多只能生成新实例，这可能并不理想。 若要深入了解标记扩展，请参阅[标记扩展和 WPF XAML](markup-extensions-and-wpf-xaml.md)。  
  
### <a name="native-type-converters"></a>本机类型转换器  
 在 XAML 分析器的 WPF 和 .NET XAML 实现中，某些特定类型具有本机类型转换处理，但在传统上可能不会将这些类型视为基元。 这种类型的一个示例是 <xref:System.DateTime>。 这样做的原因基于.NET Framework 体系结构的工作原理： 类型<xref:System.DateTime>在 mscorlib，在.NET 中最基本的库中定义。 <xref:System.DateTime> 不允许使用来自引入依赖关系的另一个程序集的属性特性 (<xref:System.ComponentModel.TypeConverterAttribute>来自系统) 因此不能支持通过特性的正常类型转换器发现机制。 相反，XAML 分析器具有需要此类本机处理的类型的列表，它可通过与真正基元的处理方式类似的方式来处理这些类型。 (的情况下<xref:System.DateTime>这涉及调用<xref:System.DateTime.Parse%2A>。)  
  
<a name="Implementing_a_Type_Converter"></a>   
## <a name="implementing-a-type-converter"></a>实现类型转换器  
  
### <a name="typeconverter"></a>TypeConverter  
 在中<xref:System.Windows.Point>以前，给定类的示例<xref:System.Windows.PointConverter>提到过。 适用于 XAML 的.NET 实现，用于 XAML 目的的所有类型转换器都是从基类派生的类<xref:System.ComponentModel.TypeConverter>。 <xref:System.ComponentModel.TypeConverter>类存在于版本的.NET Framework 出现之前的 XAML 中; 其原始用法之一是提供可视化设计器中的属性对话框的字符串转换。 为 XAML 的角色<xref:System.ComponentModel.TypeConverter>扩展以包含要启用分析字符串特性值，并可能返回到一个字符串处理特定对象属性的运行时间值的字符串到和从字符串转换类的基类为属性的序列化。  
  
 <xref:System.ComponentModel.TypeConverter> 定义了四个成员与相关的转换以及从 XAML 处理用途的字符串转换为：  
  
-   <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A>  
  
-   <xref:System.ComponentModel.TypeConverter.CanConvertFrom%2A>  
  
-   <xref:System.ComponentModel.TypeConverter.ConvertTo%2A>  
  
-   <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A>  
  
 其中，最重要的方法是<xref:System.ComponentModel.TypeConverter.ConvertFrom%2A>。 此方法将输入字符串转换为所需的对象类型。 严格地说，<xref:System.ComponentModel.TypeConverter.ConvertFrom%2A>方法可以实现更广泛的类型转换为转换器的预期的目标类型，并因此有超出 XAML，如支持运行时的转换，但出于 XAML 目的的用途这是可以处理的代码路径<xref:System.String>很重要的输入。  
  
 下一步最重要的方法是<xref:System.ComponentModel.TypeConverter.ConvertTo%2A>。 如果应用程序转换为标记表示形式 （例如，如果它已保存到 XAML 作为一个文件），<xref:System.ComponentModel.TypeConverter.ConvertTo%2A>负责生成标记表示形式。 在这种情况下，对 XAML 很重要的代码路径是传递`destinationType`的<xref:System.String>。  
  
 <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A> 和 <xref:System.ComponentModel.TypeConverter.CanConvertFrom%2A> 是在服务查询 <xref:System.ComponentModel.TypeConverter> 实现的功能时使用的支持方法。 必须实现这些方法以便为转换器的等效转换方法支持的特定于类型的情况返回 `true` 。 对于 XAML 用途，这通常意味着 <xref:System.String> 类型。  
  
### <a name="culture-information-and-type-converters-for-xaml"></a>XAML 的区域性信息和类型转换器  
 每个<xref:System.ComponentModel.TypeConverter>实现可以有其自己的什么构成有效的字符串转换，解释，还可以使用或忽略作为参数传递的类型说明。 对于区域性和 XAML 类型转换，有一个重要的注意事项。 XAML 完全支持使用可本地化的字符串作为特性值。 但不支持将该可本地化字符串用作具有特定区域性要求的类型转换器输入，因为 XAML 特性值的类型转换器包含一个必要的固定语言分析行为，该行为使用 `en-US` 区域性。 有关此限制的设计原因的更多信息，请查阅 XAML 语言规范 ([\[MS-XAML\]](https://go.microsoft.com/fwlink/?LinkId=114525))。  
  
 区域性可能会产生问题的示例之一是，某些区域性使用逗号作为数字的小数点分隔符。 这将与许多 WPF XAML 类型转换器所具有的使用逗号作为分隔符的行为发生冲突（根据常用的 X,Y 形式等过去的先例，或逗号分隔的列表）。 即使在周围的 XAML 中传递区域性（将 `Language` 或 `xml:lang` 设置为 `sl-SI` 区域性，以此方式使用逗号作为小数点的区域性的一个示例）也不能解决此问题。  
  
### <a name="implementing-convertfrom"></a>实现 ConvertFrom  
 若要能够用作支持 XAML 的 <xref:System.ComponentModel.TypeConverter> 实现，该转换器的 <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> 方法必须接受字符串作为 `value` 参数。 如果字符串的有效格式，并可以通过转换<xref:System.ComponentModel.TypeConverter>实现中，则返回的对象必须支持强制转换为属性预期的类型。 否则， <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> 实现必须返回 `null`。  
  
 每个<xref:System.ComponentModel.TypeConverter>实现可以具有其自己的什么构成有效的字符串转换，解释，还可以使用或忽略作为参数传递的类型说明或区域性上下文。 但是，WPF XAML 处理可能不会在所有情况下都将值传递给类型说明上下文，还可能不会基于 `xml:lang` 传递区域性。  
  
> [!NOTE]
>  请勿使用大括号字符（尤其是 {）作为字符串格式的可能元素。 这些字符保留作为标记扩展序列的入口和出口。  
  
### <a name="implementing-convertto"></a>实现 ConvertTo  
 <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> 可能用于序列化支持。 通过 <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> 为自定义类型及其类型转换器实现的序列化支持不是绝对要求。 但是，如果要实现控件，或使用序列化作为类的功能或设计的一部分，则应实现 <xref:System.ComponentModel.TypeConverter.ConvertTo%2A>。  
  
 若要能够用作<xref:System.ComponentModel.TypeConverter>支持 XAML，实现<xref:System.ComponentModel.TypeConverter.ConvertTo%2A>该转换器的方法必须接受的类型 （或值），它支持实例作为`value`参数。 当`destinationType`参数的类型为<xref:System.String>，则返回的对象必须能够强制转换为<xref:System.String>。 返回字符串必须表示 `value`的序列化值。 理想情况下，你选择的序列化格式应能够生成相同的值，如果该字符串传递到<xref:System.ComponentModel.TypeConverter.ConvertFrom%2A>而丢失大量信息不相同转换器的实现。  
  
 如果值不能序列化，或转换器不支持序列化<xref:System.ComponentModel.TypeConverter.ConvertTo%2A>实现必须返回`null`，并允许在此情况下引发异常。 如果引发了异常，则应报告无法使用该转换作为的一部分，但你<xref:System.ComponentModel.TypeConverter.CanConvertTo%2A>实现，以便检查功能的最佳做法<xref:System.ComponentModel.TypeConverter.CanConvertTo%2A>首先以避免异常支持。  
  
 如果`destinationType`参数的类型不是<xref:System.String>，可以选择自己的转换器处理。 通常情况下，你要恢复处理，这会在最基本的基实现<xref:System.ComponentModel.TypeConverter.ConvertTo%2A>引发特定异常。  
  
### <a name="implementing-canconvertto"></a>实现 CanConvertTo  
 对于 <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A> 类型的 `true` ， `destinationType` 实现应返回 <xref:System.String>，否则遵从基实现。  
  
### <a name="implementing-canconvertfrom"></a>实现 CanConvertFrom  
 对于 <xref:System.ComponentModel.TypeConverter.CanConvertFrom%2A> 类型的 `true` ， `sourceType` 实现应返回 <xref:System.String>，否则遵从基实现。  
  
<a name="Applying_the_TypeConverterAttribute"></a>   
## <a name="applying-the-typeconverterattribute"></a>应用 TypeConverterAttribute  
 为了使你的自定义类型转换器作为使用由 XAML 处理器的自定义类的类型转换器，必须应用[!INCLUDE[TLA#tla_netframewkattr](../../../../includes/tlasharptla-netframewkattr-md.md)]<xref:System.ComponentModel.TypeConverterAttribute>向类定义。 通过特性指定的 <xref:System.ComponentModel.TypeConverterAttribute.ConverterTypeName%2A> 必须是自定义类型转换器的类型名。 应用此特性后，当 XAML 处理器处理属性类型使用自定义类类型的值时，它可以输入字符串并返回对象实例。  
  
 还可以基于每个属性提供类型转换器。 应将 [!INCLUDE[TLA#tla_netframewkattr](../../../../includes/tlasharptla-netframewkattr-md.md)] <xref:System.ComponentModel.TypeConverterAttribute> 应用于属性定义（主定义，不是它包含的 `get`/`set` 的实现），而不是将它应用于类定义。 属性的类型必须与自定义类型转换器处理的类型匹配。 应用此特性后，当 XAML 处理器处理该属性的值时，它可以处理输入字符串并返回对象实例。 每个属性类型转换器方法会特别有用，如果您选择使用 Microsoft.NET Framework 中或某些其他库其中无法控制类定义并且无法应用的属性类型<xref:System.ComponentModel.TypeConverterAttribute>存在。  
  
## <a name="see-also"></a>请参阅
- <xref:System.ComponentModel.TypeConverter>
- [XAML 概述 (WPF)](xaml-overview-wpf.md)
- [标记扩展和 WPF XAML](markup-extensions-and-wpf-xaml.md)
- [XAML 语法详述](xaml-syntax-in-detail.md)
