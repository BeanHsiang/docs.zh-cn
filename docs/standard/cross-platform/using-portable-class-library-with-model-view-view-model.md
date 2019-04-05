---
title: 将可移植类库与模型-视图-视图模型配合使用
ms.date: 07/18/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Portable Class Library [.NET Framework], and MVVM
- MVVM, and Portable Class Library
ms.assetid: 41a0b9f8-15a2-431a-bc35-e310b2953b03
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 8b48dc67e18411d82f03d29ab244d57575d6d720
ms.sourcegitcommit: bd28ff1e312eaba9718c4f7ea272c2d4781a7cac
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/26/2019
ms.locfileid: "56835780"
---
# <a name="using-portable-class-library-with-model-view-view-model"></a>将可移植类库与模型-视图-视图模型配合使用
可以使用.NET Framework[可移植类库](../../../docs/standard/cross-platform/cross-platform-development-with-the-portable-class-library.md)实现模型-视图-视图模型 (MVVM) 模式并跨多个平台共享程序集。

[!INCLUDE[standard](../../../includes/pcl-to-standard.md)]

 MVVM 是将用户界面与基础业务逻辑相隔离的应用程序模式。 您可以实现中的模型和视图模型类[!INCLUDE[net_portable](../../../includes/net-portable-md.md)]项目在 Visual Studio 2012 中，然后创建针对不同平台自定义的视图。 通过此方法，只需编写数据模型和业务逻辑一次，即可将该代码用于 .NET Framework、Silverlight、Windows Phone 和 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 应用，如下图所示。

 ![可移植的 MVVM 关系图](../../../docs/standard/cross-platform/media/portablemvvmdiagram.png "PortableMVVMdiagram")

 本主题不提供有关 MVVM 模式的一般信息。 它仅提供有关如何使用信息[!INCLUDE[net_portable](../../../includes/net-portable-md.md)]来实现 MVVM。 有关 MVVM 的详细信息，请参阅[MVVM 快速入门使用 Prism Library 5.0 的 WPF](https://docs.microsoft.com/previous-versions/msp-n-p/gg430857(v=pandp.40))。

## <a name="classes-that-support-mvvm"></a>支持 MVVM 类
 当你针对[!INCLUDE[net_v45](../../../includes/net-v45-md.md)]， [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)]，Silverlight 或 Windows Phone 7.5 的应用[!INCLUDE[net_portable](../../../includes/net-portable-md.md)]项目中，下列类是可用于实现 MVVM 模式：

-   <xref:System.Collections.ObjectModel.ObservableCollection%601?displayProperty=nameWithType> 类

-   <xref:System.Collections.ObjectModel.ReadOnlyObservableCollection%601?displayProperty=nameWithType> 类

-   <xref:System.Collections.Specialized.INotifyCollectionChanged?displayProperty=nameWithType> 类

-   <xref:System.Collections.Specialized.NotifyCollectionChangedAction?displayProperty=nameWithType> 类

-   <xref:System.Collections.Specialized.NotifyCollectionChangedEventArgs?displayProperty=nameWithType> 类

-   <xref:System.Collections.Specialized.NotifyCollectionChangedEventHandler?displayProperty=nameWithType> 类

-   <xref:System.ComponentModel.DataErrorsChangedEventArgs?displayProperty=nameWithType> 类

-   <xref:System.ComponentModel.INotifyDataErrorInfo?displayProperty=nameWithType> 类

-   <xref:System.ComponentModel.INotifyPropertyChanged?displayProperty=nameWithType> 类

-   <xref:System.Windows.Input.ICommand?displayProperty=nameWithType> 类

-   中的所有类<xref:System.ComponentModel.DataAnnotations?displayProperty=nameWithType>命名空间

## <a name="implementing-mvvm"></a>实现 MVVM
 若要实现 MVVM，您通常创建模型和视图模型中的[!INCLUDE[net_portable](../../../includes/net-portable-md.md)]项目，因为[!INCLUDE[net_portable](../../../includes/net-portable-md.md)]项目不能引用不可移植的项目。 模型和视图模型可以是同一个项目中或单独的项目中。 如果使用单独的项目，添加从视图模型项目到模型项目的引用。

 编译模型并查看模型项目后，您引用的包含视图的应用中的这些程序集。 如果该视图仅与视图模型进行交互，只需引用包含视图模型的程序集。

### <a name="model"></a>模型
 下面的示例演示可驻留在简化的模型类[!INCLUDE[net_portable](../../../includes/net-portable-md.md)]项目。

 [!code-csharp[PortableClassLibraryMVVM#1](../../../samples/snippets/csharp/VS_Snippets_CLR/portableclasslibrarymvvm/cs/customer.cs#1)]
 [!code-vb[PortableClassLibraryMVVM#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/portableclasslibrarymvvm/vb/customer.vb#1)]

 下面的示例演示填充、 检索和更新中的数据的简单方法[!INCLUDE[net_portable](../../../includes/net-portable-md.md)]项目。 在实际应用中，将从 Windows Communication Foundation (WCF) 服务等源检索数据。

 [!code-csharp[PortableClassLibraryMVVM#2](../../../samples/snippets/csharp/VS_Snippets_CLR/portableclasslibrarymvvm/cs/customerrepository.cs#2)]
 [!code-vb[PortableClassLibraryMVVM#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/portableclasslibrarymvvm/vb/customerrepository.vb#2)]

### <a name="view-model"></a>视图模型
 在实现 MVVM 模式时，经常添加的视图模型的基类。 下面的示例显示了一个基类。

 [!code-csharp[PortableClassLibraryMVVM#3](../../../samples/snippets/csharp/VS_Snippets_CLR/portableclasslibrarymvvm/cs/viewmodelbase.cs#3)]
 [!code-vb[PortableClassLibraryMVVM#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/portableclasslibrarymvvm/vb/viewmodelbase.vb#3)]

 实现<xref:System.Windows.Input.ICommand>接口经常采用 MVVM 模式。 下面的示例演示 <xref:System.Windows.Input.ICommand> 接口的实现。

 [!code-csharp[PortableClassLibraryMVVM#4](../../../samples/snippets/csharp/VS_Snippets_CLR/portableclasslibrarymvvm/cs/relaycommand.cs#4)]
 [!code-vb[PortableClassLibraryMVVM#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/portableclasslibrarymvvm/vb/relaycommand.vb#4)]

 下面的示例显示了一个简化的视图模型。

 [!code-csharp[PortableClassLibraryMVVM#5](../../../samples/snippets/csharp/VS_Snippets_CLR/portableclasslibrarymvvm/cs/mainpageviewmodel.cs#5)]
 [!code-vb[PortableClassLibraryMVVM#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/portableclasslibrarymvvm/vb/customerviewmodel.vb#5)]  
  
### <a name="view"></a>视图  
 从[!INCLUDE[net_v45](../../../includes/net-v45-md.md)]应用程序中，[!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]应用、 基于 Silverlight 的应用或 Windows Phone 7.5 应用程序，可以引用包含模型和视图模型项目的程序集。  您然后创建视图模型进行交互的视图。 下面的示例演示一个简化的 Windows Presentation Foundation (WPF) 应用检索和更新视图模型中的数据。 可以在 Silverlight 中，Windows Phone 创建类似的视图或[!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]应用。  
  
 [!code-xaml[PortableClassLibraryMVVM#6](../../../samples/snippets/csharp/VS_Snippets_CLR/portableclasslibrarymvvm/cs/mainwindow.xaml#6)]  
  
## <a name="see-also"></a>请参阅

- [可移植类库](../../../docs/standard/cross-platform/cross-platform-development-with-the-portable-class-library.md)
