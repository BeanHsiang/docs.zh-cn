---
title: ICorDebugType 接口
ms.date: 03/30/2017
api_name:
- ICorDebugType
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugType
helpviewer_keywords:
- ICorDebugType interface [.NET Framework debugging]
ms.assetid: 94e02e31-67ea-4b00-8148-a46740a4571d
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 3e3d1173ac6fb14a380cdbc99882fd9baee6552a
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56966024"
---
# <a name="icordebugtype-interface"></a>ICorDebugType 接口
表示的类型，基本或复杂 （是，用户定义的）。 如果该类型是泛型类型，则 `ICorDebugType` 表示未实例化的泛型类型。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[EnumerateTypeParameters 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugtype-enumeratetypeparameters-method.md)|获取一个接口指针到引用泛型 ICorDebugTypeEnum<xref:System.Type>引用此类参数`ICorDebugType`。|  
|[GetBase 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugtype-getbase-method.md)|获取到的接口指针`ICorDebugType`引用此引用的类的基类`ICorDebugType`，如果存在一个。|  
|[GetClass 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugtype-getclass-method.md)|获取一个接口指针到引用此类型化的构造函数 ICorDebugClass `ICorDebugType`。|  
|[GetFirstTypeParameter 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugtype-getfirsttypeparameter-method.md)|获取到的接口指针`ICorDebugType`引用的第一个泛型<xref:System.Type>此引用的类，构造函数参数`ICorDebugType`。|  
|[GetRank 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugtype-getrank-method.md)|获取数组类型中的维度数。|  
|[GetStaticFieldValue 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugtype-getstaticfieldvalue-method.md)|获取为包含值的按指定字段引用的静态字段 ICorDebugValue 接口指针标记中指定的堆栈帧。|  
|[GetType 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugtype-gettype-method.md)|获取用于描述公共语言运行时的本机类型的 CorElementType 值<xref:System.Type>引用此`ICorDebugType`。|  
  
## <a name="remarks"></a>备注  
 如果类型是泛型，`ICorDebugClass`表示未实例化的类型。 `ICorDebugType`接口表示实例化泛型类型。 例如，哈希表\<K，V > 将由表示`ICorDebugClass`，而哈希表\<Int32，String > 将由表示`ICorDebugType`。  
  
 非泛型类型表示由`ICorDebugClass`和`ICorDebugType`。 在处理类型实例化在.NET Framework 2.0 版中引入的后一种接口。  
  
> [!NOTE]
>  此接口不支持跨计算机或跨进程远程调用。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [调试接口](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
