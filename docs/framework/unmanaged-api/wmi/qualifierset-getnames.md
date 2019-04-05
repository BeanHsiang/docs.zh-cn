---
title: QualifierSet_GetNames 函数 （非托管 API 参考）
description: QualifierSet_GetNames 函数从某个对象或属性检索的限定符的名称。
ms.date: 11/06/2017
api_name:
- QualifierSet_GetNames
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- QualifierSet_GetNames
helpviewer_keywords:
- QualifierSet_GetNames function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: da6321e50082c3f73477b8187cc5bf671655df21
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57365940"
---
# <a name="qualifiersetgetnames-function"></a>QualifierSet_GetNames 函数

检索所有的限定符或某些来自当前对象或属性的限定符的名称。

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>语法

```cpp
HRESULT QualifierSet_GetNames (
   [in] int                  vFunc,
   [in] IWbemQualifierSet*   ptr,
   [in] LONG                 lFlags,
   [out] SAFEARRAY (BSTR)**  pstrNames
);
```

## <a name="parameters"></a>参数

`vFunc`\
[in]此参数是未使用。

`ptr`\
[in]一个指向[IWbemQualifierSet](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemqualifierset)实例。

`lFlags`\
[in]以下标志或值，该值指定要在枚举中包括哪些名称之一。

|返回的常量  |值  |描述  |
|---------|---------|---------|
|  | 0 | 返回所有限定符的名称。 |
| `WBEM_FLAG_LOCAL_ONLY` | 0x10 | 返回限定符的名称特定于当前的属性或对象。 <br/> 属性：返回仅特定于 （包括重写） 的属性限定符，而不从类定义传播这些限定符。 <br/> 实例：返回的是仅特定于实例的限定符名称。 <br/> 类：要派生的类的特定返回仅限定符。
|`WBEM_FLAG_PROPAGATED_ONLY` | 0x20 | 返回名称的列是限定符传播从另一个对象。 <br/> 属性：返回时仅限定符传播给此属性从类定义中，而不从该属性本身。 <br/> 实例：仅这些限定符传播从返回的类定义。 <br/> 类：返回从父类继承仅这些限定符名称。 |

`pstrNames`\
[out]一个新`SAFEARRAY`，其中包含请求的名称。 该数组可以具有 0 个元素。 如果发生错误，新`SAFEARRAY`不会返回。

## <a name="return-value"></a>返回值

此函数返回以下值中定义*WbemCli.h*标头文件，也可以在定义它们为常量在代码中：

|返回的常量  |值  |描述  |
|---------|---------|---------|
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | 参数不是有效的。 |
|`WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 没有足够的内存，可开始新的枚举。 |
|`WBEM_S_NO_ERROR` | 0 | 函数调用成功。  |

## <a name="remarks"></a>备注

此函数包装对的调用[IWbemQualifierSet::GetNames](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemqualifierset-getnames)方法。

已检索到的限定符名称后, 您可以访问每个限定符的名称通过调用[QualifierSet_Get](qualifierset-get.md)函数。

它不是给定的对象具有零个限定符，因此错误中的字符串数`pstrNames`返回时可为 0，即使该函数将返回`WBEM_S_NO_ERROR`。

## <a name="requirements"></a>要求

**平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。

**标头：** WMINet_Utils.idl

**.NET Framework 版本：**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>请参阅

- [WMI 和性能计数器 （非托管 API 参考）](index.md)