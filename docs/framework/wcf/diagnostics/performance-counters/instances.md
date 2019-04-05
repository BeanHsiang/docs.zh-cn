---
title: 实例数
ms.date: 03/30/2017
ms.assetid: c8cf3460-0ca1-4411-8262-e9ecaf7f0a31
ms.openlocfilehash: 1b2801b5df3a5d2ca6d7fd03299ecdf4b7df426a
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54520253"
---
# <a name="instances"></a>实例数
计数器名称：实例。  
  
## <a name="description"></a>描述  
 服务当前包含的实例上下文的数量。  
  
 在大部分时间里，实例上下文的数量都等于实例数。 但是，下列方案例外。  
  
-   服务方法显式调用 <xref:System.ServiceModel.Dispatcher.IInstanceProvider.ReleaseInstance%2A> 方法。  
  
-   一个 <xref:System.ServiceModel.ReleaseInstanceMode> 被应用于一个 <xref:System.ServiceModel.OperationBehaviorAttribute> 实例。  
  
## <a name="see-also"></a>请参阅
- <xref:System.ServiceModel.OperationBehaviorAttribute>
