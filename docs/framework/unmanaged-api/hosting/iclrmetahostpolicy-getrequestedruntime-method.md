---
title: ICLRMetaHostPolicy::GetRequestedRuntime 方法
ms.date: 03/30/2017
api_name:
- ICLRMetaHostPolicy.GetRequestedRuntime
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRMetaHostPolicy::GetRequestedRuntime
helpviewer_keywords:
- GetRequestedRuntime method [.NET Framework hosting]
- ICLRMetaHostPolicy::GetRequestedRuntime method [.NET Framework hosting]
ms.assetid: 59ec1832-9cc1-4b5c-983d-03407e51de56
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 73d5c98500c510630b1f8d6081b654a6dbd88a5b
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57501690"
---
# <a name="iclrmetahostpolicygetrequestedruntime-method"></a>ICLRMetaHostPolicy::GetRequestedRuntime 方法

提供基于宿主策略、托管程序集、版本字符串和配置流的公共语言运行时 (CLR) 的首选版本的接口。 此方法不会真正加载或激活 CLR，而只是返回[ICLRRuntimeInfo](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-interface.md)表示策略结果的接口。 此方法取代[GetRequestedRuntimeInfo](../../../../docs/framework/unmanaged-api/hosting/getrequestedruntimeinfo-function.md)， [GetRequestedRuntimeVersion](../../../../docs/framework/unmanaged-api/hosting/getrequestedruntimeversion-function.md)， [CorBindToRuntimeHost](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimehost-function.md)， [CorBindToRuntimeByCfg](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimebycfg-function.md)，并[GetCORRequiredVersion](../../../../docs/framework/unmanaged-api/hosting/getcorrequiredversion-function.md)方法。

## <a name="syntax"></a>语法

```cpp
HRESULT GetRequestedRuntime(
    [in]  METAHOST_POLICY_FLAGS dwPolicyFlags,
    [in]  LPCWSTR pwzBinary,
    [in]  IStream *pCfgStream,
    [in, out, size_is(*pcchVersion)] LPWSTR pwzVersion,
    [in, out]  DWORD *pcchVersion,
    [out, size_is(*pcchImageVersion)] LPWSTR pwzImageVersion,
    [in, out]  DWORD *pcchImageVersion,
    [out] DWORD *pdwConfigFlags,
    [in]  REFIID  riid
    [out, iid_is(riid), retval] LPVOID *ppRuntime);
```

## <a name="parameters"></a>参数

|“属性”|描述|
|----------|-----------------|
|`dwPolicyFlags`|[in] 必需。 指定的成员[METAHOST_POLICY_FLAGS](../../../../docs/framework/unmanaged-api/hosting/metahost-policy-flags-enumeration.md)枚举，表示某个绑定策略，以及任意数量的修饰符。 当前可用的策略只有[METAHOST_POLICY_HIGHCOMPAT](../../../../docs/framework/unmanaged-api/hosting/metahost-policy-flags-enumeration.md)。<br /><br /> 修饰符包括[METAHOST_POLICY_EMULATE_EXE_LAUNCH](../../../../docs/framework/unmanaged-api/hosting/metahost-policy-flags-enumeration.md)， [METAHOST_POLICY_APPLY_UPGRADE_POLICY](../../../../docs/framework/unmanaged-api/hosting/metahost-policy-flags-enumeration.md)， [METAHOST_POLICY_SHOW_ERROR_DIALOG](../../../../docs/framework/unmanaged-api/hosting/metahost-policy-flags-enumeration.md)， [METAHOST_POLICY_USE_PROCESS_IMAGE_PATH](../../../../docs/framework/unmanaged-api/hosting/metahost-policy-flags-enumeration.md)，并[METAHOST_POLICY_ENSURE_SKU_SUPPORTED](../../../../docs/framework/unmanaged-api/hosting/metahost-policy-flags-enumeration.md)。|
|`pwzBinary`|[in] 可选。 指定程序集文件路径。|
|`pCfgStream`|[in] 可选。 指定配置文件作为 <xref:System.Runtime.InteropServices.ComTypes.IStream?displayProperty=nameWithType>。|
|`pwzVersion`|[in, out] 可选。 指定或返回要加载的首选 CLR 版本。|
|`pcchVersion`|[in, out] 必需。 输入时指定 `pwzVersion` 的预期的大小，以避免缓冲区溢出。 如果 `pwzVersion` 为 null，则当 `GetRequestedRuntime` 返回时，`pcchVersion` 包含 `pwzVersion` 的预期的大小以允许预分配；否则为 `pcchVersion` 包含写入 `pwzVersion` 的字符数量。|
|`pwzImageVersion`|[out] 可选。 当`GetRequestedRuntime`返回，则包含 CLR 版本对应于[ICLRRuntimeInfo](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-interface.md)返回的接口。|
|`pcchImageVersion`|[in, out] 可选。 输入时指定 `pwzImageVersion` 的预期的大小以避免缓冲区溢出。 如果 `pwzImageVersion` 为 null，则当 `GetRequestedRuntime` 返回时，`pcchImageVersion` 包含 `pwzImageVersion` 的所需大小，以允许预分配。|
|`pdwConfigFlags`|[out] 可选。 如果`GetRequestedRuntime`时返回，在绑定过程中，使用配置文件`pdwConfigFlags`包含[METAHOST_CONFIG_FLAGS](../../../../docs/framework/unmanaged-api/hosting/metahost-config-flags-enumeration.md)值，该值指示是否[\<启动 >](../../../../docs/framework/configure-apps/file-schema/startup/startup-element.md)元素具有`useLegacyV2RuntimeActivationPolicy`属性集以及属性的值。 将应用[METAHOST_CONFIG_FLAGS_LEGACY_V2_ACTIVATION_POLICY_MASK](../../../../docs/framework/unmanaged-api/hosting/metahost-config-flags-enumeration.md)屏蔽到`pdwConfigFlags`若要获取这些值与相关`useLegacyV2RuntimeActivationPolicy`。|
|`riid`|[in]指定请求的接口标识符 IID_ICLRRuntimeInfo [ICLRRuntimeInfo](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-interface.md)接口。|
|`ppRuntime`|[out]当`GetRequestedRuntime`返回，包含指向相应[ICLRRuntimeInfo](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-interface.md)接口。|

## <a name="remarks"></a>备注

如果此方法成功，当且仅当一个或多个以下元素存在于 `<configuration><runtime>` 部分内的配置流中时，该方法具有将其他标志与返回运行时接口的当前默认启动标志结合的副作用：

- `<gcServer enabled="true"/>` 导致 `STARTUP_SERVER_GC` 将被设置。

- `<etwEnable enabled="true"/>` 导致 `STARTUP_ETW` 将被设置。

- `<appDomainResourceMonitoring enabled="true"/>` 导致 `STARTUP_ARM` 将被设置。

产生的默认 `STARTUP_FLAGS` 值是从前述列表设置的值与默认启动标志的按位“或”组合。

## <a name="return-value"></a>返回值

此方法返回以下特定 HRESULT 以及表示方法失败的 HRESULT 错误。

|HRESULT|描述|
|-------------|-----------------|
|S_OK|该方法已成功完成。|
|E_POINTER|`pwzVersion` 不为 null 且 `pcchVersion` 为 null。<br /><br /> 或<br /><br /> `pwzImageVersion` 不为 null 且 `pcchImageVersion` 为 null。|
|E_INVALIDARG|`dwPolicyFlags` 未指定 `METAHOST_POLICY_HIGHCOMPAT`。|
|ERROR_INSUFFICIENT_BUFFER|分配给 `pwzVersion` 的内存不足。<br /><br /> 或<br /><br /> 分配给 `pwzImageVersion` 的内存不足。|
|CLR_E_SHIM_RUNTIMELOAD|`dwPolicyFlags` 包括 METAHOST_POLICY_APPLY_UPGRADE_POLICY，并且 `pwzVersion` 和 `pcchVersion` 均为 null。|

## <a name="requirements"></a>要求

**平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。

**标头：** MetaHost.h

**库：** 包含为 MSCorEE.dll 中的资源

**.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]

## <a name="see-also"></a>请参阅

- [ICLRMetaHostPolicy 接口](../../../../docs/framework/unmanaged-api/hosting/iclrmetahostpolicy-interface.md)
- [.NET Framework 4 和 4.5 中添加的 CLR 承载接口](../../../../docs/framework/unmanaged-api/hosting/clr-hosting-interfaces-added-in-the-net-framework-4-and-4-5.md)
- [承载接口](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
- [承载](../../../../docs/framework/unmanaged-api/hosting/index.md)
