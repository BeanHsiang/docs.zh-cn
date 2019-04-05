---
title: COR_PRF_STATIC_TYPE 枚举
ms.date: 03/30/2017
api_name:
- COR_PRF_STATIC_TYPE
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_STATIC_TYPE
helpviewer_keywords:
- COR_PRF_STATIC_TYPE enumeration [.NET Framework profiling]
ms.assetid: 441d7809-5b65-41a5-ba64-2910a8008315
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 34a2ca5b505c504115af47402c3d92a05ec0676f
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54737622"
---
# <a name="corprfstatictype-enumeration"></a>COR_PRF_STATIC_TYPE 枚举
指示字段是否为静态的，并在字段为静态字段时指示应用于该字段的静态质量。 这些值可以组合使用位或运算来指示该字段具有多个不同的静态质量。  
  
## <a name="syntax"></a>语法  
  
```  
typedef enum {  
    COR_PRF_FIELD_NOT_A_STATIC = 0x0,  
    COR_PRF_FIELD_APP_DOMAIN_STATIC = 0x1,  
    COR_PRF_FIELD_THREAD_STATIC = 0x2,  
    COR_PRF_FIELD_CONTEXT_STATIC = 0x4,  
    COR_PRF_FIELD_RVA_STATIC = 0x8  
} COR_PRF_STATIC_TYPE;  
```  
  
## <a name="members"></a>成员  
  
|成员|描述|  
|------------|-----------------|  
|`COR_PRF_FIELD_NOT_A_STATIC`|该字段不是静态的。|  
|`COR_PRF_FIELD_APP_DOMAIN_STATIC`|该字段是应用程序域静态。|  
|`COR_PRF_FIELD_THREAD_STATIC`|线程静态字段。|  
|`COR_PRF_FIELD_CONTEXT_STATIC`|该字段为静态上下文。|  
|`COR_PRF_FIELD_RVA_STATIC`|该字段是相对虚拟地址 (RVA) 的静态。|  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorProf.idl, CorProf.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [分析枚举](../../../../docs/framework/unmanaged-api/profiling/profiling-enumerations.md)
