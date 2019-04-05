---
title: ICorDebugHeapValue2::CreateHandle 方法
ms.date: 03/30/2017
api_name:
- ICorDebugHeapValue2.CreateHandle
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugHeapValue2::CreateHandle
helpviewer_keywords:
- CreateHandle method [.NET Framework debugging]
- ICorDebugHeapValue2::CreateHandle method [.NET Framework debugging]
ms.assetid: fbc418e8-fa22-420d-84ec-e0e1800db041
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 078dfd7162c250f0279b8bc372aeb39662aa0119
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57498531"
---
# <a name="icordebugheapvalue2createhandle-method"></a>ICorDebugHeapValue2::CreateHandle 方法
创建此 ICorDebugHeapValue2 对象所表示的堆值的指定类型的句柄。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT CreateHandle (  
    [in] CorDebugHandleType      type,   
    [out] ICorDebugHandleValue   **ppHandle  
);  
```  
  
## <a name="parameters"></a>参数  
 `type`  
 [in]CorDebugHandleType 枚举，指定要创建的句柄的类型的值。  
  
 `ppHandle`  
 [out]指向一个 ICorDebugHandleValue 对象，表示此堆值的新句柄的地址的指针。  
  
## <a name="remarks"></a>备注  
 句柄将与堆值相关联的应用程序域中创建和将变为无效，如果应用程序域被卸载。  
  
 多次调用相同的堆值此函数调用将创建多个句柄。 句柄的垃圾回收器性能影响，因为调试器应限制自身到相对较少的一次处于活动状态的句柄 (大约 256)。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
