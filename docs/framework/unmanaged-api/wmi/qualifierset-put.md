---
title: QualifierSet_Put 函数 （非托管 API 参考）
description: QualifierSet_Put 函数写入指定的限定符和其值。
ms.date: 11/06/2017
api_name:
- QualifierSet_Put
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- QualifierSet_Put
helpviewer_keywords:
- QualifierSet_Put function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 0e42cf3440bef030f5c7bec71ed1b4b875b79a61
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57378813"
---
# <a name="qualifiersetput-function"></a>QualifierSet_Put 函数

写入命名限定符和值。 新限定符将覆盖具有相同名称的以前的值。 如果限定符不存在，则创建它。

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>语法

```cpp
HRESULT QualifierSet_Put (
   [in] int                  vFunc,
   [in] IWbemQualifierSet*   ptr,
   [in] LPCWSTR              wszName,
   [in] VARIANT*             pVal,
   [in] LONG                 lFlavor
);
```

## <a name="parameters"></a>参数

`vFunc`\
[in]此参数是未使用。

`ptr`\
[in]一个指向[IWbemQualifierSet](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemqualifierset)实例。

`wszName`\
[in]要写入的限定符的名称。

`pVal`\
[in]指向一个有效的指针`VARIANT`，其中包含要写入的限定符。 此参数不能为 `null`。

`lFlavor`\
[in]定义此限定符的所需的限定符特色信息的以下常量之一。 默认值是`WBEM_FLAVOR_OVERRIDABLE`(0)。

|返回的常量  |值  |描述  |
|---------|---------|---------|
| `WBEM_FLAVOR_OVERRIDABLE` | 0 | 可以在派生的类或实例中重写限定符。 **这是默认值。** |
| `WBEM_FLAVOR_FLAG_PROPAGATE_TO_INSTANCE` | 1 | 限定符传播到实例。 |
| `WBEM_FLAVOR_FLAG_PROPAGATE_TO_DERIVED_CLASS` | 2 | 将限定符传播给派生类。 |
| `WBEM_FLAVOR_NOT_OVERRIDABLE` | 0x10 | 不能在派生类或实例中重写限定符。 |
| `WBEM_FLAVOR_AMENDED` | 0x80 | 本地化限定符。 |

## <a name="return-value"></a>返回值

此函数返回以下值中定义*WbemCli.h*标头文件，也可以在定义它们为常量在代码中：

|返回的常量  |“值”  |描述  |
|---------|---------|---------|
| `WBEM_E_CANNOT_BE_KEY` | 0x8004101f | 出现非法尝试指定**密钥**限定符不能为键的属性。 指定密钥 om c; 对象 a 定义并不能在每个实例的基础上更改。 |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | 参数不是有效的。 |
| `WBEM_E_INVALID_QUALIFIER_TYPE` | 0x80041029 | `pVal`参数不是合法的限定符类型。 |
| `WBEM_E_OVERRIDE_NOT_ALLOWED` | 0x8004101a | 不能调用`QualifierSet_Put`方法对限定符因为所属对象不允许重写。 |
| `WBEM_S_NO_ERROR` | 0 | 函数调用成功。  |

## <a name="remarks"></a>备注

此函数包装对的调用[IWbemQualifierSet::Put](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemqualifierset-put)方法。

## <a name="requirements"></a>要求

**平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。

**标头：** WMINet_Utils.idl

**.NET Framework 版本：**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>请参阅

- [WMI 和性能计数器 （非托管 API 参考）](index.md)