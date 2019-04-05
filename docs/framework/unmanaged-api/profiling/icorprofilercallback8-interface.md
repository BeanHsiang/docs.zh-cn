---
title: ICorProfilerCallback8 Interface
ms.date: 04/10/2018
api_name:
- ICorProfilerCallback8
api_location:
- mscorwks.dll
- corprof.idl
api_type:
- COM
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a3bdf79582619777a22c80caac5b4e90d603f3a8
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54675010"
---
# <a name="icorprofilercallback8-interface"></a>ICorProfilerCallback8 Interface
[.NET Framework 4.7 和更高版本中受支持]  

 子类[ICorProfilerCallback7](icorprofilercallback7-interface.md)提供公共语言运行时用于通知探查器中的动态方法的 JIT 编译已启动和完成的回调方法。 
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[DynamicMethodJITCompilationStarted 方法](icorprofilercallback8-dynamicmethodjitcompilationstarted-method.md)|通知探查器已启动的动态方法的 JIT 编译。|  
|[DynamicMethodJITCompilationFinished 方法](icorprofilercallback8-dynamicmethodjitcompilationfinished-method.md)|通知探查器已完成的动态方法的 JIT 编译。|  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../get-started/system-requirements.md)。  
  
 **标头：** CorProf.idl, CorProf.h  
  
**.NET Framework 版本：**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  

## <a name="see-also"></a>请参阅
- [Profiling 接口](profiling-interfaces.md)
- [ICorProfilerCallback9 接口](icorprofilercallback9-interface.md)
