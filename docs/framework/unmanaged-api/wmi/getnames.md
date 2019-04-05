---
title: GetNames 函数 （非托管 API 参考）
description: GetNames 函数检索的对象的属性的名称。
ms.date: 11/06/2017
api_name:
- GetNames
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- GetNames
helpviewer_keywords:
- GetNames function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b0065b2cbbd17c5bb3dca6773951cdb8729e59fa
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54583556"
---
# <a name="getnames-function"></a>GetNames 函数
检索对象属性的子集或所有名称。 

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
    
## <a name="syntax"></a>语法  
  
```  
HRESULT GetNames (
   [in] int                 vFunc, 
   [in] IWbemClassObject*   ptr, 
   [in] LPCWSTR             wszQualifierName,
   [in] LONG                lFlags,
   [in] VARIANT*            pQualifierValue,
   [out] SAFEARRAY (BSTR)** pstrNames
); 
```  

## <a name="parameters"></a>参数

`vFunc`  
[in]此参数是未使用。

`ptr`  
[in]一个指向[IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)实例。

`wszQualifierName`  
[in]指向一个有效的指针`LPCWSTR`，指定作为筛选器的一部分进行操作的限定符名称。 有关详细信息，请参阅[备注](#remarks)部分。 此参数可以为 `null`。 

`lFlags`  
[in]位域的组合。 有关详细信息，请参阅[备注](#remarks)部分。

`pQualifierValue`   
[in]指向一个有效的指针`VARIANT`结构初始化为一个筛选器值。 此参数可以为 `null`。 

`pstrNames`  
[out]一个`SAFEARRAY`结构，其中包含属性名称。 在进入时，此参数必须始终为一个指向`null`。 请参阅[备注](#remarks)部分，了解详细信息。 

## <a name="return-value"></a>返回值

此函数返回以下值中定义*WbemCli.h*标头文件，也可以在定义它们为常量在代码中：

|返回的常量  |“值”  |描述  |
|---------|---------|---------|
|`WBEM_E_FAILED` | 0x80041001 | 已存在时的常见错误。 |
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | 一个或多个参数无效，或者指定了不正确的标志和参数组合。 |
|`WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 没有足够的内存是可用于完成该操作。 |
|`WBEM_S_NO_ERROR` | 0 | 函数调用成功。  |
  
## <a name="remarks"></a>备注

此函数包装对的调用[IWbemClassObject::GetNames](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-getnames)方法。

由组合的标志和参数控制返回的命名。 例如，该函数可以返回所有属性的名称或键属性的名称。  中指定主要筛选器`lFlags`参数，并使用其他参数不同，具体取决于它。

中的标志值`lFlags`是位域


可以作为传递的标志`lEnumFlags`自变量是在中定义的位域*WbemCli.h*标头文件，也可以在定义它们为常量在代码中。  可以结合任何其他组中的任何标志每个组中的一个标志。 但是，在同一组中的标志是互斥的。 

| 组 1 标志 |“值”  |描述  |
|---------|---------|---------|
| `WBEM_FLAG_ALWAYS` | 0 | 返回所有属性名称。 `strQualifierName` 和`pQualifierVal`未使用。 |
| `WBEM_FLAG_ONLY_IF_TRUE` | 1 | 返回具有指定的名称的限定符的唯一属性`strQualifierName`参数。 如果使用此标志，则必须指定`strQualifierName`。 |
|`WBEM_FLAG_ONLY_IF_FALSE` | 2 |  返回不具有指定的名称的限定符的唯一属性`strQualifierName`参数。 如果使用此标志，则必须指定`strQualifierName`。 |
|`WBEM_FLAG_ONLY_IF_IDENTICAL` | 3 | 返回具有指定的名称的限定符的属性`wszQualifierName`参数和也有值与指定的相同`pQualifierVal`结构。 如果使用此标志，则必须指定这两`wszQualifierName`和一个`pQualifierValue`。 |

| 组 2 标志 |值  |描述  |
|---------|---------|---------|
|`WBEM_FLAG_KEYS_ONLY` | 0x4 | 返回定义的键的属性的名称。 |
|`WBEM_FLAG_REFS_ONLY` | 0x8 | 返回唯一属性名称的对象引用。 |

| 组 3 标志 |“值”  |描述  |
|---------|---------|---------|
| `WBEM_FLAG_LOCAL_ONLY` | 0x10 | 返回属于派生程度最高的类的属性名称。 从父类中排除的属性。 |
| `WBEM_FLAG_PROPAGATED_ONLY` |  0x20 | 返回属于父类的属性名称。 |
|`WBEM_FLAG_SYSTEM_ONLY` | 0x30 | 返回系统属性的名称。 |
|`WBEM_FLAG_NONSYSTEM_ONLY` | 0x40 | 返回仅非系统属性的名称。 |

该函数始终会分配一个新`SAFEARRAY`如果它返回`WBEM_S_NO_ERROR`，和`pstrNames`始终设置为指向它。 如果没有属性与指定筛选器匹配，则返回的数组可以有 0 个元素。 如果该函数将返回一个值，而不`WBM_S_NO_ERROR`，新`SAFEARRAY`结构，则不返回。
 
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** WMINet_Utils.idl  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>请参阅
- [WMI 和性能计数器 （非托管 API 参考）](index.md)
