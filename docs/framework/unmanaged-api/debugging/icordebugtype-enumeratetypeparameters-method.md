---
title: ICorDebugType::EnumerateTypeParameters 方法
ms.date: 03/30/2017
api_name:
- ICorDebugType.EnumerateTypeParameters
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugType::EnumerateTypeParameters
helpviewer_keywords:
- EnumerateTypeParameters method, ICorDebugType interface [.NET Framework debugging]
- ICorDebugType::EnumerateTypeParameters method [.NET Framework debugging]
ms.assetid: 1ee1f6e6-1bd7-4ebb-83b8-ff9a08ca03de
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b8fa39a54437e60737aa052c495f58422bc0d3fe
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57474444"
---
# <a name="icordebugtypeenumeratetypeparameters-method"></a>ICorDebugType::EnumerateTypeParameters 方法
获取指向包含 ICorDebugTypeEnum 接口指针<xref:System.Type>此 ICorDebugType 所引用的类的参数。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT EnumerateTypeParameters (  
    [out] ICorDebugTypeEnum   **ppTyParEnum  
);  
```  
  
## <a name="parameters"></a>参数  
 `ppTyParEnum`  
 [out]指向的地址的指针`ICorDebugTypeEnum`包含类型的参数。  
  
## <a name="remarks"></a>备注  
 可以使用`EnumerateTypeParameters`如果返回的 CorElementType 值[icordebugtype:: Gettype](../../../../docs/framework/unmanaged-api/debugging/icordebugtype-gettype-method.md)是 ELEMENT_TYPE_CLASS、 ELEMENT_TYPE_VALUETYPE、 ELEMENT_TYPE_ARRAY、 ELEMENT_TYPE_SZARRAY、 ELEMENT_TYPE_BYREF、 ELEMENT_TYPE_PTR 或 typ ELEMENT_TYPE_FNPTR。 参数和它们的顺序的数目取决于该类型：  
  
-   ELEMENT_TYPE_CLASS 或 ELEMENT_TYPE_VALUETYPE:中包含的类型参数的数目`ICorDebugTypeEnum`，此方法返回时，将取决于相应类的正式类型参数的数目。 例如，如果该类型是`class Dict<String,int32>`，然后`EnumerateTypeParameters`将返回`ICorDebugTypeEnum`，其中包含表示的对象`String`和`int32`序列中。  
  
-   TYP ELEMENT_TYPE_FNPTR:中包含的类型参数的数目`ICorDebugTypeEnum`将一个大于该函数接受的参数数目。 中包含的第一个类型参数`ICorDebugTypeEnum`是该函数的返回类型和后续类型参数是函数的参数。  
  
-   ELEMENT_TYPE_ARRAY、 ELEMENT_TYPE_SZARRAY、 ELEMENT_TYPE_BYREF 或 ELEMENT_TYPE_PTR:将返回一个类型参数。 例如，如果类型为数组类型，如`int32[]`，`EnumerateTypeParameters`将返回`ICorDebugTypeEnum`，其中包含一个对象，表示`int32`。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
