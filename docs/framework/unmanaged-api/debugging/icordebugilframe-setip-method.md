---
title: ICorDebugILFrame::SetIP 方法
ms.date: 03/30/2017
api_name:
- ICorDebugILFrame.SetIP
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugILFrame::SetIP
helpviewer_keywords:
- SetIP method, ICorDebugILFrame interface [.NET Framework debugging]
- ICorDebugILFrame::SetIP method [.NET Framework debugging]
ms.assetid: 23f38dc1-85e4-4263-9235-2d05bbb6a833
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a25e52c6b858aaa602ffade0e407b1aaf6e5c67e
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57471385"
---
# <a name="icordebugilframesetip-method"></a>ICorDebugILFrame::SetIP 方法
将指令指针设置为 Microsoft 中间语言 (MSIL) 代码中的指定偏移量位置。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT SetIP (  
    [in] ULONG32 nOffset  
);  
```  
  
## <a name="parameters"></a>参数  
 `nOffset`  
 中的 MSIL 代码的偏移量的位置。  
  
## <a name="remarks"></a>备注  
 调用`SetIP`立即使所有帧和当前线程的链都无效。 如果调试器需要后调用的帧信息`SetIP`，则必须执行新的堆栈跟踪。  
  
 [ICorDebug](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md)将尝试在有效状态中保留的堆栈帧。 但是，即使在帧处于有效状态，仍可能有问题，例如未初始化的局部变量。 调用方负责确保正在运行的程序的一致性。  
  
 在 64 位平台上不能共移动指令指针`catch`或`finally`块。 如果`SetIP`称为若要使这种移动 64 位平台上的，它将返回一个 HRESULT，指示失败。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
