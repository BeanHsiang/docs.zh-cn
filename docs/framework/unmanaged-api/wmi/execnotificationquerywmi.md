---
title: ExecNotificationQueryWmi 函数 （非托管 API 参考）
description: ExecNotificationQueryWmi 函数执行查询以接收事件。
ms.date: 11/06/2017
api_name:
- ExecNotificationQueryWmi
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- ExecNotificationQueryWmi
helpviewer_keywords:
- ExecNotificationQueryWmi function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9cac00ff96d0c7007bdd6135282c3f767217385e
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57352875"
---
# <a name="execnotificationquerywmi-function"></a>ExecNotificationQueryWmi function

执行查询以接收事件。 调用立即返回，并且调用方可以轮询返回的枚举器的事件到达。 释放返回的枚举器取消查询。

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>语法

```cpp
HRESULT ExecNotificationQueryWmi (
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
[in]影响此函数的行为的以下两个标志的组合。 这些值中定义*WbemCli.h*标头文件，也可以在定义它们为常量在代码中。

| 返回的常量 | 值  | 描述  |
|---------|---------|---------|
| `WBEM_FLAG_RETURN_IMMEDIATELY` | 0x10 | 该标志会导致半同步调用。 如果未设置此标志，则调用失败。 这是因为事件接收连续，这意味着用户必须轮询返回的枚举器。 无限期地阻止此调用，将无法进行。 |
| `WBEM_FLAG_FORWARD_ONLY` | 0x20 | 该函数返回的只进的枚举器。 通常情况下，只进的枚举器速度更快，并使用较少的内存比传统的枚举器，但它们不允许对调用[克隆](clone.md)。 |

`pCtx`\
[in]通常情况下，此值是`null`。 否则，它是一个指向[IWbemContext](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemcontext)可由提供请求的事件提供程序的实例。

`ppEnum`\
[out]如果未发生错误，接收允许调用方检索查询的结果集中的实例的枚举器的指针。 请参阅[备注](#remarks)部分，了解详细信息。

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

|返回的常量  |值  |描述  |
|---------|---------|---------|
| `WBEM_E_ACCESS_DENIED` | 0x80041003 | 用户没有权限查看一个或多个函数可以返回的类。 |
| `WBEM_E_FAILED` | 0x80041001 | 发生未知的错误。 |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | 参数不是有效的。 |
| `WBEM_E_INVALID_CLASS` | 0x80041010 | 该查询指定不存在的类。 |
| `WBEMESS_E_REGISTRATION_TOO_PRECISE` | 0x80042002 | 已请求中传递的事件过多精度。 必须指定更大的轮询容差。 |
| `WBEMESS_E_REGISTRATION_TOO_BROAD` | 0x80042001 | 查询请求比提供 Windows 管理的详细信息。 这`HRESULT`事件查询导致轮询一个命名空间中的所有对象的请求时返回。 |
| `WBEM_E_INVALID_QUERY` | 0x80041017 | 查询发生了语法错误。 |
| `WBEM_E_INVALID_QUERY_TYPE` | 0x80041018 | 不支持请求的查询语言。 |
| `WBEM_E_QUOTA_VIOLATION` | 0x8004106c | 查询太过复杂。 |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 没有足够的内存是可用于完成该操作。 |
| `WBEM_E_SHUTTING_DOWN` | 0x80041033 | WMI 是可能已停止并重新启动。 调用[ConnectServerWmi](connectserverwmi.md)试。 |
| `WBEM_E_TRANSPORT_FAILURE` | 0x80041015 | 之间的当前进程和 WMI 的远程过程调用 (RPC) 链接已失败。 |
| `WBEM_E_UNPARSABLE_QUERY` | 0x80041058 | 无法分析查询。 |
| `WBEM_S_NO_ERROR` | 0 | 函数调用成功。  |

## <a name="remarks"></a>备注

此函数包装对的调用[IWbemServices::ExecNotificationQuery](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemservices-execnotificationquery)方法。

该函数返回后，调用方定期传递返回`ppEnum`对象传递给[下一步](next.md)函数以了解是否有任何事件。

有数限制`AND`和`OR`可以在 WQL 查询中使用的关键字。 大量的复杂查询中使用的 WQL 关键字可能会导致 WMI 返回`WBEM_E_QUOTA_VIOLATION`（或 0x8004106c） 错误代码为`HRESULT`值。 WQL 关键字的限制取决于复杂的查询是。

如果函数调用失败，则可以通过调用获取其他错误信息[GetErrorInfo](geterrorinfo.md)函数。

## <a name="requirements"></a>要求

**平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。

**标头：** WMINet_Utils.idl

**.NET Framework 版本：**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>请参阅

- [WMI 和性能计数器 （非托管 API 参考）](index.md)