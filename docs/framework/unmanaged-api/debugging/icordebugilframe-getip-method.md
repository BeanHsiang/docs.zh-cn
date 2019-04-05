---
title: ICorDebugILFrame::GetIP 方法
ms.date: 03/30/2017
api_name:
- ICorDebugILFrame.GetIP
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugILFrame::GetIP
helpviewer_keywords:
- GetIP method, ICorDebugILFrame interface [.NET Framework debugging]
- ICorDebugILFrame::GetIP method [.NET Framework debugging]
ms.assetid: 18217ba1-1776-4297-a3b9-f77e64b0fead
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7a7b8985e7580282d0e38205f9b1d6078f86cee6
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57479761"
---
# <a name="icordebugilframegetip-method"></a>ICorDebugILFrame::GetIP 方法
获取指令指针的值和一个说明如何获取指令指针的值的按位组合值。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT GetIP (  
    [out] ULONG32               *pnOffset,   
    [out] CorDebugMappingResult *pMappingResult  
);  
```  
  
## <a name="parameters"></a>参数  
 `pnOffset`  
 [out]指令指针的值。  
  
 `pMappingResult`  
 [out]指向介绍如何获取指令指针的值的 CorDebugMappingResult 枚举值的按位组合的指针。  
  
## <a name="remarks"></a>备注  
 指令指针的值是函数的 Microsoft 中间语言 (MSIL) 代码中的堆栈帧的偏移量位置。 如果堆栈帧处于活动状态，此地址将是下一步要执行的指令。 如果堆栈帧未处于活动状态，此地址是执行堆栈帧重新激活时的下一个指令。  
  
 如果此帧中实时 (JIT) 编译的帧，指令指针的值将确定通过向后将映射从实际的本机指令指针，因此该值可能只是近似。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
