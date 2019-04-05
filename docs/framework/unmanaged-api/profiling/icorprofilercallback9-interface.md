---
title: ICorProfilerCallback9 Interface
ms.date: 04/10/2018
api_name:
- ICorProfilerCallback9
api_location:
- mscorwks.dll
- corprof.idl
api_type:
- COM
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a6c480af921fb0259ef85beec8d8f65bdd430522
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54689297"
---
# <a name="icorprofilercallback9-interface"></a>ICorProfilerCallback9 Interface
[.NET Framework 4.7.2 及更高版本中受支持]  

 子类[ICorProfilerCallback8](icorprofilercallback8-interface.md)提供公共语言运行时用于通知探查器动态方法已被垃圾回收并随后卸载的回调方法。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[DynamicMethodUnloaded 方法](ICorProfilerCallback9-dynamicmethodunloaded-method.md)|通知探查器动态方法已被垃圾回收并随后卸载。|  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../get-started/system-requirements.md)。  
  
 **标头：** CorProf.idl, CorProf.h  
  
**.NET Framework 版本：**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  

## <a name="see-also"></a>请参阅
- [Profiling 接口](profiling-interfaces.md)
- [ICorProfilerCallback8 接口](icorprofilercallback9-interface.md)
- [ICorProfilerCallback8.DynamicMethodJITCompilationStarted 方法](icorprofilercallback8-dynamicmethodjitcompilationstarted-method.md)
- [ICorProfilerCallback8.DynamicMethodJITCompilationFinished 方法](icorprofilercallback8-dynamicmethodjitcompilationfinished-method.md)
