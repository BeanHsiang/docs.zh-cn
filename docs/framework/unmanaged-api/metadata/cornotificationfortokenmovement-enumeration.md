---
title: CorNotificationForTokenMovement 枚举
ms.date: 03/30/2017
api_name:
- CorNotificationForTokenMovement
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorNotificationForTokenMovement
helpviewer_keywords:
- CorNotificationForTokenMovement enumeration [.NET Framework metadata]
ms.assetid: 1edd1670-976a-4fc8-bef7-7c41e60ad989
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 745ba18fd1a36789f06bcd3dd4d183c9b28b9875
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54650101"
---
# <a name="cornotificationfortokenmovement-enumeration"></a>CorNotificationForTokenMovement 枚举
指定标记重新映射发生时将发送到元数据 API 客户端的通知。  
  
## <a name="syntax"></a>语法  
  
```  
typedef enum CorNotificationForTokenMovement {  
  
    MDNotifyDefault             = 0x0000000f,  
    MDNotifyAll                 = 0xffffffff,  
    MDNotifyNone                = 0x00000000,  
    MDNotifyMethodDef           = 0x00000001,  
    MDNotifyMemberRef           = 0x00000002,  
    MDNotifyFieldDef            = 0x00000004,  
    MDNotifyTypeRef             = 0x00000008,  
  
    MDNotifyTypeDef             = 0x00000010,  
    MDNotifyParamDef            = 0x00000020,  
    MDNotifyInterfaceImpl       = 0x00000040,  
    MDNotifyProperty            = 0x00000080,  
    MDNotifyEvent               = 0x00000100,  
    MDNotifySignature           = 0x00000200,  
    MDNotifyTypeSpec            = 0x00000400,  
    MDNotifyCustomAttribute     = 0x00000800,  
    MDNotifySecurityValue       = 0x00001000,  
    MDNotifyPermission          = 0x00002000,  
    MDNotifyModuleRef           = 0x00004000,  
  
    MDNotifyNameSpace           = 0x00008000,  
  
    MDNotifyAssemblyRef         = 0x01000000,  
    MDNotifyFile                = 0x02000000,  
    MDNotifyExportedType        = 0x04000000,  
    MDNotifyResource            = 0x08000000  
  
} CorNotificationForTokenMovement;  
```  
  
## <a name="members"></a>成员  
  
|成员|描述|  
|------------|-----------------|  
|`MDNotifyDefault`|通知时间`mdTypeRef`， `mdMethodDef`， `mdMemberRef`，或`mdFieldDef`令牌移动。|  
|`MDNotifyAll`|在任何标记移动时通知。|  
|`MDNotifyNone`|不会通知标记移动时。|  
|`MDNotifyMethodDef`|通知时间`mdMethodDef`标记移动。|  
|`MDNotifyMemberRef`|通知时间`mdMemberRef`标记移动。|  
|`MDNotifyFieldDef`|通知时间`mdFieldDef`标记移动。|  
|`MDNotifyTypeRef`|通知时间`mdTypeRef`标记移动。|  
|`MDNotifyTypeDef`|通知时间`mdTypeDef`标记移动。|  
|`MDNotifyParamDef`|通知时间`mdParamDef`标记移动。|  
|`MDNotifyInterfaceImpl`|通知时间`mdInterfaceImpl`标记移动。|  
|`MDNotifyProperty`|通知时间`mdProperty`标记移动。|  
|`MDNotifyEvent`|通知时间`mdEvent`标记移动。|  
|`MDNotifySignature`|通知时间`mdSignature`标记移动。|  
|`MDNotifyTypeSpec`|通知时间`mdTypeSpec`标记移动。|  
|`MDNotifyCustomAttribute`|通知时间`mdCustomAttribute`标记移动。|  
|`MDNotifySecurityValue`|通知时间`mdSecurityValue`标记移动。|  
|`MDNotifyPermission`|通知时间`mdPermission`标记移动。|  
|`MDNotifyModuleRef`|通知时间`mdModuleRef`标记移动。|  
|`MDNotifyNameSpace`|通知时间`mdNameSpace`标记移动。|  
|`MDNotifyAssemblyRef`|通知时间`mdAssemblyRef`标记移动。|  
|`MDNotifyFile`|通知时间`mdFile`标记移动。|  
|`MDNotifyExportedType`|通知时间`mdExportedType`标记移动。|  
|`MDNotifyResource`|通知时间`mdManifestResource`标记移动。|  
  
## <a name="remarks"></a>备注  
 令牌可能会重新映射 （即移动） 期间元数据合并。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorHdr.h  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [Metadata 枚举](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
