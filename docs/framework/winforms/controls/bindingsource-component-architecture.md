---
title: BindingSource 组件体系结构
ms.date: 03/30/2017
helpviewer_keywords:
- BindingSource component [Windows Forms], architecture
- Windows Forms, data binding
- BindingSource component [Windows Forms], about BindingSource component
- data binding [Windows Forms], BindingSource component
ms.assetid: 7bc69c90-8a11-48b1-9336-3adab5b41591
ms.openlocfilehash: 9348d44697b2c617481b55242faa83ab517e6226
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57707815"
---
# <a name="bindingsource-component-architecture"></a>BindingSource 组件体系结构
使用<xref:System.Windows.Forms.BindingSource>组件，普遍可以将所有 Windows 窗体控件都绑定到数据源。  
  
 <xref:System.Windows.Forms.BindingSource>组件简化将控件绑定到数据源的过程，并通过传统的数据绑定有以下优点：  
  
-   使设计时绑定到业务对象。  
  
-   封装<xref:System.Windows.Forms.CurrencyManager>功能，并公开<xref:System.Windows.Forms.CurrencyManager>在设计时的事件。  
  
-   简化了创建列表支持<xref:System.ComponentModel.IBindingList>针对本机不支持列表的数据源更改通知，从而列表更改通知的接口。  
  
-   提供的扩展点<xref:System.ComponentModel.IBindingList.AddNew%2A?displayProperty=nameWithType>方法。  
  
-   提供数据源和控件之间的间接级别。 在运行时可能会更改数据源时，这种间接方式很重要。  
  
-   特别是与其他数据相关的 Windows 窗体控件，互操作<xref:System.Windows.Forms.BindingNavigator>和<xref:System.Windows.Forms.DataGridView>控件。  
  
 出于这些原因，<xref:System.Windows.Forms.BindingSource>组件是在 Windows 窗体控件绑定到数据源的首选的方法。  
  
## <a name="bindingsource-features"></a>BindingSource 功能  
 <xref:System.Windows.Forms.BindingSource>组件提供了用于控件绑定到数据的多个功能。 使用这些功能，可以实现几乎无需编码即可您的大多数数据绑定方案。  
  
 <xref:System.Windows.Forms.BindingSource>组件来实现此目的通过用于访问许多不同类型的数据源提供一致的接口。 这意味着绑定到任何类型使用相同的过程。 例如，您可以将附加<xref:System.Windows.Forms.BindingSource.DataSource%2A>属性设置为<xref:System.Data.DataSet>或对业务对象和在这两种情况下使用同一组属性、 方法和事件来操作数据源。  
  
 提供的一致界面<xref:System.Windows.Forms.BindingSource>组件极大地简化了数据绑定到控件的过程。 针对数据源类型提供的更改通知，<xref:System.Windows.Forms.BindingSource>组件会自动进行通信的控件和数据源之间的更改。 对于不提供更改通知的数据源类型，事件都是提供可用于引发更改通知。 以下列表显示了支持的功能<xref:System.Windows.Forms.BindingSource>组件：  
  
-   间接寻址。  
  
-   当前项管理。  
  
-   作为列表的数据源。  
  
-   <xref:System.Windows.Forms.BindingSource> 作为<xref:System.ComponentModel.IBindingList>。  
  
-   自定义项的创建。  
  
-   事务的项的创建。  
  
-   <xref:System.Collections.IEnumerable> 支持。  
  
-   设计时支持。  
  
-   静态<xref:System.Windows.Forms.ListBindingHelper>方法。  
  
-   排序和筛选与<xref:System.ComponentModel.IBindingListView>接口。  
  
-   与集成<xref:System.Windows.Forms.BindingNavigator>。  
  
### <a name="indirection"></a>间接寻址  
 <xref:System.Windows.Forms.BindingSource>组件提供了一个控件和数据源之间的间接级别。 而不是将控件绑定到数据源，将绑定到控件<xref:System.Windows.Forms.BindingSource>，并将附加到数据源<xref:System.Windows.Forms.BindingSource>组件的<xref:System.Windows.Forms.BindingSource.DataSource%2A>属性。  
  
 使用此级别的间接寻址，可以更改数据源，而重置控件绑定。 这为您提供以下功能：  
  
-   可以将附加<xref:System.Windows.Forms.BindingSource>到不同的数据源，同时保留当前的控件绑定。  
  
-   可更改数据源中的项，并通知绑定的控件。 有关详细信息，请参阅[如何：反映在使用 BindingSource 的 Windows 窗体控件中的数据源更新](reflect-data-source-updates-in-a-wf-control-with-the-bindingsource.md)。  
  
-   可以将绑定到<xref:System.Type>而不是在内存中的对象。 有关详细信息，请参阅[如何：将 Windows 窗体控件绑定到类型](how-to-bind-a-windows-forms-control-to-a-type.md)。 你可以然后绑定到对象在运行时。  
  
### <a name="currency-management"></a>当前项管理  
 <xref:System.Windows.Forms.BindingSource>组件实现<xref:System.Windows.Forms.ICurrencyManagerProvider>接口来处理您的货币管理。 与<xref:System.Windows.Forms.ICurrencyManagerProvider>接口，您还可以访问到的货币管理器<xref:System.Windows.Forms.BindingSource>，另一个的货币管理器除了<xref:System.Windows.Forms.BindingSource>绑定到同一<xref:System.Windows.Forms.BindingSource.DataMember%2A>。  
  
 <xref:System.Windows.Forms.BindingSource>组件封装<xref:System.Windows.Forms.CurrencyManager>功能，并公开最常见<xref:System.Windows.Forms.CurrencyManager>属性和事件。 下表介绍了一些与货币管理相关的成员。  
  
 <xref:System.Windows.Forms.ICurrencyManagerProvider.CurrencyManager%2A> 属性  
 获取与关联的货币管理器<xref:System.Windows.Forms.BindingSource>。  
  
 <xref:System.Windows.Forms.ICurrencyManagerProvider.GetRelatedCurrencyManager%2A> 方法  
 如果还有一种<xref:System.Windows.Forms.BindingSource>绑定到指定的数据成员，则获取其当前项管理器。  
  
 <xref:System.Windows.Forms.BindingSource.Current%2A> 属性  
 获取数据源的当前项。  
  
 <xref:System.Windows.Forms.BindingSource.Position%2A> 属性  
 获取或设置基础列表中的当前位置。  
  
 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> 方法  
 将挂起的更改应用于基础数据源。  
  
 <xref:System.Windows.Forms.BindingSource.CancelEdit%2A> 方法  
 取消当前的编辑操作。  
  
### <a name="data-source-as-a-list"></a>作为列表的数据源  
 <xref:System.Windows.Forms.BindingSource>组件实现<xref:System.ComponentModel.IBindingListView>和<xref:System.ComponentModel.ITypedList>接口。 此实现中，您可以使用<xref:System.Windows.Forms.BindingSource>组件本身作为数据源，而无需任何外部存储。  
  
 当<xref:System.Windows.Forms.BindingSource>组件连接到数据源，它作为列表的数据源。  
  
 <xref:System.Windows.Forms.BindingSource.DataSource%2A>属性可以设置为多个数据源。 其中包括类型、 对象和类型的列表。 产生的数据源将公开为一个列表。 下表显示了一些常见的数据源和生成的列表计算。  
  
|数据源属性|列表结果|  
|-------------------------|------------------|  
|空引用（在 Visual Basic 中为 `Nothing`）|一个空<xref:System.ComponentModel.IBindingList>的对象。 将项添加到所添加项的类型设置的列表。|  
|Null 引用 (`Nothing`在 Visual Basic 中) 与<xref:System.Windows.Forms.BindingSource.DataMember%2A>设置|不支持;引发<xref:System.ArgumentException>。|  
|非列表类型或者"T"类型的对象|一个空<xref:System.ComponentModel.IBindingList>的"T"类型。|  
|数组实例|<xref:System.ComponentModel.IBindingList>包含数组元素。|  
|<xref:System.Collections.IEnumerable> 实例|<xref:System.ComponentModel.IBindingList>包含<xref:System.Collections.IEnumerable>项|  
|列出"T"的包含类型的实例|<xref:System.ComponentModel.IBindingList>包含"T"类型的实例。|  
  
 此外，<xref:System.Windows.Forms.BindingSource.DataSource%2A>可以设置为其他列表类型，如<xref:System.ComponentModel.IListSource>并<xref:System.ComponentModel.ITypedList>，和<xref:System.Windows.Forms.BindingSource>将适当地处理。 在这种情况下，列表中包含的类型应具有默认构造函数。  
  
### <a name="bindingsource-as-an-ibindinglist"></a>作为 IBindingList BindingSource  
 <xref:System.Windows.Forms.BindingSource>组件提供用于访问和操作基础数据作为成员<xref:System.ComponentModel.IBindingList>。 下表描述了其中几个成员。  
  
|成员|描述|  
|------------|-----------------|  
|<xref:System.Windows.Forms.BindingSource.List%2A> 属性|获取的计算结果的列表<xref:System.Windows.Forms.BindingSource.DataSource%2A>或<xref:System.Windows.Forms.BindingSource.DataMember%2A>属性。|  
|<xref:System.Windows.Forms.BindingSource.AddNew%2A> 方法|在基础列表中添加一个新项。 适用于实现的数据源<xref:System.ComponentModel.IBindingList>接口，并允许添加项 (即<xref:System.Windows.Forms.BindingSource.AllowNew%2A>属性设置为`true`)。|  
  
### <a name="custom-item-creation"></a>自定义项的创建  
 您可以处理<xref:System.Windows.Forms.BindingSource.AddingNew>事件，以便提供您自己的项创建逻辑。 <xref:System.Windows.Forms.BindingSource.AddingNew>发生事件的新对象添加到之前<xref:System.Windows.Forms.BindingSource>。 此事件后引发<xref:System.Windows.Forms.BindingSource.AddNew%2A>调用方法时，新项添加到基础列表之前。 通过处理此事件，可以提供自定义项创建行为，而无需派生自<xref:System.Windows.Forms.BindingSource>类。 有关详细信息，请参阅[如何：使用自定义项添加 Windows 窗体 BindingSource](how-to-customize-item-addition-with-the-windows-forms-bindingsource.md)。  
  
### <a name="transactional-item-creation"></a>事务的项的创建  
 <xref:System.Windows.Forms.BindingSource>组件实现<xref:System.ComponentModel.ICancelAddNew>接口，这使事务的项的创建。 通过使用调用暂时创建一个新项后<xref:System.Windows.Forms.BindingSource.AddNew%2A>，可能会提交或回滚按以下方式添加：  
  
-   <xref:System.ComponentModel.ICancelAddNew.EndNew%2A>方法显式提交挂起的添加。  
  
-   执行另一个集合操作，例如插入、 删除或移动的同时，将隐式提交挂起的添加。  
  
-   <xref:System.ComponentModel.ICancelAddNew.CancelNew%2A>方法将挂起的添加时回滚该方法不已提交。  
  
### <a name="ienumerable-support"></a>IEnumerable 支持  
 <xref:System.Windows.Forms.BindingSource>组件允许控件绑定到<xref:System.Collections.IEnumerable>数据源。 与此组件，您可以将绑定到数据源如<xref:System.Data.SqlClient.SqlDataReader?displayProperty=nameWithType>。  
  
 当<xref:System.Collections.IEnumerable>数据源分配给<xref:System.Windows.Forms.BindingSource>组件，<xref:System.Windows.Forms.BindingSource>创建<xref:System.ComponentModel.IBindingList>，并将添加的内容<xref:System.Collections.IEnumerable>到列表的数据源。  
  
### <a name="design-time-support"></a>设计时支持  
 某些对象类型不能创建在设计时，例如从工厂类创建的对象或 Web 服务返回的对象。 有时必须将您的控件绑定到这些类型，在设计时，即使在您的控件可以绑定到的内存中没有任何对象。 例如，可能需要标签的列标题<xref:System.Windows.Forms.DataGridView>控件自定义类型的公共属性的名称。  
  
 若要支持此方案中，<xref:System.Windows.Forms.BindingSource>组件支持绑定到<xref:System.Type>。 将分配<xref:System.Type>到<xref:System.Windows.Forms.BindingSource.DataSource%2A>属性，<xref:System.Windows.Forms.BindingSource>组件创建一个空<xref:System.ComponentModel.BindingList%601>的<xref:System.Type>项。 随后绑定到任何控件<xref:System.Windows.Forms.BindingSource>在设计时或在运行时，会出现的属性或类型的架构收到警报的组件。 有关详细信息，请参阅[如何：将 Windows 窗体控件绑定到类型](how-to-bind-a-windows-forms-control-to-a-type.md)。  
  
### <a name="static-listbindinghelper-methods"></a>静态 ListBindingHelper 方法  
 <xref:System.Windows.Forms.BindingContext?displayProperty=nameWithType>， <xref:System.Windows.Forms.CurrencyManager?displayProperty=nameWithType>，并<xref:System.Windows.Forms.BindingSource>类型的所有共享通用逻辑生成从列表`DataSource` / `DataMember`对。 此外，此常见逻辑将公开用于控件作者和其他第三方在下面的示例`static`方法：  
  
-   <xref:System.Windows.Forms.ListBindingHelper.GetListItemProperties%2A>  
  
-   <xref:System.Windows.Forms.ListBindingHelper.GetList%2A>。  
  
-   <xref:System.Windows.Forms.ListBindingHelper.GetListName%2A>  
  
-   <xref:System.Windows.Forms.ListBindingHelper.GetListItemType%2A>  
  
### <a name="sorting-and-filtering-with-the-ibindinglistview-interface"></a>排序和筛选与 IBindingListView 接口  
 <xref:System.Windows.Forms.BindingSource>组件实现<xref:System.ComponentModel.IBindingListView>接口，它扩展了<xref:System.ComponentModel.IBindingList>接口。 <xref:System.ComponentModel.IBindingList>提供了单个列进行排序和<xref:System.ComponentModel.IBindingListView>提供高级排序和筛选。 使用<xref:System.ComponentModel.IBindingListView>，可以进行排序和筛选器项中的数据源，如果数据源还实现这些接口之一。 <xref:System.Windows.Forms.BindingSource>组件不提供这些成员的参考实现。 相反，将调用转发给基础列表。  
  
 下表介绍用于排序和筛选的属性。  
  
|成员|描述|  
|------------|-----------------|  
|<xref:System.Windows.Forms.BindingSource.Filter%2A> 属性|如果数据源是 <xref:System.ComponentModel.IBindingListView>，则获取或设置用于筛选已查看的行的表达式。|  
|<xref:System.Windows.Forms.BindingSource.Sort%2A> 属性|如果数据源是 <xref:System.ComponentModel.IBindingList>，则获取或设置用于排序的列名称并对顺序信息进行排序。<br /><br /> 或<br /><br /> 如果数据源是<xref:System.ComponentModel.IBindingListView>和支持高级排序，则获取用于排序和排序顺序的多个列名称|  
  
### <a name="integration-with-bindingnavigator"></a>与 BindingNavigator 的集成  
 可以使用<xref:System.Windows.Forms.BindingSource>组件将任何 Windows 窗体控件绑定到数据源，但<xref:System.Windows.Forms.BindingNavigator>控件专门用于处理<xref:System.Windows.Forms.BindingSource>组件。 <xref:System.Windows.Forms.BindingNavigator>控件提供用户界面，用于控制<xref:System.Windows.Forms.BindingSource>组件的当前项。 默认情况下<xref:System.Windows.Forms.BindingNavigator>控件提供导航方法相对应的按钮<xref:System.Windows.Forms.BindingSource>组件。 有关详细信息，请参阅[如何：使用 Windows 窗体 BindingNavigator 控件导航数据](how-to-navigate-data-with-the-windows-forms-bindingnavigator-control.md)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.BindingSource>
- <xref:System.Windows.Forms.BindingNavigator>
- [BindingSource 组件概述](bindingsource-component-overview.md)
- [BindingNavigator 控件](bindingnavigator-control-windows-forms.md)
- [Windows 窗体数据绑定](../windows-forms-data-binding.md)
- [在 Windows 窗体上使用的控件](controls-to-use-on-windows-forms.md)
- [如何：将 Windows 窗体控件绑定到类型](how-to-bind-a-windows-forms-control-to-a-type.md)
- [如何：反映在使用 BindingSource 的 Windows 窗体控件中的数据源更新](reflect-data-source-updates-in-a-wf-control-with-the-bindingsource.md)
