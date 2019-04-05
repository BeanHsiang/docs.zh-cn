---
title: COR_ARRAY_LAYOUT 结构
ms.date: 03/30/2017
api_name:
- COR_ARRAY_LAYOUT
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- COR_ARRAY_LAYOUT
helpviewer_keywords:
- COR_DEBUG_IL_TO_NATIVE_MAP structure [.NET Framework debugging]
ms.assetid: aa20ac3d-6f60-4aa2-91c5-f3a86f82eba8
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: e6fee91146e99ba1f63ecafcbbdaae9d42675848
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54731135"
---
# <a name="corarraylayout-structure"></a>COR_ARRAY_LAYOUT 结构
提供有关内存中数组对象的布局的信息。  
  
## <a name="syntax"></a>语法  
  
```  
typedef struct COR_ARRAY_LAYOUT {  
    COR_TYPEID componentID;  
    CorElementType componentType;  
    ULONG32 firstElementOffset;  
    ULONG32 elementSize;  
    ULONG32 countOffset;   
    ULONG32 rankSize;   
    ULONG32 numRanks;   
    ULONG32 rankOffset;   
} COR_ARRAY_LAYOUT;  
```  
  
## <a name="members"></a>成员  
  
|成员|描述|  
|------------|-----------------|  
|`componentID`|该数组包含的对象的类型的标识符。|  
|`componentType`|CorElementType 枚举值，该值指示组件是否是垃圾回收引用、 值类或基元。|  
|`firstElementOffset`|到数组中的第一个元素的偏移量。|  
|`elementSize`|每个元素的大小。|  
|`countOffset`|到数组中的元素数的偏移量。|  
|`rankSize`|秩，以字节为单位的大小。|  
|`numRanks`|数组中的排名数。|  
|`rankOffset`|排名开始的偏移量。|  
  
## <a name="remarks"></a>备注  
 `rankSize`字段多维数组中指定级别的大小。 它是一维数组也为准确的。  
  
 值`numRanks`为 1 的一维数组并`N`多维数组的`N`维度。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [调试结构](../../../../docs/framework/unmanaged-api/debugging/debugging-structures.md)
- [调试](../../../../docs/framework/unmanaged-api/debugging/index.md)
