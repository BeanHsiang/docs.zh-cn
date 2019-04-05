---
title: 结构化导航概述
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- structured navigation [WPF]
ms.assetid: 025d30ef-fec5-436d-ad7a-5d5483331c26
ms.openlocfilehash: 7c8c1697ff18e919711e84e724b5b8698dfe088e
ms.sourcegitcommit: 16aefeb2d265e69c0d80967580365fabf0c5d39a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/16/2019
ms.locfileid: "58125598"
---
# <a name="structured-navigation-overview"></a>结构化导航概述
可以通过承载的内容[!INCLUDE[TLA#tla_xbap](../../../../includes/tlasharptla-xbap-md.md)]、 一个<xref:System.Windows.Controls.Frame>，或<xref:System.Windows.Navigation.NavigationWindow>组成可以标识包的页面[!INCLUDE[TLA#tla_uri#plural](../../../../includes/tlasharptla-urisharpplural-md.md)]和导航到超链接的。 页面的结构以及导航页面的方式（通过超链接来定义）称为导航拓扑。 此类拓扑适合各种应用程序类型，尤其适合在文档之间导航的应用程序类型。 对于此类应用程序，用户可以从一个页面导航到另一个页面，并且其中任一页面都无需了解另一页面的任何信息。  
  
 但是，对于其他类型的应用程序，在其页面之间导航时，确实需要了解这些页面信息。 例如，假设一个人力资源应用程序，它具有一个列出组织中所有员工的页面，即“员工列表”页。 此页还允许用户通过单击超链接添加新员工。 单击超链接后，页面会导航到“添加员工”页以收集新员工的详细信息，并将其返回到“员工列表”页以创建新员工并更新列表。 这种样式的导航与调用方法来执行某些处理并返回值（称为结构化编程）类似。 同样，这种样式的导航称为*结构化导航*。  
  
 <xref:System.Windows.Controls.Page>类未实现对结构化导航的支持。 相反，<xref:System.Windows.Navigation.PageFunction%601>类派生自<xref:System.Windows.Controls.Page>并将其扩展具有所需的结构化导航的基本构造。 本主题演示如何建立结构化的导航使用<xref:System.Windows.Navigation.PageFunction%601>。  
  
 
  
<a name="Structured_Navigation"></a>   
## <a name="structured-navigation"></a>结构化导航  
 在结构化导航中，当一个页面调用另一个页面时需要以下部分或全部行为：  
  
-   调用页导航到被调用页，并且可以选择性地传递被调用页所需的参数。  
  
-   当用户已使用完调用页时，被调用页将专门返回到调用页，并且可以：  
  
    -   返回描述调用页是如何完成（例如，用户按的是“确定”按钮还是“取消”按钮）的状态信息。  
  
    -   返回从用户那里收集的数据（例如，新员工的详细信息）。  
  
-   当调用页返回到被调用页时，被调用页会从导航历史记录中删除，以便将被调用页的一个实例与另一个实例隔离开。  
  
 下图说明了这些行为：  
  
 ![屏幕截图显示了调用页和被调用的页之间的流。](./media/structured-navigation-overview/flow-between-calling-page-called-page.png)  
  
 您可以通过使用实现这些行为<xref:System.Windows.Navigation.PageFunction%601>作为被调用页。  
  
<a name="Structured_Navigation_with_PageFunction"></a>   
## <a name="structured-navigation-with-pagefunction"></a>使用 PageFunction 进行结构化导航  
 本主题演示如何实现包含一个结构化导航的基本机制<xref:System.Windows.Navigation.PageFunction%601>。 在此示例中，<xref:System.Windows.Controls.Page>调用<xref:System.Windows.Navigation.PageFunction%601>若要获取<xref:System.String>用户值，并将其返回。  
  
### <a name="creating-a-calling-page"></a>创建调用页  
 调用页<xref:System.Windows.Navigation.PageFunction%601>可以是<xref:System.Windows.Controls.Page>或<xref:System.Windows.Navigation.PageFunction%601>。 在此示例中，它是<xref:System.Windows.Controls.Page>，如下面的代码中所示。  
  
 [!code-xaml[StructuredNavigationSample#CallingPageDefaultMARKUP1](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CallingPage.xaml#callingpagedefaultmarkup1)]  
[!code-xaml[StructuredNavigationSample#CallingPageDefaultMARKUP2](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CallingPage.xaml#callingpagedefaultmarkup2)]  
  
 [!code-csharp[StructuredNavigationSample#CallingPageDefaultCODEBEHIND1](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CallingPage.xaml.cs#callingpagedefaultcodebehind1)]
 [!code-vb[StructuredNavigationSample#CallingPageDefaultCODEBEHIND1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CallingPage.xaml.vb#callingpagedefaultcodebehind1)]  
[!code-csharp[StructuredNavigationSample#CallingPageDefaultCODEBEHIND2](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CallingPage.xaml.cs#callingpagedefaultcodebehind2)]
[!code-vb[StructuredNavigationSample#CallingPageDefaultCODEBEHIND2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CallingPage.xaml.vb#callingpagedefaultcodebehind2)]  
[!code-csharp[StructuredNavigationSample#CallingPageDefaultCODEBEHIND3](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CallingPage.xaml.cs#callingpagedefaultcodebehind3)]
[!code-vb[StructuredNavigationSample#CallingPageDefaultCODEBEHIND3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CallingPage.xaml.vb#callingpagedefaultcodebehind3)]  
  
### <a name="creating-a-page-function-to-call"></a>创建要调用的页函数  
 因为调用页可以使用被调用的页收集并返回从用户数据<xref:System.Windows.Navigation.PageFunction%601>作为其类型参数指定的被调用的页将返回的值类型的泛型类实现。 下面的代码演示实现被调用页上，使用<xref:System.Windows.Navigation.PageFunction%601>，它将返回<xref:System.String>。  
  
 [!code-xaml[StructuredNavigationSample#CalledPageFunctionMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CalledPageFunction.xaml#calledpagefunctionmarkup)]  
  
 [!code-csharp[StructuredNavigationSample#CalledPageFunctionCODEBEHIND1](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CalledPageFunction.xaml.cs#calledpagefunctioncodebehind1)]
 [!code-vb[StructuredNavigationSample#CalledPageFunctionCODEBEHIND1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CalledPageFunction.xaml.vb#calledpagefunctioncodebehind1)]  
[!code-csharp[StructuredNavigationSample#CalledPageFunctionCODEBEHIND2](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CalledPageFunction.xaml.cs#calledpagefunctioncodebehind2)]
[!code-vb[StructuredNavigationSample#CalledPageFunctionCODEBEHIND2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CalledPageFunction.xaml.vb#calledpagefunctioncodebehind2)]  
  
 声明<xref:System.Windows.Navigation.PageFunction%601>类似于声明<xref:System.Windows.Controls.Page>添加了类型自变量。 从代码示语例中可以看出，在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 标记和代码隐藏中均指定了类型自变量，前者使用 `x:TypeArguments` 属性，后者使用标准的泛型类型参数语法。  
  
 不必仅使用 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 类作为类型自变量。 一个<xref:System.Windows.Navigation.PageFunction%601>无法调用以收集抽象化为自定义类型的特定于域的数据。 下面的代码演示如何使用自定义类型的类型参数作为<xref:System.Windows.Navigation.PageFunction%601>。  
  
 [!code-csharp[CustomTypePageFunctionSnippets#CustomTypeCODE1](~/samples/snippets/csharp/VS_Snippets_Wpf/CustomTypePageFunctionSnippets/CSharp/CustomType.cs#customtypecode1)]
 [!code-vb[CustomTypePageFunctionSnippets#CustomTypeCODE1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CustomTypePageFunctionSnippets/VisualBasic/CustomType.vb#customtypecode1)]  
[!code-csharp[CustomTypePageFunctionSnippets#CustomTypeCODE2](~/samples/snippets/csharp/VS_Snippets_Wpf/CustomTypePageFunctionSnippets/CSharp/CustomType.cs#customtypecode2)]
[!code-vb[CustomTypePageFunctionSnippets#CustomTypeCODE2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CustomTypePageFunctionSnippets/VisualBasic/CustomType.vb#customtypecode2)]  
  
 [!code-xaml[CustomTypePageFunctionSnippets#CustomTypePageFunctionMARKUP1](~/samples/snippets/csharp/VS_Snippets_Wpf/CustomTypePageFunctionSnippets/CSharp/CustomTypePageFunction.xaml#customtypepagefunctionmarkup1)]  
[!code-xaml[CustomTypePageFunctionSnippets#CustomTypePageFunctionMARKUP2](~/samples/snippets/csharp/VS_Snippets_Wpf/CustomTypePageFunctionSnippets/CSharp/CustomTypePageFunction.xaml#customtypepagefunctionmarkup2)]  
  
 [!code-csharp[CustomTypePageFunctionSnippets#CustomTypePageFunctionCODEBEHIND1](~/samples/snippets/csharp/VS_Snippets_Wpf/CustomTypePageFunctionSnippets/CSharp/CustomTypePageFunction.xaml.cs#customtypepagefunctioncodebehind1)]
 [!code-vb[CustomTypePageFunctionSnippets#CustomTypePageFunctionCODEBEHIND1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CustomTypePageFunctionSnippets/VisualBasic/CustomTypePageFunction.xaml.vb#customtypepagefunctioncodebehind1)]  
[!code-csharp[CustomTypePageFunctionSnippets#CustomTypePageFunctionCODEBEHIND2](~/samples/snippets/csharp/VS_Snippets_Wpf/CustomTypePageFunctionSnippets/CSharp/CustomTypePageFunction.xaml.cs#customtypepagefunctioncodebehind2)]
[!code-vb[CustomTypePageFunctionSnippets#CustomTypePageFunctionCODEBEHIND2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CustomTypePageFunctionSnippets/VisualBasic/CustomTypePageFunction.xaml.vb#customtypepagefunctioncodebehind2)]  
  
 类型参数<xref:System.Windows.Navigation.PageFunction%601>为以下各节所述调用页与被调用的页之间的通信奠定了基础。  
  
 正如您将看到的使用的声明标识的类型<xref:System.Windows.Navigation.PageFunction%601>发挥着重要作用中返回数据从<xref:System.Windows.Navigation.PageFunction%601>向调用页。  
  
### <a name="calling-a-pagefunction-and-passing-parameters"></a>调用 PageFunction 和传递参数  
 若要调用一个页面，调用页必须实例化被调用的页并导航到该使用<xref:System.Windows.Navigation.NavigationService.Navigate%2A>方法。 这使得调用页可以将初始数据传递给被调用页，例如，被调用页收集的数据的默认值。  
  
 下面的代码演示使用非默认构造函数从调用页接受参数的被调用页。  
  
 [!code-csharp[StructuredNavigationSample#AcceptsInitialDataCODEBEHIND1](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CalledPageFunction.xaml.cs#acceptsinitialdatacodebehind1)]
 [!code-vb[StructuredNavigationSample#AcceptsInitialDataCODEBEHIND1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CalledPageFunction.xaml.vb#acceptsinitialdatacodebehind1)]  
[!code-csharp[StructuredNavigationSample#AcceptsInitialDataCODEBEHIND2](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CalledPageFunction.xaml.cs#acceptsinitialdatacodebehind2)]
[!code-vb[StructuredNavigationSample#AcceptsInitialDataCODEBEHIND2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CalledPageFunction.xaml.vb#acceptsinitialdatacodebehind2)]  
[!code-csharp[StructuredNavigationSample#AcceptsInitialDataCODEBEHIND3](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CalledPageFunction.xaml.cs#acceptsinitialdatacodebehind3)]
[!code-vb[StructuredNavigationSample#AcceptsInitialDataCODEBEHIND3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CalledPageFunction.xaml.vb#acceptsinitialdatacodebehind3)]  
[!code-csharp[StructuredNavigationSample#AcceptsInitialDataCODEBEHIND4](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CalledPageFunction.xaml.cs#acceptsinitialdatacodebehind4)]
[!code-vb[StructuredNavigationSample#AcceptsInitialDataCODEBEHIND4](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CalledPageFunction.xaml.vb#acceptsinitialdatacodebehind4)]  
  
 下面的代码演示调用页处理<xref:System.Windows.Documents.Hyperlink.Click>事件的<xref:System.Windows.Documents.Hyperlink>实例化被调用的页，并将其传递初始字符串值。  
  
 [!code-xaml[StructuredNavigationSample#PassingDataMARKUP2](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CallingPage.xaml#passingdatamarkup2)]  
[!code-csharp[StructuredNavigationSample#PassingDataCODEBEHIND1](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CallingPage.xaml.cs#passingdatacodebehind1)]
[!code-vb[StructuredNavigationSample#PassingDataCODEBEHIND1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CallingPage.xaml.vb#passingdatacodebehind1)]  
[!code-csharp[StructuredNavigationSample#PassingDataCODEBEHIND2](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CallingPage.xaml.cs#passingdatacodebehind2)]
[!code-vb[StructuredNavigationSample#PassingDataCODEBEHIND2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CallingPage.xaml.vb#passingdatacodebehind2)]  
[!code-csharp[StructuredNavigationSample#PassingDataCODEBEHIND3](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CallingPage.xaml.cs#passingdatacodebehind3)]
[!code-vb[StructuredNavigationSample#PassingDataCODEBEHIND3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CallingPage.xaml.vb#passingdatacodebehind3)]  
  
 不必向被调用页传递参数。 可以执行以下操作：  
  
-   从调用页：  
  
    1.  实例化被调用<xref:System.Windows.Navigation.PageFunction%601>使用默认构造函数。  
  
    2.  存储中的参数<xref:System.Windows.Application.Properties%2A>。  
  
    3.  导航到被调用<xref:System.Windows.Navigation.PageFunction%601>。  
  
-   从被调用<xref:System.Windows.Navigation.PageFunction%601>:  
  
    -   检索和使用存储在参数<xref:System.Windows.Application.Properties%2A>。  
  
 但是，你不久就会看到，你仍然需要使用代码来实例化并导航到被调用页，以收集被调用页返回的数据。 出于此原因，<xref:System.Windows.Navigation.PageFunction%601>需求保持活动状态; 否则为下次导航到<xref:System.Windows.Navigation.PageFunction%601>，[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]实例化<xref:System.Windows.Navigation.PageFunction%601>使用默认构造函数。  
  
 但是，在被调用页返回前，需要返回可以由调用页检索的数据。  
  
### <a name="returning-task-result-and-task-data-from-a-task-to-a-calling-page"></a>将任务的任务结果和任务数据返回到调用页  
 在用户使用完被调用页后（在本示例中通过按“确定”或“取消”按钮来表示），被调用页需要返回。 因为调用页已使用被调用页来从用户那里收集数据，所以调用页需要两种类型的信息：  
  
1.  用户是否取消了被调用页（在此示例中通过按“确定”或“取消”按钮）。 这使得调用页可以确定是否处理调用页从用户那里收集的数据。  
  
2.  用户提供的数据。  
  
 若要返回的信息，<xref:System.Windows.Navigation.PageFunction%601>实现<xref:System.Windows.Navigation.PageFunction%601.OnReturn%2A>方法。 下面的代码演示如何调用它。  
  
 [!code-csharp[StructuredNavigationSample#ReturnCODEBEHIND1](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CalledPageFunction.xaml.cs#returncodebehind1)]
 [!code-vb[StructuredNavigationSample#ReturnCODEBEHIND1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CalledPageFunction.xaml.vb#returncodebehind1)]  
[!code-csharp[StructuredNavigationSample#ReturnCODEBEHIND2](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CalledPageFunction.xaml.cs#returncodebehind2)]
[!code-vb[StructuredNavigationSample#ReturnCODEBEHIND2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CalledPageFunction.xaml.vb#returncodebehind2)]  
  
 在此示例中，如果用户按“取消”按钮，则会向调用页返回 `null` 值。 如果按“确定”按钮，则返回用户提供的字符串值。 <xref:System.Windows.Navigation.PageFunction%601.OnReturn%2A> 是`protected virtual`调用以向调用页返回数据的方法。 你的数据需要打包的泛型实例中<xref:System.Windows.Navigation.ReturnEventArgs%601>类型，其类型参数指定的类型值<xref:System.Windows.Navigation.ReturnEventArgs%601.Result%2A>返回。 这样一来，在声明时<xref:System.Windows.Navigation.PageFunction%601>使用特定类型自变量，即指明<xref:System.Windows.Navigation.PageFunction%601>将返回指定的类型参数的类型的实例。 在此示例中，类型参数和返回值，因此，属于类型<xref:System.String>。  
  
 当<xref:System.Windows.Navigation.PageFunction%601.OnReturn%2A>调用时，调用页需要某种方法来接收的返回值<xref:System.Windows.Navigation.PageFunction%601>。 出于此原因，<xref:System.Windows.Navigation.PageFunction%601>实现<xref:System.Windows.Navigation.PageFunction%601.Return>调用页来处理的事件。 当<xref:System.Windows.Navigation.PageFunction%601.OnReturn%2A>调用时，<xref:System.Windows.Navigation.PageFunction%601.Return>引发，以便调用页可以向注册<xref:System.Windows.Navigation.PageFunction%601.Return>来接收通知。  
  
 [!code-csharp[StructuredNavigationSample#ProcessResultCODEBEHIND1](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CallingPage.xaml.cs#processresultcodebehind1)]
 [!code-vb[StructuredNavigationSample#ProcessResultCODEBEHIND1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CallingPage.xaml.vb#processresultcodebehind1)]  
[!code-csharp[StructuredNavigationSample#ProcessResultCODEBEHIND2](~/samples/snippets/csharp/VS_Snippets_Wpf/StructuredNavigationSample/CSharp/CallingPage.xaml.cs#processresultcodebehind2)]
[!code-vb[StructuredNavigationSample#ProcessResultCODEBEHIND2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StructuredNavigationSample/VisualBasic/CallingPage.xaml.vb#processresultcodebehind2)]  
  
### <a name="removing-task-pages-when-a-task-completes"></a>当任务完成时删除任务页  
 当被调用页返回，并且用户未取消被调用页时，调用页将处理由用户提供并且从被调用页返回的数据。 这种方式的数据采集通常是独立的活动；当被调用页返回时，调用页需要创建并导航到新的调用页来捕获更多数据。  
  
 不过，除非已从日志中删除被调用页，否则用户将能够向后导航到调用页的上一个实例。 是否<xref:System.Windows.Navigation.PageFunction%601>保留在日志由<xref:System.Windows.Navigation.PageFunctionBase.RemoveFromJournal%2A>属性。 默认情况下，页函数会自动删除何时<xref:System.Windows.Navigation.PageFunction%601.OnReturn%2A>称为，因为<xref:System.Windows.Navigation.PageFunctionBase.RemoveFromJournal%2A>设置为`true`。 若要导航历史记录中后保留页函数<xref:System.Windows.Navigation.PageFunction%601.OnReturn%2A>调用时，设置<xref:System.Windows.Navigation.PageFunctionBase.RemoveFromJournal%2A>到`false`。  
  
<a name="Other_Types_of_Structured_Navigation"></a>   
## <a name="other-types-of-structured-navigation"></a>其他类型的结构化导航  
 本主题说明了最基本的用法<xref:System.Windows.Navigation.PageFunction%601>以支持调用/返回结构化导航。 这一基础使你能够创建更复杂的结构化导航类型。  
  
 例如，有时调用页需要多个页面来从用户那里收集足够的数据或者执行任务。 多个页面的使用称为“向导”。  
  
 在其他情况下，应用程序可能具有依赖于结构化导航来有效操作的复杂导航拓扑。 有关详细信息，请参阅[导航拓扑概述](navigation-topologies-overview.md)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Navigation.PageFunction%601>
- <xref:System.Windows.Navigation.NavigationService>
- [导航拓扑概述](navigation-topologies-overview.md)
