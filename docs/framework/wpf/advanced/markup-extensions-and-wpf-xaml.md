---
title: 标记扩展和 WPF XAML
ms.date: 03/30/2017
helpviewer_keywords:
- brace character [WPF]
- Binding markup extensions [WPF]
- RelativeSource markup extensions [WPF]
- XAML [WPF], markup extensions
- markup extensions [WPF]
- nesting extension syntax [WPF]
- curly brace characters ({})
- TemplateBinding markup extensions [WPF]
- StaticResource markup extensions [WPF]
- literal curly brace characters ({})
- characters [WPF], curly brace
- DynamicResource markup extensions [WPF]
ms.assetid: 618dc745-8b14-4886-833f-486d2254bb78
ms.openlocfilehash: e678dcf9606c3ad545e93a4389bccb3d49423dec
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57355228"
---
# <a name="markup-extensions-and-wpf-xaml"></a>标记扩展和 WPF XAML
本主题介绍 XAML 的标记扩展概念，包括其语法规则、用途以及作为其基础的类对象模型。 标记扩展是 XAML 语言以及 XAML 服务的 .NET 实现的常规功能。 本主题专门详细讨论用于 WPF XAML 的标记扩展。  
  
  
<a name="XAML_Processors_and_Markup_Extensions"></a>   
## <a name="xaml-processors-and-markup-extensions"></a>XAML 处理器和标记扩展  
 通常，XAML 分析器可将特性值解释为可转换成基元的文本字符串，或可通过某种方法将特性值转换为对象。 其中一种方法是引用类型转换器；详情请参阅主题 [TypeConverters 和 XAML](typeconverters-and-xaml.md)。 不过，也存在要求其他行为的情况。 例如，可以指示 XAML 处理器，特性的值不应在对象图中生成新对象。 相反，特性应生成引用对象图另一部分中的已构造对象或引用静态对象的对象图。 另一种情况是，可以指示 XAML 处理器使用向对象的构造函数提供非默认参数的语法。 在这些类型的情况中，标记扩展可以提供解决方案。  
  
<a name="Basic_Markup_Extension_Syntax"></a>   
## <a name="basic-markup-extension-syntax"></a>基本标记扩展语法  
 可以实现标记扩展来为特性用法中的属性和/或属性元素用法中的属性提供值。  
  
 当用于提供特性值时，将标记扩展序列与 XAML 处理器区分开的语法是左右大括号（{ 和 }）。 然后，由紧跟在左大括号后面的字符串标记来标识标记扩展的类型。  
  
 当用在属性元素语法中时，标记扩展在外观上与任何其他用于提供属性元素值的元素相同，即：一个将标记扩展类作为元素引用并以尖括号 (<>) 括起的 XAML 元素声明。  
  
<a name="XAML_Defined_Markup_Extensions"></a>   
## <a name="xaml-defined-markup-extensions"></a>XAML 定义的标记扩展  
 存在这么几种标记扩展，它们并非特定于 XAML 的 WPF 实现，而是语言形式的 XAML 的内部函数或功能的实现。 这些标记扩展在 System.Xaml 程序集中作为常规 .NET Framework XAML 服务的一部分而实现，并且位于 XAML 语言 XAML 命名空间内。 就常见标记用法而言，这些标记扩展通常可由用法中的 `x:` 前缀标识。 <xref:System.Windows.Markup.MarkupExtension>基类 （也在 System.Xaml 中定义） 提供了所有标记扩展应都使用以支持在 XAML 读取器和 XAML 编写器，包括 WPF XAML 中的模式。  
  
-   `x:Type` 为命名类型提供 <xref:System.Type> 对象。 此扩展最常用于样式和模板。 有关详细信息，请参阅 [x:Type 标记扩展](../../xaml-services/x-type-markup-extension.md)。  
  
-   `x:Static` 生成静态值。 这些值来自于值类型代码实体，它们不直接是目标属性值的类型，但可以计算为该类型。 有关详细信息，请参阅 [x:Static 标记扩展](../../xaml-services/x-static-markup-extension.md)。  
  
-   `x:Null` 将 `null` 指定为属性的值，可用于特性或属性元素值。 有关详细信息，请参阅 [x:Null 标记扩展](../../xaml-services/x-null-markup-extension.md)。  
  
-   在特意不使用 WPF 基元素和控件模型提供的集合支持的情况下，`x:Array` 为 XAML 语法中常规数组的创建提供支持。 有关详细信息，请参阅 [x:Array 标记扩展](../../xaml-services/x-array-markup-extension.md)。  
  
> [!NOTE]
>  `x:` 前缀在 XAML 文件或生成的根元素中用于 XAML 语言内部函数的典型 XAML 命名空间映射。 例如，WPF 应用程序的 Visual Studio 模板启动使用这一个 XAML 文件`x:`映射。 可以在自己的 XAML 命名空间映射中选择不同的前缀标记，但本文档将采用默认的 `x:` 映射，并通过它来标识属于 XAML 语言的 XAML 命名空间已定义部分的那些实体，这与 WPF 默认命名空间或与特定框架不相关的其他 XAML 命名空间相反。  
  
<a name="WPF_Specific_Markup_Extensions"></a>   
## <a name="wpf-specific-markup-extensions"></a>特定于 WPF 的标记扩展  
 WPF 编程中最常用的标记扩展是支持资源引用的标记扩展（`StaticResource` 和 `DynamicResource`），和支持数据绑定的标记扩展 (`Binding`)。  
  
-   `StaticResource` 通过替换已定义资源的值来为属性提供值。 `StaticResource` 计算最终在 XAML 加载时进行，并且在运行时没有访问对象图的权限。 有关详细信息，请访问 [StaticResource 标记扩展](staticresource-markup-extension.md)。  
  
-   `DynamicResource` 通过将值推迟为对资源的运行时引用来为属性提供值。 动态资源引用强制在每次访问此类资源时都进行新查找，且在运行时有权访问对象图。 为了获取此访问权限，WPF 属性系统中的依赖项属性和计算出的表达式支持 `DynamicResource` 概念。 因此，只能对依赖项属性目标使用 `DynamicResource`。 有关详细信息，请参阅 [DynamicResource 标记扩展](dynamicresource-markup-extension.md)。  
  
-   `Binding` 使用在运行时应用于父对象的数据上下文来为属性提供数据绑定值。 此标记扩展相对复杂，因为它会启用大量内联语法来指定数据绑定。 有关详细信息，请参阅 [Binding 标记扩展](binding-markup-extension.md)。  
  
-   `RelativeSource` 提供源信息<xref:System.Windows.Data.Binding>，可以定位在运行时对象树中的若干可能关系。 对于在多用途模板中创建的绑定，或在未充分了解周围的对象树的情况下以代码创建的绑定，此标记扩展为其提供专用源。 有关详细信息，请参阅 [RelativeSource 标记扩展](relativesource-markupextension.md)。  
  
-   `TemplateBinding` 使控件模板能够使用模板化属性的值，这些属性来自于将使用该模板的类的对象模型定义属性。 换言之，模板定义中的属性可访问仅在应用了模板之后才存在的上下文。 有关详细信息，请参阅 [TemplateBinding 标记扩展](templatebinding-markup-extension.md)。 有关 `TemplateBinding` 的实际使用的详细信息，请参阅[使用 ControlTemplates 设置样式示例](https://github.com/Microsoft/WPF-Samples/tree/master/Styles%20&%20Templates/IntroToStylingAndTemplating)。  
  
-   `ColorConvertedBitmap` 支持相对高级的映像方案。 有关详细信息，请参阅 [ColorConvertedBitmap 标记扩展](colorconvertedbitmap-markup-extension.md)。  
  
-   `ComponentResourceKey` 和 `ThemeDictionary` 支持资源查找的各个方面，特别是支持查找与自定义控件一起打包的资源和主题。 有关详细信息，请参阅 [ComponentResourceKey 标记扩展](componentresourcekey-markup-extension.md)、[ThemeDictionary 标记扩展](themedictionary-markup-extension.md)或[控件创作概述](../controls/control-authoring-overview.md)。  
  
<a name="StarExtension"></a>   
## <a name="extension-classes"></a>*Extension 类  
 对于常规 XAML 语言和特定于 WPF 的标记扩展，通过一个 XAML 处理器的标识的每个标记扩展行为`*Extension`派生的类<xref:System.Windows.Markup.MarkupExtension>，并提供的实现<xref:System.Windows.Markup.StaticExtension.ProvideValue%2A>方法。 每个扩展上的此方法都会提供在计算标记扩展时返回的对象。 通常会基于传递给标记扩展的各个字符串标记来计算返回的对象。  
  
 例如，<xref:System.Windows.StaticResourceExtension>类提供实际资源查找的图面实现，以便其<xref:System.Windows.Markup.MarkupExtension.ProvideValue%2A>实现返回一个字符串，用于该特定实现的输入请求的对象查找资源通过其`x:Key`。 如果使用的是现有标记扩展，则其大部分实现详细信息都无关紧要。  
  
 有些标记扩展不使用字符串标记参数。 这是因为它们返回静态值或一致的值，或者因为应返回何值的上下文可通过经 `serviceProvider` 参数传递的服务之一提供。  
  
 `*Extension` 命名模式的目的是为了实现方便和一致。 XAML 处理器不必将该类标识为支持标记扩展。 只要基本代码包含 System.Xaml 并使用.NET Framework XAML 服务实现，仅需以被识别为 XAML 标记扩展是从派生<xref:System.Windows.Markup.MarkupExtension>和以支持构造语法。 WPF 定义标记扩展启用类不遵循`*Extension`命名模式，例如<xref:System.Windows.Data.Binding>。 原因通常是该类支持纯标记扩展支持以外的方案。 情况下<xref:System.Windows.Data.Binding>，类具有与 XAML 无关的情况下支持运行时访问方法和对象的属性。  
  
### <a name="extension-class-interpretation-of-initialization-text"></a>初始化文本的扩展类解释  
 跟在标记扩展名称后且仍在括号内的字符串标记由 XAML 处理器通过以下方式之一进行解释：  
  
-   逗号始终表示各个标记的分隔符。  
  
-   如果各个分隔的标记不包含任何等号，则每个标记都将被视为构造函数参数。 必须按该签名所期望的类型和该签名所期望的适当顺序给出每个构造函数参数。  
  
    > [!NOTE]
    >  XAML 处理器必须调用与对的数量这一参数计数匹配的构造函数。 出于此原因，如果要实现自定义标记扩展，不提供多个构造函数具有相同数量的参数。 如果多个标记扩展构造函数路径具有相同的参数计数，则不会定义 XAML 处理器的行为方式，但应预计到如果这种情况存在于标记扩展类型定义中，则会允许 XAML 处理器引发有关使用情况的异常。  
  
-   如果各个分隔的标记包含等号，则 XAML 处理器会首先为标记扩展调用默认构造函数。 之后，每个“名称=值”对会解释为标记扩展上存在的属性名称以及赋给该属性的值。  
  
-   如果标记扩展中的构造函数行为与属性设置行为之间存在并行结果，则使用哪个行为都无关紧要。 较常见的用法是将“属性`=`值”对用于具有多个可设置属性的标记扩展，因为这可使标记意图性更强，并减少意外转置构造函数参数的可能性。 （当指定“属性=值”对时，这些属性可以按任意顺序排列。）另外，无法保证标记扩展提供设置其每个可设置属性的构造函数参数。 例如，<xref:System.Windows.Data.Binding>是标记扩展，具有许多可通过扩展以设置的属性*属性*`=`*值*窗体，但<xref:System.Windows.Data.Binding>仅支持两个构造函数： 默认构造函数和一个设置初始路径。  
  
-   文本逗号在未转义的情况下无法传递给标记扩展。  
  
<a name="EscapeSequences"></a>   
## <a name="escape-sequences-and-markup-extensions"></a>转义序列和标记扩展  
 XAML 处理器中的特性处理使用大括号作为标记扩展序列的指示符。 必要时，也可以使用后跟文本大括号的空大括号对输入转义序列，来生成文本大括号字符特性值。 请参阅[{}转义序列-标记扩展](../../xaml-services/escape-sequence-markup-extension.md)。  
  
<a name="Nesting"></a>   
## <a name="nesting-markup-extensions-in-xaml-usage"></a>XAML 中的嵌套标记扩展用法  
 支持多个标记扩展的嵌套，并且将首先计算每个标记扩展的最里层。 例如，考虑下面的用法：  
  
```  
<Setter Property="Background"  
  Value="{DynamicResource {x:Static SystemColors.ControlBrushKey}}" />  
```  
  
 在此用法中，将首先计算 `x:Static` 语句并返回字符串。 该字符串随后用作 `DynamicResource` 的参数。  
  
## <a name="markup-extensions-and-property-element-syntax"></a>标记扩展和属性元素语法  
 当用作填写属性元素值的对象元素时，标记扩展类在外观上与可用在 XAML 中的基于典型类型的对象元素没有区别。 典型对象元素与标记扩展之间的实际差异是，标记扩展要么计算为类型化值，要么延迟为表达式。 因此，标记扩展的属性值的任何可能类型错误的机制都将是不同的，这与在其他编程模型中处理后期绑定属性的方式类似。 普通对象元素将针对分析 XAML 时它设置的目标属性进行类型匹配计算。  
  
 当用在对象元素语法中以填充属性元素时，大多数标记扩展都不会包含任何内容或深层属性元素语法。 这样你便可以关闭对象元素标记，而不提供任何子元素。 不论何时 XAML 处理器遇到任何对象元素，都会调用该类的构造函数来实例化从已分析元素创建的对象。 标记扩展类也一样：如果希望标记扩展可在对象元素语法中使用，就必须提供默认构造函数。 有些现有标记扩展具有至少一个必需的属性值，必须指定该属性值才能使实例化生效。 如果是这样，该属性值通常会作为对象元素上的属性特性而给出。 在[XAML Namespace （x:）语言功能](../../xaml-services/xaml-namespace-x-language-features.md)并[WPF XAML 扩展](wpf-xaml-extensions.md)参考页中，将显示具有所需的属性 （和所需属性的名称） 的扩展的标记。 参考页还将指出特定标记扩展是否禁止使用对象元素语法或特性语法。 需要注意 [x:Array 标记扩展](../../xaml-services/x-array-markup-extension.md)，它无法支持特性语法，因为该数组的内容必须在标记内作为内容指定。 数组内容的处理方式与常规对象一样，因此特性可以没有默认的类型转换器。 此外，[x:Array 标记扩展](../../xaml-services/x-array-markup-extension.md)需要 `type` 参数。  
  
## <a name="see-also"></a>请参阅
- [XAML 概述 (WPF)](xaml-overview-wpf.md)
- [XAML Namespace （x:）语言功能](../../xaml-services/xaml-namespace-x-language-features.md)
- [WPF XAML 扩展](wpf-xaml-extensions.md)
- [StaticResource 标记扩展](staticresource-markup-extension.md)
- [绑定标记扩展](binding-markup-extension.md)
- [DynamicResource 标记扩展](dynamicresource-markup-extension.md)
- [x:Type 标记扩展](../../xaml-services/x-type-markup-extension.md)
