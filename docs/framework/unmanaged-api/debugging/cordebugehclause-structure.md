---
title: CorDebugEHClause 结构
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- CorDebugEHClause
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: 0e350a1b-6997-46d0-bfc5-962a5011ef43
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: be5d580c28a15a58cad6c5a2231d3a87e25c0e7a
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54495340"
---
# <a name="cordebugehclause-structure"></a>CorDebugEHClause 结构
[仅在 .NET Framework 4.5.2 及更高版本中受支持]  
  
 表示给定的一段中间语言 (IL) 代码的异常处理 (EH) 子句。  
  
## <a name="syntax"></a>语法  
  
```cpp
typedef struct _CorDebugEHClause {  
   ULONG32 Flags;  
   ULONG32 TryOffset;  
   ULONG32 TryLength;  
   ULONG32 HandlerOffset;  
   ULONG32 HandlerLength;  
   ULONG32 ClassToken;  
   ULONG32 FilterOffset;  
} CorDebugEHClause;  
```  
  
## <a name="members"></a>成员  
  
|成员|描述|  
|------------|-----------------|  
|`Flags`|描述 EH 子句中的异常信息的位字段。 有关详细信息，请参阅“备注”部分。|  
|`TryOffset`|方法主体开头的 `try` 块的偏移量（以字节为单位）。|  
|`TryLength`|`try` 块的长度（以字节为单位）。|  
|`HandlerOffset`|此 `try` 块的处理程序的位置。|  
|`HandlerLength`|处理程序代码的大小（以字节为单位）。|  
|`ClassToken`|基于类型的异常处理程序的元数据标记。|  
|`FilterOffset`|基于筛选器的异常处理程序的方法主体开头的偏移量（以字节为单位）。|  
  
## <a name="remarks"></a>备注  
 一个数组`CoreDebugEHClause`返回的值[GetEHClauses](../../../../docs/framework/unmanaged-api/debugging/icordebugilcode-getehclauses-method.md)方法。  
  
 EH 子句信息由 CLI 规范定义。 有关详细信息，请参阅[标准 ECMA-355:公共语言基础结构 (CLI)，第 6 版](https://www.ecma-international.org/publications/standards/Ecma-335.htm)。  
  
 `flags` 字段可以包含以下标志。 请注意，它们不会在 CorDebug.idl 或 CorDebug.h 中定义。  
  
|Flag|值|描述|  
|----------|-----------|-----------------|  
|`COR_ILEXCEPTION_CLAUSE_EXCEPTION`|0x00000000|键入的异常子句。|  
|`COR_ILEXCEPTION_CLAUSE_FILTER`|0x00000001|异常筛选器和处理程序子句。|  
|`COR_ILEXCEPTION_CLAUSE_FINALLY`|0x00000002|`finally` 子句。|  
|`COR_ILEXCEPTION_CLAUSE_FAULT`|0x00000004|Fault 子句（仅当引发异常时才调用的 `finally` 子句）。|  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [GetEHClauses 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugilcode-getehclauses-method.md)
- [调试结构](../../../../docs/framework/unmanaged-api/debugging/debugging-structures.md)
