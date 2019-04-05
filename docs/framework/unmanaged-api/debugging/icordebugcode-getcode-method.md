---
title: ICorDebugCode::GetCode 方法
ms.date: 03/30/2017
api_name:
- ICorDebugCode.GetCode
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugCode::GetCode
helpviewer_keywords:
- ICorDebugCode::GetCode method [.NET Framework debugging]
- GetCode method, ICorDebugCode interface [.NET Framework debugging]
ms.assetid: 7137e3d1-1dad-48d8-8c37-16ac816534d3
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7b69970d50652da203ecf1ae6fe8d604ccee06cf
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57483570"
---
# <a name="icordebugcodegetcode-method"></a>ICorDebugCode::GetCode 方法
获取指定的函数的反汇编格式的所有代码。 .NET Framework 2.0 版中，此方法已弃用。 使用[ICorDebugCode2::GetCodeChunks](../../../../docs/framework/unmanaged-api/debugging/icordebugcode2-getcodechunks-method.md)相反。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT GetCode (  
    [in] ULONG32     startOffset,   
    [in] ULONG32     endOffset,  
    [in] ULONG32     cBufferAlloc,  
    [out, size_is(cBufferAlloc),  
        length_is(*pcBufferSize)] BYTE buffer[],  
    [out] ULONG32    *pcBufferSize  
);  
```  
  
## <a name="parameters"></a>参数  
 `startOffset`  
 [in]该函数的开头的偏移量。  
  
 `endOffset`  
 [in]该函数的末尾的偏移量。  
  
 `cBufferAlloc`  
 [in]大小`buffer`数组转换返回的代码。  
  
 `buffer`  
 [out]代码将返回到其中的数组。  
  
 `pcBufferSize`  
 [out]返回的字节数。  
  
## <a name="remarks"></a>备注  
 如果该函数的代码都分成多个块区，系统会将它们连接起来递增本机偏移量的顺序。 不检查指令边界。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET framework 版本：** 1.1, 1.0  
  
## <a name="see-also"></a>请参阅
- [GetCodeChunks 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugcode2-getcodechunks-method.md)

