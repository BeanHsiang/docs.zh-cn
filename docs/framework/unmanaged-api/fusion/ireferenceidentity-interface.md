---
title: IReferenceIdentity 接口
ms.date: 03/30/2017
api_name:
- IReferenceIdentity
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- IReferenceIdentity
helpviewer_keywords:
- IReferenceIdentity interface [.NET Framework fusion]
ms.assetid: 9180ac5a-7019-4716-9f83-8a91d157239a
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: bb8686342b20bd6afe0a4c4803d64428ed95c98b
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54665768"
---
# <a name="ireferenceidentity-interface"></a>IReferenceIdentity 接口
表示代码对象的唯一签名的引用。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|`IReferenceIdentity::Clone`|为新获取的接口指针`IReferenceIdentity`是否与此实例`IReferenceIdentity`，除了指定的属性更改。|  
|`IReferenceIdentity::EnumAttributes`|获取到的接口指针`IEnumIDENTITY_ATTRIBUTE`实例，它包含与此相关联的属性`IReferenceIdentity`。|  
|`IReferenceIdentity::GetAttribute`|获取具有指定名称的指定命名空间中的属性的值。|  
|`IReferenceIdentity::SetAttribute`|设置具有指定的命名空间和指定的值将指定的名称的特性。|  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** Isolation.h  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [合成接口](../../../../docs/framework/unmanaged-api/fusion/fusion-interfaces.md)
- [IEnumIDENTITY_ATTRIBUTE 接口](../../../../docs/framework/unmanaged-api/fusion/ienumidentity-attribute-interface.md)
