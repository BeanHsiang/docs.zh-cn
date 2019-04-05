---
title: CorDebugUnmappedStop 枚举
ms.date: 03/30/2017
api_name:
- CorDebugUnmappedStop
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugUnmappedStop
helpviewer_keywords:
- CorDebugUnmappedStop enumeration [.NET Framework debugging]
ms.assetid: a684f7d7-d0c2-4690-b721-639e613f11f8
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a6f22c045be9af71644415ae3b6b5e64d3e399dd
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54495430"
---
# <a name="cordebugunmappedstop-enumeration"></a>CorDebugUnmappedStop 枚举
指定未映射代码的类型，这些代码可以中断分档器代码执行。  
  
## <a name="syntax"></a>语法  
  
```  
typedef enum CorDebugUnmappedStop {  
    STOP_NONE               = 0x0,  
    STOP_PROLOG             = 0x01,  
    STOP_EPILOG             = 0x02,  
    STOP_NO_MAPPING_INFO    = 0x04,  
    STOP_OTHER_UNMAPPED     = 0x08,  
    STOP_UNMANAGED          = 0x10,  
    STOP_ALL                = 0xffff,  
} CorDebugUnmappedStop;  
```  
  
## <a name="members"></a>成员  
  
|成员|描述|  
|------------|-----------------|  
|`STOP_NONE`|不停止任何类型的非托管代码中。|  
|`STOP_PROLOG`|停止在 prolog 代码中。|  
|`STOP_EPILOG`|停止在 epilog 代码。|  
|`STOP_NO_MAPPING_INFO`|在没有映射的信息的代码中停止。|  
|`STOP_OTHER_UNMAPPED`|停止不适合 prolog、 epilog、 无映射信息或非托管的类别的未映射代码中。|  
|`STOP_UNMANAGED`|在非托管代码中停止。 此值是有效仅使用互操作调试。|  
|`STOP_ALL`|停止所有类型的非托管代码中。|  
  
## <a name="remarks"></a>备注  
 使用[icordebugstepper:: Setunmappedstopmask](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-setunmappedstopmask-method.md)方法设置标志，用于指定将在其中停止分档器未映射的代码。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [调试枚举](../../../../docs/framework/unmanaged-api/debugging/debugging-enumerations.md)
