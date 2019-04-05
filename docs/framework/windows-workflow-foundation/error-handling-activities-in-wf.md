---
title: WF 中的错误处理活动
ms.date: 03/30/2017
ms.assetid: 24b68bd3-cef5-4413-ab82-2e2625f209aa
ms.openlocfilehash: 410c481745cc62a55a2b6e840d82b01fcc7f5766
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57707672"
---
# <a name="error-handling-activities-in-wf"></a>WF 中的错误处理活动
[!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)]提供多个系统提供的活动，用于实现错误处理和恢复。 有关更多信息，请参见 [异常](exceptions.md)中定义的接口的私有 C++ 特定实现。  
  
## <a name="error-handling-activities"></a>错误处理活动  
  
|||  
|-|-|  
|<xref:System.Activities.Statements.Rethrow>|重新引发从 `TryCatch` 活动中引发的最后一个异常。|  
|<xref:System.Activities.Statements.Throw>|引发异常。|  
|<xref:System.Activities.Statements.TryCatch>|实现异常处理。|
