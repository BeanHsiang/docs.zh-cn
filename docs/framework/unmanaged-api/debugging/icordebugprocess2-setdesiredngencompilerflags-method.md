---
title: ICorDebugProcess2::SetDesiredNGENCompilerFlags 方法
ms.date: 03/30/2017
api_name:
- ICorDebugProcess2.SetDesiredNGENCompilerFlags
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess2::SetDesiredNGENCompilerFlags
helpviewer_keywords:
- ICorDebugProcess2::SetDesiredNGENCompilerFlags method [.NET Framework debugging]
- SetDesiredNGENCompilerFlags method [.NET Framework debugging]
ms.assetid: 98320175-7c5e-4dbb-8683-86fa82e2641f
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: e1cab24f949ddae55d5e699e6ad82851007504dd
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57475692"
---
# <a name="icordebugprocess2setdesiredngencompilerflags-method"></a>ICorDebugProcess2::SetDesiredNGENCompilerFlags 方法
设置必须按顺序运行时便会将该映像加载到当前进程的预编译映像中嵌入的标志。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT SetDesiredNGENCompilerFlags (  
    [in] DWORD    pdwFlags  
);  
```  
  
## <a name="parameters"></a>参数  
 `pdwFlags`  
 [in]值为[CorDebugJITCompilerFlags](../../../../docs/framework/unmanaged-api/debugging/cordebugjitcompilerflags-enumeration.md)枚举，用于指定编译器标志用于选择正确的预编译的映像。  
  
## <a name="remarks"></a>备注  
 `SetDesiredNGENCompilerFlags`方法指定，以便在运行时将该图像加载到此过程必须预编译的图像中嵌入的标志。 此方法设置的标志仅用于选择正确的预编译的映像。 如果不存在任何此类映像，在运行时将加载 Microsoft 中间语言 (MSIL) 映像，并在实时 (JIT) 编译器。 在这种情况下，仍必须使用调试器[ICorDebugModule2::SetJITCompilerFlags](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule2-setjitcompilerflags-method.md)方法以根据需要进行 JIT 编译设置标志。  
  
 如果已加载图像，但某些 JIT 编译，则必须执行对该映像 （这也是如此，如果映像包含泛型），由指定的编译器标志`SetDesiredNGENCompilerFlags`方法将应用到额外的 JIT 编译。  
  
 `SetDesiredNGENCompilerFlags`必须在调用方法[icordebugmanagedcallback:: Createprocess](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-createprocess-method.md)回调。 尝试调用`SetDesiredNGENCompilerFlags`方法之后将失败。 此外，尝试设置标志，也可以定义在`CorDebugJITCompilerFlags`枚举或不合法给定进程将失败。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [ICorDebug 接口](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md)
- [ICorDebugManagedCallback 接口](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-interface.md)
