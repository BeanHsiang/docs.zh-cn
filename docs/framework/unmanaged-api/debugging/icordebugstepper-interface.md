---
title: ICorDebugStepper 接口
ms.date: 03/30/2017
api_name:
- ICorDebugStepper
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStepper
helpviewer_keywords:
- ICorDebugStepper interface [.NET Framework debugging]
ms.assetid: ed8364eb-f01b-46f6-b5e3-5dda9cae2dfe
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1bd650178c787440941b9fd9a84b1e85c55aac61
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56973712"
---
# <a name="icordebugstepper-interface"></a>ICorDebugStepper 接口
表示在代码执行过程中由调试器执行的一个步骤。此步骤作为命令颁发和完成之间的标识符使用，可以实现取消对某个步骤的执行。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[Deactivate 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-deactivate-method.md)|这将导致`ICorDebugStepper`取消它收到的最后一个步骤命令。|  
|[IsActive 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-isactive-method.md)|获取一个值，该值指示是否此`ICorDebugStepper`当前正在执行一个步骤。|  
|[SetInterceptMask 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-setinterceptmask-method.md)|设置一个 CorDebugIntercept 值，指定的单步执行代码的类型。|  
|[SetRangeIL 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-setrangeil-method.md)|设置一个值，该值指示是否调用[icordebugstepper:: Steprange](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-steprange-method.md)传递参数值相对于本机代码或单步执行方法的 Microsoft 中间语言 (MSIL) 代码。|  
|[SetUnmappedStopMask 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-setunmappedstopmask-method.md)|设置 CorDebugUnmappedStop 值，该值指定在其中执行都将停止的代码未映射的类型。|  
|[Step 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-step-method.md)|这将导致`ICorDebugStepper`单步执行其包含的线程，并 （可选） 到继续单步执行通过该线程中调用的函数。|  
|[StepOut 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-stepout-method.md)|这将导致`ICorDebugStepper`单步执行其包含的线程，并完成时的当前帧将控制权返回给调用的帧。|  
|[StepRange 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-steprange-method.md)|这将导致`ICorDebugStepper`单步执行其包含的线程，并返回时达到超出指定范围的最后一个代码。|  
  
## <a name="remarks"></a>备注  
 `ICorDebugStepper`接口具有以下用途：  
  
-   它充当颁发步骤命令和命令的完成之间的标识符。  
  
-   它提供了一个中央的界面来封装所有单步执行可执行。  
  
-   它提供了过早地取消单步执行操作的方法。  
  
 可以有多个分档器每个线程。 例如，可能会命中的断点时逐过程执行函数，而用户可能想要启动新的单步执行操作，在该函数内部。 负责调试器来确定如何处理这种情况。 调试器可能想要取消原始单步执行操作或嵌套两个操作。 `ICorDebugStepper`接口支持这两种选择。  
  
 如果公共语言运行时 (CLR) 进行跨线程的封送调用，分档器可能会在线程间迁移。  
  
> [!NOTE]
>  此接口不支持跨计算机或跨进程远程调用。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [调试接口](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
