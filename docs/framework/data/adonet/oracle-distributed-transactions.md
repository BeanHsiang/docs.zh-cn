---
title: Oracle 分布式事务
ms.date: 03/30/2017
ms.assetid: c340ca81-ef79-402f-b204-c5156b890fe5
ms.openlocfilehash: 8e7530621254881402570b59b47a22052b40f2b5
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54713233"
---
# <a name="oracle-distributed-transactions"></a>Oracle 分布式事务
<xref:System.Data.OracleClient.OracleConnection> 对象自动在现有分布式事务中登记（如果确定某个事务是活动的）。 如果连接从连接池中打开或检索，将自动登记事务。 可以禁用现有事务中的自动登记，方法是将  
  
```  
Enlist=false  
```  
  
 指定为 <xref:System.Data.OracleClient.OracleConnection> 的连接字符串参数。  
  
## <a name="see-also"></a>请参阅
- [Oracle 和 ADO.NET](../../../../docs/framework/data/adonet/oracle-and-adonet.md)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
