---
title: ICLRProfiling::AttachProfiler 方法
ms.date: 03/30/2017
api_name:
- IClrProfiling.AttachProfiler Method
api_location:
- Mscorwks.dll
api_type:
- COM
f1_keywords:
- IClrProfiling::AttachProfiler
helpviewer_keywords:
- AttachProfiler method [.NET Framework profiling]
- IClrProfiling::AttachProfiler method [.NET Framework profiling]
ms.assetid: 535a6839-c443-405b-a6f4-e2af90725d5b
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 7fcbc75d17f0c154671d5997d7e6cbb59ef8440e
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57468996"
---
# <a name="iclrprofilingattachprofiler-method"></a>ICLRProfiling::AttachProfiler 方法
将指定的探查器附加到指定的进程中。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT AttachProfiler(  
  [in] DWORD dwProfileeProcessID,  
  [in] DWORD dwMillisecondsMax,                     // optional  
  [in] const CLSID * pClsidProfiler,  
  [in] LPCWSTR wszProfilerPath,                     // optional  
  [in] size_is(cbClientData)] void * pvClientData,  // optional  
  [in] UINT cbClientData);                          // optional  
```  
  
## <a name="parameters"></a>参数  
 `dwProfileeProcessID`  
 [in] 应附加探查器的进程的进程 ID。 在 64 位计算机上，被分析进程的位数必须匹配调用 `AttachProfiler` 的触发进程的位数。 如果调用 `AttachProfiler` 的用户帐户具有管理特权，则目标进程可能是系统上的任何进程。 否则，相同的用户帐户必须拥有目标进程。  
  
 `dwMillisecondsMax`  
 [in] `AttachProfiler` 完成的持续时间（以毫秒为单位）。 触发器进程应传递一个特定探查器足以完成其初始化的已知超时。  
  
 `pClsidProfiler`  
 [in] 指向要加载的探查器 CLSID 的指针。 
  `AttachProfiler` 返回后，触发器进程可重用此内存。  
  
 `wszProfilerPath`  
 [in] 要加载的探查器 DLL 文件的完整路径。 此字符串应包含不超过 260 个字符，包括 null 终止符。 如果 `wszProfilerPath` 为 null 或为空字符串，公共语言运行时 (CLR) 将通过在 `pClsidProfiler` 指向的 CLSID 的注册表中查找探查器的 DLL 文件的位置。  
  
 `pvClientData`  
 [in]指向要传递给探查器数据[ICorProfilerCallback3::InitializeForAttach](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback3-initializeforattach-method.md)方法。 
  `AttachProfiler` 返回后，触发器进程可重用此内存。 如果 `pvClientData` 为 null，`cbClientData` 必须为 0（零）。  
  
 `cbClientData`  
 [in] `pvClientData` 指向的数据的大小（以字节为单位）。  
  
## <a name="return-value"></a>返回值  
 此方法将返回以下 HRESULT。  
  
|HRESULT|描述|  
|-------------|-----------------|  
|S_OK|指定的探查器已成功附加到目标进程中。|  
|CORPROF_E_PROFILER_ALREADY_ACTIVE|已有活动的或附加到目标进程的探查器。|  
|CORPROF_E_PROFILER_NOT_ATTACHABLE|指定的探查器不支持附件。 触发进程可能会尝试附加不同的探查器。|  
|CORPROF_E_PROFILEE_INCOMPATIBLE_WITH_TRIGGER|无法请求探查器附件，因为目标进程的版本与当前正在调用 `AttachProfiler` 的进程不兼容。|  
|HRESULT_FROM_WIN32(ERROR_ACCESS_DENIED)|触发进程的用户没有访问目标进程的权限。|  
|HRESULT_FROM_WIN32(ERROR_PRIVILEGE_NOT_HELD)|触发进程的用户没有将探查器附加到给定的目标进程所必需的特权。 应用程序事件日志可能包含详细信息。|  
|CORPROF_E_IPC_FAILED|与目标进程进行通信时发生错误。 通常在目标进程已关闭时，会发生此类错误。|  
|HRESULT_FROM_WIN32(ERROR_FILE_NOT_FOUND)|目标进程中不存在或未运行支持附件的 CLR。 这可能表示，自调用运行时枚举方法时，就已卸载 CLR。|  
|HRESULT_FROM_WIN32(ERROR_TIMEOUT)|尚未开始加载探查器，超时就已过期。 可重试附加操作。 当目标进程中的终结器运行时间长于超时值时，就会出现超时。|  
|E_INVALIDARG|一个或多个参数具有无效值。|  
|E_FAIL|出现其他未指定错误。|  
|其他错误代码|如果探查器的[ICorProfilerCallback3::InitializeForAttach](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback3-initializeforattach-method.md)方法返回一个 HRESULT，指示失败，`AttachProfiler`返回相同的 HRESULT。 在这种情况下，E_NOTIMPL 将转换为 CORPROF_E_PROFILER_NOT_ATTACHABLE。|  
  
## <a name="remarks"></a>备注  
  
## <a name="memory-management"></a>内存管理  
 与 COM 约定一致，`AttachProfiler` 的调用方（例如，由探查器开发人员创作的触发器代码）将负责分配和释放 `pvClientData` 参数指向的数据的内存。 当 CLR 执行 `AttachProfiler` 调用时，会创建 `pvClientData` 指向的内存的副本，并将其传输到目标进程中。 当目标进程内部的 CLR 接收到自己的 `pvClientData` 块副本时，会通过 `InitializeForAttach` 方法将块传递给探查器，然后从目标进程释放其 `pvClientData` 块的副本。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorProf.idl, CorProf.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [ICorProfilerCallback 接口](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
- [ICorProfilerInfo3 接口](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-interface.md)
- [Profiling 接口](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
- [分析](../../../../docs/framework/unmanaged-api/profiling/index.md)
