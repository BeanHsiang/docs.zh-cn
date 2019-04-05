---
title: DataView 性能
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 90820e49-9d46-41f6-9a3d-6c0741bbd8eb
ms.openlocfilehash: 1384103f6ca35bab02280e6019d717a5d2f333cc
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54684718"
---
# <a name="dataview-performance"></a>DataView 性能
本主题讨论使用 <xref:System.Data.DataView.Find%2A> 类的 <xref:System.Data.DataView.FindRows%2A> 和 <xref:System.Data.DataView> 方法并在 Web 应用程序中缓存 <xref:System.Data.DataView> 时所具有的性能优势。  
  
## <a name="find-and-findrows"></a>Find 和 FindRows  
 <xref:System.Data.DataView> 构造一个索引。 索引包含从表或视图中的一个或多个列生成的键。 这些键存储在结构中，这种结构可使 <xref:System.Data.DataView> 能够快速有效地查找行或与键值关联的行。 操作使用的索引，如筛选和排序，请参阅大大提高性能。 创建 <xref:System.Data.DataView> 及修改任何排序或筛选信息时，均会生成 <xref:System.Data.DataView> 的索引。 创建 <xref:System.Data.DataView> 然后设置排序或筛选信息会使索引生成至少两次：一次是在创建 <xref:System.Data.DataView> 时，另一次是在修改任何排序或筛选属性时。 有关筛选和排序的详细信息<xref:System.Data.DataView>，请参阅[使用 DataView 进行筛选](../../../../docs/framework/data/adonet/filtering-with-dataview-linq-to-dataset.md)并[使用 DataView 进行排序](../../../../docs/framework/data/adonet/sorting-with-dataview-linq-to-dataset.md)。  
  
 如果要返回特定数据查询的结果而不是提供数据子集的动态视图，则可以使用 <xref:System.Data.DataView.Find%2A> 的 <xref:System.Data.DataView.FindRows%2A> 或 <xref:System.Data.DataView> 方法，而不设置 <xref:System.Data.DataView.RowFilter%2A> 属性。 <xref:System.Data.DataView.RowFilter%2A> 属性最适合用于用绑定控件显示筛选结果的数据绑定应用程序。 设置 <xref:System.Data.DataView.RowFilter%2A> 属性会重新生成数据的索引，从而增加应用程序的系统开销并降低性能。 <xref:System.Data.DataView.Find%2A> 和 <xref:System.Data.DataView.FindRows%2A> 方法使用当前索引，而不要求重新生成索引。 如果只想调用 <xref:System.Data.DataView.Find%2A> 或 <xref:System.Data.DataView.FindRows%2A> 一次，则应使用现有的 <xref:System.Data.DataView>。 如果想要调用 <xref:System.Data.DataView.Find%2A> 或 <xref:System.Data.DataView.FindRows%2A> 多次，则应该创建一个新的 <xref:System.Data.DataView> 以便对想要搜索的列重新生成索引，然后调用 <xref:System.Data.DataView.Find%2A> 或 <xref:System.Data.DataView.FindRows%2A> 方法。 有关详细信息<xref:System.Data.DataView.Find%2A>并<xref:System.Data.DataView.FindRows%2A>方法，请参阅[查找行](../../../../docs/framework/data/adonet/dataset-datatable-dataview/finding-rows.md)。  
  
 下面的示例使用 <xref:System.Data.DataView.Find%2A> 方法来查找姓氏为“Zhu”的联系人。  
  
 [!code-csharp[DP DataView Samples#LDVFromQueryOrderByFind](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvfromqueryorderbyfind)]
 [!code-vb[DP DataView Samples#LDVFromQueryOrderByFind](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvfromqueryorderbyfind)]  
  
 下面的示例使用 <xref:System.Data.DataView.FindRows%2A> 方法来查找所有红颜色的产品。  
  
 [!code-csharp[DP DataView Samples#LDVFromQueryFindRows](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvfromqueryfindrows)]
 [!code-vb[DP DataView Samples#LDVFromQueryFindRows](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvfromqueryfindrows)]  
  
## <a name="aspnet"></a>ASP.NET  
 ASP.NET 具有一种缓存机制，允许您在内存中存储需要创建大量服务器资源的对象。 缓存这些类型的资源可以显著提高应用程序的性能。 缓存由 <xref:System.Web.Caching.Cache> 类实现，缓存实例专用于每个应用程序。 由于创建新的 <xref:System.Data.DataView> 对象需要大量资源，因此您可能希望在 Web 应用程序中使用此缓存功能，使得每次刷新网页时，不必重新生成 <xref:System.Data.DataView>。  
  
 在下面的示例中，对 <xref:System.Data.DataView> 进行缓存以便在刷新该页时不必对数据重新排序。  
  
```vb  
If (Cache("ordersView") = Nothing) Then  
  
Dim dataSet As New DataSet()  
  
   FillDataSet(dataSet)  
  
   Dim orders As DataTable = dataSet.Tables("SalesOrderHeader")  
  
   Dim query = _  
                    From order In orders.AsEnumerable() _  
                    Where order.Field(Of Boolean)("OnlineOrderFlag") = True _  
                    Order By order.Field(Of Decimal)("TotalDue") _  
                    Select order  
  
   Dim view As DataView = query.AsDataView()  
  
   Cache.Insert("ordersView", view)  
  
End If  
  
Dim ordersView = CType(Cache("ordersView"), DataView)  
  
GridView1.DataSource = ordersView  
GridView1.DataBind()  
```  
  
```csharp  
if (Cache["ordersView"] == null)  
{  
   // Fill the DataSet.                  
   DataSet dataSet = FillDataSet();  
  
   DataTable orders = dataSet.Tables["SalesOrderHeader"];  
  
   EnumerableRowCollection<DataRow> query =  
                        from order in orders.AsEnumerable()  
                        where order.Field<bool>("OnlineOrderFlag") == true  
                        orderby order.Field<decimal>("TotalDue")  
                        select order;  
  
   DataView view = query.AsDataView();  
   Cache.Insert("ordersView", view);  
}  
  
DataView ordersView = (DataView)Cache["ordersView"];  
  
GridView1.DataSource = ordersView;  
GridView1.DataBind();  
```  
  
## <a name="see-also"></a>请参阅
- [数据绑定和 LINQ to DataSet](../../../../docs/framework/data/adonet/data-binding-and-linq-to-dataset.md)
