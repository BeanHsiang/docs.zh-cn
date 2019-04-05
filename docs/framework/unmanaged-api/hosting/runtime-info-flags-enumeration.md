---
title: RUNTIME_INFO_FLAGS 枚举
ms.date: 03/30/2017
api_name:
- RUNTIME_INFO_FLAGS
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- RUNTIME_INFO_FLAGS
helpviewer_keywords:
- RUNTIME_INFO_FLAGS enumeration [.NET Framework hosting]
ms.assetid: adba37be-f775-4cdb-8919-5746ce694f33
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 713591de414c367e415c5bf524c297cfcabb3b6e
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54555409"
---
# <a name="runtimeinfoflags-enumeration"></a>RUNTIME_INFO_FLAGS 枚举
包含指示应返回有关公共语言运行时 (CLR) 的哪些信息的值。  
  
## <a name="syntax"></a>语法  
  
```  
typedef enum {  
  
    RUNTIME_INFO_UPGRADE_VERSION             = 0x01,  
    RUNTIME_INFO_REQUEST_IA64                = 0x02,  
    RUNTIME_INFO_REQUEST_AMD64               = 0x04,  
    RUNTIME_INFO_REQUEST_X86                 = 0x08,  
    RUNTIME_INFO_DONT_RETURN_DIRECTORY       = 0x10,  
    RUNTIME_INFO_DONT_RETURN_VERSION         = 0x20,  
    RUNTIME_INFO_DONT_SHOW_ERROR_DIALOG      = 0x40,  
    RUNTIME_INFO_IGNORE_ERROR_MODE           = 0x1000  
  
} RUNTIME_INFO_FLAGS;  
```  
  
## <a name="members"></a>成员  
  
|成员|描述|  
|------------|-----------------|  
|`RUNTIME_INFO_DONT_RETURN_DIRECTORY`|指示不应包含目录信息。|  
|`RUNTIME_INFO_DONT_RETURN_VERSION`|指示不应包含版本信息。|  
|`RUNTIME_INFO_DONT_SHOW_ERROR_DIALOG`|指示在失败时应不显示错误对话框。|  
|`RUNTIME_INFO_IGNORE_ERROR_MODE`|指示调用的效果[SetErrorMode](https://go.microsoft.com/fwlink/p/?LinkId=255242) SEM_FAILCRITICALERRORS 标志的函数应重写。 也就是说，安装对话框中应显示失败，而不是所抑制。|  
|`RUNTIME_INFO_REQUEST_AMD64`|指示有关 AMD 64 兼容版本的运行时信息的请求。|  
|`RUNTIME_INFO_REQUEST_IA64`|指示有关 IA 64 兼容版本的运行时信息的请求。|  
|`RUNTIME_INFO_REQUEST_X86`|指示有关 x86 可兼容版本的运行时信息的请求。|  
|`RUNTIME_INFO_UPGRADE_VERSION`|指示应包含版本升级的信息。|  
  
## <a name="remarks"></a>备注  
 以下平台体系结构标志可以是一次只能指定的一个，并且不能结合使用：  
  
-   RUNTIME_INFO_REQUEST_IA64  
  
-   RUNTIME_INFO_REQUEST_AMD64  
  
-   RUNTIME_INFO_REQUEST_X86  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** MSCorEE.h  
  
 **库：** MSCorEE.dll  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [承载枚举](../../../../docs/framework/unmanaged-api/hosting/hosting-enumerations.md)
