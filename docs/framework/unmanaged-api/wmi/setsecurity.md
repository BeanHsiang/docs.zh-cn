---
title: SetSecurity 函数 （非托管 API 参考）
description: SetSecurity 函数检索当前线程的模拟令牌。
ms.date: 11/06/2017
api_name:
- SetSecurity
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- SetSecurity
helpviewer_keywords:
- SetSecurity function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7200e3a19fcadabb5e149c38b620b3f60907c392
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57377412"
---
# <a name="setsecurity-function"></a>SetSecurity 函数

检索与当前线程关联的模拟令牌。 

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>语法

```
HRESULT SetSecurity (
   [out] boolean* pNeedToReset, 
   [out] HANDLE* pCurrentThreadToken
); 
```

## <a name="parameters"></a>参数

`pNeedToReset`\
[out]该函数返回时，包含一个指向`boolean`，该值指示令牌是否应通过调用重置[ResetSecurity](resetsecurity.md)函数。

`token`\
[out]当函数返回时，包含与当前线程关联的模拟令牌句柄的指针。 其值可以是`null`是否存在任何与当前线程关联的令牌。 

## <a name="return-value"></a>返回值

如果函数成功，返回值是`S_OK`(0)。

如果函数失败，返回值是一个非零错误代码。 若要获得扩展错误信息，请调用[GetErrorInfo](geterrorinfo.md)函数。

## <a name="requirements"></a>要求

 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。

 **标头：** WMINet_Utils.idl

 **.NET Framework 版本：**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>请参阅

- [WMI 和性能计数器 （非托管 API 参考）](index.md)