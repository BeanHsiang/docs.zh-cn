---
title: STARTUP_FLAGS 枚举
ms.date: 03/30/2017
api_name:
- STARTUP_FLAGS
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- STARTUP_FLAGS
helpviewer_keywords:
- STARTUP_FLAGS enumeration [.NET Framework hosting]
ms.assetid: 4f043594-0c45-4bc6-988e-a6793f0d8d06
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6a4a9bda348ce4c0dfd1e41d4154cad88d4966a1
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54701750"
---
# <a name="startupflags-enumeration"></a>STARTUP_FLAGS 枚举
包含指示公共语言运行时 (CLR) 的启动行为的值。 默认情况下，垃圾回收是非并发，只有在基类库加载到非特定于域的区域。  
  
## <a name="syntax"></a>语法  
  
```  
typedef enum {  
    STARTUP_CONCURRENT_GC                         = 0x1,  
    STARTUP_LOADER_OPTIMIZATION_MASK              = 0x3<<1,  
    STARTUP_LOADER_OPTIMIZATION_SINGLE_DOMAIN     = 0x1<<1,  
    STARTUP_LOADER_OPTIMIZATION_MULTI_DOMAIN      = 0x2<<1,  
    STARTUP_LOADER_OPTIMIZATION_MULTI_DOMAIN_HOST = 0x3<<1,  
  
    STARTUP_LOADER_SAFEMODE                       = 0x10,  
    STARTUP_LOADER_SETPREFERENCE                  = 0x100,  
  
    STARTUP_SERVER_GC                             = 0x1000,  
    STARTUP_HOARD_GC_VM                           = 0x2000,  
  
    STARTUP_SINGLE_VERSION_HOSTING_INTERFACE      = 0x4000,  
    STARTUP_LEGACY_IMPERSONATION                  = 0x10000,  
    STARTUP_DISABLE_COMMITTHREADSTACK             = 0x20000,  
    STARTUP_ALWAYSFLOW_IMPERSONATION              = 0x40000,  
    STARTUP_TRIM_GC_COMMIT                        = 0x80000,  
  
    STARTUP_ETW                                   = 0x100000,  
    STARTUP_ARM                                   = 0x400000  
} STARTUP_FLAGS;  
```  
  
## <a name="members"></a>成员  
  
|成员|描述|  
|------------|-----------------|  
|`STARTUP_CONCURRENT_GC`|指定应使用并发垃圾回收。 如果在单处理器计算机上，调用方要求的服务器版本和并发垃圾回收，工作站版本和非并发垃圾回收是改为运行。 **注意：** 在应用程序运行在 WOW64 中不支持并发垃圾回收 x86 仿真程序上实现 Intel Itanium 体系结构 （以前称为 IA-64） 的 64 位系统。 有关在 64 位 Windows 系统上使用 WOW64 的详细信息，请参阅[运行 32 位应用程序](/windows/desktop/WinProg64/running-32-bit-applications)。|  
|`STARTUP_LOADER_OPTIMIZATION_MASK`|指定只应出现加载程序优化。|  
|`STARTUP_LOADER_OPTIMIZATION_SINGLE_DOMAIN`|不指定的任何程序集加载为非特定于域。|  
|`STARTUP_LOADER_OPTIMIZATION_MULTI_DOMAIN`|指定的所有程序集加载为非特定于域。|  
|`STARTUP_LOADER_OPTIMIZATION_MULTI_DOMAIN_HOST`|指定所有强名称的程序集将作为非特定于域的加载。|  
|`STARTUP_LOADER_SAFEMODE`|指定 CLR 版本策略将不应用于传入的版本。 将加载指定的 clr 的确切版本。 填充程序不评估策略，以确定最新的兼容版本。|  
|`STARTUP_LOADER_SETPREFERENCE`|指定首选的运行时将设置，但不是实际启动。|  
|`STARTUP_SERVER_GC`|指定将使用服务器垃圾回收。|  
|`STARTUP_HOARD_GC_VM`|指定垃圾回收，将保留使用的虚拟地址。|  
|`STARTUP_SINGLE_VERSION_HOSTING_INTERFACE`|指定，将不会允许混合使用托管接口。|  
|`STARTUP_LEGACY_IMPERSONATION`|指定模拟应不流经异步点默认情况下。|  
|`STARTUP_DISABLE_COMMITTHREADSTACK`|指定在线程开始运行时不应提交完整线程堆栈。|  
|`STARTUP_ALWAYSFLOW_IMPERSONATION`|指定托管的模拟并通过平台来实现的模拟调用将流经异步点。 默认情况下，仅托管的模拟将流经异步点。|  
|`STARTUP_TRIM_GC_COMMIT`|指定当系统内存不足时，垃圾回收会占用较少的提交空间。 请参阅`gcTrimCommitOnLowMemory`中[针对共享的 Web 承载优化](../../../../docs/standard/garbage-collection/optimization-for-shared-web-hosting.md)。|  
|`STARTUP_ETW`|指定启用公共语言运行时事件的事件跟踪的 Windows (ETW)。 从 Windows Vista 开始，事件是始终启用跟踪，因此此标志无效。 请参阅[控制.NET Framework 日志记录](../../../../docs/framework/performance/controlling-logging.md)。|  
|`STARTUP_ARM`|指定启用应用程序域资源监视。 请参阅<xref:System.AppDomain.MonitoringIsEnabled%2A?displayProperty=nameWithType>属性和[ \<appDomainResourceMonitoring > 元素](../../../../docs/framework/configure-apps/file-schema/runtime/appdomainresourcemonitoring-element.md)。|  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** MSCorEE.h  
  
 **库：** MSCorEE.dll  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [承载枚举](../../../../docs/framework/unmanaged-api/hosting/hosting-enumerations.md)
