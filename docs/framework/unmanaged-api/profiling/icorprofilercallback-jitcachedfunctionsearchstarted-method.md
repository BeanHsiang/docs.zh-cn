---
title: ICorProfilerCallback::JITCachedFunctionSearchStarted 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.JITCachedFunctionSearchStarted
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::JITCachedFunctionSearchStarted
helpviewer_keywords:
- JITCachedFunctionSearchStarted method [.NET Framework profiling]
- ICorProfilerCallback::JITCachedFunctionSearchStarted method [.NET Framework profiling]
ms.assetid: 5cba642c-0d80-48ee-889d-198c5044d821
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 526059e0895604d18025e8ad2fd037690243ff59
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57503068"
---
# <a name="icorprofilercallbackjitcachedfunctionsearchstarted-method"></a>ICorProfilerCallback::JITCachedFunctionSearchStarted 方法
通知探查器以前使用本机映像生成器 (NGen.exe) 编译的函数已开始搜索。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT JITCachedFunctionSearchStarted(  
    [in]  FunctionID functionId,  
    [out] BOOL *pbUseCachedFunction);  
```  
  
## <a name="parameters"></a>参数  
 `functionId`  
 [in]为其执行搜索的函数的 ID。  
  
 `pbUseCachedFunction`  
 [out]`true`如果执行引擎应使用的缓存的版本的函数 （如果可用）; 否则为`false`。 如果值为`false`，则执行引擎将执行 JIT 编译的函数而不是使用不是 JIT 编译的版本。  
  
## <a name="remarks"></a>备注  
 在.NET Framework 2.0 版中，`JITCachedFunctionSearchStarted`并[icorprofilercallback:: Jitcachedfunctionsearchfinished 方法](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-jitcachedfunctionsearchfinished-method.md)回调不会为正则 NGen 映像中的所有函数。 仅为配置文件优化 NGen 映像将在图中生成的所有函数的回调。 但是，由于的额外开销，探查器应请求探查器优化 NGen 映像仅当它要使用这些回调以强制对函数进行编译中实时 (JIT)。 否则，探查器应使用延迟策略，用于收集函数的信息。  
  
 探查器必须支持的分析的应用程序的多个线程同时调用相同的方法的情况。 例如，一个线程调用`JITCachedFunctionSearchStarted`，并通过设置响应探查器*pbUseCachedFunction*为 FALSE，以强制执行 JIT 编译。 随后将调用的线程[icorprofilercallback:: Jitcompilationstarted](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-jitcompilationstarted-method.md)并[icorprofilercallback:: Jitcompilationfinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-jitcompilationfinished-method.md)。  
  
 现在，线程 B 调用`JITCachedFunctionSearchStarted`相同的函数。 即使探查器已声明其意图到 JIT 编译的函数，探查器收到第二个回调，因为探查器已答复了线程 A 的调用之前，线程 B 发送回调`JITCachedFunctionSearchStarted`。 线程调用的顺序取决于如何计划的线程。  
  
 在探查器收到重复的回调，它必须设置由引用的值`pbUseCachedFunction`为相同的值的所有重复的回调。 也就是说，当`JITCachedFunctionSearchStarted`多次调用具有相同`functionId`值，探查器必须响应相同每次。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorProf.idl, CorProf.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [ICorProfilerCallback 接口](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
