---
title: ICorDebugDataTarget 接口
ms.date: 03/30/2017
api_name:
- ICorDebugDataTarget
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugDataTarget
helpviewer_keywords:
- ICorDebugDataTarget interface [.NET Framework debugging]
ms.assetid: df5f05be-bed7-4f3c-bc89-dbb435d79a0b
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 53c054b59376a78eda83181e75aec94548e92f17
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54499812"
---
# <a name="icordebugdatatarget-interface"></a>ICorDebugDataTarget 接口
提供一个回调接口，该接口可提供对特定目标进程的访问。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[GetPlatform 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugdatatarget-getplatform-method.md)|提供有关平台，包括处理器体系结构和操作系统，目标进程正在其运行的信息。|  
|[ReadVirtual 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugdatatarget-readvirtual-method.md)|获取从指定地址处开始的连续内存块，并返回它所提供的缓冲区中。|  
|[GetThreadContext 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugdatatarget-getthreadcontext-method.md)|请求对指定线程的当前线程上下文。|  
  
## <a name="remarks"></a>备注  
 `ICorDebugDataTarget` 其方法具有以下特征：  
  
-   调试服务对此接口来访问内存和其他数据目标进程中的调用方法。  
  
-   调试器客户端必须实现此接口作为适用于特定目标 （例如，实时进程或内存转储）。  
  
-   `ICorDebugDataTarget`方法可以实现其他的方法内调用只能从`ICorDebug*`接口。 这可确保调试器客户端已通过哪个线程调用，以及何时进行控制。  
  
-   `ICorDebugDataTarget`实现必须始终返回有关目标的最新信息。  
  
 目标进程应停止，并以任何方式时不更改`ICorDebug*`接口 (并因此`ICorDebugDataTarget`方法) 正被调用。 如果目标是将其状态更改，并实时过程[iclrdebugging:: Openvirtualprocess](../../../../docs/framework/unmanaged-api/debugging/iclrdebugging-openvirtualprocess-method.md)方法必须再次调用以提供替换 ICorDebugProcess 实例。  
  
> [!NOTE]
>  此接口不支持跨计算机或跨进程远程调用。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [调试接口](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
- [调试](../../../../docs/framework/unmanaged-api/debugging/index.md)
