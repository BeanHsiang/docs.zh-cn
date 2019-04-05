---
title: IReferenceAppId 接口
ms.date: 03/30/2017
api_name:
- IReferenceAppId
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- IReferenceAppId
helpviewer_keywords:
- IReferenceAppId interface [.NET Framework fusion]
ms.assetid: 8eb9e565-f358-43ce-900e-a8f8a5aa6cfb
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2289a9a75311c9642a764844ee466adcc5838655
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54744344"
---
# <a name="ireferenceappid-interface"></a>IReferenceAppId 接口
表示为当前作用域中的应用程序的唯一标识符的引用。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|`IReferenceAppId::get_CodeBase`|获取此引用的应用程序的指针的代码标识符的字符串表示形式`IReferenceAppId`。|  
|`IReferenceAppId::put_CodeBase`|设置此引用的应用程序的代码标识符`IReferenceAppId`。|  
|`IReferenceAppId::EnumAppPath`|获取到的接口指针`IEnumReferenceIdentity`实例，包含`IReferenceIdentity`表示此成员的实例`IReferenceAppId`。|  
|`IReferenceAppId::get_SubscriptionId`|获取一个指针指向的标记标识符的字符串表示形式与此订阅`IReferenceAppId`。|  
|`IReferenceAppId::put_SubscriptionId`|设置与此订阅的标记标识符`IReferenceAppId`到指定的字符串值。|  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** Isolation.h  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [合成接口](../../../../docs/framework/unmanaged-api/fusion/fusion-interfaces.md)
- [IEnumReferenceIdentity 接口](../../../../docs/framework/unmanaged-api/fusion/ienumreferenceidentity-interface.md)
- [IReferenceIdentity 接口](../../../../docs/framework/unmanaged-api/fusion/ireferenceidentity-interface.md)
