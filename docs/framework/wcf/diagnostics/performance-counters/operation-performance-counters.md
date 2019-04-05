---
title: 操作性能计数器
ms.date: 03/30/2017
ms.assetid: 333a51e0-f56e-4e1a-b359-5c91ff390568
ms.openlocfilehash: 16608132c6557f8612d42402a2cb2c49fcc29637
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54566081"
---
# <a name="operation-performance-counters"></a>操作性能计数器
使用性能监视器 (Perfmon.exe) 查看时，可以在 `ServiceModelOperation 4.0.0.0` 性能对象下找到操作性能计数器。 每个操作都有一个单独的实例。 也就是说，如果给定的协定具有 10 个操作，则有 10 个操作计数器实例与该协定相关联。 对象实例按下面的模式命名：  
  
```  
(ServiceName).(ContractName).(OperationName)@(first endpoint listener address)  
```  
  
 使用此计数器可以衡量调用的使用方式以及操作的执行情况。  
  
> [!CAUTION]
>  性能计数器实例的名称长度存在限制。 当 Windows Communication Foundation (WCF) 计数器实例名称超出了最大长度时，WCF 会将实例名称的一部分替换为哈希值。  
  
## <a name="see-also"></a>请参阅
- [性能计数器](../../../../../docs/framework/wcf/diagnostics/performance-counters/index.md)
