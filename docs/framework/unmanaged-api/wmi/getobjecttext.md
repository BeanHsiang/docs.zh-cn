---
title: GetObjectText 函数 （非托管 API 参考）
description: GetObjectText 函数用 MOF 语法返回一个对象的文本呈现。
ms.date: 11/06/2017
api_name:
- GetObjectText
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- GetObjectText
helpviewer_keywords:
- GetObjectText function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: e3a7d606f64dfe1a1abfd3da930fd00957da90a3
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54583572"
---
# <a name="getobjecttext-function"></a>GetObjectText 函数
返回托管对象格式 (MOF) 语法中的对象的文本呈现。

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
    
## <a name="syntax"></a>语法  
  
```  
HRESULT GetObjectText (
   [in] int                vFunc, 
   [in] IWbemClassObject*   ptr, 
   [in] LONG                lFlags,
   [out] BSTR*              pstrObjectText
); 
```  

## <a name="parameters"></a>参数

`vFunc`  
[in]此参数是未使用。

`ptr`  
[in]一个指向[IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)实例。

`lFlags`  
[in]通常情况下 0。 如果`WBEM_FLAG_NO_FLAVORS`（或 0x1） 指定，限定符是包含但不传播或风格的信息。

`pstrObjectText`   
[out]一个指向`null`条目。 返回时，新分配`BSTR`，其中包含的对象的 MOF 语法呈现。  

## <a name="return-value"></a>返回值

此函数返回以下值中定义*WbemCli.h*标头文件，也可以在定义它们为常量在代码中：

|返回的常量  |值  |描述  |
|---------|---------|---------|
|`WBEM_E_FAILED` | 0x80041001 | 已存在时的常见错误。 |
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | 参数不是有效的。 |
|`WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 没有足够的内存是可用于完成该操作。 |
|`WBEM_S_NO_ERROR` | 0 | 函数调用成功。  |
  
## <a name="remarks"></a>备注

此函数包装对的调用[IWbemClassObject::GetObjectText](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-getobjecttext)方法。

返回的 MOF 文本不包含所有对象的信息，但仅 MOF 编译器要能够重新创建原始对象的足够信息。 例如，没有传播的限定符或父类属性中包含。

使用以下算法来重新构造方法的参数的文本：

1. 参数被 resequenced 按其标识符值的顺序。
1. 指定为参数`[in]`和`[out]`合并到单个参数。
 
`pstrObjectText` 必须是指向指针`null`时调用的函数; 它必须指向是方法调用前有效，因为将释放指针的字符串。

## <a name="requirements"></a>要求  
**平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** WMINet_Utils.idl  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>请参阅
- [WMI 和性能计数器 （非托管 API 参考）](index.md)
