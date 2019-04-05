---
title: CompareTo 函数 （非托管 API 参考）
description: CompareTo 函数将对象与其他 WMI 对象进行比较。
ms.date: 11/06/2017
api_name:
- CompareTo
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- CompareTo
helpviewer_keywords:
- CompareTo function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: fb5a26fccf7ceb56089aae4bd4f0732b8a405ba0
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57376229"
---
# <a name="compareto-function"></a>CompareTo 函数

将对象与另一个 Windows 管理对象进行比较。

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>语法

```cpp
HRESULT CompareTo (
   [in] int               vFunc,
   [in] IWbemClassObject* ptr,
   [in] LONG              flags,
   [in] IWbemClassObject* pCompareTo
);
```

## <a name="parameters"></a>参数

`vFunc`\
[in]此参数是未使用。

`ptr`\
[in]一个指向[IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)实例。

`flags`\
[in]指定要考虑的比较的对象特征的标志的按位组合。 请参阅[备注](#remarks)部分，了解详细信息。

`pCompareTo`\
[in]进行比较的对象。 `pCompareTo` 必须是有效[IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)实例; 它不能为`null`。

## <a name="return-value"></a>返回值

此函数返回以下值中定义*WbemCli.h*标头文件，也可以在定义它们为常量在代码中：

|返回的常量  |“值”  |描述  |
|---------|---------|---------|
| `WBEM_E_FAILED` | 0x80041001 | 发生未知的错误。 |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | 参数无效。 |
| `WBEM_E_UNEXPECTED` | 0x8004101d | 第二次调用`BeginEnumeration`而无需对的干预调用进行[ `EndEnumeration` ](endenumeration.md)。 |
| `WBEM_S_NO_ERROR` | 0 | 函数调用成功。  |
| `WBEM_S_DIFFERENT` | 0x40003 | 对象不同。 |
| `WBEM_S_SAME` | 0 | 对象是相同的基础的比较标志。 |

## <a name="remarks"></a>备注

此函数包装对的调用[IWbemClassObject::CompareTo](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-compareto)方法。

可以作为传递的标志`lEnumFlags`中定义参数*WbemCli.h*标头文件，也可以在定义它们为常量在代码中。 通过指定以下标志的按位组合，可以指定在比较中涉及的各个特征：

|返回的常量  |值  |描述  |
|---------|---------|---------|
| `WBEM_FLAG_IGNORE_OBJECT_SOURCE` | 2 | 忽略源 （在服务器和它们原来的位置的命名空间）。 |
| `WBEM_FLAG_IGNORE_QUALIFIERS` | 1 | 忽略所有限定符 (包括**键**并**动态**) |
| `WBEM_FLAG_IGNORE_DEFAULT_VALUES` | 4 | 忽略属性的默认的值。 此标志仅适用于的类的比较。 |
| `WBEM_FLAG_IGNORE_FLAVOR` | 0x20 | 忽略限定符特色信息。 此标志仍将限定符考虑在内，但会忽略风格差别，如传播规则和重写的限制。 |
| `WBEM_FLAG_IGNORE_CASE` | 0x10 | 忽略大小写比较字符串值。 这同时适用于字符串和限定符值。 属性名称和限定符名称比较始终是区分大小写，而不考虑是否设置了此标志。 |
| `WBEM_FLAG_IGNORE_CLASS` | 0x8 | 假定要比较的对象都是相同的类的实例。 因此，此标志将与实例相关信息进行比较。 使用此标志来优化性能。 如果对象不属于同一个类，则结果不确定。 |

也可以指定单个复合标志，如下所示：

|返回的常量  |值  |描述  |
|---------|---------|---------|
|`WBEM_COMPARISON_INCLUDE_ALL` | 0 | 请考虑在比较中的所有功能。 |

## <a name="requirements"></a>要求

**平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。

**标头：** WMINet_Utils.idl

**.NET Framework 版本：**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>请参阅

- [WMI 和性能计数器 （非托管 API 参考）](index.md)