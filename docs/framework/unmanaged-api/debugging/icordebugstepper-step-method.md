---
title: ICorDebugStepper::Step 方法
ms.date: 03/30/2017
api_name:
- ICorDebugStepper.Step
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStepper::Step
helpviewer_keywords:
- Step method, ICorDebugStepper interface [.NET Framework debugging]
- ICorDebugStepper::Step method [.NET Framework debugging]
ms.assetid: 38c1940b-ada1-40ba-8295-4c0833744e1e
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 444390622ca68244661b91dc85814b05556b12a2
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57493019"
---
# <a name="icordebugstepperstep-method"></a>ICorDebugStepper::Step 方法
导致此单步执行其包含的线程，并 （可选） 到 ICorDebugStepper 继续单步执行通过该线程中调用的函数。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT Step (  
    [in] BOOL   bStepIn  
);  
```  
  
## <a name="parameters"></a>参数  
 `bStepIn`  
 [in]设置为`true`来单步执行的线程内调用的函数。 设置为`false`到逐过程执行函数。  
  
## <a name="remarks"></a>备注  
 步骤完成时公共语言运行时执行此单步调试器的帧中的下一步托管的指令。 如果`Step`是分档器上调用，这不是在托管代码中，该步骤完成后，将由线程执行的下一个托管的代码指令。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
