---
title: ICorDebugEval::CallFunction 方法
ms.date: 03/30/2017
api_name:
- ICorDebugEval.CallFunction
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugEval::CallFunction
helpviewer_keywords:
- ICorDebugEval::CallFunction method [.NET Framework debugging]
- CallFunction method [.NET Framework debugging]
ms.assetid: 7f470c5c-e1c0-4d8d-aad8-830f113ae751
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 66e51dc15f7d44ede26634571fa04c58e9735694
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57364146"
---
# <a name="icordebugevalcallfunction-method"></a>ICorDebugEval::CallFunction 方法

设置了对指定函数的调用。

此方法是在.NET Framework 2.0 版中已过时。 使用[ICorDebugEval2::CallParameterizedFunction](icordebugeval2-callparameterizedfunction-method.md)相反。

## <a name="syntax"></a>语法

```cpp
HRESULT CallFunction (
    [in] ICorDebugFunction  *pFunction,
    [in] ULONG32            nArgs,
    [in, size_is(nArgs)] ICorDebugValue *ppArgs[]
);
```

## <a name="parameters"></a>参数

`pFunction`\
[in]指向一个 ICorDebugFunction 对象，指定要调用的函数指针。

`nArgs`\
[in]函数的参数数目。

`ppArgs`\
[in]一个指针数组，其中每个指向一个 ICorDebugValue 对象，指定要传递给函数的参数。

## <a name="remarks"></a>备注

如果该函数是虚拟的`CallFunction`将执行虚拟调度。 如果函数是在不同的应用程序域中，将发生转换，前提是所有参数也都是该应用程序域中。

## <a name="requirements"></a>要求

**平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。

**标头：** CorDebug.idl、 CorDebug.h

**库：** CorGuids.lib

**.NET framework 版本：** 1.1, 1.0

## <a name="see-also"></a>请参阅

- [CallParameterizedFunction 方法](icordebugeval2-callparameterizedfunction-method.md)