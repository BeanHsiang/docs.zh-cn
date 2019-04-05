---
title: WPF 版本 4.5 的新增功能
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Presentation Foundation [WPF], what's new
- WPF [WPF], what's new
ms.assetid: db086ae4-70bb-4862-95db-2eaca5216bc3
ms.openlocfilehash: 92f69d0f9ad962dff231308ed3f5d59a0d406792
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57368163"
---
# <a name="whats-new-in-wpf-version-45"></a>WPF 版本 4.5 的新增功能
<a name="introduction"></a> 本主题包含有关新的和增强功能的信息[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]版本 4.5。  
  
 本主题包含以下各节：  
  
-   [功能区控件](#ribbon_control)  
  
-   [显示大型分组数据集时增强的性能](#grouped_virtualization)  
  
-   [VirtualizingPanel 的新增功能](#VirtualizingPanel)  
  
-   [绑定到静态属性](#static_properties)  
  
-   [访问非 UI 线程上的集合](#xthread_access)  
  
-   [同步和异步验证数据](#INotifyDataErrorInfo)  
  
-   [自动更新数据绑定源](#delay)  
  
-   [绑定到实现 ICustomTypeProvider 的类型](#ICustomTypeProvider)  
  
-   [从绑定表达式中检索数据绑定信息](#binding_state)  
  
-   [检查有效的 DataContext 对象](#DisconnectedSource)  
  
-   [在数据值发生更改时重新定位数据（实时数据整理）](#live_shaping)  
  
-   [对建立事件的弱引用的增强支持](#weak_event_pattern)  
  
-   [用于调度程序类的新方法](#async)  
  
-   [事件的标记扩展](#events_markup_extenions)  
  
<a name="ribbon_control"></a>   
## <a name="ribbon-control"></a>功能区控件  
 WPF 4.5 附带<xref:System.Windows.Controls.Ribbon.Ribbon>承载快速访问工具栏、 应用程序菜单和选项卡的控件。  有关详细信息，请参阅[功能区概述](/visualstudio/vsto/ribbon-overview)。  
  
<a name="grouped_virtualization"></a>   
## <a name="improved-performance-when-displaying-large-sets-of-grouped-data"></a>显示大型分组数据集时增强的性能  
 当根据哪些项在屏幕上可见来从大量数据项中生成用户界面 (UI) 元素的子集时，将发生 UI 虚拟化。 <xref:System.Windows.Controls.VirtualizingPanel>定义<xref:System.Windows.Controls.VirtualizingPanel.IsVirtualizingWhenGrouping%2A>附加启用 UI 虚拟化分组数据的属性。  有关对数据进行分组的详细信息，请参阅如何：排序和分组数据在 XAML 中使用视图。  有关虚拟化的详细信息分组数据，请参阅<xref:System.Windows.Controls.VirtualizingPanel.IsVirtualizingWhenGrouping%2A>附加属性。  
  
<a name="VirtualizingPanel"></a>   
## <a name="new-features-for-the-virtualizingpanel"></a>VirtualizingPanel 的新增功能  
  
1.  您可以指定是否<xref:System.Windows.Controls.VirtualizingPanel>，如<xref:System.Windows.Controls.VirtualizingStackPanel>，通过使用显示部分项<xref:System.Windows.Controls.VirtualizingPanel.ScrollUnit%2A>附加属性。 如果<xref:System.Windows.Controls.VirtualizingPanel.ScrollUnit%2A>设置为<xref:System.Windows.Controls.ScrollUnit.Item>，则<xref:System.Windows.Controls.VirtualizingPanel>将仅显示完全可见的项。 如果<xref:System.Windows.Controls.VirtualizingPanel.ScrollUnit%2A>设置为<xref:System.Windows.Controls.ScrollUnit.Pixel>，则<xref:System.Windows.Controls.VirtualizingPanel>可以显示部分可见的项。  
  
2.  您可以指定缓存的大小，视区前后时<xref:System.Windows.Controls.VirtualizingPanel>通过使用虚拟化<xref:System.Windows.Controls.VirtualizingPanel.CacheLength%2A>附加属性。  缓存是视区（其中的项未虚拟化）上方或下方的空间量。  使用缓存避免生成 UI 元素（因为系统会将它们滚动到视图中）可以提高性能。 在较低优先级填充缓存，以便应用程序在操作期间能够响应。 <xref:System.Windows.Controls.VirtualizingPanel.CacheLengthUnit%2A?displayProperty=nameWithType>属性确定使用的度量单位<xref:System.Windows.Controls.VirtualizingPanel.CacheLength%2A?displayProperty=nameWithType>。  
  
<a name="static_properties"></a>   
## <a name="binding-to-static-properties"></a>绑定到静态属性  
 可以将静态属性用作数据绑定的源。 如果属性值更改时引发了静态事件，数据绑定引擎将会识别。  例如，如果类 `SomeClass` 定义了名为 `MyProperty` 的静态属性，则 `SomeClass` 可以定义 `MyProperty` 的值发生更改时所引发的静态事件。  静态事件可以使用以下签名之一。  
  
-   `public static event EventHandler MyPropertyChanged;`  
  
-   `public static event EventHandler<PropertyChangedEventArgs> StaticPropertyChanged;`  
  
 请注意，在第一种情况下，类将公开名为的静态事件*PropertyName* `Changed`通过<xref:System.EventArgs>到事件处理程序。  在第二种情况下，该类会公开名为的静态事件`StaticPropertyChanged`通过<xref:System.ComponentModel.PropertyChangedEventArgs>到事件处理程序。 实现静态属性的类可以选择使用任一方法引发属性更改通知。  
  
<a name="xthread_access"></a>   
## <a name="accessing-collections-on-non-ui-threads"></a>访问非 UI 线程上的集合  
 WPF 允许访问和修改线程上的数据集合，创建该集合的线程除外。  这可允许使用后台线程接收来自外部源（例如数据库）的数据，并在 UI 线程上显示该数据。  通过使用另一线程来修改该集合，用户界面将仍可继续响应用户交互。  
  
<a name="INotifyDataErrorInfo"></a>   
## <a name="synchronously-and-asynchronously-validating-data"></a>同步和异步验证数据  
 <xref:System.ComponentModel.INotifyDataErrorInfo>接口使数据实体类能够实现自定义验证规则并以异步方式公开验证结果。 此接口还支持自定义错误对象、每个属性具有多个错误、跨属性错误和实体级别的错误。  有关详细信息，请参阅 <xref:System.ComponentModel.INotifyDataErrorInfo>。  
  
<a name="delay"></a>   
## <a name="automatically-updating-the-source-of-a-data-binding"></a>自动更新数据绑定源  
 如果使用数据绑定来更新数据源，则可以使用<xref:System.Windows.Data.BindingBase.Delay%2A>属性来指定要更新源之前对目标属性发生更改后经过的时间量。  例如，假设您有<xref:System.Windows.Controls.Slider>具有其<xref:System.Windows.Controls.Primitives.RangeBase.Value%2A>属性数据双向绑定到数据对象的属性和<xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A>属性设置为<xref:System.Windows.Data.UpdateSourceTrigger.PropertyChanged>。  在此示例中，当用户移动<xref:System.Windows.Controls.Slider>，每个像素的源更新的<xref:System.Windows.Controls.Slider>移动。  源对象通常需要滑块的值时，才滑块的<xref:System.Windows.Controls.Primitives.RangeBase.Value%2A>停止更改。  若要防止对源进行过于频繁更新，请使用<xref:System.Windows.Data.BindingBase.Delay%2A>指定直到一定的时间结束后在缩略图停止移动不应更新源。  
  
<a name="ICustomTypeProvider"></a>   
## <a name="binding-to-types-that-implement-icustomtypeprovider"></a>绑定到实现 ICustomTypeProvider 的类型  
 WPF 支持数据绑定到实现的对象<xref:System.Reflection.ICustomTypeProvider>，也称为自定义类型。  在以下情况下，可以使用自定义类型。  
  
1.  作为<xref:System.Windows.PropertyPath>在数据绑定。 例如，<xref:System.Windows.Data.Binding.Path%2A>属性的<xref:System.Windows.Data.Binding>可以引用自定义类型的属性。  
  
2.  值作为<xref:System.Windows.DataTemplate.DataType%2A>属性。  
  
3.  确定自动生成的列中的类型为<xref:System.Windows.Controls.DataGrid>。  
  
<a name="binding_state"></a>   
## <a name="retrieving-data-binding-information-from-a-binding-expression"></a>从绑定表达式中检索数据绑定信息  
 在某些情况下，可能会收到<xref:System.Windows.Data.BindingExpression>的<xref:System.Windows.Data.Binding>并且需要有关绑定的源和目标对象的信息。  使用已添加新的 API 可获取源或目标对象或关联的属性。  当你具有<xref:System.Windows.Data.BindingExpression>，使用以下 Api 来获取有关目标和源的信息。  
  
|查找绑定的值|使用此 API|  
|---------------------------------------|------------------|  
|目标对象|<xref:System.Windows.Data.BindingExpressionBase.Target%2A?displayProperty=nameWithType>|  
|目标属性|<xref:System.Windows.Data.BindingExpressionBase.TargetProperty%2A?displayProperty=nameWithType>|  
|源对象|<xref:System.Windows.Data.BindingExpression.ResolvedSource%2A?displayProperty=nameWithType>|  
|源属性|<xref:System.Windows.Data.BindingExpression.ResolvedSourcePropertyName%2A?displayProperty=nameWithType>|  
|是否<xref:System.Windows.Data.BindingExpression>属于 <xref:System.Windows.Data.BindingGroup>|<xref:System.Windows.Data.BindingExpressionBase.BindingGroup%2A?displayProperty=nameWithType>|  
|所有者 <xref:System.Windows.Data.BindingGroup>|<xref:System.Windows.Data.BindingGroup.Owner%2A>|  
  
<a name="DisconnectedSource"></a>   
## <a name="checking-for-a-valid-datacontext-object"></a>检查有效的 DataContext 对象  
 某些情况下，<xref:System.Windows.FrameworkElement.DataContext%2A>中的项容器的<xref:System.Windows.Controls.ItemsControl>断开连接。  项容器是显示中的项的 UI 元素<xref:System.Windows.Controls.ItemsControl>。  当<xref:System.Windows.Controls.ItemsControl>是数据绑定到集合时，项容器为每个项生成。 在某些情况下，会从可视化树中删除项容器。 其中删除一个项容器的两种典型情况是从基础集合删除项的时间和当在上启用虚拟化<xref:System.Windows.Controls.ItemsControl>。 在这些情况下，<xref:System.Windows.FrameworkElement.DataContext%2A>项容器的属性将设置为返回的 sentinel 对象<xref:System.Windows.Data.BindingOperations.DisconnectedSource%2A?displayProperty=nameWithType>静态属性。  应检查是否<xref:System.Windows.FrameworkElement.DataContext%2A>等同于<xref:System.Windows.Data.BindingOperations.DisconnectedSource%2A>然后才能访问对象<xref:System.Windows.FrameworkElement.DataContext%2A>的项容器。  
  
<a name="live_shaping"></a>   
## <a name="repositioning-data-as-the-datas-values-change-live-shaping"></a>在数据值发生更改时重新定位数据（实时数据整理）  
 可以对数据集合进行分组、排序或筛选。 WPF 4.5 允许在修改数据时重新排列数据。 例如，假设应用程序使用<xref:System.Windows.Controls.DataGrid>列出股票市场中的股票和股票按股票值。 如果在股票的上启用实时排序<xref:System.Windows.Data.CollectionView>中的股票的位置<xref:System.Windows.Controls.DataGrid>移动时的股票值将成为更高版本或小于另一个股票的值。   有关详细信息，请参阅<xref:System.ComponentModel.ICollectionViewLiveShaping>接口。  
  
<a name="weak_event_pattern"></a>   
## <a name="improved-support-for-establishing-a-weak-reference-to-an-event"></a>对建立事件的弱引用的增强支持  
 现在实现弱事件模式更加容易，因为可以借助事件的订阅服务器并且无需实现附加接口。  泛型<xref:System.Windows.WeakEventManager>类还可使订阅服务器参与弱事件模式，如果专用<xref:System.Windows.WeakEventManager>不存在特定事件。  有关详细信息，请参阅[弱事件模式](../advanced/weak-event-patterns.md)。  
  
<a name="async"></a>   
## <a name="new-methods-for-the-dispatcher-class"></a>用于调度程序类的新方法  
 调度程序类定义同步和异步操作的新方法。  同步<xref:System.Windows.Threading.Dispatcher.Invoke%2A>方法定义采用重载<xref:System.Action>或<xref:System.Func%601>参数。 新的异步方法， <xref:System.Windows.Threading.Dispatcher.InvokeAsync%2A>，还会<xref:System.Action>或<xref:System.Func%601>作为回调参数并返回<xref:System.Windows.Threading.DispatcherOperation>或<xref:System.Windows.Threading.DispatcherOperation%601>。   <xref:System.Windows.Threading.DispatcherOperation>并<xref:System.Windows.Threading.DispatcherOperation%601>类定义<xref:System.Threading.Tasks.Task>属性。  当您调用<xref:System.Windows.Threading.Dispatcher.InvokeAsync%2A>，可以使用`await`使用的关键字<xref:System.Windows.Threading.DispatcherOperation>或关联<xref:System.Threading.Tasks.Task>。 如果你需要同步等待<xref:System.Threading.Tasks.Task>返回的<xref:System.Windows.Threading.DispatcherOperation>或<xref:System.Windows.Threading.DispatcherOperation%601>，调用<xref:System.Windows.Threading.TaskExtensions.DispatcherOperationWait%2A>扩展方法。 调用<xref:System.Threading.Tasks.Task.Wait%2A?displayProperty=nameWithType>在调用线程上排队操作将导致死锁。 有关使用详细信息<xref:System.Threading.Tasks.Task>若要执行异步操作，请参阅[任务并行 （任务并行库）](../../../standard/parallel-programming/task-based-asynchronous-programming.md)。  
  
<a name="events_markup_extenions"></a>   
## <a name="markup-extensions-for-events"></a>事件的标记扩展  
 WPF 4.5 支持事件的标记扩展。  虽然 WPF 未定义用于事件的标记扩展，但第三方能够创建可与事件配合使用的标记扩展。  
  
## <a name="see-also"></a>请参阅
- [.NET Framework 中的新增功能](../../whats-new/index.md)
