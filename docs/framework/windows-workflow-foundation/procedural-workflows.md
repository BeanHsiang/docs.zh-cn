---
title: 程序工作流
ms.date: 03/30/2017
ms.assetid: 52401de9-9115-472d-8fd9-047af6a072b9
ms.openlocfilehash: fcf50296a8ce3e7e2e0631057467af8a8efd9215
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57715706"
---
# <a name="procedural-workflows"></a>程序工作流
程序工作流使用的流控制方法与程序语言中使用的流控制方法类似。 这些构造包括 `While` 和 `If`。 使用 <xref:System.Activities.Statements.Flowchart> 和 <xref:System.Activities.Statements.Sequence> 等其他流控制活动，可以随意组合这些工作流。  
  
## <a name="controlling-execution-flow"></a>控制执行流  
 工作流活动库包含的活动可用于对程序语言中使用的大多数流控制方法进行建模， 这些问题包括：  
  
-   <xref:System.Activities.Statements.While>  
  
-   <xref:System.Activities.Statements.DoWhile>  
  
-   <xref:System.Activities.Statements.ForEach%601>  
  
-   <xref:System.Activities.Statements.Parallel>  
  
-   <xref:System.Activities.Statements.ParallelForEach%601>  
  
-   <xref:System.Activities.Statements.If>  
  
-   <xref:System.Activities.Statements.Switch%601>  
  
-   <xref:System.Activities.Statements.Pick>  
  
 若要使用流控制活动，拖放它们从**活动**组成一个复合活动设计器窗口中的工具箱。  
  
> [!NOTE]
>  如果使用 [!INCLUDE[dublin](../../../includes/dublin-md.md)] 在网络场上承载工作流，则 AppFabric 将在不同 AppFabric 服务器之间移动实例。 这就需要资源在所有节点之间可以共享。  默认 NET 4 工作流活动不包含访问本地资源的任何操作。 由于 AppFabric 没有提供将工作流标记为可移动的机制，所以开发人员不能在移动工作流时创建自定义活动。  
  
## <a name="see-also"></a>请参阅
- [流程图工作流](flowchart-workflows.md)
