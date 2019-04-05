---
title: ConnectServerWmi 函数 （非托管 API 参考）
description: ConnectServerWmi 函数使用 DCOM 来创建与 WMI 命名空间的连接。
ms.date: 11/06/2017
api_name:
- ConnectServerWmi
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- ConnectServerWmi
helpviewer_keywords:
- ConnectServerWmi function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 548c6007d4ed685c521676de87c5a98f56a222a4
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57376983"
---
# <a name="connectserverwmi-function"></a>ConnectServerWmi 函数
通过 DCOM 创建到指定计算机上的 WMI 命名空间的连接。

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>语法

```
HRESULT ConnectServerWmi (
   [in] BSTR               strNetworkResource,
   [in] BSTR               strUser,
   [in] BSTR               strPassword,
   [in] BSTR               strLocale,
   [in] long               lSecurityFlags,
   [in] BSTR               strAuthority,
   [in] IWbemContext*      pCtx,
   [out] IWbemServices**   ppNamespace,
   [in] DWORD              impLevel, 
   [in] DWORD              authLevel
);
```
## <a name="parameters"></a>参数

`strNetworkResource`\
[in]指向有效`BSTR`包含正确的 WMI 命名空间的对象路径。 请参阅[备注](#remarks)部分，了解详细信息。

`strUser`\
[in]指向一个有效的指针`BSTR`，其中包含的用户名称。 一个`null`值指示当前的安全上下文。 如果用户是从不同的域与当前`strUser`还可以包含一个反斜杠分隔的域和用户名称。 `strUser` 也可以是用户主体名称 (UPN) 格式，如`userName@domainName`。 请参阅[备注](#remarks)部分，了解详细信息。

`strPassword`\
[in]指向一个有效的指针`BSTR`包含的密码。 一个`null`指示当前的安全上下文。 空字符串 ("") 指示有效长度为零的密码。

`strLocale`\
[in]指向一个有效的指针`BSTR`，该值指示正确的区域设置的信息检索。 对于 Microsoft 区域设置标识符的字符串的格式是"MS\_*xxx*"，其中*xxx*是一个字符串中指示的区域设置标识符 (LCID) 的十六进制格式。 如果指定了无效的区域设置，该方法返回`WBEM_E_INVALID_PARAMETER`上 Windows 7，其中的服务器的默认区域设置改为使用除外。 如果使用 null1，当前区域设置。 
 
`lSecurityFlags`\
[in]要传递给标志`ConnectServerWmi`方法。 此参数为零 (0) 的值将导致调用`ConnectServerWmi`返回才建立到服务器的连接。 这可能导致应用程序未响应无限期地服务器已中断。 其他有效值为：

| 返回的常量  | “值”  | 描述  |
|---------|---------|---------|
| `CONNECT_REPOSITORY_ONLY` | 0x40 | 保留以供内部使用。 请勿使用。 |
| `WBEM_FLAG_CONNECT_USE_MAX_WAIT` | 0x80 | `ConnectServerWmi` 返回在两分钟或更少。 |

`strAuthority`\
[in]用户的域名。 可以有下列值：

| “值” | 描述 |
|---------|---------|
| 空白 | 使用 NTLM 身份验证，并使用当前用户的 NTLM 域。 如果`strUser`指定域 （推荐位置），它必须未在此处指定。 该函数将返回`WBEM_E_INVALID_PARAMETER`如果两个参数中指定的域。 |
| Kerberos:*主体名称* | 使用 Kerberos 身份验证，并且此参数包含 Kerberos 主体名称。 |
| NTLMDOMAIN:*域名* | 使用 NT LAN Manager 身份验证，并且此参数包含的 NTLM 域名。 |

`pCtx`\
[in]通常情况下，此参数是`null`。 否则，它是一个指向[IWbemContext](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemcontext)对象所需的一个或多个动态类提供程序。 

`ppNamespace`\
[out]当函数返回时，接收一个指向[IWbemServices](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemservices)对象绑定到指定的命名空间。 它设置为指向`null`时出现错误。

`impLevel`\
[in]模拟级别。

`authLevel`\
[in]授权级别。

## <a name="return-value"></a>返回值

此函数返回以下值中定义*WbemCli.h*标头文件，也可以在定义它们为常量在代码中：

|返回的常量  |值  |描述  |
|---------|---------|---------|
| `WBEM_E_FAILED` | 0x80041001 | 已存在时的常见错误。 |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | 参数不是有效的。 |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 没有足够的内存是可用于完成该操作。 |
| `WBEM_S_NO_ERROR` | 0 | 函数调用成功。  |

## <a name="remarks"></a>备注

此函数包装对的调用[IWbemLocator::ConnectServer](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemlocator-connectserver)方法。

为本地访问默认命名空间`strNetworkResource`可以是简单的对象路径:"root\default"或"\\.\root\default"。 用于访问远程计算机上的默认命名空间使用 COM 或 Microsoft 兼容的网络，包含计算机名称:"\\myserver\root\default"。 计算机名称也可以是 DNS 名称或 IP 地址。 `ConnectServerWmi`函数还可以连接运行 IPv6 的计算机使用 IPv6 地址。

`strUser` 不能为空字符串。 如果在指定了域`strAuthority`，它不还必须包含在`strUser`，或该函数将返回`WBEM_E_INVALID_PARAMETER`。


## <a name="requirements"></a>要求

 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。

 **标头：** WMINet_Utils.idl

 **.NET Framework 版本：**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>请参阅

- [WMI 和性能计数器 （非托管 API 参考）](index.md)