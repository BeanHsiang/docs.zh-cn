---
title: End <keyword> 语句 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.EndDefinition
helpviewer_keywords:
- End keyword [Visual Basic]
ms.assetid: 42d6e088-ab0f-4cda-88e8-fdce3e5fcf4f
ms.openlocfilehash: 96dc8ce6b0d3b7545f5caeef43358936e426f566
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55273525"
---
# <a name="end-keyword-statement-visual-basic"></a>结束\<关键字 > 语句 (Visual Basic)

在后面带有其他关键字，终止由该关键字引入的语句块的定义。

## <a name="syntax"></a>语法

```vb
End AddHandler
End Class
End Enum
End Event
End Function
End Get
End If
End Interface
End Module
End Namespace
End Operator
End Property
End RaiseEvent  
End RemoveHandler  
End Select
End Set
End Structure
End Sub
End SyncLock
End Try
End While
End With  
```  
  
## <a name="parts"></a>部件

|部件|描述|
|---|---|
|`End`|必需。 终止编程元素的定义。|
|`AddHandler`|必选`AddHandler`访问器是匹配的开始`AddHandler`语句在自定义[Event 语句](event-statement.md)。|
|`Class`|类定义开始是匹配的必选[Class 语句](class-statement.md)。|
|`Enum`|枚举定义开始是匹配的必选[Enum 语句](enum-statement.md)。|
|`Event`|必选`Custom`是匹配的开始事件定义[Event 语句](event-statement.md)。|  
|`Function`|必选`Function`过程定义是匹配的开始[Function 语句](function-statement.md)。 如果执行时遇到`End Function`语句，控件返回到调用代码。|
|`Get`|必选`Property`过程定义是匹配的开始[Get 语句](get-statement.md)。 如果执行时遇到`End Get`语句，控件返回到请求的属性值的语句。|
|`If`|必选`If`...`Then`...`Else`块定义是匹配的开始`If`语句。 请参阅[如果...然后...Else 语句](if-then-else-statement.md)。|
|`Interface`|终止开始是匹配的接口定义所需[Interface 语句](interface-statement.md)。|
|`Module`|模块定义开始是匹配的必选[Module 语句](module-statement.md)。|
|`Namespace`|必选命名空间定义是匹配的开始[Namespace 语句](namespace-statement.md)。|
|`Operator`|运算符定义开始是匹配的必选[Operator Statement](operator-statement.md)。|
|`Property`|必选属性定义是匹配的开始[Property Statement](property-statement.md)。|
|`RaiseEvent`|必选`RaiseEvent`访问器是匹配的开始`RaiseEvent`语句在自定义[Event 语句](event-statement.md)。|
|`RemoveHandler`|必选`RemoveHandler`访问器是匹配的开始`RemoveHandler`语句在自定义[Event 语句](event-statement.md)。|
|`Select`|必选`Select`...`Case`块定义是匹配的开始`Select`语句。 请参阅[选择...Case 语句](select-case-statement.md)。  
|`Set`|必选`Property`过程定义是匹配的开始[Set 语句](set-statement.md)。 如果执行时遇到`End Set`语句，控件返回到设置属性的值的语句。  
|`Structure`|终止是匹配的开始的结构定义所需[Structure 语句](structure-statement.md)。  
|`Sub`|必选`Sub`过程定义是匹配的开始[Sub 语句](sub-statement.md)。 如果执行时遇到`End Sub`语句，控件返回到调用代码。  
|`SyncLock`|必选`SyncLock`块定义是匹配的开始`SyncLock`语句。 请参阅[SyncLock 语句](synclock-statement.md)。  
|`Try`|必选`Try`...`Catch`...`Finally`块定义是匹配的开始`Try`语句。 请参阅[尝试...Catch...Finally 语句](try-catch-finally-statement.md)。  
|`While`|必选`While`循环是匹配的开始定义`While`语句。 请参阅[时...While 语句结束](while-end-while-statement.md)。  
|`With`| 必选`With`块定义是匹配的开始`With`语句。 请参阅[使用...使用语句结束](with-end-with-statement.md)。  
|||
  
## <a name="directives"></a>指令

时前面加一个数字符号 (`#`)，则`End`关键字终止由相应的指令引入的预处理块。  

```vb
#End ExternalSource
#End If
#End Region
```

|部件|描述|
|---|---|
|`#End`|必需。 终止预处理块的定义。|
|`ExternalSource`|必选开始是匹配的一个外部源块[#ExternalSource 指令](../directives/externalsource-directive.md)。|
|`If`|终止条件编译块开始是匹配的所需`#If`指令。 请参阅[#If......#Else 指令](../directives/if-then-else-directives.md)。|
|`Region`|必选开始是匹配的源区域块[#Region 指令](../directives/region-directive.md)。|
|||

## <a name="remarks"></a>备注

[End 语句](end-statement.md)，而无需其他的关键字，将立即终止执行。

## <a name="smart-device-developer-notes"></a>智能设备开发人员说明  

`End`不支持语句，而无需其他关键字。  
  
## <a name="see-also"></a>请参阅

- [End 语句](end-statement.md)
