---
title: CreateClassEnumWmi 函数 （非托管 API 参考）
description: CreateClassEnumWmi 函数返回满足指定的条件的所有类的枚举器。
ms.date: 11/06/2017
api_name:
- CreateClassEnumWmi
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- CreateClassEnumWmi
helpviewer_keywords:
- CreateClassEnumWmi function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 0a4d2c2bd28640d0ac7124f8e0864e9e72fb1eb9
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57372329"
---
# <a name="createclassenumwmi-function"></a>CreateClassEnumWmi 函数
返回满足指定选择条件的所有类的枚举器。

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>语法

```cpp
HRESULT CreateClassEnumWmi (
   [in] BSTR                    strSuperclass,
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

`strSuperclass`\
[in]如果不是`null`或为空，指定名称的父类; 枚举器返回仅此类的子类。 如果它是`null`或空白和`lFlags`为 WBEM_FLAG_SHALLOW，则返回仅顶级类 （与任何父类的类）。 如果它是`null`或为空并`lFlags`是`WBEM_FLAG_DEEP`，命名空间中返回的所有类。

`lFlags`\
[in]影响此函数的行为的标志的组合。 以下值中定义*WbemCli.h*标头文件，也可以在定义它们为常量在代码中：

|返回的常量  |值  |描述  |
|---------|---------|---------|
| `WBEM_FLAG_USE_AMENDED_QUALIFIERS` | 0x20000 | 如果集，该函数检索当前连接的区域设置的本地化命名空间中存储已修正的限定符。 <br/> 如果未设置，此函数检索仅立即命名空间中存储的限定符。 |
| `WBEM_FLAG_DEEP` | 0 | 枚举在层次结构，但不是此类中包含所有子类。 |
| `WBEM_FLAG_SHALLOW` | 1 | 枚举包括此类的仅纯实例，但不包括的子类提供此类中找不到属性的所有实例。 |
| `WBEM_FLAG_RETURN_IMMEDIATELY` | 0x10 | 该标志会导致半同步调用。 |
| `WBEM_FLAG_FORWARD_ONLY` | 0x20 | 该函数返回的只进的枚举器。 通常情况下，只进的枚举器速度更快，并使用较少的内存比传统的枚举器，但它们不允许对调用[克隆](clone.md)。 |
| `WBEM_FLAG_BIDIRECTIONAL` | 0 | WMI 将保留指向对象的枚举中的指针，直到它们被释放。 |

建议的标志`WBEM_FLAG_RETURN_IMMEDIATELY`和`WBEM_FLAG_FORWARD_ONLY`为了获得最佳性能。

`pCtx`\
[in]通常情况下，此值是`null`。 否则，它是一个指向[IWbemContext](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemcontext)可由提供程序提供请求的类的实例。

`ppEnum`\
[out]接收对枚举器的指针。

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
| `WBEM_E_INVALID_CLASS` | 0x80041010 | `strSuperClass` 不存在。 |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | 参数不是有效的。 |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 没有足够的内存是可用于完成该操作。 |
| `WBEM_E_SHUTTING_DOWN` | 0x80041033 | WMI 是可能已停止并重新启动。 调用[ConnectServerWmi](connectserverwmi.md)试。 |
| `WBEM_E_TRANSPORT_FAILURE` | 0x80041015 | 之间的当前进程和 WMI 的远程过程调用 (RPC) 链接已失败。 |
|`WBEM_S_NO_ERROR` | 0 | 函数调用成功。  |

## <a name="remarks"></a>备注

此函数包装对的调用[iwbemservices:: Createclassenum](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemservices-createclassenum)方法。

如果函数调用失败，则可以通过调用获取其他错误信息[GetErrorInfo](geterrorinfo.md)函数。

## <a name="requirements"></a>要求

**平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。

**标头：** WMINet_Utils.idl

**.NET Framework 版本：**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>请参阅

- [WMI 和性能计数器 （非托管 API 参考）](index.md)