---
title: CloneEnumWbemClassObject 函数 （非托管 API 参考）
description: CloneEnumWbemClassObject 函数创建枚举器的逻辑副本。
ms.date: 11/06/2017
api_name:
- CloneEnumWbemClassObject
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- CloneEnumWbemClassObject
helpviewer_keywords:
- CloneEnumWbemClassObject function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ac85ed86ea968fa945e07f95db8977a33c5d12a6
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57367098"
---
# <a name="cloneenumwbemclassobject-function"></a>CloneEnumWbemClassObject 函数
制作枚举器的逻辑副本，并保留其在枚举中的当前位置。

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>语法

```
HRESULT CloneEnumWbemClassObject (
   [out] IEnumWbemClassObject**  ppEnum, 
   [in] DWORD                    authLevel,
   [in] DWORD                    impLevel,
   [in] IEnumWbemClassObject*    pCurrentEnumWbemClassObject, 
   [in] BSTR                     strUser,
   [in] BSTR                     strPassword,
   [in BSTR]                     strAuthority 
); 
```

## <a name="parameters"></a>参数

`ppEnum`\
[out]接收到一个新指针[IEnumWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-ienumwbemclassobject)。

`authLevel`\
[in]授权级别。

`impLevel`\
[in]模拟级别。

`pCurrentEnumWbemClassObject`\
[out]一个指向[IEnumWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-ienumwbemclassobject)要克隆的实例。

`strUser`\
[in]用户名称。 请参阅[ConnectServerWmi](connectserverwmi.md)函数的详细信息。

`strPassword`\
[in]密码。 请参阅[ConnectServerWmi](connectserverwmi.md)函数的详细信息。

`strAuthority`\ [in] 用户的域名。 请参阅[ConnectServerWmi](connectserverwmi.md)函数的详细信息。

## <a name="return-value"></a>返回值

此函数返回以下值中定义*WbemCli.h*标头文件，也可以在定义它们为常量在代码中：

|返回的常量  |值  |描述  |
|---------|---------|---------|
| `WBEM_E_FAILED` | 0x80041001 | 已存在时的常见错误。 |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | 参数无效。 |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 不足够的内存完成操作。 |
| `WBEM_E_TRANSPORT_FAILURE` | 0x80041015 | 之间的当前进程和 WMI 的远程过程调用 (RPC) 链接已失败。 |
| `WBEM_S_NO_ERROR` | 0 | 函数调用成功。  |

## <a name="remarks"></a>备注

此函数包装对的调用[IEnumWbemClassObject::Clone](/windows/desktop/api/wbemcli/nf-wbemcli-ienumwbemclassobject-clone)方法。

此方法将生成仅"最大程度"的副本。 由于许多 CIM 对象的动态特性，就可以新枚举器不会枚举与源枚举器相同的对象集。

如果函数调用失败，则可以通过调用获取其他错误信息[GetErrorInfo](geterrorinfo.md)函数。

## <a name="example"></a>示例

有关示例，请参阅[IEnumWbemClassObject::Clone](/windows/desktop/api/wbemcli/nf-wbemcli-ienumwbemclassobject-clone)方法。

## <a name="requirements"></a>要求
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。

 **标头：** WMINet_Utils.idl

 **.NET Framework 版本：**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>请参阅

- [WMI 和性能计数器 （非托管 API 参考）](index.md)