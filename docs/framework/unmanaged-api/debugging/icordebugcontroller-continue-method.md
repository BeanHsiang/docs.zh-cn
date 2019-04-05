---
title: ICorDebugController::Continue 方法
ms.date: 03/30/2017
api_name:
- ICorDebugController.Continue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugController::Continue
helpviewer_keywords:
- Continue method [.NET Framework debugging]
- ICorDebugController::Continue method [.NET Framework debugging]
ms.assetid: 8684cd06-ad3e-48ef-832e-15320e1f43a2
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 4f448a0383d3ad121cbddb59e13acef46a336261
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57485728"
---
# <a name="icordebugcontrollercontinue-method"></a>ICorDebugController::Continue 方法
恢复托管线程执行后调用[停止方法](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-stop-method.md)。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT Continue (  
    [in] BOOL fIsOutOfBand  
);  
```  
  
## <a name="parameters"></a>参数  
 `fIsOutOfBand`  
 [in]设置为`true`如果继续从带外事件; 否则设置为`false`。  
  
## <a name="remarks"></a>备注  
 `Continue` 在调用后继续执行过程`ICorDebugController::Stop`方法。  
  
 在进行混合模式调试时，不要调用`Continue`上 Win32 事件线程除非您要从带外事件继续执行。  
  
 *带内事件*托管的事件或正常非托管事件，在此期间，调试器支持与托管进程的状态的交互事件。 在这种情况下，调试器将接收[icordebugunmanagedcallback:: Debugevent](../../../../docs/framework/unmanaged-api/debugging/icordebugunmanagedcallback-debugevent-method.md)具有回调其`fOutOfBand`参数设置为`false`。  
  
 *的带事件*是在此期间与托管状态的进程的交互是不可能同时由于事件停止该进程的非托管的事件。 在这种情况下，调试器将接收`ICorDebugUnmanagedCallback::DebugEvent`具有回调其`fOutOfBand`参数设置为`true`。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅

