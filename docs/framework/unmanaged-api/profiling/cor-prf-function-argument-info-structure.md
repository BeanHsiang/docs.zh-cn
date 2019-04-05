---
title: COR_PRF_FUNCTION_ARGUMENT_INFO 结构
ms.date: 03/30/2017
api_name:
- COR_PRF_FUNCTION_ARGUMENT_INFO
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_FUNCTION_ARGUMENT_INFO
helpviewer_keywords:
- COR_PRF_FUNCTION_ARGUMENT_INFO structure [.NET Framework profiling]
ms.assetid: 07cf3bab-e193-4991-8205-3f41cf2d67b3
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 0bb92f9ba8ff0aed1c6eb1fa44fb4d7c9abc186a
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54714225"
---
# <a name="corprffunctionargumentinfo-structure"></a>COR_PRF_FUNCTION_ARGUMENT_INFO 结构
按从左向右的顺序表示函数的自变量。  
  
## <a name="syntax"></a>语法  
  
```  
typedef struct _COR_PRF_FUNCTION_ARGUMENT_INFO {  
    ULONG numRanges;  
    ULONG totalArgumentSize;  
    COR_PRF_FUNCTION_ARGUMENT_RANGE ranges[1];  
} COR_PRF_FUNCTION_ARGUMENT_INFO;  
```  
  
## <a name="members"></a>成员  
  
|成员|描述|  
|------------|-----------------|  
|`numRanges`|自变量的块的数目。 也就是说，此值是数[COR_PRF_FUNCTION_ARGUMENT_RANGE](../../../../docs/framework/unmanaged-api/profiling/cor-prf-function-argument-range-structure.md)结构中`ranges`数组。|  
|`totalArgumentSize`|所有自变量的总大小。 换而言之，此值是参数长度的总和。|  
|`ranges`|一个数组`COR_PRF_FUNCTION_ARGUMENT_RANGE`结构，其中每个表示一个函数自变量的块。|  
  
## <a name="remarks"></a>备注  
 一个函数可能会有多的参数。 不可能在内存中连续存储这些参数。 你可能在一个位置的三个参数的块、 在另一个位置中的两个参数的块和一个自变量的不同位置中的最后一个块。 这些参数均为相同的功能;它们只存储在不同的位置。  
  
 `COR_PRF_FUNCTION_ARGUMENT_INFO`结构表示的单个函数的所有自变量。 它使用数组引用的函数自变量的所有块。 因此，对于单个函数，具有单个`COR_PRF_FUNCTION_ARGUMENT_INFO`结构，它引用多个`COR_PRF_FUNCTION_ARGUMENT_RANGE`结构，其中每个点对一个或多个函数参数。  
  
 存储在寄存器中的参数将溢出到内存中才能生成结构。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorProf.idl  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [分析结构](../../../../docs/framework/unmanaged-api/profiling/profiling-structures.md)
