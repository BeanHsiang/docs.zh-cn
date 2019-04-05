---
title: ICorDebugThread2::GetActiveFunctions 方法
ms.date: 03/30/2017
api_name:
- ICorDebugThread2.GetActiveFunctions
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread2::GetActiveFunctions
helpviewer_keywords:
- GetActiveFunctions method [.NET Framework debugging]
- ICorDebugThread2::GetActiveFunctions method [.NET Framework debugging]
ms.assetid: 27fae01a-ecec-423a-973e-24f8de55826c
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ed13f78d5a1f6d54b12c86613715f4878a521bfa
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57489925"
---
# <a name="icordebugthread2getactivefunctions-method"></a>ICorDebugThread2::GetActiveFunctions 方法
在每个此线程的帧中获取有关活动函数的信息。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT GetActiveFunctions (  
    [in]   ULONG32             cFunctions,  
    [out]  ULONG32             *pcFunctions,  
    [in, out, size_is(cFunctions), length_is(*pcFunctions)]  
        COR_ACTIVE_FUNCTION    pFunctions[]  
);  
```  
  
## <a name="parameters"></a>参数  
 `cFunctions`  
 [in] `pFunctions` 数组的大小。  
  
 `pcFunctions`  
 [out]指向中返回的对象数的`pFunctions`数组。 返回的对象数目将等于在堆栈上的托管帧数。  
  
 `pFunctions`  
 [in、 out]COR_ACTIVE_FUNCTION 对象数组，其中每个包含有关此线程的帧中的活动函数的信息。  
  
 第一个元素将用于叶帧，因此，在返回到堆栈的根。  
  
## <a name="remarks"></a>备注  
 如果`pFunctions`的输入，为 null`GetActiveFunctions`只返回数的函数的堆栈上。 也就是说，如果`pFunctions`的输入，为 null`GetActiveFunctions`返回的值仅在`pcFunctions`。  
  
 `GetActiveFunctions`方法旨在作为一种优化，通过从堆栈跟踪中的帧中获取相同信息并包括，则必须 ICorDebugILFrame 对象为其完整的堆栈跟踪中的帧。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
