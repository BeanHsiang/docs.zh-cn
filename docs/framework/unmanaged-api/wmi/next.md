---
title: 下一步函数 （非托管 API 参考）
description: 下一步函数检索枚举中的下一个属性。
ms.date: 11/06/2017
api_name:
- Next
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- Next
helpviewer_keywords:
- Next function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 240544330fa352cbfdc01944e4be6bcad28dc96f
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57373188"
---
# <a name="next-function"></a>下一个函数
检索到的调用开始枚举中的下一步属性[BeginEnumeration](beginenumeration.md)。

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>语法

```cpp
HRESULT Next (
   [in] int               vFunc,
   [in] IWbemClassObject* ptr,
   [in] LONG              lFlags,
   [out] BSTR*            pstrName,
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

`lFlags`\
[in] 保留。 此参数必须为 0。

`pstrName`\
[out]一个新`BSTR`，其中包含属性名称。 可以将此参数设置为`null`如果名称不需要。

`pVal`\
[out]一个`VARIANT`填充的属性的值。 可以将此参数设置为`null`如果不需要值。 如果该函数将返回错误代码，`VARIANT`传递给`pVal`左侧不被修改。

`pvtType`\
[out]一个指向`CIMTYPE`变量 (`LONG`属性的类型放置)。 此属性的值可以是`VT_NULL_VARIANT`，在这种情况下有必要以确定该属性的实际类型。 此参数也可以是`null`。

`plFlavor`\
[out]`null`，或接收信息来源的属性的值。 请参阅 [备注] 有关可能的值。

## <a name="return-value"></a>返回值

此函数返回以下值中定义*WbemCli.h*标头文件，也可以在定义它们为常量在代码中：

|返回的常量  |“值”  |描述  |
|---------|---------|---------|
| `WBEM_E_FAILED` | 0x80041001 | 已存在时的常见错误。 |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | 参数无效。 |
| `WBEM_E_UNEXPECTED` | 0x8004101d | 出现不需要调用[ `BeginEnumeration` ](beginenumeration.md)函数。 |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 没有足够的内存，可开始新的枚举。 |
| `WBEM_E_TRANSPORT_FAILURE` | 0x80041015 | 远程过程调用之间的当前进程和失败的 Windows 管理。 |
| `WBEM_S_NO_ERROR` | 0 | 函数调用成功。  |
| `WBEM_S_NO_MORE_DATA` | 0x40005 | 枚举中没有更多属性。 |

## <a name="remarks"></a>备注

此函数包装对的调用[IWbemClassObject::Next](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-next)方法。

此方法也会返回系统属性。

如果该属性的基础类型的对象路径、 日期或时间或另一种特殊类型，则返回的类型不包含足够的信息。 调用方必须检查`CIMTYPE`来确定属性是否是对象引用、 日期或时间或另一种特殊类型的指定属性。

如果`plFlavor`不是`null`，则`LONG`值接收围绕原点的属性的信息，如下所示：

|返回的常量  |值  |描述  |
|---------|---------|---------|
| `WBEM_FLAVOR_ORIGIN_SYSTEM` | 0x40 | 该属性是标准系统属性。 |
| `WBEM_FLAVOR_ORIGIN_PROPAGATED` | 0x20 | 类：属性继承自的父类。 <br> 实例：属性，继承自的父类，而未已修改的实例。  |
| `WBEM_FLAVOR_ORIGIN_LOCAL` | 0 | 类：属性属于派生类。 <br> 实例：实例; 修改属性也就是说，却提供了值，或限定符已添加或修改。 |

## <a name="requirements"></a>要求

**平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。

**标头：** WMINet_Utils.idl

**.NET Framework 版本：**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>请参阅

- [WMI 和性能计数器 （非托管 API 参考）](index.md)