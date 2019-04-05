---
title: CorSerializationType 枚举
ms.date: 03/30/2017
api_name:
- CorSerializationType
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorSerializationType
helpviewer_keywords:
- CorSerializationType enumeration [.NET Framework metadata]
ms.assetid: 6b1fcd11-c7fb-4be2-8910-abc862d4caf4
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 70d2d4ed0d2b923b1095fd0ce898330c319fa5cf
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54637367"
---
# <a name="corserializationtype-enumeration"></a>CorSerializationType 枚举
指定公共语言运行时如何序列化对象。  
  
## <a name="syntax"></a>语法  
  
```  
typedef enum CorSerializationType {  
  
    SERIALIZATION_TYPE_UNDEFINED     = 0,  
    SERIALIZATION_TYPE_BOOLEAN       = ELEMENT_TYPE_BOOLEAN,  
    SERIALIZATION_TYPE_CHAR          = ELEMENT_TYPE_CHAR,  
    SERIALIZATION_TYPE_I1            = ELEMENT_TYPE_I1,  
    SERIALIZATION_TYPE_U1            = ELEMENT_TYPE_U1,  
    SERIALIZATION_TYPE_I2            = ELEMENT_TYPE_I2,  
    SERIALIZATION_TYPE_U2            = ELEMENT_TYPE_U2,  
    SERIALIZATION_TYPE_I4            = ELEMENT_TYPE_I4,  
    SERIALIZATION_TYPE_U4            = ELEMENT_TYPE_U4,  
    SERIALIZATION_TYPE_I8            = ELEMENT_TYPE_I8,  
    SERIALIZATION_TYPE_U8            = ELEMENT_TYPE_U8,  
    SERIALIZATION_TYPE_R4            = ELEMENT_TYPE_R4,  
    SERIALIZATION_TYPE_R8            = ELEMENT_TYPE_R8,  
    SERIALIZATION_TYPE_STRING        = ELEMENT_TYPE_STRING,  
    SERIALIZATION_TYPE_SZARRAY       = ELEMENT_TYPE_SZARRAY,  
    SERIALIZATION_TYPE_TYPE          = 0x50,  
    SERIALIZATION_TYPE_TAGGED_OBJECT = 0x51,  
    SERIALIZATION_TYPE_FIELD         = 0x53,  
    SERIALIZATION_TYPE_PROPERTY      = 0x54,  
    SERIALIZATION_TYPE_ENUM          = 0x55  
  
} CorSerializationType;  
```  
  
## <a name="members"></a>成员  
  
|成员|描述|  
|------------|-----------------|  
|`SERIALIZATION_TYPE_UNDEFINED`|序列化的对象是未定义。|  
|`SERIALIZATION_TYPE_BOOLEAN`|将对象序列化为布尔值类型|  
|`SERIALIZATION_TYPE_CHAR`|将对象序列化为字符类型。|  
|`SERIALIZATION_TYPE_I1`|对象序列化为 1 字节有符号整数。|  
|`SERIALIZATION_TYPE_U1`|对象序列化为 1 字节无符号整数。|  
|`SERIALIZATION_TYPE_I2`|对象序列化为 2 字节有符号整数。|  
|`SERIALIZATION_TYPE_U2`|对象序列化为 2 字节无符号整数。|  
|`SERIALIZATION_TYPE_I4`|对象序列化为 4 字节有符号整数。|  
|`SERIALIZATION_TYPE_U4`|对象序列化为 4 字节无符号整数。|  
|`SERIALIZATION_TYPE_I8`|对象序列化为 8 字节有符号整数。|  
|`SERIALIZATION_TYPE_U8`|对象序列化为一个无符号的 8 字节整数。|  
|`SERIALIZATION_TYPE_R4`|将对象序列化为 4 字节浮点数。|  
|`SERIALIZATION_TYPE_R8`|将对象序列化为 8 字节浮点数。|  
|`SERIALIZATION_TYPE_STRING`|将对象序列化为 System.String 类型。|  
|`SERIALIZATION_TYPE_SZARRAY`|将对象序列化为一维，零的下限的数组。|  
|`SERIALIZATION_TYPE_TYPE`|将对象序列化为泛型类型。|  
|`SERIALIZATION_TYPE_TAGGED_OBJECT`|将对象序列化为一个标记对象。|  
|`SERIALIZATION_TYPE_FIELD`|将对象序列化为一个字段。|  
|`SERIALIZATION_TYPE_PROPERTY`|将对象序列化为一个属性。|  
|`SERIALIZATION_TYPE_ENUM`|将对象序列化为一个枚举。|  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorHdr.h  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [Metadata 枚举](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
