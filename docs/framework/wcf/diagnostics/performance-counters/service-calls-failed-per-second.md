---
title: 服务：Calls Failed Per Second（每秒失败的调用次数）
ms.date: 03/30/2017
ms.assetid: 5a2c7939-107d-4f0c-b43c-e02e079e8a9d
ms.openlocfilehash: a043cf30fa67707aca3edf50cf23372ade5e5a42
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54559887"
---
# <a name="service-calls-failed-per-second"></a>服务：Calls Failed Per Second（每秒失败的调用次数）
计数器名称：每秒失败的调用。  
  
## <a name="description"></a>描述  
 一秒钟内由此服务收到且具有未处理异常的调用次数。  
  
 此计数器为性能计数器类型[PERF_COUNTER_COUNTER](https://go.microsoft.com/fwlink/?LinkID=94649)，使用以下公式计算其值。  
  
 (N 1 - N 0 ) / ( (D 1 -D 0 ) / F)  
  
 在托管代码中，出现错误条件时引发异常。  
  
 在托管代码中，出现错误条件时引发异常。  
  
 此服务中每出现一个未处理异常，此计数器就会递增。  
  
## <a name="see-also"></a>请参阅
- [在协定和服务中指定并处理错误](../../../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md)
