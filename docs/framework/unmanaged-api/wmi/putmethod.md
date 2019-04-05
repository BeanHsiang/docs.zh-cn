---
title: PutMethod 函数 （非托管 API 参考）
description: PutMethod 函数创建一个方法。
ms.date: 11/06/2017
api_name:
- PutMethod
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- PutMethod
helpviewer_keywords:
- PutMethod function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 74654cf18d87fed8ad5ce9a4cd4249d56fdb4343
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54693446"
---
# <a name="putmethod-function"></a>PutMethod 函数
创建方法。

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
    
## <a name="syntax"></a>语法  
  
```  
HRESULT PutMethod (
   [in] int                vFunc, 
   [in] IWbemClassObject*  ptr, 
   [in] LPCWSTR            wszName,
   [in] LONG               lFlags,
   [in] IWbemClassObject*  pInSignature,
   [in] IWbemClassObject*  pOutSignature
); 
```  

## <a name="parameters"></a>参数

`vFunc`  
[in]此参数是未使用。

`ptr`  
[in]一个指向[IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)实例。

`wszName`  
[in]若要创建的方法的名称。 

`lFlags`  
[in] 保留。 此参数必须为 0。

`pSignatureIn`  
[in]指向一份[__Parameters 系统类](/windows/desktop/WmiSdk/--parameters)，其中包含`in`方法的参数。 如果忽略此参数设置为`null`。  

`pSignatureOut`  
[in] 指向一份[__Parameters 系统类](/windows/desktop/WmiSdk/--parameters)，其中包含`out`方法的参数。 如果忽略此参数设置为`null`。
 

## <a name="return-value"></a>返回值

此函数返回以下值中定义*WbemCli.h*标头文件，也可以在定义它们为常量在代码中：

|返回的常量  |值  |描述  |
|---------|---------|---------|
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | 一个或多个参数是无效的。 |
| `WBEM_E_INVALID_DUPLICATE_PARAMETER` | 0x80041043 | `[in, out]`方法参数中指定*pInSignature*并*pOutSignature*对象具有不同的限定符。
| `WBEM_E_MISSING_PARAMETER_ID` | 0x80041036 | 方法参数缺少的规范**ID**限定符。 |
| `WBEM_E_NONCONSECUTIVE_PARAMETER_IDS` | 0x80041038 | 分配到方法参数的 ID 序列不是连续或不在 0 时不启动。 |
| `WBEM_E_PARAMETER_ID_ON_RETVAL` | 0x80041039 | 一种方法的返回值具有**ID**限定符。 |
| `WBEM_E_PROPAGATED_METHOD` | 0x80041034 | 尝试重用现有的父类，方法名称和签名不匹配。 |
| `WBEM_S_NO_ERROR` | 0 | 函数调用成功。 |
  
## <a name="remarks"></a>备注

此函数包装对的调用[IWbemClassObject::PutMethod](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-putmethod)方法。

当此方法调用时才支持`ptr`是 CIM 类定义。 方法操作不能从[IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)指向 CIM 实例的指针。

用户无法创建方法名称的开头或下划线结尾。 这被保留给系统类和属性。

对于方法，请`in`并`out`参数为中的属性，请参见[IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)对象。

`[in/out]`参数可通过将相同属性添加到指向这两个对象定义`pInSignature`和`pOutSignature`参数。 在这种情况下，属性共用同一个**ID**限定符的值。

在每个属性[__Parameters](/windows/desktop/WmiSdk/--parameters)不是类对象`ReturnValue`必须具有**ID**限定符、 从零开始的数字值，用于标识参数的显示的顺序。 没有两个参数可以具有相同**ID**值，但未**ID**可以跳过值。 如果任何一种情况发生，`PutMethod`函数返回`WBEM_E_NONCONSECUTIVE_PARAMETER_IDS`。

## <a name="example"></a>示例

有关示例，请参阅[IWbemClassObject::PutMethod](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-putmethod)方法。

## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** WMINet_Utils.idl  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>请参阅
- [WMI 和性能计数器 （非托管 API 参考）](index.md)
