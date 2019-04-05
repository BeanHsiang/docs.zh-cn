---
title: CorGenericParamAttr 枚举
ms.date: 03/30/2017
api_name:
- CorGenericParamAttr
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorGenericParamAttr
helpviewer_keywords:
- CorGenericParamAttr enumeration [.NET Framework metadata]
ms.assetid: 36c76266-71d8-48dc-bd89-54943fa659c1
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: cf73f382c1da15e0285ee95be9e8bce39575ae0a
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54557353"
---
# <a name="corgenericparamattr-enumeration"></a>CorGenericParamAttr 枚举
包含值，用于描述<xref:System.Type>泛型类型，作为调用中使用参数[IMetaDataEmit2::DefineGenericParam](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-definegenericparam-method.md)。  
  
## <a name="syntax"></a>语法  
  
```  
typedef enum CorGenericParamAttr {  
  
    gpVarianceMask                     =   0x0003,  
    gpNonVariant                       =   0x0000,   
    gpCovariant                        =   0x0001,  
    gpContravariant                    =   0x0002,  
  
    gpSpecialConstraintMask            =   0x001C,  
    gpNoSpecialConstraint              =   0x0000,  
    gpReferenceTypeConstraint          =   0x0004,   
    gpNotNullableValueTypeConstraint   =   0x0008,  
    gpDefaultConstructorConstraint     =   0x0010  
  
} CorGenericParamAttr;  
```  
  
## <a name="members"></a>成员  
  
|成员|描述|  
|------------|-----------------|  
|`gpVarianceMask`|参数的变体仅应用于接口和委托的泛型参数。|  
|`gpNonVariant`|表示不存在的方差。|  
|`gpCovariant`|指示协方差。|  
|`gpContravariant`|指示逆变。|  
|`gpSpecialConstraintMask`|可以将特殊约束应用于任何<xref:System.Type>参数。|  
|`gpNoSpecialConstraint`|指示没有约束应用于<xref:System.Type>参数。|  
|`gpReferenceTypeConstraint`|指示<xref:System.Type>参数必须是引用类型。|  
|`gpNotNullableValueTypeConstraint`|指示<xref:System.Type>参数必须是值类型，不能为 null 值。|  
|`gpDefaultConstructorConstraint`|指示<xref:System.Type>参数必须具有不带参数的默认公共构造函数。|  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorHdr.h  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [Metadata 枚举](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
