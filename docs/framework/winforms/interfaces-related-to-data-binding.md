---
title: 与数据绑定相关的接口
ms.date: 03/30/2017
helpviewer_keywords:
- data [Windows Forms], data-binding interfaces
- INotifyPropertyChanged interface
- IBindingListView interface
- IList interface [Windows Forms], Windows Forms data binding
- IBindingList interface [Windows Forms], Windows Forms data binding
- interfaces [Windows Forms], Windows Forms data binding
- IEditableObject interface [Windows Forms], Windows Forms data binding
- data binding [Windows Forms], interfaces
- IDataErrorInfo interface [Windows Forms], Windows Forms data binding
ms.assetid: 14e49a2e-3e46-47ca-b491-70d546333277
ms.openlocfilehash: ec72b67da72bde9392d523787e8c0d4d0981ad7b
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57703525"
---
# <a name="interfaces-related-to-data-binding"></a>与数据绑定相关的接口
使用 [!INCLUDE[vstecado](../../../includes/vstecado-md.md)]，可以创建许多不同的数据结构，以满足应用程序和正在处理的数据的绑定需要。 你可能希望创建自己的类，以便在 Windows 窗体中提供或使用数据。 这些对象可以提供各种级别的功能和复杂性，从基本的数据绑定，到提供设计时支持、错误检查、更改通知，甚至是支持对数据本身所做更改的结构化回退。  
  
## <a name="consumers-of-data-binding-interfaces"></a>数据绑定接口的使用者  
 以下部分描述两组接口对象。 第一组列出数据源作者在数据源上实现的接口。 这些接口旨在由数据源使用者使用，在多数情况下，这些使用者是 Windows 窗体控件或组件。 第二组列出面向组件作者设计的接口。 组件作者在创建支持数据绑定的组件时使用这些接口，以便它们能够被 Windows 窗体数据绑定引擎使用。 可以在与窗体关联的类中实现这些接口以启用数据绑定；每种情况都表示一个类，该类所实现的接口支持与数据进行交互。 Visual Studio 快速应用程序开发 (RAD) 数据设计体验工具已经利用此功能。  
  
### <a name="interfaces-for-implementation-by-data-source-authors"></a>要由数据源作者实现的接口  
 下列接口设计为由 Windows 窗体控件使用：  
  
-   <xref:System.Collections.IList> 接口  
  
     实现的类<xref:System.Collections.IList>接口可能<xref:System.Array>， <xref:System.Collections.ArrayList>，或<xref:System.Collections.CollectionBase>。 这些是类型的项的索引的列表<xref:System.Object>。 这些列表必须包含同源类型，因为索引中的第一项确定类型。 <xref:System.Collections.IList> 将可用于仅在运行时绑定。  
  
    > [!NOTE]
    >  如果你想要用 Windows 窗体中创建的绑定的业务对象的列表，则应考虑使用<xref:System.ComponentModel.BindingList%601>。 <xref:System.ComponentModel.BindingList%601>是可扩展的类实现双向 Windows 窗体数据绑定所需的主要接口。  
  
-   <xref:System.ComponentModel.IBindingList> 接口  
  
     实现的类<xref:System.ComponentModel.IBindingList>接口提供了高得多的数据绑定功能。 此实现在列表项更改时（例如，客户列表中的第三项更改了 Address 字段）和列表本身更改时（例如，列表中项的数量增加或减少）都提供基本的排序功能和更改通知。 如果计划将多个控件绑定到同一个数据，但是希望将在其中某个控件中进行的数据更改传播到其他绑定控件，更改通知就非常重要。  
  
    > [!NOTE]
    >  为启用更改通知<xref:System.ComponentModel.IBindingList>通过接口<xref:System.ComponentModel.IBindingList.SupportsChangeNotification%2A>属性的当`true`，将引发<xref:System.ComponentModel.IBindingList.ListChanged>更改事件，指示已更改的列表或列表中的项。  
  
     所描述的更改类型<xref:System.ComponentModel.ListChangedType>属性的<xref:System.ComponentModel.ListChangedEventArgs>参数。 因此，当数据模型进行更新时，任何依赖视图（例如，绑定到同一个数据源的其他控件）也会进行更新。 但是，在列表中包含的对象必须在更改，以便该列表可以引发时通知该列表<xref:System.ComponentModel.IBindingList.ListChanged>事件。  
  
    > [!NOTE]
    >  <xref:System.ComponentModel.BindingList%601>提供的泛型实现<xref:System.ComponentModel.IBindingList>接口。  
  
-   <xref:System.ComponentModel.IBindingListView> 接口  
  
     实现的类<xref:System.ComponentModel.IBindingListView>接口提供的实现的所有功能<xref:System.ComponentModel.IBindingList>以及为筛选和高级排序功能。 此实现使用属性描述符-方向对提供基于字符串的筛选和多列排序能力。  
  
-   <xref:System.ComponentModel.IEditableObject> 接口  
  
     实现的类<xref:System.ComponentModel.IEditableObject>接口允许对象以控制何时进行永久更改对该对象。 此实现可为你提供<xref:System.ComponentModel.IEditableObject.BeginEdit%2A>， <xref:System.ComponentModel.IEditableObject.EndEdit%2A>，和<xref:System.ComponentModel.IEditableObject.CancelEdit%2A>方法，以便你能够回滚对对象所做的更改。 下面是简要解释的正常运行<xref:System.ComponentModel.IEditableObject.BeginEdit%2A>， <xref:System.ComponentModel.IEditableObject.EndEdit%2A>，和<xref:System.ComponentModel.IEditableObject.CancelEdit%2A>方法以及它们如何协同工作以启用对数据所做的更改可能回滚中工作：  
  
    -   <xref:System.ComponentModel.IEditableObject.BeginEdit%2A>方法表示对象上编辑操作的开始。 实现此接口的对象需要存储任何更新之后<xref:System.ComponentModel.IEditableObject.BeginEdit%2A>中，可以放弃所更新的方式的方法调用如果<xref:System.ComponentModel.IEditableObject.CancelEdit%2A>调用方法。 在数据绑定 Windows 窗体，您可以调用<xref:System.ComponentModel.IEditableObject.BeginEdit%2A>多次的单个作用域内编辑事务 (例如， <xref:System.ComponentModel.IEditableObject.BeginEdit%2A>， <xref:System.ComponentModel.IEditableObject.BeginEdit%2A>， <xref:System.ComponentModel.IEditableObject.EndEdit%2A>)。 实现<xref:System.ComponentModel.IEditableObject>，确定是否应跟踪<xref:System.ComponentModel.IEditableObject.BeginEdit%2A>已调用并忽略对后续调用<xref:System.ComponentModel.IEditableObject.BeginEdit%2A>。 可以多次调用此方法，因为它是重要的后续调用非破坏性;也就是说，后续<xref:System.ComponentModel.IEditableObject.BeginEdit%2A>调用不能销毁所做的或更改已保存的数据的更新在第一天<xref:System.ComponentModel.IEditableObject.BeginEdit%2A>调用。  
  
    -   <xref:System.ComponentModel.IEditableObject.EndEdit%2A>方法将推送之后的任何更改<xref:System.ComponentModel.IEditableObject.BeginEdit%2A>当前编辑模式的对象是否调用到基础对象。  
  
    -   <xref:System.ComponentModel.IEditableObject.CancelEdit%2A>方法会放弃对对象所做的任何更改。  
  
     详细了解如何<xref:System.ComponentModel.IEditableObject.BeginEdit%2A>， <xref:System.ComponentModel.IEditableObject.EndEdit%2A>，并<xref:System.ComponentModel.IEditableObject.CancelEdit%2A>方法起作用，请参阅[将数据保存回数据库](/visualstudio/data-tools/save-data-back-to-the-database)。  
  
     这种事务性概念的数据功能由<xref:System.Windows.Forms.DataGridView>控件。  
  
-   <xref:System.ComponentModel.ICancelAddNew> 接口  
  
     实现的类<xref:System.ComponentModel.ICancelAddNew>接口实现了通常<xref:System.ComponentModel.IBindingList>接口，并允许回滚对数据源所做的补充<xref:System.ComponentModel.IBindingList.AddNew%2A>方法。 如果你的数据源实现<xref:System.ComponentModel.IBindingList>接口，您还应当让其实现<xref:System.ComponentModel.ICancelAddNew>接口。  
  
-   <xref:System.ComponentModel.IDataErrorInfo> 接口  
  
     实现的类<xref:System.ComponentModel.IDataErrorInfo>接口允许对象提供自定义错误信息向绑定控件：  
  
    -   <xref:System.ComponentModel.IDataErrorInfo.Error%2A>属性返回常规错误消息文本 （例如，"出现错误"）。  
  
    -   <xref:System.ComponentModel.IDataErrorInfo.Item%2A>属性返回带有特定的错误消息的字符串列 (例如，"中的值`State`列无效，")。  
  
-   <xref:System.Collections.IEnumerable> 接口  
  
     实现的类<xref:System.Collections.IEnumerable>接口通常由[!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)]。 此接口的 Windows 窗体支持才可通过<xref:System.Windows.Forms.BindingSource>组件。  
  
    > [!NOTE]
    >  <xref:System.Windows.Forms.BindingSource>组件将复制所有<xref:System.Collections.IEnumerable>出于绑定目的一个单独的列表项。  
  
-   <xref:System.ComponentModel.ITypedList> 接口  
  
     实现的集合类<xref:System.ComponentModel.ITypedList>接口提供了控制顺序和向绑定控件公开的属性集的能力。  
  
    > [!NOTE]
    >  当您实现<xref:System.ComponentModel.ITypedList.GetItemProperties%2A>方法，和<xref:System.ComponentModel.PropertyDescriptor>数组不为 null，数组中的最后一项将描述是另一个列表项的列表属性的属性描述符。  
  
-   <xref:System.ComponentModel.ICustomTypeDescriptor> 接口  
  
     实现的类<xref:System.ComponentModel.ICustomTypeDescriptor>接口提供了有关其自身的动态信息。 此接口是类似于<xref:System.ComponentModel.ITypedList>，但用于对象而非列表。 此接口由<xref:System.Data.DataRowView>基础行的架构。 简单实现<xref:System.ComponentModel.ICustomTypeDescriptor>提供的<xref:System.ComponentModel.CustomTypeDescriptor>类。  
  
    > [!NOTE]
    >  若要支持设计时绑定到类型实现<xref:System.ComponentModel.ICustomTypeDescriptor>，该类型还必须实现<xref:System.ComponentModel.IComponent>并且存在于窗体上的实例。  
  
-   <xref:System.ComponentModel.IListSource> 接口  
  
     实现的类<xref:System.ComponentModel.IListSource>接口使非列表对象上的基于列表的绑定。 <xref:System.ComponentModel.IListSource.GetList%2A>方法<xref:System.ComponentModel.IListSource>用于从不继承的对象返回可绑定列表<xref:System.Collections.IList>。 <xref:System.ComponentModel.IListSource> 由<xref:System.Data.DataSet>类。  
  
-   <xref:System.ComponentModel.IRaiseItemChangedEvents> 接口  
  
     实现的类<xref:System.ComponentModel.IRaiseItemChangedEvents>接口是可绑定的列表，还实现<xref:System.ComponentModel.IBindingList>接口。 此接口用于指示类型是否引发<xref:System.ComponentModel.IBindingList.ListChanged>类型的事件<xref:System.ComponentModel.ListChangedType.ItemChanged>通过其<xref:System.ComponentModel.IRaiseItemChangedEvents.RaisesItemChangedEvents%2A>属性。  
  
    > [!NOTE]
    >  应实现<xref:System.ComponentModel.IRaiseItemChangedEvents>如果您的数据源提供的属性来列出事件转换前面所述，并与之交互<xref:System.Windows.Forms.BindingSource>组件。 否则为<xref:System.Windows.Forms.BindingSource>也将执行属性来列出事件转换导致性能下降。  
  
-   <xref:System.ComponentModel.ISupportInitialize> 接口  
  
     实现的组件<xref:System.ComponentModel.ISupportInitialize>接口可利用批处理优化来设置属性并初始化共存属性。 <xref:System.ComponentModel.ISupportInitialize>包含两个方法：  
  
    -   <xref:System.ComponentModel.ISupportInitialize.BeginInit%2A> 通知对象初始化即将开始。  
  
    -   <xref:System.ComponentModel.ISupportInitialize.EndInit%2A> 通知对象初始化已完成。  
  
-   <xref:System.ComponentModel.ISupportInitializeNotification> 接口  
  
     实现的组件<xref:System.ComponentModel.ISupportInitializeNotification>接口还实现<xref:System.ComponentModel.ISupportInitialize>接口。 此接口，可以通知其他<xref:System.ComponentModel.ISupportInitialize>组件初始化已完成。 <xref:System.ComponentModel.ISupportInitializeNotification>接口包含两个成员：  
  
    -   <xref:System.ComponentModel.ISupportInitializeNotification.IsInitialized%2A> 返回`boolean`值，该值指示是否初始化该组件。  
  
    -   <xref:System.ComponentModel.ISupportInitializeNotification.Initialized> 发生时<xref:System.ComponentModel.ISupportInitialize.EndInit%2A>调用。  
  
-   <xref:System.ComponentModel.INotifyPropertyChanged> 接口  
  
     实现此接口的类是一个在其任何属性值更改时都会引发事件的类型。 此接口旨在替换控件的每个属性都有一个更改事件这种模式。 在中使用时<xref:System.ComponentModel.BindingList%601>，业务对象应当实现<xref:System.ComponentModel.INotifyPropertyChanged>接口，BindingList\`1 会将转换<xref:System.ComponentModel.INotifyPropertyChanged.PropertyChanged>事件<xref:System.ComponentModel.BindingList%601.ListChanged>类型的事件<xref:System.ComponentModel.ListChangedType.ItemChanged>。  
  
    > [!NOTE]
    >  对于更改通知出现在绑定客户端和数据之间的绑定源绑定的数据源类型应是实现<xref:System.ComponentModel.INotifyPropertyChanged>接口 （首选） 或您可以提供*propertyName* `Changed`事件的绑定的类型，但您不应执行这项。  
  
### <a name="interfaces-for-implementation-by-component-authors"></a>要由组件作者实现的接口  
 下列接口设计为由 Windows 窗体数据绑定引擎使用：  
  
-   <xref:System.Windows.Forms.IBindableComponent> 接口  
  
     实现此接口的类是支持数据绑定的非控件组件。 此类返回的数据绑定和绑定上下文的通过组件<xref:System.Windows.Forms.IBindableComponent.DataBindings%2A>和<xref:System.Windows.Forms.IBindableComponent.BindingContext%2A>此接口的属性。  
  
    > [!NOTE]
    >  如果你的组件继承自<xref:System.Windows.Forms.Control>，不需要实现<xref:System.Windows.Forms.IBindableComponent>接口。  
  
-   <xref:System.Windows.Forms.ICurrencyManagerProvider> 接口  
  
     实现的类<xref:System.Windows.Forms.ICurrencyManagerProvider>接口是提供其自己的组件<xref:System.Windows.Forms.CurrencyManager>来管理与此特定组件关联的绑定。 自定义权<xref:System.Windows.Forms.CurrencyManager>提供的<xref:System.Windows.Forms.ICurrencyManagerProvider.CurrencyManager%2A>属性。  
  
    > [!NOTE]
    >  继承的类<xref:System.Windows.Forms.Control>管理绑定通过自动及其<xref:System.Windows.Forms.Control.BindingContext%2A>属性，因此，您需要实现<xref:System.Windows.Forms.ICurrencyManagerProvider>相当罕见。  
  
## <a name="see-also"></a>请参阅
- [数据绑定和 Windows 窗体](data-binding-and-windows-forms.md)
- [如何：创建 Windows 窗体上的简单绑定控件](how-to-create-a-simple-bound-control-on-a-windows-form.md)
- [Windows 窗体数据绑定](windows-forms-data-binding.md)
