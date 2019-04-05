---
title: 如何：在 XAML 中使用视图对数据进行排序和分组
ms.date: 03/30/2017
helpviewer_keywords:
- data binding [WPF], grouping data in views in XAML
- XAML [WPF], sorting data in views
- grouping data in views in XAML [WPF]
- data binding [WPF], sorting data in views in XAML
- sorting data in views in XAML [WPF]
- XAML [WPF], grouping data in views
- views [WPF], sorting data
- views [WPF], grouping data
ms.assetid: 145c8c3f-dbdd-4d0d-816f-90b35eba7eda
ms.openlocfilehash: 01cbd113502c3f953bd701930df6db090844fefa
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57351419"
---
# <a name="how-to-sort-and-group-data-using-a-view-in-xaml"></a>如何：在 XAML 中使用视图对数据进行排序和分组
此示例演示如何在[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]中创建数据集合的视图。 视图提供分组、排序、筛选功能和当前项的概念。  
  
## <a name="example"></a>示例  
 在下面的示例中，名为 *places* 的静态资源被定义为 *Place* 对象的集合，其中每个 *Place* 对象包含城市名和州。 前缀 *src* 映射到定义 *Places* 数据源的命名空间。 前缀 *scm* 映射到`"clr-namespace:System.ComponentModel;assembly=WindowsBase"`，*dat* 映射到`"clr-namespace:System.Windows.Data;assembly=PresentationFramework"`。  
  
 下面的示例创建数据集合的视图，数据按城市名称排序，并按州分组。  
  
 [!code-xaml[CollectionViewSource#1](~/samples/snippets/csharp/VS_Snippets_Wpf/CollectionViewSource/CS/window1.xaml#1)]  
  
 然后，该视图可以是绑定源，如以下示例所示：  
  
 [!code-xaml[CollectionViewSource#2](~/samples/snippets/csharp/VS_Snippets_Wpf/CollectionViewSource/CS/window1.xaml#2)]  
  
 绑定到 <xref:System.Windows.Data.XmlDataProvider> 资源中定义的 XML 数据时，XML 名称前面要加上 @ 符号。  
  
 [!code-xaml[CollectionViewSource#XDPChunk](~/samples/snippets/csharp/VS_Snippets_Wpf/CollectionViewSource/CS/window1.xaml#xdpchunk)]  
  
 [!code-xaml[CollectionViewSource#Attribute](~/samples/snippets/csharp/VS_Snippets_Wpf/CollectionViewSource/CS/window1.xaml#attribute)]  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Data.CollectionViewSource>
- [获取数据集合的默认视图](how-to-get-the-default-view-of-a-data-collection.md)
- [数据绑定概述](data-binding-overview.md)
- [帮助主题](data-binding-how-to-topics.md)
