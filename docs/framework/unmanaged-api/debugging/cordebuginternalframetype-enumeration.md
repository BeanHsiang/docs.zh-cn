---
title: CorDebugInternalFrameType 枚举
ms.date: 03/30/2017
api_name:
- CorDebugInternalFrameType
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugInternalFrameType
helpviewer_keywords:
- CorDebugInternalFrameType enumeration [.NET Framework debugging]
ms.assetid: e4412dc2-c338-4cfb-94d8-f682095dd2b1
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6cf4c0eb3f9bb36cb45aa93c576b4efddaa93482
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54736528"
---
# <a name="cordebuginternalframetype-enumeration"></a>CorDebugInternalFrameType 枚举
标识堆栈帧的类型。 此枚举由[icordebuginternalframe:: Getframetype](../../../../docs/framework/unmanaged-api/debugging/icordebuginternalframe-getframetype-method.md)方法。  
  
## <a name="syntax"></a>语法  
  
```  
typedef enum CorDebugInternalFrameType {  
  
    STUBFRAME_NONE                 = 0x00000000,  
    STUBFRAME_M2U                  = 0x00000001,  
    STUBFRAME_U2M                  = 0x00000002,  
    STUBFRAME_APPDOMAIN_TRANSITION = 0x00000003,  
    STUBFRAME_LIGHTWEIGHT_FUNCTION = 0x00000004,  
    STUBFRAME_FUNC_EVAL            = 0x00000005,  
    STUBFRAME_INTERNALCALL         = 0x00000006,  
    STUBFRAME_CLASS_INIT           = 0x00000007,  
    STUBFRAME_EXCEPTION            = 0x00000008,  
    STUBFRAME_SECURITY             = 0x00000009,  
    STUBFRAME_JIT_COMPILATION     = 0x0000000a,  
} CorDebugInternalFrameType;  
```  
  
## <a name="members"></a>成员  
  
|成员|描述|  
|------------|-----------------|  
|`STUBFRAME_NONE`|Null 值。 `ICorDebugInternalFrame::GetFrameType`方法永远不会返回此值。|  
|`STUBFRAME_M2U`|托管到非托管存根 （stub） 框架。|  
|`STUBFRAME_U2M`|非托管到托管存根 （stub） 的帧。|  
|`STUBFRAME_APPDOMAIN_TRANSITION`|应用程序域之间的转换。|  
|`STUBFRAME_LIGHTWEIGHT_FUNCTION`|轻量的方法调用。|  
|`STUBFRAME_FUNC_EVAL`|函数计算的开始。|  
|`STUBFRAME_INTERNALCALL`|内部调入公共语言运行时。|  
|`STUBFRAME_CLASS_INIT`|类初始化开始。|  
|`STUBFRAME_EXCEPTION`|引发异常。|  
|`STUBFRAME_SECURITY`|使用代码访问安全性的帧。|  
|`STUBFRAME_JIT_COMPILATION`|运行时 JIT 编译的方法。|  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [调试枚举](../../../../docs/framework/unmanaged-api/debugging/debugging-enumerations.md)
