---
title: ICorDebugILFrame3::GetReturnValueForILOffset 方法
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
api_name:
- ICorDebugILFrame3.GetReturnValueForILOffset
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: 06522727-5f64-4391-9331-11386883c352
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a01e2fcc7dc00d3a57272abb04ebcecc6d5f74a6
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57467061"
---
# <a name="icordebugilframe3getreturnvalueforiloffset-method"></a>ICorDebugILFrame3::GetReturnValueForILOffset 方法
获取封装函数的返回值的"ICorDebugValue"对象。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetReturnValueForILOffset(  
    ULONG32 ILoffset,   
    [out] ICorDebugValue **ppReturnValue  
);  
```  
  
## <a name="parameters"></a>参数  
 `ILOffset`  
 IL 偏移量。 请参见“备注”部分。  
  
 `ppReturnValue`  
 指向提供有关返回值的函数调用信息"ICorDebugValue"接口对象的地址的指针。  
  
## <a name="remarks"></a>备注  
 此方法使用连同[ICorDebugCode3::GetReturnValueLiveOffset](../../../../docs/framework/unmanaged-api/debugging/icordebugcode3-getreturnvalueliveoffset-method.md)方法以获取一种方法的返回值。 它是在其返回值将被忽略，如以下两个代码示例所示的方法的情况下特别有用。 第一个示例调用<xref:System.Int32.TryParse%2A?displayProperty=nameWithType>方法，但忽略方法的返回值。  
  
 [!code-csharp[Unmanaged.Debugging.MRV#1](../../../../samples/snippets/csharp/VS_Snippets_CLR/unmanaged.debugging.mrv/cs/mrv1.cs#1)]
 [!code-vb[Unmanaged.Debugging.MRV#1](../../../../samples/snippets/visualbasic/VS_Snippets_CLR/unmanaged.debugging.mrv/vb/mrv1.vb#1)]  
  
 第二个示例说明了在调试更常见的问题。 由于一种方法用作方法调用中的自变量，因此，仅当调试器单步通过调用的方法，才可访问其返回值。 在许多情况下，尤其是在调用的方法定义中的外部库时，不能。  
  
 [!code-csharp[Unmanaged.Debugging.MRV#2](../../../../samples/snippets/csharp/VS_Snippets_CLR/unmanaged.debugging.mrv/cs/mrv2.cs#2)]
 [!code-vb[Unmanaged.Debugging.MRV#2](../../../../samples/snippets/visualbasic/VS_Snippets_CLR/unmanaged.debugging.mrv/vb/mrv2.vb#2)]  
  
 如果传递[ICorDebugCode3::GetReturnValueLiveOffset](../../../../docs/framework/unmanaged-api/debugging/icordebugcode3-getreturnvalueliveoffset-method.md)一个 IL 偏移量至函数调用站点的方法，它将返回一个或多个本机偏移量。 调试程序然后可以在函数中的本机偏移量上设置断点。 当调试器遇到其中一个断点时，然后可以将相同的 IL 偏移量传递给此方法以获取返回值进行传递。 然后调试器应该清除此设置的所有断点。  
  
> [!WARNING]
>  [ICorDebugCode3::GetReturnValueLiveOffset Method](../../../../docs/framework/unmanaged-api/debugging/icordebugcode3-getreturnvalueliveoffset-method.md)和`ICorDebugILFrame3::GetReturnValueForILOffset`方法，你可以获得仅为引用类型的返回值信息。 从值类型检索返回值信息 (即，派生的所有类型<xref:System.ValueType>) 不受支持。  
  
 指定的 IL 偏移量`ILOffset`参数应在函数调用站点，并应在返回的本机偏移量处设置断点处停止调试对象[ICorDebugCode3::GetReturnValueLiveOffset](../../../../docs/framework/unmanaged-api/debugging/icordebugcode3-getreturnvalueliveoffset-method.md)方法为相同的 IL 偏移量。 如果未在指定的 IL 偏移量的正确位置停止调试对象，该 API 将失败。  
  
 如果函数调用不会返回一个值，该 API 将失败。  
  
 `ICorDebugILFrame3::GetReturnValueForILOffset`方法是仅适用于基于 x86 和 AMD64 系统。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v451plus](../../../../includes/net-current-v451plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [GetReturnValueLiveOffset 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugcode3-getreturnvalueliveoffset-method.md)
- [ICorDebugILFrame3 接口](../../../../docs/framework/unmanaged-api/debugging/icordebugilframe3-interface.md)
