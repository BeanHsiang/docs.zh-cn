---
title: ICorDebugThread::SetDebugState 方法
ms.date: 03/30/2017
api_name:
- ICorDebugThread.SetDebugState
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread::SetDebugState
helpviewer_keywords:
- ICorDebugThread::SetDebugState method [.NET Framework debugging]
- SetDebugState method [.NET Framework debugging]
ms.assetid: 6382bdf6-d488-4952-b653-cb09b6e1c6c2
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d29f5cefd22592fa8949ff5361109c09c0972b24
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57499688"
---
# <a name="icordebugthreadsetdebugstate-method"></a>ICorDebugThread::SetDebugState 方法
设置描述此 ICorDebugThread 的调试状态的标志。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT SetDebugState (  
    [in] CorDebugThreadState state  
);  
```  
  
## <a name="parameters"></a>参数  
 `state`  
 [in]CorDebugThreadState 枚举值，用于指定此线程调试状态的按位组合。  
  
## <a name="remarks"></a>备注  
 `SetDebugState` 设置线程的当前调试状态。 （"当前的调试状态"表示的调试状态进程是否要继续，不实际的当前状态。）为此标准的值是 THREAD_RUNNING。 仅在调试器可能会影响线程的调试状态。 调试状态执行上一次之间仍然存在，因此如果你想要保留多个通过 thread_suspend 继续一个线程，你可以设置一次和此后不需要担心。 挂起线程和继续执行该过程可能会导致死锁，但通常不大可能。 这是一种内部函数的质量的线程和进程，按设计。 调试程序可以以异步方式中断和恢复来打断死锁的线程。 如果线程的用户状态包括 USER_UNSAFE_POINT，线程可能会阻止垃圾回收 (GC)。 这意味着暂停的线程具有较高可能导致死锁。 这可能会影响的调试事件已排入队列。 因此，调试程序应漏整个事件队列 (通过调用[icordebugcontroller:: Hasqueuedcallbacks](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-hasqueuedcallbacks-method.md)) 挂起或恢复线程之前。 否则它可能会认为它已经具有挂起的线程上收到事件。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
