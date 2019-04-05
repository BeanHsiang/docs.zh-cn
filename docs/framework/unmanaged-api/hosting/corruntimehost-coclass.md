---
title: CorRuntimeHost 组件类
ms.date: 03/30/2017
api_name:
- CorRuntimeHost Coclass
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorRuntimeHost
helpviewer_keywords:
- CoRuntimeHost coclass [.NET Framework hosting]
ms.assetid: 5833740b-7d67-44b4-865c-b5bf45e291e3
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7c81a39acee31986421c810e2814a4f7e6c4d970
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54597523"
---
# <a name="corruntimehost-coclass"></a>CorRuntimeHost 组件类
提供用于管理应用程序正在执行公共语言运行时的接口。  
  
## <a name="syntax"></a>语法  
  
```  
coclass CorRuntimeHost {  
    [default] interface ICorRuntimeHost;  
    interface IGCHost;  
    interface ICorConfiguration;  
    interface IValidator;  
    interface IDebuggerInfo;  
};  
```  
  
## <a name="interfaces"></a>接口  
  
|接口|描述|  
|---------------|-----------------|  
|[ICorConfiguration 接口](../../../../docs/framework/unmanaged-api/hosting/icorconfiguration-interface.md)|提供用于配置公共语言运行时 (CLR) 方法。|  
|[ICorRuntimeHost 接口](../../../../docs/framework/unmanaged-api/hosting/icorruntimehost-interface.md)|提供了使宿主能够显式启动和停止公共语言运行时，若要创建和配置应用程序域，若要访问默认域，并要枚举的进程中运行的所有域的方法。|  
|[IDebuggerInfo 接口](../../../../docs/framework/unmanaged-api/hosting/idebuggerinfo-interface.md)|提供用于获取有关调试的服务的状态信息的方法。|  
|[IGCHost 接口](../../../../docs/framework/unmanaged-api/hosting/igchost-interface.md)|提供方法用于获取有关垃圾回收系统的信息以及用于控制垃圾回收的某些方面。|  
|"IValidator"|提供了用于验证的可移植可执行映像和详细报告验证错误的方法。|  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** MSCorEE.idl  
  
 **库：** 包含为 MSCorEE.dll 中的资源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [承载组件类](../../../../docs/framework/unmanaged-api/hosting/hosting-coclasses.md)
