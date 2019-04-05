---
title: 数据和数据对象
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data transfer [WPF], drag-and-drop
- DataFormats class [WPF]
- DataObject class [WPF]
ms.assetid: 5967d557-1867-420f-a524-ae3af78402da
ms.openlocfilehash: 483491ea7408c1df57f31b4b984116b085ea50ba
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57367539"
---
# <a name="data-and-data-objects"></a>数据和数据对象
拖放操作的一部分传输的数据存储在数据对象。  从概念上讲，数据对象包含一个或多个以下对：  
  
-   <xref:System.Object> ，其中包含实际数据。  
  
-   对应的数据格式标识符。  
  
 数据本身可以包含任何可以表示为基本<xref:System.Object>。  相应的数据格式是一个字符串或<xref:System.Type>，它提供有关设置数据的格式的提示是在中。  数据对象支持托管多个数据/数据格式对;这样一个数据对象提供多种格式的数据。  
  
<a name="Data_and_Data_Objects"></a>   
## <a name="data-objects"></a>数据对象  
 所有数据对象必须都实现<xref:System.Windows.IDataObject>接口，它提供了启用和进行数据传输方法的以下标准集。  
  
|方法|总结|  
|------------|-------------|  
|<xref:System.Windows.IDataObject.GetData%2A>|检索指定的数据格式的数据对象。|  
|<xref:System.Windows.IDataObject.GetDataPresent%2A>|检查以查看是否现已推出，或者可以转换为指定格式数据。|  
|<xref:System.Windows.IDataObject.GetFormats%2A>|返回此数据对象中的数据存储，或可以转换为的格式的列表。|  
|<xref:System.Windows.IDataObject.SetData%2A>|此数据对象中存储指定的数据。|  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供的基本实现<xref:System.Windows.IDataObject>在<xref:System.Windows.DataObject>类。 股票<xref:System.Windows.DataObject>类足以满足许多常见的数据传输方案。  
  
 有几个预定义的格式，如位图、 CSV、 文件、 HTML、 RTF、 字符串、 文本和音频。 有关随一起提供的预定义的数据格式信息[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]，请参阅<xref:System.Windows.DataFormats>类参考主题。  
  
 数据对象通常包括一个工具，以便自动将转换为其他格式的一种格式中提取数据; 时存储的数据此工具称为自动转换。 查询时可用的数据对象中的数据格式，可以通过调用筛选从本机数据格式自动转换的数据格式<xref:System.Windows.DataObject.GetFormats%28System.Boolean%29>或<xref:System.Windows.DataObject.GetDataPresent%28System.String%2CSystem.Boolean%29>方法并指定`autoConvert`作为参数`false`。  将数据添加到具有的数据对象时<xref:System.Windows.DataObject.SetData%28System.String%2CSystem.Object%2CSystem.Boolean%29>方法，自动转换的数据，可以通过设置禁止`autoConvert`参数`false`。  
  
<a name="Working_with_Data_Objects"></a>   
## <a name="working-with-data-objects"></a>使用数据对象  
 本部分介绍用于创建和使用数据对象的常见方法。  
  
### <a name="creating-new-data-objects"></a>创建新的数据对象  
 <xref:System.Windows.DataObject>类提供了多个重载的构造函数，便于您填充一个新<xref:System.Windows.DataObject>具有单一数据格式对实例。  
  
 下面的代码示例创建一个新的数据对象，并使用重载的构造函数之一<xref:System.Windows.DataObject.%23ctor%2A>(<xref:System.Windows.DataObject.%23ctor(System.String,System.Object)>) 来初始化具有一个字符串，指定的数据格式的数据对象。  一个字符串; 在这种情况下，指定数据格式<xref:System.Windows.DataFormats>类提供了一组预定义的类型字符串。 默认情况下允许存储的数据的自动转换。  
  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_TypeString](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_createdataobject_typestring)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_TypeString](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_createdataobject_typestring)]  
  
 有关创建数据对象的代码的更多示例，请参阅[创建数据对象](how-to-create-a-data-object.md)。  
  
### <a name="storing-data-in-multiple-formats"></a>以多种格式存储数据  
 单个数据对象是能够以多种格式存储数据。   战略使用单个数据对象中的多种数据格式可能会使数据对象可以使用更多种类的放置目标比如果仅可以表示单一数据格式。  请注意，一般情况下，拖动源必须是不可知的数据格式的使用可能放置目标的索引。  
  
 下面的示例演示如何使用<xref:System.Windows.DataObject.SetData%28System.String%2CSystem.Object%29>方法将数据添加到多个格式中的数据对象。  
  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_StoreMultipleFormats](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_storemultipleformats)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_StoreMultipleFormats](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_storemultipleformats)]  
  
### <a name="querying-a-data-object-for-available-formats"></a>查询可用的格式数据对象  
 由于单个数据对象可以包含任意数目的数据格式，数据对象包含用于检索可用的数据格式的列表的功能。  
  
 下面的示例代码使用<xref:System.Windows.DataObject.GetFormats%2A>重载获取表示所有可用数据对象 （本机和通过自动转换） 中的数据格式的字符串数组。  
  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_GetAllDataFormats](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_getalldataformats)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_GetAllDataFormats](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_getalldataformats)]  
  
 查询可用的数据格式的数据对象的代码的更多示例，请参阅[列出数据对象中的数据格式](how-to-list-the-data-formats-in-a-data-object.md)。  查询是否存在特定的数据格式的数据对象的示例，请参阅[确定数据格式是否存在于数据对象中](how-to-determine-if-a-data-format-is-present-in-a-data-object.md)。  
  
### <a name="retrieving-data-from-a-data-object"></a>从数据对象中检索数据  
 从特定格式的数据对象中检索数据仅涉及调用之一<xref:System.Windows.DataObject.GetData%2A>方法并指定所需的数据格式。  其中一个<xref:System.Windows.DataObject.GetDataPresent%2A>方法可用于检查是否存在特定的数据格式。  <xref:System.Windows.DataObject.GetData%2A> 在将数据返回<xref:System.Object>; 具体取决于数据格式，此对象可强制转换为特定于类型的容器。  
  
 下面的示例代码使用<xref:System.Windows.DataObject.GetDataPresent%28System.String%29>重载来检查是否可指定的数据格式 （本机编译或通过自动转换）。 如果指定的格式不可用，该示例通过检索数据<xref:System.Windows.DataObject.GetData%28System.String%29>方法。  
  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_GetSpecificDataFormat](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_getspecificdataformat)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_GetSpecificDataFormat](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_getspecificdataformat)]  
  
 数据对象中检索数据的代码的更多示例，请参阅[特定数据格式检索数据](how-to-retrieve-data-in-a-particular-data-format.md)。  
  
### <a name="removing-data-from-a-data-object"></a>从数据对象中删除数据  
 从数据对象不能直接删除数据。  若要有效地从数据对象中删除数据，请按照下列步骤：  
  
1.  创建新的数据对象将包含你想要保留数据。  
  
2.  "复制"到新的数据对象从旧的数据对象所需的数据。  若要复制数据，请使用之一<xref:System.Windows.DataObject.GetData%2A>方法来检索<xref:System.Object>，其中包含原始数据，然后执行下列任一<xref:System.Windows.DataObject.SetData%2A>方法将数据添加到新的数据对象。  
  
3.  替换为新旧数据对象。  
  
> [!NOTE]
>  <xref:System.Windows.DataObject.SetData%2A>方法仅将数据添加到数据对象; 但仍数据，即使数据和数据格式完全与上一次调用相同。 调用<xref:System.Windows.DataObject.SetData%2A>两次以相同的数据和数据格式将导致数据/数据格式存在的数据对象中两次。
