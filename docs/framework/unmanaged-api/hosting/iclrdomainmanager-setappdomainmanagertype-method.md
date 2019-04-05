---
title: ICLRDomainManager::SetAppDomainManagerType 方法
ms.date: 03/30/2017
api_name:
- ICLRDomainManager.SetAppDomainManagerType
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRDomainManager::SetAppDomainManagerType
helpviewer_keywords:
- SetAppDomainManagerType method, ICLRDomainManager interface [.NET Framework hosting]
- ICLRDomainManager::SetAppDomainManagerType method [.NET Framework hosting]
ms.assetid: ee91abb0-cb74-41dd-927b-e117fb8ffdf4
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 5c2927195b650f1098292f3d59cd887e084aea21
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57490055"
---
# <a name="iclrdomainmanagersetappdomainmanagertype-method"></a>ICLRDomainManager::SetAppDomainManagerType 方法
指定的类型，派生自<xref:System.AppDomainManager?displayProperty=nameWithType>的将用来初始化默认应用程序域的应用程序域管理器类。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT SetAppDomainManagerType(  
    [in] LPCWSTR wszAppDomainManagerAssembly,  
    [in] LPCWSTR wszAppDomainManagerType,  
    [in] EInitializeNewDomainFlags dwInitializeDomainFlags  
);  
```  
  
## <a name="parameters"></a>参数  
 `wszAppDomainManagerAssembly`  
 [in]包含应用程序域管理器类型、 程序集的显示名称例如："AdMgrExample，版本 = 1.0.0.0，区域性 = 中性，PublicKeyToken = 6856bccf150f00b3"。  
  
 `wszAppDomainManagerType`  
 [in]应用程序域管理器，包括命名空间的类型名称。  
  
 `dwInitializeDomainFlags`  
 [in]组合[EInitializeNewDomainFlags](../../../../docs/framework/unmanaged-api/hosting/einitializenewdomainflags-enumeration.md)提供有关应用程序域管理器的信息的枚举值。  
  
## <a name="return-value"></a>返回值  
 此方法返回以下特定 HRESULT 以及表示方法失败的 HRESULT 错误。  
  
|HRESULT|描述|  
|-------------|-----------------|  
|S_OK|该方法已成功完成。|  
|HOST_E_CLRNOTAVAILABLE|公共语言运行时 (CLR) 尚未加载到进程中，或处于不能运行托管的代码或已成功处理调用的状态。|  
  
## <a name="remarks"></a>备注  
 目前，唯一定义的值为`dwInitializeDomainFlags`是`eInitializeNewDomainFlags_NoSecurityChanges`，它将告诉公共语言运行时 (CLR) 的应用程序域管理器的执行期间将不修改安全设置<xref:System.AppDomainManager.InitializeNewDomain%2A?displayProperty=nameWithType>方法。 这样，若要优化的条件性的程序集加载的 CLR <xref:System.Security.AllowPartiallyTrustedCallersAttribute> (APTCA) 特性。 如果此集的程序集的传递闭包很大，这可能导致启动时间得到显著提高。  
  
> [!IMPORTANT]
>  如果指定了主机`eInitializeNewDomainFlags_NoSecurityChanges`应用程序域管理器中，为<xref:System.InvalidOperationException>如果尝试修改应用程序域的安全，将引发。  
  
 调用[iclrcontrol:: Setappdomainmanagertype](../../../../docs/framework/unmanaged-api/hosting/iclrcontrol-setappdomainmanagertype-method.md)方法相当于调用`ICLRDomainManager::SetAppDomainManagerType`与`eInitializeNewDomainFlags_None`。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** MetaHost.h  
  
 **库：** 包含为 MSCorEE.dll 中的资源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [承载](../../../../docs/framework/unmanaged-api/hosting/index.md)
- [ICLRDomainManager 接口](../../../../docs/framework/unmanaged-api/hosting/iclrdomainmanager-interface.md)
- [EInitializeNewDomainFlags 枚举](../../../../docs/framework/unmanaged-api/hosting/einitializenewdomainflags-enumeration.md)
