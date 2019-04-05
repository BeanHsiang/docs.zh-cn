---
title: COR_HEAPOBJECT 结构
ms.date: 03/30/2017
api_name:
- COR_HEAPOBJECT
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- COR_HEAPOBJECT
helpviewer_keywords:
- COR_HEAPOBJECT structure [.NET Framework debugging]
ms.assetid: a92fdf95-492b-49ae-a741-2186e5c1d7c5
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 34b02dfa3fb0f1e5f4cfadc297194dc4f3160c8a
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54628469"
---
# <a name="corheapobject-structure"></a>COR_HEAPOBJECT 结构
提供有关托管堆上的对象的信息。  
  
## <a name="syntax"></a>语法  
  
```  
typedef struct _COR_HEAPOBJECT {  
    CORDB_ADDRESS address;    
    ULONG64 size;             
    COR_TYPEID type;          
} COR_HEAPOBJECT;  
```  
  
## <a name="members"></a>成员  
  
|成员|描述|  
|------------|-----------------|  
|`address`|在内存中对象的地址。|  
|`size`|对象，以字节为单位的总大小。|  
|`type`|一个[COR_TYPEID](../../../../docs/framework/unmanaged-api/debugging/cor-typeid-structure.md)表示的对象类型的令牌。|  
  
## <a name="remarks"></a>备注  
 `COR_HEAPOBJECT` 实例可以检索通过枚举[ICorDebugHeapEnum](../../../../docs/framework/unmanaged-api/debugging/icordebugheapenum-interface.md)接口对象通过调用来填充[ICorDebugProcess5::EnumerateHeap](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess5-enumerateheap-method.md)方法。  
  
 一个`COR_HEAPOBJECT`实例提供了有关托管堆上一个活动对象或不根路径的任何对象，但尚未被垃圾回收器回收的对象有关的信息。  
  
 为了提高性能，`COR_HEAPOBJECT.address`字段是`CORDB_ADDRESS`值而不是 ICorDebugValue 接口在很多调试 API 中使用的值。 若要获取给定的对象地址的 ICorDebugValue 对象，可以将传递`CORDB_ADDRESS`值设为[ICorDebugProcess5::GetObject](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess5-getobject-method.md)方法。  
  
 为了提高性能，`COR_HEAPOBJECT.type`字段是`COR_TYPEID`值而不是 ICorDebugType 接口在很多调试 API 中使用的值。 若要获取给定的类型 ID ICorDebugType 对象，可以将传递`COR_TYPEID`值设为[ICorDebugProcess5::GetTypeForTypeID](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess5-gettypefortypeid-method.md)方法。  
  
 `COR_HEAPOBJECT`结构包含引用计数 COM 接口。 如果检索`COR_HEAPOBJECT`通过调用枚举器中的实例[icordebugheapenum:: Next](../../../../docs/framework/unmanaged-api/debugging/icordebugheapenum-next-method.md)方法，随后必须释放该引用。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [调试结构](../../../../docs/framework/unmanaged-api/debugging/debugging-structures.md)
- [调试](../../../../docs/framework/unmanaged-api/debugging/index.md)
