---
title: EClrEvent 枚举
ms.date: 03/30/2017
api_name:
- EClrEvent
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- EClrEvent
helpviewer_keywords:
- EClrEvent enumeration [.NET Framework hosting]
ms.assetid: 7c36a7c2-75a2-4971-bc23-abf54c812154
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d66e010340d186eed2222ae2ba8cfb24b8e8d7b0
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54658567"
---
# <a name="eclrevent-enumeration"></a>EClrEvent 枚举
描述主机可为其注册回调的公共语言运行时 (CLR) 事件。  
  
## <a name="syntax"></a>语法  
  
```  
typedef enum {  
    Event_ClrDisabled,  
    Event_DomainUnload,  
    Event_MDAFired,  
    Event_StackOverflow  
} EClrEvent;  
```  
  
## <a name="members"></a>成员  
  
|成员|描述|  
|------------|-----------------|  
|`Event_ClrDisabled`|指定错误的 CLR。|  
|`Event_DomainUnload`|指定卸载特定<xref:System.AppDomain>。|  
|`Event_MDAFired`|指定已生成的托管调试助手 (MDA) 消息。|  
|`Event_StackOverflow`|指定已发生堆栈溢出错误。|  
  
## <a name="remarks"></a>备注  
 宿主可以注册任何所描述的事件类型的回调`EClrEvent`通过调用的方法[ICLROnEventManager](../../../../docs/framework/unmanaged-api/hosting/iclroneventmanager-interface.md)接口。 主机通过调用此接口获取指向[iclrcontrol:: Getclrmanager](../../../../docs/framework/unmanaged-api/hosting/iclrcontrol-getclrmanager-method.md)方法。  
  
 `Event_CLRDisabled`和`Event_DomainUnload`不止一次和来自不同线程发出信号卸载或禁用 CLR 可以引发事件。  
  
 `Event_MDAFired`事件引发的创建[MDAInfo](../../../../docs/framework/unmanaged-api/hosting/mdainfo-structure.md)实例，它包含 MDA 消息的详细信息。 Mda 的详细信息，请参阅[使用托管调试助手诊断错误](../../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** MSCorEE.h  
  
 **库：** MSCorEE.dll  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [IActionOnCLREvent 接口](../../../../docs/framework/unmanaged-api/hosting/iactiononclrevent-interface.md)
- [ICLRControl 接口](../../../../docs/framework/unmanaged-api/hosting/iclrcontrol-interface.md)
- [承载枚举](../../../../docs/framework/unmanaged-api/hosting/hosting-enumerations.md)
