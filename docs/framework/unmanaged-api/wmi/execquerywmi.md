---
title: ExecQueryWmi 函数 （非托管 API 参考）
description: ExecQueryWmi 函数执行查询以检索对象。
ms.date: 11/06/2017
api_name:
- ExecQueryWmi
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- ExecQueryWmi
helpviewer_keywords:
- ExecQueryWmi function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 402bbcb9ad5e462a55c5ec2716417f512f03ee19
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57373213"
---
# <a name="execquerywmi-function"></a>ExecQueryWmi 函数

执行查询以检索对象。

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>语法

```cpp
HRESULT ExecQueryWmi (
   [in] BSTR                    strQueryLanguage,
   [in] BSTR                    strQuery,
   [in] long                    lFlags,
   [in] IWbemContext*           pCtx,
   [out] IEnumWbemClassObject** ppEnum,
   [in] DWORD                   authLevel,
   [in] DWORD                   impLevel,
   [in] IWbemServices*          pCurrentNamespace,
   [in] BSTR                    strUser,
   [in] BSTR                    strPassword,
   [in] BSTR                    strAuthority
);
```

## <a name="parameters"></a>参数

`strQueryLanguage`\
[in]具有支持的 Windows 管理的有效的查询语言的字符串。 它必须是"WQL"，WMI 查询语言的缩写词。

`strQuery`\
[in]查询的文本。 此参数不能为 `null`。

`lFlags`\
[in]影响此函数的行为的标志的组合。 以下值中定义*WbemCli.h*标头文件，也可以在定义它们为常量在代码中：

| 返回的常量 | “值”  | 描述  |
|---------|---------|---------|
| `WBEM_FLAG_USE_AMENDED_QUALIFIERS` | 0x20000 | 如果集，该函数检索当前连接的区域设置的本地化命名空间中存储已修正的限定符。 <br/> 如果未设置，此函数检索仅立即命名空间中存储的限定符。 |
| `WBEM_FLAG_RETURN_IMMEDIATELY` | 0x10 | 该标志会导致半同步调用。 |
| `WBEM_FLAG_FORWARD_ONLY` | 0x20 | 该函数返回的只进的枚举器。 通常情况下，只进的枚举器速度更快，并使用较少的内存比传统的枚举器，但它们不允许对调用[克隆](clone.md)。 |
| `WBEM_FLAG_BIDIRECTIONAL` | 0 | WMI 将保留指向对象的枚举中的指针，直到它们被释放。 |
| `WBEM_FLAG_ENSURE_LOCATABLE` | 0x100 | 可确保任何返回的对象中都有足够的信息，因此该系统属性，如 **__PATH**， **__RELPATH**，并 **__SERVER**，不是`null`。 |
| `WBEM_FLAG_PROTOTYPE` | 2 | 此标志用于原型制作。 它不会执行查询，并改为返回类似于典型的结果对象的对象。 |
| `WBEM_FLAG_DIRECT_READ` | 0x200 | 原因直接访问该提供程序不考虑其父类或任意子类的情况下指定的类。 |

建议的标志`WBEM_FLAG_RETURN_IMMEDIATELY`和`WBEM_FLAG_FORWARD_ONLY`为了获得最佳性能。

`pCtx`\
[in]通常情况下，此值是`null`。 否则，它是一个指向[IWbemContext](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemcontext)可由提供程序提供请求的类的实例。

`ppEnum`\
[out]如果未发生错误，接收允许调用方检索查询的结果集中的实例的枚举器的指针。 查询可以有一个结果集具有零个实例。 请参阅[备注](#remarks)部分，了解详细信息。

`authLevel`\
[in]授权级别。

`impLevel`\
[in]模拟级别。

`pCurrentNamespace`\
[in]一个指向[IWbemServices](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemservices)对象，表示当前命名空间。

`strUser`\
[in]用户名称。 请参阅[ConnectServerWmi](connectserverwmi.md)函数的详细信息。

`strPassword`\
[in]密码。 请参阅[ConnectServerWmi](connectserverwmi.md)函数的详细信息。

`strAuthority`\
[in]用户的域名。 请参阅[ConnectServerWmi](connectserverwmi.md)函数的详细信息。

## <a name="return-value"></a>返回值

此函数返回以下值中定义*WbemCli.h*标头文件，也可以在定义它们为常量在代码中：

|返回的常量  |“值”  |描述  |
|---------|---------|---------|
| `WBEM_E_ACCESS_DENIED` | 0x80041003 | 用户没有权限查看一个或多个函数可以返回的类。 |
| `WBEM_E_FAILED` | 0x80041001 | 发生未知的错误。 |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | 参数不是有效的。 |
| `WBEM_E_INVALID_QUERY` | 0x80041017 | 查询发生了语法错误。 |
| `WBEM_E_INVALID_QUERY_TYPE` | 0x80041018 | 不支持请求的查询语言。 |
| `WBEM_E_QUOTA_VIOLATION` | 0x8004106c | 查询太过复杂。 |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 没有足够的内存是可用于完成该操作。 |
| `WBEM_E_SHUTTING_DOWN` | 0x80041033 | WMI 是可能已停止并重新启动。 调用[ConnectServerWmi](connectserverwmi.md)试。 |
| `WBEM_E_TRANSPORT_FAILURE` | 0x80041015 | 之间的当前进程和 WMI 的远程过程调用 (RPC) 链接已失败。 |
| `WBEM_E_NOT_FOUND` | 0x80041002 | 该查询指定不存在的类。 |
| `WBEM_S_NO_ERROR` | 0 | 函数调用成功。  |

## <a name="remarks"></a>备注

此函数包装对的调用[IWbemServices::ExecQuery](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemservices-execquery)方法。

此函数将处理中指定的查询`strQuery`参数，并创建通过其调用方可以访问查询结果的枚举器。 枚举器是一个指向[IEnumWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-ienumwbemclassobject)接口; 查询结果是通过提供的类对象的实例[IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)接口。

有数限制`AND`和`OR`可以在 WQL 查询中使用的关键字。 大量的复杂查询中使用的 WQL 关键字可能会导致 WMI 返回`WBEM_E_QUOTA_VIOLATION`（或 0x8004106c） 错误代码为`HRESULT`值。 WQL 关键字的限制取决于复杂的查询是。

如果函数调用失败，则可以通过调用获取其他错误信息[GetErrorInfo](geterrorinfo.md)函数。

## <a name="requirements"></a>要求

**平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。

**标头：** WMINet_Utils.idl

**.NET Framework 版本：**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>请参阅

- [WMI 和性能计数器 （非托管 API 参考）](index.md)