---
title: ICorDebugThread::GetCurrentException 方法
ms.date: 03/30/2017
api_name:
- ICorDebugThread.GetCurrentException
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread::GetCurrentException
helpviewer_keywords:
- ICorDebugThread::GetCurrentException method [.NET Framework debugging]
- GetCurrentException method [.NET Framework debugging]
ms.assetid: 331ed465-a195-4359-8584-b82c6098b29b
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c4baa4eb4da48b923ab0137ca25d9d819c94e33d
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57487338"
---
# <a name="icordebugthreadgetcurrentexception-method"></a>ICorDebugThread::GetCurrentException 方法
获取表示当前由托管代码引发的异常的 ICorDebugValue 对象的接口指针。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT GetCurrentException (  
    [out] ICorDebugValue **ppExceptionObject  
);  
```  
  
## <a name="parameters"></a>参数  
 `ppExceptionObject`  
 [out]指向的地址的指针`ICorDebugValue`对象，表示当前由引发的异常的托管代码。  
  
## <a name="remarks"></a>备注  
 从异常到结束的时间将存在的异常对象`catch`块。 函数求值，由 ICorDebugEval 方法执行，则将清除异常对象上设置，并在完成还原。  
  
 可以嵌套异常，（例如，如果筛选器中或在函数求值，将引发异常），因此可能在单个线程上的多个未处理异常。 `GetCurrentException` 返回的最新的异常。  
  
 异常对象和类型可能会更改整个生命周期中的异常。 例如，将引发异常的类型为 x 后，公共语言运行时 (CLR) 可能导致内存不足，并将其升级到内存不足异常。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
