---
title: 绑定源概述
ms.date: 03/30/2017
helpviewer_keywords:
- binding data [WPF], binding sources
- data binding [WPF], binding source
- binding sources [WPF]
ms.assetid: 2df2cd11-6aac-4bdf-ab7b-ea5f464cd5ca
ms.openlocfilehash: 857175c65c62d8abad07a93baf72aa3709e5cb6b
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57375631"
---
# <a name="binding-sources-overview"></a>绑定源概述
在数据绑定中，绑定源对象是指用户从其获取数据的对象。 本主题讨论可用作绑定源的对象类型。  
  
  
  
<a name="binding_sources"></a>   
## <a name="binding-source-types"></a>绑定源类型  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 数据绑定支持以下绑定源类型：  
  
|绑定源|描述|  
|--------------------|-----------------|  
|[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 对象|可以绑定到任何 [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 对象的公有属性、子属性以及索引器。 绑定引擎使用 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 反射来获取属性值。 或者，对象实现<xref:System.ComponentModel.ICustomTypeDescriptor>或注册了<xref:System.ComponentModel.TypeDescriptionProvider>也适用于绑定引擎。<br /><br /> 有关如何实现可用作绑定源的类的详细信息，请参阅本主题后面的[为绑定源实现类](#classes)。|  
|动态对象|可以将绑定到可用的属性和实现的对象的索引器<xref:System.Dynamic.IDynamicMetaObjectProvider>接口。 如果可以访问代码中的成员，则可以绑定到该成员。 例如，如果动态对象使用户可以通过 `someObjet.AProperty` 访问代码中的成员，则可以通过将绑定路径设置为 `AProperty` 来绑定到该成员。|  
|[!INCLUDE[TLA#tla_adonet](../../../../includes/tlasharptla-adonet-md.md)] 对象|可以将绑定到[!INCLUDE[TLA2#tla_adonet](../../../../includes/tla2sharptla-adonet-md.md)]对象，如<xref:System.Data.DataTable>。 [!INCLUDE[TLA2#tla_adonet](../../../../includes/tla2sharptla-adonet-md.md)] <xref:System.Data.DataView>实现<xref:System.ComponentModel.IBindingList>接口，它提供了绑定引擎侦听的更改通知。|  
|[!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)] 对象|你可以将绑定到并运行`XPath`查询上的<xref:System.Xml.XmlNode>， <xref:System.Xml.XmlDocument>，或<xref:System.Xml.XmlElement>。 方便地访问[!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)]标记中的绑定源的数据是使用<xref:System.Windows.Data.XmlDataProvider>对象。 有关详细信息，请参阅[使用 XMLDataProvider 和 XPath 查询绑定到 XML 数据](how-to-bind-to-xml-data-using-an-xmldataprovider-and-xpath-queries.md)。<br /><br /> 此外可以绑定到<xref:System.Xml.Linq.XElement>或<xref:System.Xml.Linq.XDocument>，或绑定到这些类型的对象上运行通过使用 LINQ to XML 查询的结果。 使用 LINQ to XML 访问 XML 数据的标记中的绑定源的简便方法是使用<xref:System.Windows.Data.ObjectDataProvider>对象。 有关详细信息，请参阅[绑定到 XDocument、XElement 或 LINQ for XML 查询结果](how-to-bind-to-xdocument-xelement-or-linq-for-xml-query-results.md)。|  
|<xref:System.Windows.DependencyObject> 对象|可以绑定到的任何依赖关系属性<xref:System.Windows.DependencyObject>。 有关示例，请参阅[绑定两个控件的属性](how-to-bind-the-properties-of-two-controls.md)。|  
  
<a name="classes"></a>   
## <a name="implementing-a-class-for-the-binding-source"></a>为绑定源实现类  
 可以创建自己的绑定源。 本部分讨论在要实现用作绑定源的类时需要了解的内容。  
  
### <a name="providing-change-notifications"></a>提供更改通知  
 如果正在使用<xref:System.Windows.Data.BindingMode.OneWay>或<xref:System.Windows.Data.BindingMode.TwoWay>绑定 (因为您希望您[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]更新绑定源属性动态更改时)，您必须实现适当的属性更改通知机制。 建议的机制是有关[!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)]或动态类，以实现<xref:System.ComponentModel.INotifyPropertyChanged>接口。 有关详细信息，请参阅[实现属性更改通知](how-to-implement-property-change-notification.md)。  
  
 如果您创建[!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)]对象，它不实现<xref:System.ComponentModel.INotifyPropertyChanged>，必须安排您自己的通知系统，以确保绑定中使用的数据保持最新。 可以通过支持要更改通知的每个属性的 `PropertyChanged` 模式来提供更改通知。 若要支持此模式，请为每个属性定义一个 *PropertyName*Changed 事件，其中 *PropertyName* 是属性的名称。 每次更改属性时都会引发该事件。  
  
 如果绑定源实现了其中一个通知机制，将会自动进行目标更新。 如果出于任何原因绑定源不提供正确的属性更改通知，可以选择要使用<xref:System.Windows.Data.BindingExpression.UpdateTarget%2A>方法来显式更新目标属性。  
  
### <a name="other-characteristics"></a>其他特性  
 下表提供了需要注意的其他要点：  
  
-   如果要在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中创建对象，类必须具有默认的构造函数。 在某些[!INCLUDE[TLA2#tla_net](../../../../includes/tla2sharptla-net-md.md)]语言，如C#，可能会为你创建的默认构造函数。  
  
-   用作绑定的绑定源属性的属性必须为类的公共属性。 不能出于绑定目的来访问显式定义的接口属性，也不能访问没有基实现的受保护、私有、内部或虚拟属性。  
  
-   不能绑定到公共字段。  
  
-   类中声明的属性类型是传递给绑定的类型。 不过，绑定最终所用的类型取决于绑定目标属性的类型，而不是绑定源属性的类型。 如果类型不同，可能需要编写一个转换器来处理自定义属性最初传递给绑定的方式。 有关详细信息，请参阅 <xref:System.Windows.Data.IValueConverter>。  
  
<a name="objects"></a>   
## <a name="using-entire-objects-as-a-binding-source"></a>将整个对象用作绑定源  
 可以将整个对象用作绑定源。 可以通过使用指定绑定源<xref:System.Windows.Data.Binding.Source%2A>或<xref:System.Windows.FrameworkElement.DataContext%2A>属性，然后提供一个空白绑定声明： `{Binding}`。 适用的场景包括绑定到属于类型字符串的对象、绑定到具有感兴趣的多个属性的对象或绑定到集合对象。 有关绑定到整个集合对象的示例，请参阅[对分层数据使用主-从模式](how-to-use-the-master-detail-pattern-with-hierarchical-data.md)。  
  
 请注意，可能需要应用自定义逻辑，以便数据对于绑定的目标属性有意义。 自定义逻辑可能采用自定义转换器形式 （如果尚不存在默认的类型转换） 或<xref:System.Windows.DataTemplate>。 有关转换器的详细信息，请参阅[数据绑定概述](data-binding-overview.md)的“数据转换”一节。 有关数据模板的详细信息，请参阅[数据模板化概述](data-templating-overview.md)。  
  
<a name="collections"></a>   
## <a name="using-collection-objects-as-a-binding-source"></a>将集合对象用作绑定源  
 通常，要用作绑定源的对象是自定义对象的集合。 每个对象都用作重复绑定的一个实例的源。 例如，可能存在由 `CustomerOrder` 对象组成的 `CustomerOrders` 集合，其中应用程序会循环访问该集合以确定存在的订单数量，以及每个订单中的数据。  
  
 可以枚举实现任何集合<xref:System.Collections.IEnumerable>接口。 但是，若要设置动态绑定，以便插入或删除集合中的更新[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]自动，该集合必须实现<xref:System.Collections.Specialized.INotifyCollectionChanged>接口。 此接口公开一个事件，只要基础集合发生更改，就必须引发该事件。  
  
 <xref:System.Collections.ObjectModel.ObservableCollection%601>类是公开的数据集合的内置实现<xref:System.Collections.Specialized.INotifyCollectionChanged>接口。 集合中的个别数据对象必须满足前面章节中所述的要求。 有关示例，请参阅[创建和绑定到 ObservableCollection](how-to-create-and-bind-to-an-observablecollection.md)。 在实现自己的集合之前, 请考虑使用<xref:System.Collections.ObjectModel.ObservableCollection%601>或一个现有集合类，如<xref:System.Collections.Generic.List%601>， <xref:System.Collections.ObjectModel.Collection%601>，和<xref:System.ComponentModel.BindingList%601>，此外还有许多其他。  
  
 WPF 从不直接绑定到集合。 如果指定集合作为绑定源，WPF 实际上会绑定到该集合的默认视图。 有关默认视图的信息，请参阅[数据绑定概述](data-binding-overview.md)。  
  
 如果有高级的方案，并且您想要实现自己的集合，请考虑使用<xref:System.Collections.IList>接口。 <xref:System.Collections.IList> 提供了可按照索引，这可以提高性能单独访问的对象的非泛型集合。  
  
<a name="permissions"></a>   
## <a name="permission-requirements-in-data-binding"></a>数据绑定中的权限要求  
 当进行数据绑定时，必须考虑应用程序的信任级别。 下表总结了在完全信任或部分信任级别下执行的应用程序中可以绑定到的属性类型：  
  
|属性类型<br /><br /> （所有访问修饰符）|动态对象属性|动态对象属性|CLR 属性|CLR 属性|依赖属性|依赖属性|  
|------------------------------------------------|-----------------------------|-----------------------------|------------------|------------------|-------------------------|-------------------------|  
|**信任级别**|**完全信任**|**部分信任**|**完全信任**|**部分信任**|**完全信任**|**部分信任**|  
|公共类|是|是|是|是|是|是|  
|非公共类|是|No|是|No|是|是|  
  
 此表描述了数据绑定中有关权限要求的以下要点：  
  
-   对于 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 属性，只要绑定引擎能够使用反射访问绑定源属性，数据绑定就有效。 否则，绑定引擎会发出找不到属性的警告，并使用回退值或默认值（如果可用）。  
  
-   可以绑定到在编译时或运行时定义的动态对象上的属性。  
  
-   始终可以绑定到依赖属性。  
  
 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 绑定的权限要求非常类似。 在部分信任沙盒中，<xref:System.Windows.Data.XmlDataProvider>没有权限访问指定的数据时将失败。  
  
 具有匿名类型的对象是内部对象。 只有在完全信任级别下运行，才能绑定到匿名类型的属性。 有关匿名类型的详细信息，请参阅[匿名类型（C# 编程指南）](~/docs/csharp/programming-guide/classes-and-structs/anonymous-types.md)或[匿名类型 (Visual Basic)](~/docs/visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md) (Visual Basic)。  
  
 有关部分信任安全的详细信息，请参阅 [WPF 部分信任安全](../wpf-partial-trust-security.md)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Data.ObjectDataProvider>
- <xref:System.Windows.Data.XmlDataProvider>
- [指定绑定源](how-to-specify-the-binding-source.md)
- [数据绑定概述](data-binding-overview.md)
- [帮助主题](data-binding-how-to-topics.md)
- [使用 LINQ to XML 进行 WPF 数据绑定概述](/visualstudio/designers/wpf-data-binding-with-linq-to-xml-overview)
- [数据绑定](../advanced/optimizing-performance-data-binding.md)
