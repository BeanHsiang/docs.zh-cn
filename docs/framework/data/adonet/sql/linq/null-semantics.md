---
title: Null 语义
ms.date: 03/30/2017
ms.assetid: a97017ae-d634-4cf3-bbaf-054a528fd683
ms.openlocfilehash: 272c19d7ee64381baa93cb2eda1cc035c42a025d
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54689086"
---
# <a name="null-semantics"></a>Null 语义
下表提供了指向各个组成部分[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]文档位置`null`(`Nothing`在 Visual Basic 中) 的问题进行讨论。  
  
|主题|描述|  
|-----------|-----------------|  
|[SQL-CLR 类型不匹配](../../../../../../docs/framework/data/adonet/sql/linq/sql-clr-type-mismatches.md)|本主题的"Null 语义"部分包含的三态 SQL Boolean 与两态公共语言运行时 (CLR) 的讨论<xref:System.Boolean>，将文字`Nothing`(Visual Basic 中) 和`null`(C#)，以及其他类似问题。|  
|[标准查询运算符转换](../../../../../../docs/framework/data/adonet/sql/linq/standard-query-operator-translation.md)|本主题的“Null 语义”部分介绍 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]中的 null 比较语义。|  
|[System.String 方法](../../../../../../docs/framework/data/adonet/sql/linq/system-string-methods.md)|本主题的“与 .NET 的差异”部分说明从 <xref:System.String.LastIndexOf%2A> 返回 0 为何意味着字符串为 null 或找到的位置为 0。|  
|[计算数值序列中值的和](../../../../../../docs/framework/data/adonet/sql/linq/compute-the-sum-of-values-in-a-numeric-sequence.md)|介绍如何<xref:System.Linq.Enumerable.Sum%2A>运算符的计算结果为`null`(`Nothing`在 Visual Basic 中) 而不是 0 一个序列，其中只包含 null 或空序列。|  
  
## <a name="see-also"></a>请参阅
- [数据类型和函数](../../../../../../docs/framework/data/adonet/sql/linq/data-types-and-functions.md)
