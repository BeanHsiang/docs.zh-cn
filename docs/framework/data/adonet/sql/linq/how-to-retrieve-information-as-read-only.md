---
title: 如何：信息作为只读信息检索
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: fb09e298-0b53-47e5-97fb-ab318bcd4fad
ms.openlocfilehash: 8b83a77adb02cc2bcc01b274867143887114bb1f
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54669544"
---
# <a name="how-to-retrieve-information-as-read-only"></a>如何：信息作为只读信息检索
当您不打算更改数据时，您可以通过设法产生只读结果来提高查询性能。  
  
 通过将 <xref:System.Data.Linq.DataContext.ObjectTrackingEnabled%2A> 设置为 `false` 可实现只读处理。  
  
> [!NOTE]
>  当 <xref:System.Data.Linq.DataContext.ObjectTrackingEnabled%2A> 设置为 `false` 时，<xref:System.Data.Linq.DataContext.DeferredLoadingEnabled%2A> 将隐式设置为 `false`。  
  
## <a name="example"></a>示例  
 下面的代码检索雇员雇佣日期的只读集合。  
  
 [!code-csharp[DLinqQuerying#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQuerying/cs/Program.cs#2)]
 [!code-vb[DLinqQuerying#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQuerying/vb/Module1.vb#2)]  
  
## <a name="see-also"></a>请参阅
- [查询概念](../../../../../../docs/framework/data/adonet/sql/linq/query-concepts.md)
- [查询数据库](../../../../../../docs/framework/data/adonet/sql/linq/querying-the-database.md)
- [推迟加载与即时加载](../../../../../../docs/framework/data/adonet/sql/linq/deferred-versus-immediate-loading.md)
