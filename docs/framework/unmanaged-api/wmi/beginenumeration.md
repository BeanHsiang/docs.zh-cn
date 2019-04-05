---
title: BeginEnumeration 函数 （非托管 API 参考）
description: BeginEnumeration 函数将一个枚举数重置为枚举的开头
ms.date: 11/06/2017
api_name:
- BeginEnumeration
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- BeginEnumeration
helpviewer_keywords:
- BeginEnumeration function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 11002ac57a37b3c9ab0badfab49bb9049b0dfa79
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57369287"
---
# <a name="beginenumeration-function"></a>BeginEnumeration 函数
将枚举数重置到枚举的起点。  

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>语法  
  
```  
HRESULT BeginEnumeration (
   [in] int               vFunc, 
   [in] IWbemClassObject* ptr, 
   [in] LONG              lEnumFlags
); 
```  

## <a name="parameters"></a>参数

`vFunc`\
[in]此参数是未使用。

`ptr`\
[in]一个指向[IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)实例。

`lEnumFlags`\
[in]值中所述的标志的按位组合[备注](#remarks)部分，用于控制在枚举中包含的属性。

## <a name="return-value"></a>返回值

此函数返回以下值中定义*WbemCli.h*标头文件，也可以在定义它们为常量在代码中：

|返回的常量  |“值”  |描述  |
|---------|---------|---------|
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | 中的标志的组合`lEnumFlags`无效，或一个无效的指定的参数。 |
|`WBEM_E_UNEXPECTED` | 0x8004101d | 第二次调用`BeginEnumeration`而无需对的干预调用进行[ `EndEnumeration` ](endenumeration.md)。 |
|`WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 没有足够的内存，可开始新的枚举。 |
|`WBEM_S_NO_ERROR` | 0 | 函数调用成功。  |
  
## <a name="remarks"></a>备注

此函数包装对的调用[IWbemClassObject::BeginEnumeration](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)方法。

可以作为传递的标志`lEnumFlags`中定义参数*WbemCli.h*标头文件，也可以在定义它们为常量在代码中。  可以结合任何其他组中的任何标志每个组中的一个标志。 但是，在同一组中的标志是互斥的。 

**组 1**

|返回的常量  |值  |描述  |
|---------|---------|---------|
|`WBEM_FLAG_KEYS_ONLY` | 0x4 | 包含构成仅密钥的属性。 |
|`WBEM_FLAG_REFS_ONLY` | 0x8 | 包括仅限对象引用的属性。 |

**组 2**

返回的常量  |值  |描述  |
|---------|---------|---------|
|`WBEM_FLAG_SYSTEM_ONLY` | 0x30 | 限制为仅系统属性的枚举。 |
|`WBEM_FLAG_NONSYSTEM_ONLY` | 0x40 | 包括本地和传播属性但不枚举中的系统属性。 |

对于类：

返回的常量  |值  |描述  |
|---------|---------|---------|
|`WBEM_FLAG_CLASS_OVERRIDES_ONLY` | 0x100 | 限制到类定义中被重写的属性的枚举。 |
|`WBEM_FLAG_CLASS_LOCAL_AND_OVERRIDES` | 0x100 | 限制到当前的类定义中被重写的属性和新的类中定义的属性的枚举。 |
| `WBEM_MASK_CLASS_CONDITION` | 0x300 | 一个屏蔽 （而不是标记） 以应用针对`lEnumFlags`值以检查如果任一`WBEM_FLAG_CLASS_OVERRIDES_ONLY`或`WBEM_FLAG_CLASS_LOCAL_AND_OVERRIDES`设置。 |
| `WBEM_FLAG_LOCAL_ONLY` | 0x10 | 限制到定义的或在类本身中修改属性的枚举。 |
| `WBEM_FLAG_PROPAGATED_ONLY` |  0x20 | 限制对从基类继承的属性的枚举。 |

实例：

返回的常量  |“值”  |描述  |
|---------|---------|---------|
| `WBEM_FLAG_LOCAL_ONLY` | 0x10 | 限制到定义的或在类本身中修改属性的枚举。 |
| `WBEM_FLAG_PROPAGATED_ONLY` |  0x20 | 限制对从基类继承的属性的枚举。 |


## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** WMINet_Utils.idl  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>请参阅

- [WMI 和性能计数器 （非托管 API 参考）](index.md)