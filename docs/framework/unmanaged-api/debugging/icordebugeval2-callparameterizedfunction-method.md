---
title: ICorDebugEval2::CallParameterizedFunction 方法
ms.date: 03/30/2017
api_name:
- ICorDebugEval2.CallParameterizedFunction
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugEval2::CallParameterizedFunction
helpviewer_keywords:
- ICorDebugEval2::CallParameterizedFunction method [.NET Framework debugging]
- CallParameterizedFunction method [.NET Framework debugging]
ms.assetid: 72f54a45-dbe6-4bb4-8c99-e879a27368e5
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: cba4eb2b76d7057a5ed66a35342a79615cb8539f
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57487715"
---
# <a name="icordebugeval2callparameterizedfunction-method"></a>ICorDebugEval2::CallParameterizedFunction 方法
设置了对可以嵌套在其构造函数采用一个类内部指定 ICorDebugFunction<xref:System.Type>参数或可以本身采取<xref:System.Type>参数。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT CallParameterizedFunction (  
    [in] ICorDebugFunction     *pFunction,  
    [in] ULONG32               nTypeArgs,  
    [in, size_is(nTypeArgs)] ICorDebugType *ppTypeArgs[],  
    [in] ULONG32               nArgs,  
    [in, size_is(nArgs)] ICorDebugValue *ppArgs[]  
);  
```  
  
## <a name="parameters"></a>参数  
 `pFunction`  
 [in]一个指向`ICorDebugFunction`对象，表示要调用的函数。  
  
 `nTypeArgs`  
 [in]该函数采用的参数数目。  
  
 `ppTypeArgs`  
 [in]一个指针数组，其中每个指向对象的表示函数的参数。  
  
 `nArgs`  
 [in]在函数中传递的值的数目。  
  
 `ppArgs`  
 [in]函数参数中传递的指针的数组，其中每个指向 ICorDebugValue 对象表示的值。  
  
## <a name="remarks"></a>备注  
 `CallParameterizedFunction` 就像[icordebugeval:: Callfunction](../../../../docs/framework/unmanaged-api/debugging/icordebugeval-callfunction-method.md)只不过该函数可能使用的类型参数的类的内部，可能本身需要和 / 或类型参数。 对于类，然后为该函数，应首先提供的类型参数。  
  
 如果该函数是在不同的应用程序域中，将发生转换。 但是，所有类型和值参数都必须在目标应用程序域中。  
  
 仅在有限情况下，可以执行函数求值。 如果`CallParameterizedFunction`或`ICorDebugEval::CallFunction`失败，返回的 HRESULT 会指示失败的最常规的可能原因。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
