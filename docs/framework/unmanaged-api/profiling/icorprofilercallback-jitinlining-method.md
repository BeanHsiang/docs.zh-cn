---
title: ICorProfilerCallback::JITInlining 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.JITInlining
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::JITInlining
helpviewer_keywords:
- JITInlining method [.NET Framework profiling]
- ICorProfilerCallback::JITInlining method [.NET Framework profiling]
ms.assetid: c2f45801-dd38-4b78-b6b7-64397dc73f83
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 92060147677fec5c772b16a61fa6ed5c294132fa
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57471483"
---
# <a name="icorprofilercallbackjitinlining-method"></a>ICorProfilerCallback::JITInlining 方法
通知探查器实时 (JIT) 编译器将要插入一个嵌入另一个函数。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT JITInlining(  
    [in]  FunctionID callerId,  
    [in]  FunctionID calleeId,  
    [out] BOOL      *pfShouldInline);  
```  
  
## <a name="parameters"></a>参数  
 `callerId`  
 [in]在其中函数的 ID`calleeId`将插入函数。  
  
 `calleeId`  
 [in]要插入该函数的 ID。  
  
 `pfShouldInline`  
 [out]`true`若要允许插入发生; 否则为`false`。  
  
## <a name="remarks"></a>备注  
 探查器可以设置`pfShouldInline`到`false`以免`calleeId`函数中要插入到`callerId`函数。 此外，探查器可以全局内联插入使用禁用的 COR_PRF_DISABLE_INLINING 值[COR_PRF_MONITOR](../../../../docs/framework/unmanaged-api/profiling/cor-prf-monitor-enumeration.md)枚举。  
  
 内联函数插入不会引发事件进入或离开。 因此，探查器必须设置`pfShouldInline`到`false`为了生成准确的调用关系图。 设置`pfShouldInline`到`false`会影响性能，因为内联插入通常会提高速度和减少了单独的插入方法的 JIT 编译事件数。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorProf.idl, CorProf.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [ICorProfilerCallback 接口](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
