---
title: 构建投影
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 745742df-0eda-479b-83f8-29bd8a80db96
ms.openlocfilehash: 9b32ee4c7745fda482561311dc116e0e38b49ab7
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54599148"
---
# <a name="formulate-projections"></a>构建投影
下面的示例演示如何`select`语句中的C#并`Select`可以与构建查询投影到其他功能结合使用 Visual Basic 中的语句。  
  
## <a name="example"></a>示例  
 下面的示例使用`Select`在 Visual Basic 中的子句 (`select`中的子句C#) 可返回的联系人姓名的序列`Customers`。  
  
 [!code-csharp[DLinqQueryExamples#57](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#57)]
 [!code-vb[DLinqQueryExamples#57](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#57)]  
  
## <a name="example"></a>示例  
 下面的示例使用`Select`在 Visual Basic 中的子句 (`select`中的子句C#) 和*匿名类型*返回一系列联系人姓名和电话号码组成`Customers`。  
  
 [!code-csharp[DLinqQueryExamples#58](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#58)]
 [!code-vb[DLinqQueryExamples#58](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#58)]  
  
## <a name="example"></a>示例  
 下面的示例使用`Select`在 Visual Basic 中的子句 (`select`中的子句C#) 和*匿名类型*返回一系列名称和电话号码组成的员工。 在产生的序列中，`FirstName` 和 `LastName` 字段组合成单个字段 (`Name`)，`HomePhone` 字段重命名为 `Phone`。  
  
 [!code-csharp[DLinqQueryExamples#59](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#59)]
 [!code-vb[DLinqQueryExamples#59](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#59)]  
  
## <a name="example"></a>示例  
 下面的示例使用`Select`在 Visual Basic 中的子句 (`select`中的子句C#) 和*匿名类型*返回的所有序列`ProductID`s 和一个名为的计算的值`HalfPrice`。 此值设置为 `UnitPrice` 的 1/2。  
  
 [!code-csharp[DLinqQueryExamples#60](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#60)]
 [!code-vb[DLinqQueryExamples#60](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#60)]  
  
## <a name="example"></a>示例  
 下面的示例使用`Select`在 Visual Basic 中的子句 (`select`中的子句C#) 和一个*条件语句*返回一系列产品名称和产品可用性。  
  
 [!code-csharp[DLinqQueryExamples#61](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#61)]
 [!code-vb[DLinqQueryExamples#61](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#61)]  
  
## <a name="example"></a>示例  
 下面的示例使用 Visual Basic`Select`子句 (`select`中的子句C#) 和一个*已知类型*(Name) 返回由雇员的姓名组成的序列。  
  
 [!code-csharp[DLinqQueryExamples#62](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#62)]
 [!code-vb[DLinqQueryExamples#62](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#62)]  
  
## <a name="example"></a>示例  
 下面的示例使用`Select`和`Where`在 Visual Basic 中 (`select`并`where`在C#) 以返回*筛选序列*的位于伦敦的客户的联系人姓名。  
  
 [!code-csharp[DLinqQueryExamples#63](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#63)]
 [!code-vb[DLinqQueryExamples#63](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#63)]  
  
## <a name="example"></a>示例  
 下面的示例使用`Select`在 Visual Basic 中的子句 (`select`中的子句C#) 和*匿名类型*返回*成形子集*有关客户数据。  
  
 [!code-csharp[DLinqQueryExamples#64](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#64)]
 [!code-vb[DLinqQueryExamples#64](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#64)]  
  
## <a name="example"></a>示例  
 下面的示例使用嵌套查询返回以下结果：  
  
-   由所有订单及其对应的 `OrderID` 组成的序列。  
  
-   由订单中具有折扣的项组成的子序列。  
  
-   不含运费时节省的资金数额。  
  
 [!code-csharp[DLinqQueryExamples#65](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#65)]
 [!code-vb[DLinqQueryExamples#65](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#65)]  
  
## <a name="see-also"></a>请参阅
- [查询示例](../../../../../../docs/framework/data/adonet/sql/linq/query-examples.md)
