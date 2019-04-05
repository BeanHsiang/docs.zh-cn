---
title: IHostAssemblyStore 接口
ms.date: 03/30/2017
api_name:
- IHostAssemblyStore
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostAssemblyStore
helpviewer_keywords:
- IHostAssemblyStore interface [.NET Framework hosting]
ms.assetid: cccb650f-abe0-41e2-9fd1-b383788eb1f6
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d3714f31d0ab58584a8671055cf4c607f04a832c
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54611054"
---
# <a name="ihostassemblystore-interface"></a>IHostAssemblyStore 接口
提供允许主机以加载程序集和模块独立于公共语言运行时 (CLR) 的方法。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[ProvideAssembly 方法](../../../../docs/framework/unmanaged-api/hosting/ihostassemblystore-provideassembly-method.md)|获取未被引用程序集的引用[ICLRAssemblyReferenceList](../../../../docs/framework/unmanaged-api/hosting/iclrassemblyreferencelist-interface.md)从调用返回[ihostassemblymanager:: Getnonhoststoreassemblies](../../../../docs/framework/unmanaged-api/hosting/ihostassemblymanager-getnonhoststoreassemblies-method.md)。|  
|[ProvideModule 方法](../../../../docs/framework/unmanaged-api/hosting/ihostassemblystore-providemodule-method.md)|解析程序集或链接 （而不是嵌入） 的资源文件中的模块。|  
  
## <a name="remarks"></a>备注  
 `IHostAssemblyStore` 提供一个主机来加载程序集有效地基于程序集标识的方法。 主机加载程序集通过返回`IStream`直接指向字节的实例。  
  
 CLR 确定主机是否已实现`IHostAssemblyStore`通过调用`IHostAssemblyManager::GetNonHostAssemblyStores`初始化时。 这样该主机，例如，控件绑定到用户程序集，而是依赖于要绑定到.NET Framework 程序集的运行时。  
  
> [!NOTE]
>  在提供的实现`IHostAssemblyStore`，该主机指定若要解决所有未被引用的程序集其意图`ICLRAssemblyReferenceList`从返回`IHostAssemblyManager::GetNonHostStoreAssemblies`。  
  
> [!NOTE]
>  .NET Framework 2.0 版不提供主机加载本机映像程序集的一种方法提供的[本机映像生成器 (Ngen.exe)](../../../../docs/framework/tools/ngen-exe-native-image-generator.md)实用程序。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** MSCorEE.h  
  
 **库：** 包含为 MSCorEE.dll 中的资源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [ICLRAssemblyReferenceList 接口](../../../../docs/framework/unmanaged-api/hosting/iclrassemblyreferencelist-interface.md)
- [IHostAssemblyManager 接口](../../../../docs/framework/unmanaged-api/hosting/ihostassemblymanager-interface.md)
- [承载接口](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
