---
title: FormatFromRawValue 函数 （非托管 API 参考）
description: FormatFromRawValue 函数将转换为指定格式的原始性能数据。
ms.date: 11/21/2017
api_name:
- FormatFromRawValue
api_location:
- PerfCounter.dll
api_type:
- DLLExport
f1_keywords:
- FormatFromRawValue
helpviewer_keywords:
- FormatFromRawValue function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 44a84b03c85cc1332c07ffbaf53187b7f01d0236
ms.sourcegitcommit: e994e47d3582bf09ae487ecbd53c0dac30aebaf7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2019
ms.locfileid: "58262471"
---
# <a name="formatfromrawvalue-function"></a>FormatFromRawValue 函数
如果格式转换是基于时间的，则将一个或两个原始性能数据值转换为指定格式。 

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>语法

```
int FormatFromRawValue (
   [in] uint                    dwCounterType, 
   [in] uint                    dwFormat, 
   [in] long*                   pTimeBase,
   [in] PDH_RAW_COUNTER*        pRawValue1,
   [in] PDH_RAW_COUNTER*        pRawValue2,
   [out] PDH_FMT_COUNTERVALUE*  pFmtValue
); 
```

## <a name="parameters"></a>参数

`dwCounterType`\
[in]计数器类型。 计数器类型的列表，请参阅[WMI 性能计数器类型](/windows/desktop/WmiSdk/wmi-performance-counter-types)。 `dwCounterType` 可以是任何计数器类型除外`PERF_LARGE_RAW_FRACTION`和`PERF_LARGE_RAW_BASE`。 

`dwFormat`\
[in]若要将原始性能数据转换为的格式。 它可以是下列值之一：

|返回的常量  |值  |描述 |
|---------|---------|---------|
| `PDH_FMT_DOUBLE` |0x00000200 | 返回作为双精度浮点值的计算的值。 | 
| `PDH_FMT_LARGE` | 0x00000400 | 以 64 位整数形式返回计算的值。 |
| `PDH_FMT_LONG` | 0x00000100 | 返回作为 32 位整数的计算的值。 |

其中一个以前的值可以是或运算的以下缩放标志之一：

|返回的常量  |“值”  |描述 |
|---------|---------|---------|
| `PDH_FMT_NOSCALE` | 0x00001000 | 不适用于计数器的比例因子。 |
| `PDH_FMT_1000` | 0x00002000 | 最终值乘以 1,000。 | 

`pTimeBase`\
[in]时间基准，如有必要格式转换为指向的指针。 如果没有格式转换所需时间基本信息，则忽略此参数的值。

`pRawValue1`\ [in] 一个指向[ `PDH_RAW_COUNTER` ](/windows/desktop/api/pdh/ns-pdh-_pdh_raw_counter)结构，它表示原始性能值。

`pRawValue2`\
[in]一个指向[ `PDH_RAW_COUNTER` ](/windows/desktop/api/pdh/ns-pdh-_pdh_raw_counter)结构，它表示第二个原始性能值。 如果第二个原始性能值不是必需的此参数应为`null`。

`pFmtValue`\
[out]一个指向[ `PDH_FMT_COUNTERVALUE` ](/windows/desktop/api/pdh/ns-pdh-_pdh_fmt_countervalue)接收格式化的性能值的结构。

## <a name="return-value"></a>返回值

此函数返回以下值：

|返回的常量  |“值”  |描述  |
|---------|---------|---------|
| `ERROR_SUCCESS` | 0 | 函数调用是成功的。 |
| `PDH_INVALID_ARGUMENT` | 0xC0000BBD | 必需的参数已丢失或不正确。 | 
| `PDH_INVALID_HANDLE` | 0xC0000BBC | 句柄不是有效的 PDH 对象。 |

## <a name="remarks"></a>备注

此函数包装对的调用[FormatFromRawValue](https://docs.microsoft.com/previous-versions/ms231047(v=vs.85))函数。

## <a name="requirements"></a>要求

 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。

 **库：** PerfCounter.dll

 **.NET Framework 版本：**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>请参阅

- [WMI 和性能计数器 （非托管 API 参考）](index.md)
