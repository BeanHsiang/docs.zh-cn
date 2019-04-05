---
title: .NET Framework XAML 服务的 XAML 命名空间
ms.date: 03/30/2017
ms.assetid: e4f15f13-c420-4c1e-aeab-9b6f50212047
ms.openlocfilehash: e9d644f4f62d70a1feec0030a680067412baa5e6
ms.sourcegitcommit: 5c1abeec15fbddcc7dbaa729fabc1f1f29f12045
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2019
ms.locfileid: "58030520"
---
# <a name="xaml-namespaces-for-net-framework-xaml-services"></a>.NET Framework XAML 服务的 XAML 命名空间
XAML 命名空间是扩展的定义中的 XML 命名空间的概念。 类似于 XML 命名空间，您可以定义 XAML 命名空间使用`xmlns`标记中的属性。 在 XAML 节点流和其他 XAML 服务 Api 中还表示 XAML 命名空间。 本主题定义 XAML 命名空间概念，并说明如何 XAML 命名空间可以定义和使用的 XAML 架构上下文和.NET Framework XAML 服务的其他方面。  
  
## <a name="xml-namespace-and-xaml-namespace"></a>XML Namespace 和 XAML Namespace  
 XAML 命名空间是一个专用的 XML 命名空间，正如 XAML 是一种特殊的形式的 XML 和其标记为使用基本的 XML 格式。 在标记中，声明 XAML 命名空间和通过其映射`xmlns`应用于某个元素的属性。 `xmlns`声明可为 XAML 命名空间声明中的同一元素。 对元素的 XAML 命名空间声明是有效的该元素，该元素的所有属性和该元素的所有子文件夹。 属性可以使用不包含属性的元素相同，只要本身的属性名称作为其标记中的属性名称的一部分引用前缀的 XAML 命名空间。  
  
 XML 命名空间可用于引用架构，或可能用于只是区分实体，而不是 XML 命名空间的 XAML 命名空间的区别。 为 XAML 的类型和成员，因为在 XAML 中使用最终必须解析为后备类型，并且很好地适应此功能不适用于 XML 架构概念。 XAML 命名空间包含的 XAML 架构上下文必须具有可用于执行此类型映射信息。  
  
## <a name="xaml-namespace-components"></a>XAML Namespace 组件  
 该 XAML 命名空间定义了两个组件： 前缀和标识符。 每个组件都存在时在标记中，声明或 XAML 类型系统中定义的 XAML 命名空间。  
  
 前缀可以是任意字符串，因为允许通过[W3C XML 1.0 规范中的命名空间](https://go.microsoft.com/fwlink/?LinkID=161735)。 按照约定的前缀是通常很短的字符串，因为该前缀典型的标记文件中重复多次。 用于在多个 XAML 实现中使用某些 XAML 命名空间使用特定的传统前缀。 例如，在 XAML 语言 XAML 命名空间值通常映射使用前缀`x`。 您可以定义默认 XAML 命名空间，其中前缀定义中未提供，但如果定义，或者查询 by.NET Framework XAML 服务 API 都表示为一个空字符串。 通常情况下，为了最大的前缀省略有意选择默认 XAML 命名空间由 XAML 实现的技术及其方案和词汇标记。  
  
 标识符可以是任何字符串，因为允许通过[W3C XML 1.0 规范中的命名空间](https://go.microsoft.com/fwlink/?LinkID=161735)。 按照惯例，XML 命名空间或 XAML 命名空间标识符通常给出了 URI 形式，通常作为协议限定的绝对 URI。 通常情况下，用于定义特定的 XAML 词汇的版本信息则暗指路径字符串的一部分。 XAML 命名空间添加一个附加标识符约定超出 XML URI 约定。 对于 XAML 命名空间标识符通信所需的 XAML 架构上下文来解析被指定为该 XAML 命名空间下的元素的类型，或将解析为成员的属性的信息。  
  
 对于信息传达给 XAML 架构上下文，XAML 命名空间的标识符仍可能采用 URI 形式。 但是，在这种情况下 URI 也声明为一个特定的程序集或程序集的列表中的匹配标识符。 这是在程序集通过使用程序集<xref:System.Windows.Markup.XmlnsDefinitionAttribute>。 此方法确定的 XAML 命名空间并支持基于 CLR 的类型解析行为中的特性化程序集的受.NET Framework XAML 服务中的默认 XAML 架构上下文。 一般来说，此约定可用于 XAML 架构上下文包含 CLR 或基于为 CLR 程序集从读取 CLR 属性是必需的默认 XAML 架构上下文的情况。  
  
 XAML 命名空间，也可以识别的 CLR 命名空间和类型定义的程序集进行通信的约定。 此约定用于在情况下，在不<xref:System.Windows.Markup.XmlnsDefinitionAttribute>归属存在于包含类型的程序集。 此约定可能比 URI 约定，更复杂而还有可能存在二义性和重复数据删除，因为有多个方法的引用程序集。  
  
 使用 CLR 命名空间和程序集约定的标识符的最基本形式如下所示：  
  
 `clr-namespace:` *clrnsName* `; assembly=` *assemblyShortName*  
  
 `clr-namespace:` 和`; assembly=`是文本的语法组件。  
  
 *clrnsName*是标识 CLR 命名空间的字符串名称。 此字符串名称包括提供有关 CLR 命名空间和其他 CLR 命名空间之间的关系的提示的任何内部圆点字符 （.）。  
  
 *程序集短名称*是定义可在 XAML 中的类型的程序集的字符串名称。 要通过声明 XAML 命名空间进行访问的类型定义的程序集，特别是在指定的 CLR 命名空间中声明预期*clrnsName*。 此字符串名称通常与信息报告的<xref:System.Reflection.AssemblyName.Name%2A?displayProperty=nameWithType>。  
  
 更完整的 CLR 命名空间和程序集约定的定义如下所示：  
  
 `clr-namespace:` *clrnsName* `; assembly=` *assemblyName*  
  
 *程序集名称*表示作为是合法的任何字符串<xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=nameWithType>输入。 此字符串可以包括区域性、 公钥或版本信息 (这些概念的定义中的参考主题定义<xref:System.Reflection.Assembly>)。 COFF 格式和证据 (由另一个重载<xref:System.Reflection.Assembly.Load%2A>) 不相关的 XAML 程序集加载目的; 所有负载信息必须都显示为字符串。  
  
 指定程序集的公共密钥是为了 XAML 安全性，也可以消除可能的多义性，如果程序集加载的简单名称或预先缓存或应用程序域中存在可存在的有用技术。 有关详细信息，请参阅[XAML 安全注意事项](xaml-security-considerations.md)。  
  
## <a name="xaml-namespace-declarations-in-the-xaml-services-api"></a>XAML 服务 API 中的 XAML Namespace 声明  
 在 XAML 服务 API 中，XAML 命名空间声明为由<xref:System.Xaml.NamespaceDeclaration>对象。 如果你将声明代码中的 XAML 命名空间，则调用<xref:System.Xaml.NamespaceDeclaration.%23ctor%28System.String%2CSystem.String%29>构造函数。 `ns`和`prefix`参数被指定为字符串，并如本主题中提供以前，要为这些参数提供的输入对应于 XAML 命名空间标识符和 XAML 命名空间前缀的定义。  
  
 如果你正在检查 XAML 节点流的一部分或通过其他访问 XAML 类型系统，为 XAML 命名空间信息<xref:System.Xaml.NamespaceDeclaration.Namespace%2A?displayProperty=nameWithType>报告的 XAML 命名空间标识符，和<xref:System.Xaml.NamespaceDeclaration.Prefix%2A?displayProperty=nameWithType>报告的 XAML 命名空间前缀。  
  
 在 XAML 节点流中，XAML 命名空间信息可以显示为 XAML 节点之前它所应用于的实体。 这包括其中的 XAML 命名空间信息之前的情况下`StartObject`的 XAML 根元素。 有关更多信息，请参见 [Understanding XAML Node Stream Structures and Concepts](understanding-xaml-node-stream-structures-and-concepts.md)。  
  
 对于使用.NET Framework XAML 服务 API 的许多情况下，应至少一个 XAML 命名空间声明存在，并声明必须包含或指的所需的 XAML 架构上下文信息。 XAML 命名空间必须指定要加载的或帮助解决命名空间和已加载或已知的 XAML 架构上下文的程序集内的特定类型的程序集。  
  
 为了生成 XAML 节点流，必须通过 XAML 架构上下文提供 XAML 类型信息。 而无需首先确定要创建每个节点相关的 XAML 命名空间，无法确定的 XAML 类型信息。 此时，尚未，创建的任何类型实例，但 XAML 架构上下文可能需要查找来自定义程序集和备份类型的信息。 例如，若要处理标记`<Party><PartyFavor/></Party>`，必须能够确定的名称和类型的 XAML 架构上下文`ContentProperty`的`Party`，并因此还必须知道的 XAML 命名空间信息`Party`和`PartyFavor`。 对于默认 XAML 架构上下文中，静态反射会报告很多在节点流中生成 XAML 类型的节点所需的 XAML 类型系统信息。  
  
 若要从 XAML 节点流生成对象图，请在原始标记中使用并记录在 XAML 节点流中的每个 XAML 前缀必须存在 XAML 命名空间声明。 此时，正在创建实例，并且会出现，则返回 true 的类型映射行为。  
  
 如果您需要用于预先填充 XAML 命名空间中的信息，其中在标记中，未定义你想要使用的 XAML 架构上下文的 XAML 命名空间的情况下可以使用一种方法是声明中的 XML 命名空间声明<xref:System.Xml.XmlParserContext>为<xref:System.Xml.XmlReader>. 然后，使用该<xref:System.Xml.XmlReader>作为 XAML 读取器，构造函数的输入或<xref:System.Xaml.XamlServices.Load%28System.Xml.XmlReader%29?displayProperty=nameWithType>。  
  
 相关的.NET Framework XAML 服务中处理的 XAML 命名空间的两个其他 API 是属性<xref:System.Windows.Markup.XmlnsDefinitionAttribute>和<xref:System.Windows.Markup.XmlnsPrefixAttribute>。 这些属性适用于程序集。 <xref:System.Windows.Markup.XmlnsDefinitionAttribute> 可供 XAML 架构上下文来解释包含 URI 的任何 XAML 命名空间声明。 <xref:System.Windows.Markup.XmlnsPrefixAttribute> 使用发出 XAML，以便特定 XAML 命名空间可以使用可预测的前缀进行序列化的工具。 有关详细信息，请参阅[XAML-Related CLR 特性自定义类型和库的](xaml-related-clr-attributes-for-custom-types-and-libraries.md)。  
  
## <a name="see-also"></a>请参阅
- [了解 XAML 节点流结构和概念](understanding-xaml-node-stream-structures-and-concepts.md)
