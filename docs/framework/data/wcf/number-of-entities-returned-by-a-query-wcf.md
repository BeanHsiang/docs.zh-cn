---
title: 如何：确定由查询 （WCF 数据服务） 返回的实体数
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, row count
ms.assetid: 03d41a82-df95-40ac-8439-a6c327d37ba8
ms.openlocfilehash: cc4ada3dabe20927f4c3a27dbb0fda78e41452c9
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54683058"
---
# <a name="how-to-determine-the-number-of-entities-returned-by-a-query-wcf-data-services"></a>如何：确定由查询 （WCF 数据服务） 返回的实体数
通过 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]，您可以确定由查询 URI 指定的实体集中的实体数量。 此计数可以与查询结果包含在一起，也可为一个整数值。 有关详细信息，请参阅[查询数据服务](../../../../docs/framework/data/wcf/querying-the-data-service-wcf-data-services.md)。  
  
 本主题中的示例使用罗斯文示例数据服务和自动生成的客户端数据服务类。 完成后，将创建此服务和客户端数据类[WCF Data Services 快速入门](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)。  
  
## <a name="example"></a>示例  
 此示例在调用 <xref:System.Data.Services.Client.DataServiceQuery%601.IncludeTotalCount%2A> 方法之后执行查询。 <xref:System.Data.Services.Client.QueryOperationResponse%601.TotalCount%2A> 属性返回 `Customers` 实体集中实体的数量。  
  
 [!code-csharp[Astoria Northwind Client#CountAllCustomers](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#countallcustomers)]
 [!code-vb[Astoria Northwind Client#CountAllCustomers](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#countallcustomers)]  
  
## <a name="example"></a>示例  
 此示例调用 <xref:System.Linq.Enumerable.Count%2A> 方法以仅返回一个整数值，该整数值是 `Customers` 实体集中的实体数量。  
  
 [!code-csharp[Astoria Northwind Client#CountAllCustomersValueOnly](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#countallcustomersvalueonly)]
 [!code-vb[Astoria Northwind Client#CountAllCustomersValueOnly](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#countallcustomersvalueonly)]  
  
## <a name="see-also"></a>请参阅
- [查询数据服务](../../../../docs/framework/data/wcf/querying-the-data-service-wcf-data-services.md)
