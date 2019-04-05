---
title: 删除函数 （非托管 API 参考）
description: 删除函数从 CIM 类定义中删除指定的属性和所有其限定符。
ms.date: 11/06/2017
api_name:
- Delete
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- Delete
helpviewer_keywords:
- Delete function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a1a26db7785a8a378fa541308ecc6aee30fa87ec
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57367113"
---
# <a name="delete-function"></a>删除函数

从 CIM 类定义中删除指定的属性和所有其限定符。

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>语法

```cpp
HRESULT Delete (
   [in] int               vFunc,
   [in] IWbemClassObject* ptr,
   [in] LPCWSTR           wszName
);
```

## <a name="parameters"></a>参数

`vFunc`\
[in]此参数是未使用。

`ptr`\
[in]一个指向[IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)实例。

`wszName`\
[in]要删除的属性的名称。 `wszName` 必须为有效指针`LPCWSTR`。

## <a name="return-value"></a>返回值

此函数返回以下值中定义*WbemCli.h*标头文件，也可以在定义它们为常量在代码中：

|返回的常量  |值  |描述  |
|---------|---------|---------|
| `WBEM_E_FAILED` | 0x80041001 | 发生未知的错误。 |
| `WBEM_E_INVALID_OPERATION` | 0x80041016 | 不能删除该属性。 |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | `wszName` 无效。 |
| `WBEM_E_NOT_FOUND` | 0x80041002 | 指定的属性不存在。 |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 没有足够的内存来完成该操作。 |
| `WBEM_E_PROPAGATED_PROPERTY` | 0x8004101c | 属性继承自的基类。 |
| `WBEM_E_SYSTEM_PROPERTY` | | 该属性是系统属性。 |
|`WBEM_S_NO_ERROR` | 0 | 函数调用成功。  |
| `WBEM_E_RESET_TO_DEFAULT` | 0x80041030 | 删除当前类重写默认值的函数。 已重新激活父类中此属性的默认值。 |

## <a name="remarks"></a>备注

此函数包装对的调用[IWbemClassObject::Delete](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-delete)方法。

## <a name="requirements"></a>要求

**平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。

**标头：** WMINet_Utils.idl

**.NET Framework 版本：**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>请参阅

- [WMI 和性能计数器 （非托管 API 参考）](index.md)