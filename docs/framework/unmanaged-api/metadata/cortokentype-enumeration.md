---
title: CorTokenType 枚举
ms.date: 03/30/2017
api_name:
- CorTokenType
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorTokenType
helpviewer_keywords:
- CorTokenType enumeration [.NET Framework metadata]
ms.assetid: 93c9a369-225f-4eff-9b78-3fbee4902cf1
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 9cc480d673648562638fbfd4a03df643dd734b9d
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54620612"
---
# <a name="cortokentype-enumeration"></a>CorTokenType 枚举
指示元数据标记的类型。  
  
## <a name="syntax"></a>语法  
  
```  
typedef enum CorTokenType {  
  
    mdtModule                       = 0x00000000,  
    mdtTypeRef                      = 0x01000000,  
    mdtTypeDef                      = 0x02000000,  
    mdtFieldDef                     = 0x04000000,  
    mdtMethodDef                    = 0x06000000,  
    mdtParamDef                     = 0x08000000,  
    mdtInterfaceImpl                = 0x09000000,  
    mdtMemberRef                    = 0x0a000000,  
    mdtCustomAttribute              = 0x0c000000,  
    mdtPermission                   = 0x0e000000,  
    mdtSignature                    = 0x11000000,  
    mdtEvent                        = 0x14000000,  
    mdtProperty                     = 0x17000000,  
    mdtModuleRef                    = 0x1a000000,  
    mdtTypeSpec                     = 0x1b000000,  
    mdtAssembly                     = 0x20000000,  
    mdtAssemblyRef                  = 0x23000000,  
    mdtFile                         = 0x26000000,  
    mdtExportedType                 = 0x27000000,  
    mdtManifestResource             = 0x28000000,  
    mdtGenericParam                 = 0x2a000000,  
    mdtMethodSpec                   = 0x2b000000,  
    mdtGenericParamConstraint       = 0x2c000000,  
    mdtString                       = 0x70000000,  
    mdtName                         = 0x71000000,  
    mdtBaseType                     = 0x72000000  
  
} CorTokenType;  
```  
  
## <a name="members"></a>成员  
  
|成员|描述|  
|------------|-----------------|  
|`mdtModule`|`mdModule`令牌。|  
|`mdtTypeRef`|`mdTypeRef`令牌。|  
|`mdtTypeDef`|`mdTypeDef`令牌。|  
|`mdtFieldDef`|`mdFieldDef`令牌。|  
|`mdtMethodDef`|`mdMethodDef`令牌。|  
|`mdtParamDef`|`mdParamDef`令牌。|  
|`mdtInterfaceImpl`|`mdInterfaceImpl`令牌。|  
|`mdtMemberRef`|`mdMemberRef`令牌。|  
|`mdtCustomAttribute`|`mdCustomAttribute`令牌。|  
|`mdtPermission`|`mdPermission`令牌。|  
|`mdtSignature`|`mdSignature`令牌。|  
|`mdtEvent`|`mdEvent`令牌。|  
|`mdtProperty`|`mdProperty`令牌。|  
|`mdtModuleRef`|`mdModuleRef`令牌。|  
|`mdtTypeSpec`|`mdTypeSpec`令牌。|  
|`mdtAssembly`|`mdAssembly`令牌。|  
|`mdtAssemblyRef`|`mdAssemblyRef`令牌。|  
|`mdtFile`|`mdFile`令牌。|  
|`mdtExportedType`|`mdExportedType`令牌。|  
|`mdtManifestResource`|`mdManifestResource`令牌。|  
|`mdtGenericParam`|`mdGenericParam`令牌。|  
|`mdtMethodSpec`|`mdMethodSpec`令牌。|  
|`mdtGenericParamConstraint`|`mdGenericParamConstraint`令牌。|  
|`mdtString`|`mdString`令牌。|  
|`mdtName`|`mdName`令牌。|  
|`mdtBaseType`|未使用。|  
  
## <a name="remarks"></a>备注  
 每个值是相应的元数据令牌中的最高位字节的值相等。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorHdr.h  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [Metadata 枚举](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
