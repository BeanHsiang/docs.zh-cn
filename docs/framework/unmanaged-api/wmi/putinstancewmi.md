---
title: PutInstanceWmi 函数 （非托管 API 参考）
description: PutInstanceWmi 函数创建或更新现有类的实例。
ms.date: 11/06/2017
api_name:
- PutInstanceWmi
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- PutInstanceWmi
helpviewer_keywords:
- PutInstanceWmi function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 19f657fd76f73c4016824511079e6f037bc3bc53
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57359367"
---
# <a name="putinstancewmi-function"></a>PutInstanceWmi 函数

创建或更新现有类的实例。 将该实例写入 WMI 存储库。

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>语法

```cpp
HRESULT PutInstanceWmi (
   [in] IWbemClassObject*    pInst,
   [in] long                 lFlags,
   [in] IWbemContext*        pCtx,
   [out] IWbemCallResult**   ppCallResult
);
```

## <a name="parameters"></a>参数

`pInst`\
[in]指向要写入的实例的指针。

`lFlags`\
[in]影响此函数的行为的标志的组合。 以下值中定义*WbemCli.h*标头文件，也可以在定义它们为常量在代码中：

|返回的常量  |值  |描述  |
|---------|---------|---------|
| `WBEM_FLAG_USE_AMENDED_QUALIFIERS` | 0x20000 | 如果设置，WMI 不存储任何与限定符**Amended**风格。 <br> 如果未设置，将假定未本地化此对象，并与此实例中存储所有的限定符。 |
| `WBEM_FLAG_CREATE_OR_UPDATE` | 0 | 如果不存在，或者覆盖它，如果它已存在，请创建该实例。 |
| `WBEM_FLAG_UPDATE_ONLY` | 1 | 更新的实例。 若要成功的调用必须存在的实例。 |
| `WBEM_FLAG_CREATE_ONLY` | 2 | 创建该实例。 如果该实例已存在，则调用将失败。 |
| `WBEM_FLAG_RETURN_IMMEDIATELY` | 0x10 | 该标志会导致半同步调用。 |

`pCtx`\
[in]通常情况下，此值是`null`。 否则，它是一个指向[IWbemContext](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemcontext)可由提供程序提供请求的类的实例。

`ppCallResult`\
[out]如果`null`，此参数未被使用。 如果`lFlags`包含`WBEM_FLAG_RETURN_IMMEDIATELY`，该函数将立即返回与`WBEM_S_NO_ERROR`。 `ppCallResult`参数接收指向新[IWbemCallResult](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemcallresult)对象。

## <a name="return-value"></a>返回值

此函数返回以下值中定义*WbemCli.h*标头文件，也可以在定义它们为常量在代码中：

|返回的常量  |值  |描述  |
|---------|---------|---------|
| `WBEM_E_ACCESS_DENIED` | 0x80041003 | 用户没有权限来更新指定类的实例。 |
| `WBEM_E_FAILED` | 0x80041001 | 发生未知的错误。 |
| `WBEM_E_INVALID_CLASS` | 0x80041010 | 支持此实例的类不是有效的。 |
| `WBEM_E_ILLEGAL_NULL` | 0x80041028 | `null`不能为属性指定了`null`，例如标记**索引**或**Not_Null**限定符。 |
| `WBEM_E_INVALID_OBJECT` | 0x8004100f | 指定的实例不是有效的。 (例如，调用`PutInstanceWmi`类将返回此值。) |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | 参数不是有效的。 |
| `WBEM_E_ALREADY_EXISTS` | 0x80041019 | `WBEM_FLAG_CREATE_ONLY`指定标志，但该实例已存在。 |
| `WBEM_E_NOT_FOUND` | 0x80041002 | `WBEM_FLAG_UPDATE_ONLY` 中指定了`lFlags`，但该实例不存在。 |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 没有足够的内存是可用于完成该操作。 |
| `WBEM_E_SHUTTING_DOWN` | 0x80041033 | WMI 是可能已停止并重新启动。 调用[ConnectServerWmi](connectserverwmi.md)试。 |
| `WBEM_E_TRANSPORT_FAILURE` | 0x80041015 | 之间的当前进程和 WMI 的远程过程调用 (RPC) 链接已失败。 |
| `WBEM_S_NO_ERROR` | 0 | 函数调用成功。 |

## <a name="remarks"></a>备注

此函数包装对的调用[IWbemServices::PutInstance](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemservices-putinstance)方法。

`PutInstanceWmi`函数支持创建实例和更新现有的类的实例。  具体取决于如何`pCtx`设置参数，则更新以下某些或所有实例的属性。

当实例指向的`pInst`属于子类，Windows 管理调用负责子类派生的类的所有提供程序。 所有这些提供程序必须成功执行原始`PutInstanceWmi`请求才能成功。 在层次结构中支持的最顶层类的提供程序首先调用。 调用顺序将继续执行的最顶层类的子类，并继续从顶部到底部 Windows 管理直到拥有由指向该实例的类的提供程序`pInst`。
Windows 管理不会调用任何实例的子类别的提供程序。

当应用程序必须更新属于类层次结构的实例时`pInst`参数必须指向包含要修改的属性的实例。 也就是说，请考虑属于的目标实例**ClassB**。 **ClassB**实例派生**ClassA**，并**ClassA**定义的属性**PropA**。 如果应用程序想要更改的值**PropA**中**ClassB**实例，它必须设置`pInst`到该实例而不是实例**ClassA**.

调用`PutInstanceWmi`不允许抽象类的实例上。

如果函数调用失败，则可以通过调用获取其他错误信息[GetErrorInfo](geterrorinfo.md)函数。

## <a name="requirements"></a>要求

**平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。

**标头：** WMINet_Utils.idl

**.NET Framework 版本：**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>请参阅

- [WMI 和性能计数器 （非托管 API 参考）](index.md)