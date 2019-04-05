---
title: IDefinitionIdentity 接口
ms.date: 03/30/2017
api_name:
- IDefinitionIdentity
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- IDefinitionIdentity
helpviewer_keywords:
- IDefinitionIdentity interface [.NET Framework fusion]
ms.assetid: ce5ba888-5fbe-4efd-91cf-f0ff94d8428b
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: fb97c545d2d57ef589b5a7a5b3618eaa2b6f364f
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54686993"
---
# <a name="idefinitionidentity-interface"></a>IDefinitionIdentity 接口
表示在当前范围内定义的应用程序的代码的唯一签名。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|`IDefinitionIdentity::Clone`|为新获取的接口指针`IDefinitionIdentity`对象，它等同于此`IDefinitionIdentity`，除了指定的属性更改。|  
|`IDefinitionIdentity::EnumAttributes`|获取到的接口指针[IEnumIDENTITY_ATTRIBUTE](../../../../docs/framework/unmanaged-api/fusion/ienumidentity-attribute-interface.md)对象，其中包含与此相关联的属性`IDefinitionIdentity`。|  
|`IDefinitionIdentity::GetAttribute`|获取具有指定名称的属性的值中指定的命名空间。|  
|`IDefinitionIdentity::SetAttribute`|设置为指定的值指定的命名空间中具有指定的名称的特性。|  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** Isolation.h  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [合成接口](../../../../docs/framework/unmanaged-api/fusion/fusion-interfaces.md)
