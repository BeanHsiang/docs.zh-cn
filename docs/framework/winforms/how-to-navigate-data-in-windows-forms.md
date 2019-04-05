---
title: 如何：在 Windows 窗体中导航数据
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- cursors [Windows Forms], data sources
- data sources [Windows Forms], Windows Forms
- Windows Forms, navigating
- CurrencyManager class [Windows Forms], navigating Windows Forms data
- data [Windows Forms], navigating
ms.assetid: 97360f7b-b181-4084-966a-4c62518f735b
ms.openlocfilehash: 920f6d6206a8f33a912d8a7d1b46a3047ed874bc
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57725326"
---
# <a name="how-to-navigate-data-in-windows-forms"></a>如何：在 Windows 窗体中导航数据
在 Windows 应用程序中，浏览数据源中的记录的最简单方法是将绑定<xref:System.Windows.Forms.BindingSource>到数据源，然后将控件绑定到组件<xref:System.Windows.Forms.BindingSource>。 您然后可以使用内置的导航方法上<xref:System.Windows.Forms.BindingSource>此类<xref:System.Windows.Forms.BindingSource.MoveNext%2A>， <xref:System.Windows.Forms.BindingSource.MoveLast%2A>，<xref:System.Windows.Forms.BindingSource.MovePrevious%2A>和<xref:System.Windows.Forms.BindingSource.MoveFirst%2A>。 使用这些方法将调整<xref:System.Windows.Forms.BindingSource.Position%2A>并<xref:System.Windows.Forms.BindingSource.Current%2A>的属性<xref:System.Windows.Forms.BindingSource>适当。 此外可以查找某个项，并将其设置为当前项，通过设置<xref:System.Windows.Forms.BindingSource.Position%2A>属性。  
  
### <a name="to-increment-the-position-in-a-data-source"></a>要递增的数据源中的位置  
  
1.  设置<xref:System.Windows.Forms.BindingSource.Position%2A>属性的<xref:System.Windows.Forms.BindingSource>绑定到的记录的位置转到数据。 下面的示例演示如何使用<xref:System.Windows.Forms.BindingSource.MoveNext%2A>方法<xref:System.Windows.Forms.BindingSource>递增<xref:System.Windows.Forms.BindingSource.Position%2A>属性时`nextButton`单击。 <xref:System.Windows.Forms.BindingSource>与相关联`Customers`数据集的表`Northwind`。  
  
    > [!NOTE]
    >  设置<xref:System.Windows.Forms.BindingSource.Position%2A>属性的第一个或最后一个记录之外的值不会导致错误，作为[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]将不允许你将位置设置为列表的边界之外的值。 如果是十分重要的应用程序以了解是否已在第一个或最后一条记录，，包括逻辑来测试是否将超过数据元素计数。  
  
     [!code-csharp[System.Windows.Forms.NavigatingData#4](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.NavigatingData/CS/Form1.cs#4)]
     [!code-vb[System.Windows.Forms.NavigatingData#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.NavigatingData/VB/Form1.vb#4)]  
  
### <a name="to-check-whether-you-have-passed-the-end-or-beginning"></a>若要检查是否已通过的末尾或开头  
  
1.  为 <xref:System.Windows.Forms.BindingSource.PositionChanged> 事件创建一个事件处理程序。 在处理程序中，你可以测试是否提议的职位值已超出实际数据元素计数。  
  
     下面的示例说明了如何测试是否已到达最后一个数据元素。 在示例中，如果对象在最后一个元素，**下一步**窗体上的按钮处于禁用状态。  
  
    > [!NOTE]
    >  请注意，您应更改在代码中导航的列表，则应重新启用**下一步**按钮，以便用户可以浏览新列表的整个长度。 另外，请注意，上述<xref:System.Windows.Forms.BindingSource.PositionChanged>事件的特定<xref:System.Windows.Forms.BindingSource>你正在使用需要是其事件处理方法关联。 下面是用于处理方法的示例<xref:System.Windows.Forms.BindingSource.PositionChanged>事件：  
  
     [!code-csharp[System.Windows.Forms.NavigatingData#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.NavigatingData/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.NavigatingData#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.NavigatingData/VB/Form1.vb#3)]  
  
### <a name="to-find-an-item-and-set-it-as-the-current-item"></a>若要查找某个项并将其设置为当前项  
  
1.  查找你想要设置为当前项的记录。 你可以使用<xref:System.Windows.Forms.BindingSource.Find%2A>方法<xref:System.Windows.Forms.BindingSource>，如果你的数据源实现<xref:System.ComponentModel.IBindingList>。 一些示例数据源实现<xref:System.ComponentModel.IBindingList>都<xref:System.ComponentModel.BindingList%601>和<xref:System.Data.DataView>。  
  
     [!code-csharp[System.Windows.Forms.NavigatingData#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.NavigatingData/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.NavigatingData#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.NavigatingData/VB/Form1.vb#2)]  
  
## <a name="see-also"></a>请参阅
- [Windows 窗体支持的数据源](data-sources-supported-by-windows-forms.md)
- [Windows 窗体数据绑定中的更改通知](change-notification-in-windows-forms-data-binding.md)
- [数据绑定和 Windows 窗体](data-binding-and-windows-forms.md)
- [Windows 窗体数据绑定](windows-forms-data-binding.md)
