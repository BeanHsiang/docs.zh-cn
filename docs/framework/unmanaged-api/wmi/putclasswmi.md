---
title: PutClassWmi 函数 （非托管 API 参考）
description: PutClassWmi 函数创建一个新类，或更新现有。
ms.date: 11/06/2017
api_name:
- PutClassWmi
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- PutClassWmi
helpviewer_keywords:
- PutClassWmi function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f9d537f7713233d363f7d408b1cef0485d99d981
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57365693"
---
# <a name="putclasswmi-function"></a>PutClassWmi 函数

创建新类或更新现有类。

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>语法

```cpp
HRESULT PutClassWmi (
   [in] IWbemClassObject*    pObject,
   [in] long                 lFlags,
   [in] IWbemContext*        pCtx,
   [out] IWbemCallResult**   ppCallResult
);
```

## <a name="parameters"></a>参数

`pObject`\
[in]指向有效的类定义的指针。 它必须正确初始化所有必需的属性值。

`lFlags`\
[in]影响此函数的行为的标志的组合。 以下值中定义*WbemCli.h*标头文件，也可以在定义它们为常量在代码中：

|返回的常量  |值  |描述  |
|---------|---------|---------|
| `WBEM_FLAG_USE_AMENDED_QUALIFIERS` | 0x20000 | 如果组，WMI 不存储任何限定符使用已修正的风格。 <br> 如果未设置，将假定未本地化此对象，并与此实例中存储所有的限定符。 |
| `WBEM_FLAG_CREATE_OR_UPDATE` | 0 | 如果不存在，或者覆盖它，如果它已存在，请创建类。 |
| `WBEM_FLAG_UPDATE_ONLY` | 1 | 更新类。 该类必须存在的调用才能成功。 |
| `WBEM_FLAG_CREATE_ONLY` | 2 | 创建的类。 如果该类已存在，则调用将失败。 |
| `WBEM_FLAG_RETURN_IMMEDIATELY` | 0x10 | 该标志会导致半同步调用。 |
| `WBEM_FLAG_OWNER_UPDATE` | 0x10000 | 调用时，推送提供程序必须指定此标志`PutClassWmi`以指示此类已更改。 |
| `WBEM_FLAG_UPDATE_COMPATIBLE` | 0 | 使类可以进行更新，如果有任何派生的类和该类的任何实例。 此外可以更新在所有情况下如果更改只需为不重要的限定符，例如说明限定符。 如果类具有实例或更改是对重要限定符，则更新失败。 |
| `WBEM_FLAG_UPDATE_SAFE_MODE` | 0x20 | 允许类的更新，即使有子类别，只要更改不会具有子类别的任何冲突。 例如，此标志将允许新的属性添加到中的任何子类不先前提到的基类。 如果类具有实例，则更新失败。 |
| `WBEM_FLAG_UPDATE_FORCE_MODE` | 0x40 | 强制更新的类时存在冲突的子类别。 例如，此标志强制执行更新，如果类限定符定义在子类中，并尝试添加相同限定符的基类与现有冲突。 在强制模式下，通过删除将被子类中发生冲突的限定符来解决本冲突。 |

`pCtx`\
[in]通常情况下，此值是`null`。 否则，它是一个指向[IWbemContext](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemcontext)可由提供程序提供请求的类的实例。

`ppCallResult`\
[out]如果`null`，此参数未被使用。 如果`lFlags`包含`WBEM_FLAG_RETURN_IMMEDIATELY`，该函数将立即返回与`WBEM_S_NO_ERROR`。 `ppCallResult`参数接收指向新[IWbemCallResult](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemcallresult)对象。

## <a name="return-value"></a>返回值

此函数返回以下值中定义*WbemCli.h*标头文件，也可以在定义它们为常量在代码中：

|返回的常量  |值  |描述  |
|---------|---------|---------|
| `WBEM_E_ACCESS_DENIED` | 0x80041003 | 用户没有权限创建或修改的类。 |
| `WBEM_E_FAILED` | 0x80041001 | 发生未知的错误。 |
| `WBEM_E_INVALID_CLASS` | 0x80041010 | 指定的类不是有效的。 通常情况下，这指示`pObject`指定的实例对象。 |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | 参数不是有效的。 |
| `WBEM_E_INVALID OPERATION` | 0x80041016 | 指定的类名称不是有效的。 |
| `WBEM_E_CLASS_HAS_CHILDREN` | 0x80041025 | 尝试进行的更改会使子类无效。 |
| `WBEM_E_ALREADY_EXISTS` | 0x80041019 | `WBEM_FLAG_CREATE_ONLY`指定标志，但该类已存在。 |
| `WBEM_E_NOT_FOUND` | 0x80041002 | `WBEM_FLAG_UPDATE_ONLY` 中指定了`lFlags`，但找不到类。 |
| `WBEM_E_INCOMPLETE_CLASS` | 0x80041020 | 所需的属性的类不是所有已设置。 |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 没有足够的内存是可用于完成该操作。 |
| `WBEM_E_SHUTTING_DOWN` | 0x80041033 | WMI 是可能已停止并重新启动。 调用[ConnectServerWmi](connectserverwmi.md)试。 |
| `WBEM_E_TRANSPORT_FAILURE` | 0x80041015 | 之间的当前进程和 WMI 的远程过程调用 (RPC) 链接已失败。 |
| `WBEM_S_NO_ERROR` | 0 | 函数调用成功。  |

## <a name="remarks"></a>备注

此函数包装对的调用[IWbemServices::PutClass](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemservices-putclass)方法。

用户可能会创建具有名称的开头或结尾使用下划线字符的类。

如果函数调用失败，则可以通过调用获取其他错误信息[GetErrorInfo](geterrorinfo.md)函数。

## <a name="requirements"></a>要求

**平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。

**标头：** WMINet_Utils.idl

**.NET Framework 版本：**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>请参阅

- [WMI 和性能计数器 （非托管 API 参考）](index.md)