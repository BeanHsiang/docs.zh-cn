---
title: Aggregate 子句 (Visual Basic)
ms.date: 08/28/2018
f1_keywords:
- vb.QueryAggregateIn
- vb.QueryAggregate
- vb.QueryAggregateInto
helpviewer_keywords:
- Aggregate clause [Visual Basic]
- Aggregate statement [Visual Basic]
- queries [Visual Basic], Aggregate
ms.assetid: 1315a814-5db6-4077-b34b-b141e11cc0eb
ms.openlocfilehash: 21781db637c71abbbe9366bc95b6ee4c89ac2246
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56981954"
---
# <a name="aggregate-clause-visual-basic"></a>Aggregate 子句 (Visual Basic)
适用于集合的一个或多个聚合函数。  
  
## <a name="syntax"></a>语法  
  
```  
Aggregate element [As type] In collection _  
  [, element2 [As type2] In collection2, [...]]  
  [ clause ]  
  Into expressionList  
```  
  
## <a name="parts"></a>部件  
  
|术语|定义|  
|---|---|  
|`element`|必需。 用于循环访问集合的元素的变量。|  
|`type`|可选。 `element` 的类型。 如果指定没有类型，则类型`element`从推断`collection`。|  
|`collection`|必需。 表示要操作的集合。|  
|`clause`|可选。 一个或多个查询子句，如`Where`子句，以优化要向其应用聚合子句的查询结果。|  
|`expressionList`|必需。 一个或多个以逗号分隔的表达式用于标识要应用于集合的聚合函数。 您可以应用于聚合函数指定为查询结果的成员名称的别名。 如果不提供别名，则使用的聚合函数的名称。 有关示例，请参阅有关本主题后面的聚合函数的部分。|  
  
## <a name="remarks"></a>备注  
 `Aggregate`子句可用于在查询中包含聚合函数。 聚合函数对一组值执行检查和计算并返回单个值。 可以通过使用查询结果类型的成员访问计算的值。 可以使用标准聚合函数都`All`， `Any`， `Average`， `Count`， `LongCount`， `Max`， `Min`，和`Sum`函数。 这些函数是熟悉的开发人员熟悉的与 SQL 中的聚合函数。 它们是本主题的以下部分中所述。  
  
 聚合函数的结果作为查询结果类型的字段包含查询结果中。 你可以提供聚合函数结果，以指定将保存的聚合值的查询结果类型的成员名称的别名。 如果不提供别名，则使用的聚合函数的名称。  
  
 `Aggregate`子句可以开始查询，也可以是作为在查询中的其他子句。 如果`Aggregate`子句开始查询，则结果为单个值中指定的聚合函数的结果`Into`子句。 如果在中指定多个聚合函数`Into`子句，查询将返回单个类型使用单独的属性引用中每个聚合函数的结果`Into`子句。 如果`Aggregate`子句是作为在查询中的其他子句，查询集合中返回的类型都具有一个单独的属性来引用中每个聚合函数的结果`Into`子句。  
  
## <a name="aggregate-functions"></a>聚合函数

以下是可与标准聚合函数`Aggregate`子句。  
  
### <a name="all"></a>全部

返回`true`如果在集合中的所有元素都满足指定的条件; 否则，返回`false`。 下面是一个示例：

 [!code-vb[VbSimpleQuerySamples#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#5)]

### <a name="any"></a>任意

返回`true`如果在集合中的任何元素满足指定的条件; 否则，返回`false`。 下面是一个示例：

 [!code-vb[VbSimpleQuerySamples#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#6)]

### <a name="average"></a>平均值

集合中的所有元素的平均值或计算的集合中的所有元素提供的表达式。 下面是一个示例：

 [!code-vb[VbSimpleQuerySamples#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#7)]

### <a name="count"></a>计数

计算集合中的元素的数目。 您可以提供一个可选`Boolean`表达式来计算仅满足条件的集合中的元素数目。 下面是一个示例：

 [!code-vb[VbSimpleQuerySamples#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#8)]

### <a name="group"></a>Group

为分组的查询结果是指`Group By`或`Group Join`子句。 `Group`函数是仅在中有效`Into`子句`Group By`或`Group Join`子句。 有关详细信息和示例，请参阅[组 By 子句](../../../visual-basic/language-reference/queries/group-by-clause.md)并[Group Join 子句](../../../visual-basic/language-reference/queries/group-join-clause.md)。

### <a name="longcount"></a>LongCount

计算集合中的元素的数目。 您可以提供一个可选`Boolean`表达式来计算仅满足条件的集合中的元素数目。 返回的结果`Long`。 有关示例，请参阅`Count`聚合函数。

### <a name="max"></a>最大值

集合中的最大值或计算的集合中的所有元素提供的表达式。 下面是一个示例：

 [!code-vb[VbSimpleQuerySamples#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#9)]

### <a name="min"></a>最小值

集合中的最小值或计算的集合中的所有元素提供的表达式。 下面是一个示例：

 [!code-vb[VbSimpleQuerySamples#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#10)]

### <a name="sum"></a>Sum

集合中的所有元素的总和或计算的集合中的所有元素提供的表达式。 下面是一个示例：

 [!code-vb[VbSimpleQuerySamples#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#15)]

## <a name="example"></a>示例  

下面的示例演示如何使用`Aggregate`子句，以将聚合函数应用到查询结果。  
  
 [!code-vb[VbSimpleQuerySamples#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#4)]  
  
## <a name="creating-user-defined-aggregate-functions"></a>创建用户定义的聚合函数

 可以在查询表达式中包括你自己的自定义聚合函数，通过添加的扩展方法<xref:System.Collections.Generic.IEnumerable%601>类型。 计算或操作已引用聚合函数的可枚举集合，然后可以执行自定义方法。 有关扩展方法的详细信息，请参阅[扩展方法](../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md)。  
  
 例如，下面的示例演示计算一系列数字的中值的自定义聚合函数。 有两种重载的`Median`扩展方法。 第一个重载接受，作为输入，类型的集合`IEnumerable(Of Double)`。 如果`Median`聚合函数调用类型的查询字段`Double`，将调用此方法。 第二个重载`Median`方法可以传递任何泛型类型。 泛型重载`Median`方法采用一个引用的第二个参数`Func(Of T, Double)`lambda 表达式，以便为相应的值类型的项目类型 （从一个集合） 的值`Double`。 它然后委托到的其他重载的中值的计算`Median`方法。 有关 lambda 表达式的详细信息，请参阅 [Lambda 表达式](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)。  
  
 [!code-vb[VbSimpleQuerySamples#18](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/UserDefinedAggregates.vb#18)]  
  
 下面的示例演示调用的示例查询`Median`聚合函数类型的集合`Integer`，和类型的集合`Double`。 调用的查询`Median`聚合函数类型的集合`Double`调用的重载`Median`方法接受类型的集合作为输入， `Double`。 调用的查询`Median`聚合函数类型的集合`Integer`调用的泛型重载`Median`方法。  
  
 [!code-vb[VbSimpleQuerySamples#19](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/UserDefinedAggregates.vb#19)]  
  
## <a name="see-also"></a>请参阅

- [Visual Basic 中的 LINQ 简介](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)
- [查询](../../../visual-basic/language-reference/queries/index.md)
- [Select 子句](../../../visual-basic/language-reference/queries/select-clause.md)
- [From 子句](../../../visual-basic/language-reference/queries/from-clause.md)
- [Where 子句](../../../visual-basic/language-reference/queries/where-clause.md)
- [Group By 子句](../../../visual-basic/language-reference/queries/group-by-clause.md)
