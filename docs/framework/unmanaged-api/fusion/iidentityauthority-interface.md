---
title: IIdentityAuthority 接口
ms.date: 03/30/2017
api_name:
- IIdentityAuthority
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- IIdentityAuthority
helpviewer_keywords:
- IIdentityAuthority interface [.NET Framework fusion]
ms.assetid: 6277f914-51a8-49be-bec6-52d6d648527d
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 263dc0f9d686440aaa23e359c26db1b4d3d09b1e
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57375958"
---
# <a name="iidentityauthority-interface"></a>IIdentityAuthority 接口

管理代码对象的标识键。

## <a name="methods"></a>方法

|方法|描述|
|------------|-----------------|
|`IIdentityAuthority::AreDefinitionsEqual`|获取一个值，该值指示两个指定[IDefinitionIdentity](../../../../docs/framework/unmanaged-api/fusion/idefinitionidentity-interface.md)实例是否相等。|
|`IIdentityAuthority::AreReferencesEqual`|获取一个值，该值指示两个指定[IReferenceIdentity](../../../../docs/framework/unmanaged-api/fusion/ireferenceidentity-interface.md)实例是否相等。|
|`IIdentityAuthority::AreTextualDefinitionsEqual`|获取一个值，该值指示两个指定的字符串定义标识的表示形式是否相等。|
|`IIdentityAuthority::AreTextualReferencesEqual`|获取一个值，该值指示两个指定的字符串引用标识的表示形式是否相等。|
|`IIdentityAuthority::CreateDefinition`|获取一个指向到新`IDefinitionIdentity`实例，它表示当前作用域中的代码对象。|
|`IIdentityAuthority::CreateReference`|获取一个指向到新`IReferenceIdentity`实例，它表示当前作用域中的代码对象。|
|`IIdentityAuthority::DefinitionToText`|获取指定的带格式的字符串版本`IDefinitionIdentity`。|
|`IIdentityAuthority::DefinitionToTextBuffer`|使用指定的字符串版本填充指定的宽字符缓冲区`IDefinitionIdentity`。|
|`IIdentityAuthority::DoesDefinitionMatchReference`|获取一个值，该值指示是否指定`IDefinitionIdentity`和`IReferenceIdentity`实例引用相同的代码对象。|
|`IIdentityAuthority::DoesTextualDefinitionMatchTextualReference`|获取一个值，该值指示指定的字符串是否引用相同的代码对象。|
|`IIdentityAuthority::GenerateDefinitionKey`|获取一个指针指向新创建的字符串键指定`IDefinitionIdentity`。|
|`IIdentityAuthority::GenerateReferenceKey`|获取一个指针指向新创建的字符串键指定`IReferenceIdentity`。|
|`IIdentityAuthority::HashDefinition`|获取指定的哈希值`IDefinitionIdentity`。|
|`IIdentityAuthority::HashReference`|获取指定的哈希值`IReferenceIdentity`。|
|`IIdentityAuthority::ReferenceToText`|获取指定的带格式的字符串版本`IReferenceIdentity`。|
|`IIdentityAuthority::ReferenceToTextBuffer`|使用指定的字符串版本填充指定的宽字符缓冲区`IReferenceIdentity`。|
|`IIdentityAuthority::TextToDefinition`|获取到的接口指针`IDefinitionIdentity`实例生成指定的格式设置字符串。|
|`IIdentityAuthority::TextToReference`|获取到的接口指针`IReferenceIdentity`实例生成指定的格式设置字符串。|

## <a name="requirements"></a>要求

**平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。

**标头：** Isolation.h

**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]

## <a name="see-also"></a>请参阅

- [合成接口](../../../../docs/framework/unmanaged-api/fusion/fusion-interfaces.md)
