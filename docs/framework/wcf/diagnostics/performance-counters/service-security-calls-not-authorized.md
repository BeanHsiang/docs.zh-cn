---
title: 服务：Security Calls Not Authorized（未授权的安全调用次数）
ms.date: 03/30/2017
ms.assetid: 3024b20a-5250-4bd1-a38c-c6d79f89610b
ms.openlocfilehash: a38b5e0eb467a5cad698fd6e3e01c0adef825d2f
ms.sourcegitcommit: db8b83057d052c1f9f249d128b08d4423af0f7c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/01/2018
ms.locfileid: "50757382"
---
# <a name="service-security-calls-not-authorized"></a>服务：Security Calls Not Authorized（未授权的安全调用次数）
计数器名称：Security Calls Not Authorized（未授权的安全调用次数）。  
  
## <a name="description"></a>描述  
 当 <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccess%2A> 方法返回 `false` 时，此计数器将递增。 它指示传入的消息来自有效的用户并得到了良好保护，但该用户没有获得执行特定任务的授权。
