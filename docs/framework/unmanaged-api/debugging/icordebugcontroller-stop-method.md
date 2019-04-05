---
title: ICorDebugController::Stop 方法
ms.date: 03/30/2017
api_name:
- ICorDebugController.Stop
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugController::Stop
helpviewer_keywords:
- Stop method, ICorDebugController interface [.NET Framework debugging]
- ICorDebugController::Stop method [.NET Framework debugging]
ms.assetid: c34e79be-a7fb-479e-8dec-d126a4c330e5
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: fbe0459824499aba86c908012f038256f9923513
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57496674"
---
# <a name="icordebugcontrollerstop-method"></a>ICorDebugController::Stop 方法
执行所有线程上的进程中运行托管的代码的同时停止。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT Stop (  
    [in] DWORD dwTimeoutIgnored  
);  
```  
  
## <a name="parameters"></a>参数  
 `dwTimeoutIgnored`  
 未使用。  
  
## <a name="remarks"></a>备注  
 `Stop` 在进程中执行的同时停止对所有线程运行托管代码。 仅托管调试会话期间，非托管的线程可以继续运行 （但在尝试调用托管的代码时会被阻止）。 在互操作调试会话，非托管的线程也会停止。 `dwTimeoutIgnored`值当前被忽略，视为 INFINITE (-1)。 如果同时停止失败由于死锁，所有线程已都暂停，并返回 E_TIMEOUT。  
  
> [!NOTE]
>  `Stop` 是唯一的同步方法调试 API 中。 当`Stop`时返回 S_OK，该过程已停止。 不执行回调都在通知停止点的侦听器。 调试器必须调用[icordebugcontroller:: Continue](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-continue-method.md)以允许恢复的过程。  
  
 调试器会维护一个停止的计数器。 当计数器回到零时，控制器将继续运行。 每次调用`Stop`或每次调度的回调递增的计数器。 每次调用`ICorDebugController::Continue`递减该计数器。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅

