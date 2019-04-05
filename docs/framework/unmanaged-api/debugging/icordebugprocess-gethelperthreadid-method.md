---
title: ICorDebugProcess::GetHelperThreadID 方法
ms.date: 03/30/2017
api_name:
- ICorDebugProcess.GetHelperThreadID
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess::GetHelperThreadID
helpviewer_keywords:
- GetHelperThreadID method [.NET Framework debugging]
- ICorDebugProcess::GetHelperThreadID method [.NET Framework debugging]
ms.assetid: 84e1e605-37c1-49a5-8e12-35db85654622
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: cd5e30d08e667dcd5a8be1f9502462f28290068e
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57494215"
---
# <a name="icordebugprocessgethelperthreadid-method"></a>ICorDebugProcess::GetHelperThreadID 方法
获取调试器的内部帮助器线程的操作系统 (OS) 线程 ID。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT GetHelperThreadID (  
    [out] DWORD *pThreadID  
);  
```  
  
## <a name="parameters"></a>参数  
 `pThreadID`  
 [out]指向操作系统线程的调试器的内部帮助器线程的 ID。  
  
## <a name="remarks"></a>备注  
 托管和非托管在调试期间，它是调试器的有责任确保具有指定 ID 的线程保持运行，如果它遇到由调试器放置一个断点。 调试器还可能想要隐藏此线程在用户。 如果没有帮助器线程在过程中，存在`GetHelperThreadID`方法将返回 0 中的 *`pThreadID`。  
  
 您不能缓存帮助程序线程的线程 ID，因为它可能会随着时间的推移进行更改。 您必须重新查询每次停止事件的线程 ID。  
  
 调试器的帮助器线程的线程 ID 将是正确的每个非托管[icordebugmanagedcallback:: Createthread](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-createthread-method.md)事件，从而允许调试器来确定其帮助器线程的线程 ID 并将其隐藏从用户。 在非托管过程标识为帮助器线程的线程`ICorDebugManagedCallback::CreateThread`事件将不会运行托管的用户代码。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl。 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
