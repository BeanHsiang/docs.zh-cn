---
title: 依赖项属性元数据
ms.date: 03/30/2017
helpviewer_keywords:
- APIs [WPF], metadata
- dependency properties [WPF], metadata
- metadata [WPF], for dependency properties
- overriding metadata [WPF]
ms.assetid: d01ed009-b722-41bf-b82f-fe1a8cdc50dd
ms.openlocfilehash: 7a9f4c2c8c9ff6c315b9d7189d5e859a902c3e4d
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57352927"
---
# <a name="dependency-property-metadata"></a>依赖项属性元数据
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 属性系统包括一个元数据报告系统，该系统不局限于可以通过反射或常规[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 特征报告的关于某个属性的内容。 依赖属性的元数据还可以由定义依赖属性的类来唯一地分配，可以在依赖属性添加到另一个类时进行更改，可以由所有从定义基类继承依赖属性的派生类来明确地重写。  
  
 
  
<a name="prerequisites"></a>   
## <a name="prerequisites"></a>系统必备  
 本主题假定你从 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 类的现有依赖属性的使用者角度了解依赖属性，并且已阅读[依赖属性概述](dependency-properties-overview.md)。 若要理解本主题中的示例，还应当了解 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 并知道如何编写 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序。  
  
<a name="dp_metadata_contents"></a>   
## <a name="how-dependency-property-metadata-is-used"></a>依赖属性元数据的使用方式  
 依赖属性的元数据作为一个对象存在，可以通过查询该对象来检查依赖属性的特征。 当属性系统处理任何给定的依赖属性时，也会经常访问这些元数据。 依赖属性的元数据对象可以包含以下类型的信息：  
  
-   依赖属性的默认值（如果通过本地值、样式和继承等信息不能确定依赖属性的其他任何值）。有关在为依赖属性赋值时，默认值如何参与属性系统所使用的优先级的完整讨论，请参阅[依赖属性值优先级](dependency-property-value-precedence.md)。  
  
-   对影响每个所有者类型的强制行为或更改通知行为的回叫实现的引用。 请注意，这些回叫通常是用非公共访问级别定义的，因此，除非实际引用位于允许的访问范围内，否则通常无法从元数据获得这些引用。 有关依赖属性回叫的详细信息，请参阅[依赖属性回调和验证](dependency-property-callbacks-and-validation.md)。  
  
-   如果所讨论的依赖属性被视为一个 WPF 框架级别的属性，则元数据中可能包含 WPF 框架级别的依赖属性特征，这些特征报告各种服务（如 WPF 框架级别的布局引擎和属性继承逻辑）的信息和状态。 有关依赖属性元数据的这一方面的详细信息，请参阅[框架属性元数据](framework-property-metadata.md)。  
  
<a name="APIs"></a>   
## <a name="metadata-apis"></a>元数据 API  
 报告的大多数属性系统使用的元数据信息的类型是<xref:System.Windows.PropertyMetadata>类。 在向属性系统注册依赖属性时，可以选择指定元数据实例，并且可以为以下附加类型再次指定这些实例：将自身作为所有者添加的类型，或者重写它们从基类依赖属性定义继承的元数据的类型。 (未指定默认值的元数据属性注册的情况下为<xref:System.Windows.PropertyMetadata>创建该类的默认值。)作为返回的已注册的元数据<xref:System.Windows.PropertyMetadata>当您调用各种<xref:System.Windows.DependencyProperty.GetMetadata%2A>获取依赖属性元数据的重载<xref:System.Windows.DependencyObject>实例。  
  
 <xref:System.Windows.PropertyMetadata>类然后派生自，如 WPF 框架级别类的体系结构区域提供更多特定元数据。 <xref:System.Windows.UIPropertyMetadata> 添加动画报告功能，和<xref:System.Windows.FrameworkPropertyMetadata>提供上一部分中提到的 WPF 框架级别属性。 注册依赖属性之后，他们可以注册使用这些<xref:System.Windows.PropertyMetadata>派生的类。 检查元数据之后，即基<xref:System.Windows.PropertyMetadata>可能进行类型转换为派生类，以使您可以检查更具体的属性。  
  
> [!NOTE]
>  可以在中指定的属性特征<xref:System.Windows.FrameworkPropertyMetadata>有时称为在本文档中称为"标志"。 当你使用新的元数据实例中创建依赖关系属性注册或元数据重写时，指定使用按标志枚举这些值<xref:System.Windows.FrameworkPropertyMetadataOptions>，然后提供到枚举的可能连接的值<xref:System.Windows.FrameworkPropertyMetadata>构造函数。 但是，构造后，这些选项特征公开内<xref:System.Windows.FrameworkPropertyMetadata>作为一系列布尔属性，而不是构造枚举值。 使用布尔属性，可以检查每个条件，而不必为了获得感兴趣的信息而向按标志枚举值应用掩码。 构造函数使用连接<xref:System.Windows.FrameworkPropertyMetadataOptions>为了使构造函数签名的长度合理的而实际构造的元数据公开不同的属性，使查询更直观的元数据。  
  
<a name="override_or_subclass"></a>   
## <a name="when-to-override-metadata-when-to-derive-a-class"></a>何时重写元数据以及何时派生类  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 属性系统已经建立了如下功能：在不必完全重新实现依赖属性的情况下，更改依赖属性的某些特征。 这是通过为特定类型上所存在的依赖属性构造不同的属性元数据实例来完成的。 请注意，现有的大多数依赖属性都不是虚拟属性，因此，严格地说，只能通过隐藏现有成员来针对继承类“重新实现”依赖属性。  
  
 如果尝试对某个类型的依赖属性启用的方案不能通过修改现有依赖属性的特征来完成，则可能有必要创建一个派生类，然后为该派生类声明一个自定义依赖属性。 自定义依赖属性与 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA#tla_api#plural](../../../../includes/tlasharptla-apisharpplural-md.md)] 定义的依赖属性具有相同的行为。 有关自定义依赖属性的更多详细信息，请参阅[自定义依赖属性](custom-dependency-properties.md)。  
  
 不能重写的依赖属性的一个显著特征就是它的值类型。 如果要继承的依赖属性的行为与所需的行为大体相同，但是要求它具有另一种类型，则必须实现一个自定义依赖属性，可能还需要通过类型转换或其他实现机制在自定义类上链接这些属性。 此外，不能替换现有<xref:System.Windows.ValidateValueCallback>，因为此回叫存在于注册字段本身而不是在其元数据。  
  
<a name="scenarios"></a>   
## <a name="scenarios-for-changing-existing-metadata"></a>更改现有元数据的方案  
 如果要处理现有依赖属性的元数据，则更改依赖属性元数据的一种常见方案是更改默认值。 更改或添加属性系统回叫是一种更高级的方案。 如果所实现的派生类的依赖属性之间具有不同的相互关系，则你可能希望这样做。 让编程模型既支持代码又支持声明性用法的条件之一就是，属性必须能够按任何顺序设置。 因此，需要在没有上下文的情况下实时设置任何依赖属性，而且可以不必知道设置顺序（例如，可能在构造函数中找到的顺序）。 有关属性系统这一方面的详细信息，请参阅[依赖属性回调和验证](dependency-property-callbacks-and-validation.md)。 请注意，验证回叫不是元数据的一部分，而是依赖属性标识符的一部分。 因此，不能通过重写元数据来更改验证回叫。  
  
 在某些情况下，可能还希望在现有的依赖属性上改变 WPF 框架级别的属性元数据选项。 这些选项将有关 WPF 框架级别属性的某些已知条件传递到其他 WPF 框架级别的进程，例如布局系统。  设置选项通常这是注册新的依赖项属性，但也可以作为的一部分更改 WPF 框架级别的属性元数据<xref:System.Windows.DependencyProperty.OverrideMetadata%2A>或<xref:System.Windows.DependencyProperty.AddOwner%2A>调用。 有关要使用的特定值以及详细信息，请参阅[框架属性元数据](framework-property-metadata.md)。 有关应当如何为新注册的依赖属性设置这些选项的详细信息，请参阅[自定义依赖属性](custom-dependency-properties.md)。  
  
<a name="dp_override_metadata"></a>   
### <a name="overriding-metadata"></a>重写元数据  
 重写元数据的主要目的在于，使你有机会更改各种派生自元数据的行为，这些行为应用于类型上存在的依赖属性。 [元数据](#dp_metadata_contents)一节中更详细地介绍了重写元数据的原因。 有关详细信息（包括一些代码示例），请参阅[重写依赖属性的元数据](how-to-override-metadata-for-a-dependency-property.md)。  
  
 属性元数据可以在注册调用期间提供的依赖项属性 (<xref:System.Windows.DependencyProperty.Register%2A>)。 但是，在许多情况下，当类继承该依赖属性时，你可能希望为该类提供特定于类型的元数据。 您可以执行此操作通过调用<xref:System.Windows.DependencyProperty.OverrideMetadata%2A>方法。  例如，从[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)]，则<xref:System.Windows.FrameworkElement>类是第一次注册的类型<xref:System.Windows.UIElement.Focusable%2A>依赖项属性。 但<xref:System.Windows.Controls.Control>类重写依赖属性提供自己的初始默认值，将它从元数据`false`到`true`，否则重新使用原始和<xref:System.Windows.UIElement.Focusable%2A>实现。  
  
 当你重写元数据时，系统会合并或替换不同的元数据特征。  
  
-   <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A> 合并。 如果您将添加一个新<xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A>，该回叫存储在元数据。 如果未指定<xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A>重写时，值<xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A>升级为从在元数据中指定它的最近上级的引用。  
  
-   实际属性系统行为<xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A>是层次结构中的所有元数据所有者的实现都保留并添加到表中，属性系统的执行顺序是首先调用派生程度最高的类的回叫。  
  
-   <xref:System.Windows.PropertyMetadata.DefaultValue%2A> 将被替换。 如果未指定<xref:System.Windows.PropertyMetadata.DefaultValue%2A>重写时，值<xref:System.Windows.PropertyMetadata.DefaultValue%2A>来自元数据中指定的最近上级。  
  
-   <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A> 实现将替换为。 如果您将添加一个新<xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A>，该回叫存储在元数据。 如果未指定<xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A>重写时，值<xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A>升级为从在元数据中指定它的最近上级的引用。  
  
-   属性系统行为是仅<xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A>调用直接元数据中。 没有对其他引用<xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A>保留层次结构中的实现。  
  
 此行为通过<xref:System.Windows.PropertyMetadata.Merge%2A>，并可以对派生的元数据类中重写。  
  
#### <a name="overriding-attached-property-metadata"></a>重写附加属性元数据  
 在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中，附加属性作为依赖属性来实现。 这意味着它们还具有能够由个别类重写的属性元数据。 中的附加属性的作用域注意事项[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]通常是，任何<xref:System.Windows.DependencyObject>可以具有在其上设置附加的属性。 因此，任何<xref:System.Windows.DependencyObject>因为它可能会设置类的实例上，派生的类可以重写任何附加属性的元数据。 可以重写默认值、回叫或 WPF 框架级别的特征报告属性。 如果针对类的实例设置了附加属性，则这些重写属性元数据特征将适用。 例如，可以重写默认值，这样，只要未以其他方式设置附加属性，重写值就会报告为类实例的附加属性的值。  
  
> [!NOTE]
>  <xref:System.Windows.FrameworkPropertyMetadata.Inherits%2A>属性不相关的附加属性。  
  
<a name="dp_add_owner"></a>   
### <a name="adding-a-class-as-an-owner-of-an-existing-dependency-property"></a>将类作为现有依赖属性的所有者来添加  
 一个类可以将其自身添加为已注册，通过使用依赖属性的所有者<xref:System.Windows.DependencyProperty.AddOwner%2A>方法。 这使得该类可以使用最初针对另一个类型注册的依赖属性。 添加类通常不是首先将该依赖属性注册为所有者的类型的派生类。 实际上，这使类及其派生类可以“继承”依赖属性实现，而不需要最初的所有者类，而且添加类也不必位于同一个实际的类层次结构中。 另外，添加类（以及所有派生类）随后可以为最初的依赖属性提供特定于类型的元数据。  
  
 添加类除了通过属性系统的实用工具方法将自身添加为所有者以外，还应当在自身声明其他公共成员，以使依赖属性向代码和标记公开，从而完全参与属性系统。 就为依赖属性公开对象模型而言，添加现有依赖属性的类与定义新的自定义依赖属性的类具有相同的职责。 要公开的第一个此类成员是依赖属性标识符字段。 此字段应`public static readonly`类型的字段<xref:System.Windows.DependencyProperty>，该值将赋给的返回值<xref:System.Windows.DependencyProperty.AddOwner%2A>调用。 要定义的第二个成员是[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)]“包装器”属性。 包装器，可以更方便地操作在代码中的依赖属性 (避免调用<xref:System.Windows.DependencyObject.SetValue%2A>每个时间，并可以在包装器本身进行此调用一次)。 包装器的实现方式与在注册自定义依赖属性时的实现方式完全相同。 有关实现依赖属性的详细信息，请参阅[自定义依赖属性](custom-dependency-properties.md)和[为依赖属性添加所有者类型](how-to-add-an-owner-type-for-a-dependency-property.md)。  
  
#### <a name="addowner-and-attached-properties"></a>AddOwner 和附加属性  
 您可以调用<xref:System.Windows.DependencyProperty.AddOwner%2A>由所有者类定义为附加属性的依赖项属性。 这样做的目的通常是为了将以前附加的属性作为非附加依赖属性来公开。 然后将公开<xref:System.Windows.DependencyProperty.AddOwner%2A>返回值作为`public static readonly`用作依赖项属性标识符字段，将定义适当的"包装"属性，以便该属性出现在成员表中并支持非附加属性在类中的使用情况。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.PropertyMetadata>
- <xref:System.Windows.DependencyObject>
- <xref:System.Windows.DependencyProperty>
- <xref:System.Windows.DependencyProperty.GetMetadata%2A>
- [依赖项属性概述](dependency-properties-overview.md)
- [框架属性元数据](framework-property-metadata.md)
