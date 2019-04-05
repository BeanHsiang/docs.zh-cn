---
title: NextMethod 函数 （非托管 API 参考）
description: NextMethod 函数检索枚举中的下一步方法。
ms.date: 11/06/2017
api_name:
- NextMethod
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- NextMethod
helpviewer_keywords:
- NextMethod function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2ebe6924dfe1a4aa640ef8ccd7b4047c1d137948
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54640038"
---
# <a name="nextmethod-function"></a>NextMethod 函数
检索到的调用开始枚举中的下一步方法[BeginMethodEnumeration](beginmethodenumeration.md)。  

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>语法  
  
```  
HRESULT NextMethod (
   [in] int                 vFunc, 
   [in] IWbemClassObject*   ptr, 
   [in] LONG                lFlags,
   [out] BSTR*              pName,
   [out] IWbemClassObject** ppInSignature,
   [out] IWbemClassObject** ppOutSignature   
); 
```  

## <a name="parameters"></a>参数

`vFunc`  
[in]此参数是未使用。

`ptr`  
[in]一个指向[IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)实例。

`lFlags`  
[in] 保留。 此参数必须为 0。

`pName`  
[out]一个指针，它指向`null`之前调用。 当该函数返回时，一个新的地址`BSTR`，其中包含方法名称。 

`ppSignatureIn`  
[out]接收指向指针的指针[IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) ，其中包含`in`方法的参数。 

`ppSignatureOut`  
[out]接收指向指针的指针[IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) ，其中包含`out`方法的参数。 

## <a name="return-value"></a>返回值

此函数返回以下值中定义*WbemCli.h*标头文件，也可以在定义它们为常量在代码中：

|返回的常量  |值  |描述  |
|---------|---------|---------|
| `WBEM_E_UNEXPECTED` | 0x8004101d | 出现不需要调用[ `BeginEnumeration` ](beginenumeration.md)函数。 |
| `WBEM_S_NO_ERROR` | 0 | 函数调用成功。  |
| `WBEM_S_NO_MORE_DATA` | 0x40005 | 枚举中没有更多属性。 |
  
## <a name="remarks"></a>备注

此函数包装对的调用[IWbemClassObject::NextMethod](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-nextmethod)方法。

调用方通过调用开始枚举序列[BeginMethodEnumeration](beginmethodenumeration.md)函数，并随后调用 [NextMethod] 函数，直到该函数将返回`WBEM_S_NO_MORE_DATA`。 （可选） 调用方通过调用完成序列[EndMethodEnumeration](endmethodenumeration.md)。 调用方可能会提前终止枚举，通过调用[EndMethodEnumeration](endmethodenumeration.md)在任何时间。

## <a name="example"></a>示例

有关 c + + 示例，请参阅[IWbemClassObject::NextMethod](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-nextmethod)方法。

## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** WMINet_Utils.idl  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>请参阅
- [WMI 和性能计数器 （非托管 API 参考）](index.md)
