---
title: EClrOperation 枚举
ms.date: 03/30/2017
api_name:
- EClrOperation
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- EClrOperation
helpviewer_keywords:
- EClrOperation enumeration [.NET Framework hosting]
ms.assetid: 5aef6808-5aac-4b2f-a2c7-fee1575c55ed
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6244f01a78f08da839b233c3313f2fd6bff44b12
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54675066"
---
# <a name="eclroperation-enumeration"></a>EClrOperation 枚举
介绍的一组操作主机可以为其应用策略的操作。  
  
## <a name="syntax"></a>语法  
  
```  
typedef enum {  
    OPR_ThreadAbort,  
    OPR_ThreadRudeAbortInNonCriticalRegion,  
    OPR_ThreadRudeAbortInCriticalRegion,  
    OPR_AppDomainUnload,  
    OPR_AppDomainRudeUnload,  
    OPR_ProcessExit,  
    OPR_FinalizerRun  
} EClrOperation;  
```  
  
## <a name="members"></a>成员  
  
|成员|描述|  
|------------|-----------------|  
|`OPR_AppDomainRudeUnload`|主机可以指定策略操作时所要采取<xref:System.AppDomain>卸载非正常 （强制） 的方式。|  
|`OPR_AppDomainUnload`|主机可以指定策略操作时所要采取<xref:System.AppDomain>卸载。|  
|`OPR_FinalizerRun`|主机可以指定要执行终结器运行时策略操作。|  
|`OPR_ProcessExit`|主机可以指定在进程退出时要执行的策略操作。|  
|`OPR_ThreadAbort`|主机可以指定当线程被中止时要采取的策略操作。|  
|`OPR_ThreadRudeAbortInCriticalRegion`|主机可以指定策略强制中止线程代码的关键区域中发生时所采取的操作。|  
|`OPR_ThreadRudeAbortInNonCriticalRegion`|主机可以指定强制中止线程发生在非关键代码区域中时所采取的策略操作。|  
  
## <a name="remarks"></a>备注  
 公共语言运行时 (CLR) 可靠性基础结构可区分中止和资源的代码和非关键的代码区域中发生的关键区域中发生的分配失败。 这一区别旨在允许设置不同的策略，具体取决于代码中发生故障的主机。  
  
 一个*的代码的关键区域*是任何区域，CLR 不能保证该中止任务或无法完成请求的资源将会影响当前的任务。 例如，如果任务持有的锁，并且收到一个 HRESULT，指示在使内存分配请求时失败，其不足，只是无法中止该任务以确保的稳定性<xref:System.AppDomain>，这是因为<xref:System.AppDomain>可能包含其他为同一个锁等待的任务。 若要放弃了当前任务可能会导致其他任务停止响应 （或挂起） 无限期。 在这种情况下，宿主需要能够卸载整个<xref:System.AppDomain>而不是风险潜在的不稳定性。  
  
 一个*的代码的非关键区域*后，就是，CLR 可以保证以中止或失败，会影响仅在其出错的任务的区域。  
  
 CLR 还可区分中止正常和不正常 （强制） 中止。 一般情况下，正常中止会竭尽全力中止任务，而强制中止则没有此类保证之前运行异常处理例程和终结器。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** MSCorEE.h  
  
 **库：** MSCorEE.dll  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [EClrFailure 枚举](../../../../docs/framework/unmanaged-api/hosting/eclrfailure-enumeration.md)
- [EPolicyAction 枚举](../../../../docs/framework/unmanaged-api/hosting/epolicyaction-enumeration.md)
- [ICLRPolicyManager 接口](../../../../docs/framework/unmanaged-api/hosting/iclrpolicymanager-interface.md)
- [IHostPolicyManager 接口](../../../../docs/framework/unmanaged-api/hosting/ihostpolicymanager-interface.md)
- [承载枚举](../../../../docs/framework/unmanaged-api/hosting/hosting-enumerations.md)
