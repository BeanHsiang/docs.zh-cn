---
title: COR_PRF_GC_GENERATION 枚举
ms.date: 03/30/2017
api_name:
- COR_PRF_GC_GENERATION
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_GC_GENERATION
helpviewer_keywords:
- COR_GC_GENERATION_FLAGS enumeration [.NET Framework profiling]
ms.assetid: d6ece160-26ad-4d39-abd7-05acd6f78c48
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 15bd3ed8f1642e44ecf9c4df49feebd72eeac8c2
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54590128"
---
# <a name="corprfgcgeneration-enumeration"></a>COR_PRF_GC_GENERATION 枚举
标识垃圾回收的代。  
  
## <a name="syntax"></a>语法  
  
```  
typedef enum {  
    COR_PRF_GC_GEN_0 = 0,  
    COR_PRF_GC_GEN_1 = 1,  
    COR_PRF_GC_GEN_2 = 2,  
    COR_PRF_GC_LARGE_OBJECT_HEAP = 3  
} COR_PRF_GC_GENERATION;  
```  
  
## <a name="members"></a>成员  
  
|成员|描述|  
|------------|-----------------|  
|`COR_PRF_GC_GEN_0`|该对象存储为第 0 代中。|  
|`COR_PRF_GC_GEN_1`|该对象存储为第 1 代。|  
|`COR_PRF_GC_GEN_2`|该对象存储为第 2 代。|  
|`COR_PRF_GC_LARGE_OBJECT_HEAP`|该对象存储在大型对象堆。|  
  
## <a name="remarks"></a>备注  
 垃圾回收器提高将对象划分为几个代根据年龄内存管理性能。 垃圾回收器当前正在使用三代，编号为 0、 1 和 2，以及用于大型对象的特殊堆段。 其大小大于特定值的对象存储在大型对象堆。 其他分配的对象最初属于第 0 代。 第 0 代中发生了垃圾回收后存在的所有对象都提升到第 1 代。 在第 1 代垃圾回收后存在的对象将移到第 2 代。  
  
 代的使用意味着，垃圾收集器在任何一次处理已分配对象的一个子集。  
  
 `COR_PRF_GC_GENERATION`枚举由[COR_PRF_GC_GENERATION_RANGE](../../../../docs/framework/unmanaged-api/profiling/cor-prf-gc-generation-range-structure.md)结构。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorProf.idl, CorProf.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [分析枚举](../../../../docs/framework/unmanaged-api/profiling/profiling-enumerations.md)
