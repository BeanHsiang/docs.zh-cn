---
title: EPolicyAction 枚举
ms.date: 03/30/2017
api_name:
- EPolicyAction
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- EPolicyAction
helpviewer_keywords:
- EPolicyAction enumeration [.NET Framework hosting]
ms.assetid: 72dd76ba-239e-45ac-9ded-318fb07d6c6d
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: aa8589b3f27ba97d32e77dbfecb190edc69dbc18
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2019
ms.locfileid: "57677326"
---
# <a name="epolicyaction-enumeration"></a>EPolicyAction 枚举
描述主机可以为通过所述的操作设置的策略操作[EClrOperation](../../../../docs/framework/unmanaged-api/hosting/eclroperation-enumeration.md)和所描述的失败[EClrFailure](../../../../docs/framework/unmanaged-api/hosting/eclrfailure-enumeration.md)。  
  
## <a name="syntax"></a>语法  
  
```  
typedef enum {  
    eNoAction,  
    eThrowException,  
    eAbortThread,  
    eRudeAbortThread,  
    eUnloadAppDomain,  
    eRudeUnloadAppDomain,  
    eExitProcess,  
    eFastExitProcess,  
    eRudeExitProcess,  
    eDisableRuntime  
} EPolicyAction;  
```  
  
## <a name="members"></a>成员  
  
|成员|描述|  
|------------|-----------------|  
|`eAbortThread`|指定公共语言运行时 (CLR) 应正常中止线程。 包括正常中止： 尝试运行所有`finally`阻止任何`catch`块与线程中止和终结器。|  
|`eDisableRuntime`|指定 CLR 应进入禁用的状态。 无需再在受影响的过程中，执行托管的代码和线程被阻止进入 CLR。|  
|`eExitProcess`|指定 CLR 应尝试的进程，包括运行终结器和执行清理和日志记录操作正常退出。|  
|`eFastExitProcess`|指定的 CLR 应立即退出进程，而无需运行终结器或执行清理和日志记录操作。 但是，将通知发送到调试器。|  
|`eNoAction`|指定应执行任何操作。|  
|`eRudeAbortThread`|指定 CLR 应执行强制中止线程。 只有那些`catch`并`finally`块标记为<xref:System.EnterpriseServices.MustRunInClientContextAttribute>执行。|  
|`eRudeExitProcess`|指定 CLR 应退出进程，而无需运行终结器或日志记录操作。|  
|`eRudeUnloadAppDomain`|指定 CLR 应执行的强制卸载<xref:System.AppDomain>。 唯一的终结器标记为<xref:System.EnterpriseServices.MustRunInClientContextAttribute>执行。 同样，所有线程与此<xref:System.AppDomain>其堆栈中接收`ThreadAbortException`，而只能`catch`并`finally`块标记为<xref:System.EnterpriseServices.MustRunInClientContextAttribute>执行。|  
|`eThrowException`|指定应引发异常的条件，例如内存不足，缓冲区溢出等，适合。|  
|`eUnloadAppDomain`|指定<xref:System.AppDomain>应卸载。 CLR 会试图运行终结器。|  
  
## <a name="remarks"></a>备注  
 主机设置的策略操作是通过调用的方法[ICLRPolicyManager](../../../../docs/framework/unmanaged-api/hosting/iclrpolicymanager-interface.md)接口。 有关原始和正常中止的信息，请参阅[EClrOperation](../../../../docs/framework/unmanaged-api/hosting/eclroperation-enumeration.md)枚举。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** MSCorEE.h  
  
 **库：** MSCorEE.dll  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [EClrFailure 枚举](../../../../docs/framework/unmanaged-api/hosting/eclrfailure-enumeration.md)
- [ICLRPolicyManager 接口](../../../../docs/framework/unmanaged-api/hosting/iclrpolicymanager-interface.md)
- [IHostPolicyManager 接口](../../../../docs/framework/unmanaged-api/hosting/ihostpolicymanager-interface.md)
- [承载枚举](../../../../docs/framework/unmanaged-api/hosting/hosting-enumerations.md)
