---
title: Put 的函数 （非托管 API 参考）
description: Put 函数将新值分配给命名的属性。
ms.date: 11/06/2017
api_name:
- Put
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- Put
helpviewer_keywords:
- Put function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 02c8ab3aa7fcc603b76fb4b1d09e7e73d04494be
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57369184"
---
# <a name="put-function"></a>Put 的函数

将命名属性设置为新值。

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>语法

```cpp
HRESULT Put (
   [in] int               vFunc,
   [in] IWbemClassObject* ptr,
   [in] LPCWSTR           wszName,
   [in] LONG              lFlags,
   [in] VARIANT*          pVal,
   [in] CIMTYPE           vtType
);
```

## <a name="parameters"></a>参数

`vFunc`\
[in]此参数是未使用。

`ptr`\
[in]一个指向[IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)实例。

`wszName`\
[in]属性的名称。 此参数不能为 `null`。

`lFlags`\
[in] 保留。 此参数必须为 0。

`pVal`\
[in]指向一个有效的指针`VARIANT`该按钮将变为新的属性值。 如果`pVal`是`null`或指向`VARIANT`类型的`VT_NULL`，该属性设置为`null`。

`vtType`\
[in]类型`VARIANT`指向的`pVal`。 请参阅[备注](#remarks)部分，了解详细信息。

## <a name="return-value"></a>返回值

此函数返回以下值中定义*WbemCli.h*标头文件，也可以在定义它们为常量在代码中：

|返回的常量  |“值”  |描述  |
|---------|---------|---------|
|`WBEM_E_FAILED` | 0x80041001 | 已存在时的常见错误。 |
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | 一个或多个参数是无效的。 |
|`WBEM_E_INVALID_PROPERTY_TYPE` | 0x8004102a | 未识别属性类型。 创建类实例，如果该类已存在时返回此值。 |
|`WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 没有足够的内存是可用于完成该操作。 |
| `WBEM_E_TYPE_MISMATCH` | 0x80041005 | 实例：指示`pVal`指向`VARIANT`属性类型不正确。 <br/> 查找类定义：属性已存在的父类、 中和新的 COM 类型都不同于旧的 COM 类型。 |
|`WBEM_S_NO_ERROR` | 0 | 函数调用成功。 |

## <a name="remarks"></a>备注

此函数包装对的调用[IWbemClassObject::Put](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-put)方法。

此函数始终覆盖使用新的当前属性值。 如果[IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)指向的类定义，`Put`创建或更新的属性值。 当[IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)指向 CIM 的实例，`Put`更新属性值; 仅`Put`不能创建一个属性值。

`__CLASS`系统属性才是可写类创建过程时它可能不为空。 所有其他系统属性是只读的。

用户不能具有名称的开头或结尾下划线 ("_") 创建属性。 这被保留给系统类和属性。

如果该属性设置的`Put`父类中存在的函数，除非属性类型与父类类型不匹配，将更改属性的默认值。 如果该属性不存在，它不是类型不匹配，则创建属性。

使用`vtType`参数仅在 CIM 类定义中创建新的属性时，`pVal`是`null`或指向`VARIANT`类型的`VT_NULL`。 在这种情况下，`vType`参数指定的属性的 CIM 类型。 在所有其他情况下，`vtType`必须为 0。 `vtType` 如果基础对象实例也必须为 0 (即使`Val`是`null`) 由于属性类型固定的不能更改。

## <a name="example"></a>示例

有关示例，请参阅[IWbemClassObject::Put](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-put)方法。

## <a name="requirements"></a>要求

**平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。

**标头：** WMINet_Utils.idl

**.NET Framework 版本：**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>请参阅

- [WMI 和性能计数器 （非托管 API 参考）](index.md)