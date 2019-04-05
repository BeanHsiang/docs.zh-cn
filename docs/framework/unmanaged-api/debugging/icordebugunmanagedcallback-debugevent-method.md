---
title: ICorDebugUnmanagedCallback::DebugEvent 方法
ms.date: 03/30/2017
api_name:
- ICorDebugUnmanagedCallback.DebugEvent
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugUnmanagedCallback::DebugEvent
helpviewer_keywords:
- DebugEvent method [.NET Framework debugging]
- ICorDebugUnmanagedCallback::DebugEvent method [.NET Framework debugging]
ms.assetid: be9cab04-65ec-44d5-a39a-f90709fdd043
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: beb2b9f17696e293d14cf997ef69deb7557ed0bb
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57479237"
---
# <a name="icordebugunmanagedcallbackdebugevent-method"></a>ICorDebugUnmanagedCallback::DebugEvent 方法
通知调试器已触发本机事件。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT DebugEvent (  
    [in] LPDEBUG_EVENT  pDebugEvent,  
    [in] BOOL           fOutOfBand  
);  
```  
  
## <a name="parameters"></a>参数  
 `pDebugEvent`  
 [in]指向本机事件的指针。  
  
 `fOutOfBand`  
 [in]`true`，如果与托管的进程状态的交互是不可能的非托管的事件发生，直到该调试器将调用后[icordebugcontroller:: Continue](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-continue-method.md); 否则为`false`。  
  
## <a name="remarks"></a>备注  
 如果正在调试的线程是 Win32 线程，则不要使用调试接口的 Win32 任何成员。 您可以调用`ICorDebugController::Continue`仅在 Win32 线程上且仅当过去的带事件继续执行。  
  
 `DebugEvent`回调不遵循标准规则进行回调。 当您调用`DebugEvent`，过程将在原始操作系统调试停止状态。 该过程将不会同步。 它会自动进入同步的状态时需满足的托管代码，这可能会导致其他嵌套有关的信息的请求`DebugEvent`回调。  
  
 调用[icordebugprocess:: Clearcurrentexception](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess-clearcurrentexception-method.md)的过程将继续过程之前忽略异常事件。 调用此方法将工作表上继续请求，而不是 DBG_EXCEPTION_NOT_HANDLED DBG_CONTINUE 和带的断点和单步异常，会自动清除。 即使正在调试的应用程序看上去已停止和未完成的带内事件已存在时，可以在任何时候，来自带外事件。  
  
 在.NET Framework 2.0 版中，调试程序应立即继续通过带外断点事件。 应使用调试器[ICorDebugProcess2::SetUnmanagedBreakpoint](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess2-setunmanagedbreakpoint-method.md)并[ICorDebugProcess2::ClearUnmanagedBreakpoint](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess2-clearunmanagedbreakpoint-method.md)方法来添加和删除断点。 这些方法将自动跳过任何带的断点。 因此，调度仅带外断点应已在指令流，如调用 Win32 中的原始断点`DebugBreak`函数。 不要尝试使用`ICorDebugProcess::ClearCurrentException`， [icordebugprocess:: Getthreadcontext](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess-getthreadcontext-method.md)， [icordebugprocess:: Setthreadcontext](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess-setthreadcontext-method.md)，或任何其他成员[调试 API](../../../../docs/framework/unmanaged-api/debugging/index.md)。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [ICorDebugUnmanagedCallback 接口](../../../../docs/framework/unmanaged-api/debugging/icordebugunmanagedcallback-interface.md)
