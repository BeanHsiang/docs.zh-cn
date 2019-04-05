---
title: Get 函数 （非托管 API 参考）
description: Get 函数检索指定的属性值。
ms.date: 11/06/2017
api_name:
- Get
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- Get
helpviewer_keywords:
- Get function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7534d760f902f80d42c6c20c57a34d52012997a7
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57369651"
---
# <a name="get-function"></a>Get 函数

检索指定的属性值，如果它存在。

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>语法

```
HRESULT Get (
   [in] int               vFunc, 
   [in] IWbemClassObject* ptr, 
   [in] LPCWSTR           wszName,
   [in] LONG              lFlags,
   [out] VARIANT*         pVal,
   [out] CIMTYPE*         pvtType,
   [out] LONG*            plFlavor
); 
```

## <a name="parameters"></a>参数

`vFunc`\
[in]此参数是未使用。

`ptr`\
[in]一个指向[IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)实例。

`wszName`\
[in]属性的名称。

`lFlags`\
[in] 保留。 此参数必须为 0。

`pVal`\
[out]如果该函数将返回成功，包含值的`wszName`属性。 `pval`参数分配正确的类型和限定符值。

`pvtType`\
[out]如果该函数将返回成功，包含[CIM 类型的常量](/windows/desktop/api/wbemcli/ne-wbemcli-tag_cimtype_enumeration)，该值指示属性类型。 其值也可以是`null`。 

`plFlavor`\
[out]如果该函数将返回成功，接收有关源的属性的信息。 其值可以是`null`，或定义中的以下 WBEM_FLAVOR_TYPE 常量之一*WbemCli.h*标头文件： 

|返回的常量  |“值”  |描述  |
|---------|---------|---------|
| `WBEM_FLAVOR_ORIGIN_SYSTEM` | 0x40 | 该属性是标准系统属性。 |
| `WBEM_FLAVOR_ORIGIN_PROPAGATED` | 0x20 | 类：属性继承自的父类。 <br> 实例：属性，继承自的父类，而未已修改的实例。  |
| `WBEM_FLAVOR_ORIGIN_LOCAL` | 0 | 类：属性属于派生类。 <br> 实例：实例; 修改属性也就是说，却提供了值，或限定符已添加或修改。 |

## <a name="return-value"></a>返回值

此函数返回以下值中定义*WbemCli.h*标头文件，也可以在定义它们为常量在代码中：

|返回的常量  |值  |描述  |
|---------|---------|---------|
|`WBEM_E_FAILED` | 0x80041001 | 已存在时的常见错误。 |
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | 一个或多个参数是无效的。 |
|`WBEM_E_NOT_FOUND` | 0x80041002 | 找不到指定的属性。 |
|`WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 没有足够的内存是可用于完成该操作。 |
|`WBEM_S_NO_ERROR` | 0 | 函数调用成功。  |

## <a name="remarks"></a>备注

此函数包装对的调用[IWbemClassObject::Get](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-get)方法。

`Get`函数还可以返回系统属性。

`pVal`自变量分配正确的类型和值限定符和 COM [VariantInit](https://docs.microsoft.com/previous-versions/windows/desktop/api/oleauto/nf-oleauto-variantinit)函数

## <a name="requirements"></a>要求

 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。

 **标头：** WMINet_Utils.idl

 **.NET Framework 版本：**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>请参阅

- [WMI 和性能计数器 （非托管 API 参考）](index.md)