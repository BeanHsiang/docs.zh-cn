---
title: SyncLock 语句 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.SyncLock
- SyncLock
helpviewer_keywords:
- threading [Visual Basic], locks
- SyncLock statement [Visual Basic]
- locks, threads
ms.assetid: 14501703-298f-4d43-b139-c4b6366af176
ms.openlocfilehash: 3a12c3ac7250ee2904d571406d5008d451c9dc35
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56979809"
---
# <a name="synclock-statement"></a>SyncLock 语句
执行块之前获取语句块的排他的锁。  
  
## <a name="syntax"></a>语法  
  
```  
SyncLock lockobject  
    [ block ]  
End SyncLock  
```  
  
## <a name="parts"></a>部件  
 `lockobject`  
 必需。 计算结果为一个对象引用的表达式。  
  
 `block`  
 可选。 要获取的锁时执行的语句块。  
  
 `End SyncLock`  
 终止`SyncLock`块。  
  
## <a name="remarks"></a>备注  
 `SyncLock`语句可确保多个线程不会在同一时间中执行的语句块。 `SyncLock` 阻止每个线程进入块，直到没有其他线程正在执行它。  
  
 最常用的`SyncLock`是由多个线程同时更新保护数据。 如果操作的数据的语句必须转到完成而不发生中断，则将它们放`SyncLock`块。  
  
 受保护的排他锁的语句块有时称为*临界区*。  
  
## <a name="rules"></a>规则  
  
-   分支。 不能分支到`SyncLock`阻止其块外部。  
  
-   锁定对象值。 值`lockobject`不能为`Nothing`。 必须先将其用于创建的锁对象`SyncLock`语句。  
  
     无法更改的值`lockobject`执行时`SyncLock`块。 该机制要求的锁对象保持不变。  
  
-   不能使用[Await](../../../visual-basic/language-reference/operators/await-operator.md)中的运算符`SyncLock`块。  
  
## <a name="behavior"></a>行为  
  
-   机制。 当一个线程到达`SyncLock`语句，它的计算结果`lockobject`表达式和挂起执行，直到它将获取由表达式返回的对象上的排他锁。 在另一个线程到达`SyncLock`语句，它并不获取锁直到第一个线程执行`End SyncLock`语句。  
  
-   受保护的数据。 如果`lockobject`是`Shared`变量，防止类的任何实例中的线程执行的排他锁`SyncLock`阻止其他线程执行时。 这将保护在所有实例间共享的数据。  
  
     如果`lockobject`是一个实例变量 (不`Shared`)，锁将阻止执行从当前实例中运行的线程`SyncLock`处的同一实例中的另一个线程在同一时间块。 这样可以保护单个实例保留的数据。  
  
-   获取和释放。 一个`SyncLock`块的行为类似于`Try...Finally`在其中构造`Try`块上获取排他锁`lockobject`和`Finally`块释放它。 正因为如此，`SyncLock`块都可确保释放锁，不管您如何退出块。 这是甚至在未处理的异常的情况下，则返回 true。  
  
-   框架将调用。 `SyncLock`块将获取并释放通过调用的排他锁`Enter`并`Exit`的方法`Monitor`类<xref:System.Threading>命名空间。  
  
## <a name="programming-practices"></a>编程做法  
 `lockobject`表达式应计算结果始终为以独占方式属于您的类的对象。 应声明`Private`对象变量来保护属于当前实例的数据或`Private Shared`对象变量来保护数据普遍适用于所有实例。  
  
 不应使用`Me`关键字提供锁定对象实例数据。 如果您的类的外部代码可以对您的类的实例的引用，它可以使用该引用的锁定对象作为`SyncLock`块完全不同，如果您保护不同的数据。 这样一来，您的类和其他类可能会互相阻塞执行其不相关`SyncLock`块。 因为使用相同的字符串的过程中的任何其他代码将共享同一个锁，同样锁定一个字符串，可能存在问题。  
  
 您也不应使用`Me.GetType`方法以提供锁定对象的共享数据。 这是因为`GetType`始终返回同一个`Type`给定的类名称的对象。 外部代码可以调用`GetType`在类上，并获取正在使用的同一个锁对象。 这将导致两个类相互阻止其`SyncLock`块。  
  
## <a name="examples"></a>示例  
  
### <a name="description"></a>描述  
 下面的示例显示了维护一个简单的消息列表的类。 它包含消息数组中而且上次使用的变量中的该数组的元素。 `addAnotherMessage`过程递增的最后一个元素，并将存储新消息。 这两项操作受`SyncLock`和`End SyncLock`语句，因为后递增的最后一个元素，任何其他线程可以再次增加的最后一个元素之前，必须将存储新消息。  
  
 如果`simpleMessageList`类共享其所有实例，这些变量之间的消息的一个列表`messagesList`并`messagesLast`将被声明为`Shared`。 在此情况下，变量`messagesLock`也应是`Shared`，以便将每个实例使用的单个锁对象。  
  
### <a name="code"></a>代码  
 [!code-vb[VbVbalrThreading#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrThreading/VB/Class1.vb#1)]  
  
### <a name="description"></a>描述  
 下面的示例使用线程和`SyncLock`。 只要`SyncLock`语句，语句块就是关键部分和`balance`永远不会是负数。 您可以注释掉`SyncLock`并`End SyncLock`语句，以查看影响省去`SyncLock`关键字。  
  
### <a name="code"></a>代码  
 [!code-vb[VbVbalrThreading#21](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrThreading/VB/class2.vb#21)]  
  
### <a name="comments"></a>注释  
  
## <a name="see-also"></a>请参阅

- <xref:System.Threading.Monitor?displayProperty=nameWithType>
- <xref:System.Threading.Interlocked?displayProperty=nameWithType>
- [同步基元概述](../../../standard/threading/overview-of-synchronization-primitives.md)
