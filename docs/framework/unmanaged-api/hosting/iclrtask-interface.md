---
title: ICLRTask 接口
ms.date: 03/30/2017
api_name:
- ICLRTask
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRTask
helpviewer_keywords:
- ICLRTask interface [.NET Framework hosting]
ms.assetid: b3a44df3-578a-4451-b55e-70c8e7695f5e
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9d5f0bb07498203d3db57ac3948efddce4f050a2
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54533710"
---
# <a name="iclrtask-interface"></a>ICLRTask 接口
提供允许主机发出请求的公共语言运行时 (CLR)，或向 CLR 有关关联的任务提供通知的方法。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[Abort 方法](../../../../docs/framework/unmanaged-api/hosting/iclrtask-abort-method.md)|CLR 中止任务的请求的当前`ICLRTask`实例所表示。|  
|[ExitTask 方法](../../../../docs/framework/unmanaged-api/hosting/iclrtask-exittask-method.md)|通知与当前任务关联的 CLR`ICLRTask`实例即将结束，并尝试正常关闭任务。|  
|[GetMemStats 方法](../../../../docs/framework/unmanaged-api/hosting/iclrtask-getmemstats-method.md)|获取由当前任务的内存资源使用统计信息`ICLRTask`实例。|  
|[LocksHeld 方法](../../../../docs/framework/unmanaged-api/hosting/iclrtask-locksheld-method.md)|获取当前任务上持有的锁数。|  
|[NeedsPriorityScheduling 方法](../../../../docs/framework/unmanaged-api/hosting/iclrtask-needspriorityscheduling-method.md)|获取一个值，该值指示主机是否应将高优先级分配给重新安排任务由当前`ICLRTask`实例。|  
|[Reset 方法](../../../../docs/framework/unmanaged-api/hosting/iclrtask-reset-method.md)|通知 CLR，宿主完成某项任务，并使 CLR 能够重复使用当前`ICLRTask`实例来表示另一个任务。|  
|[RudeAbort 方法](../../../../docs/framework/unmanaged-api/hosting/iclrtask-rudeabort-method.md)|会导致 CLR 中止表示由当前的任务`ICLRTask`实例立即，不保证会执行终结器。|  
|[SetTaskIdentifier 方法](../../../../docs/framework/unmanaged-api/hosting/iclrtask-settaskidentifier-method.md)|设置表示由当前的任务的唯一标识符`ICLRTask`实例，以便在调试中使用。|  
|[SwitchIn 方法](../../../../docs/framework/unmanaged-api/hosting/iclrtask-switchin-method.md)|通知当前所表示的任务的 CLR`ICLRTask`实例处于可操作状态。|  
|[SwitchOut 方法](../../../../docs/framework/unmanaged-api/hosting/iclrtask-switchout-method.md)|通知当前所表示的任务的 CLR`ICLRTask`实例不再处于可操作状态。|  
|[YieldTask 方法](../../../../docs/framework/unmanaged-api/hosting/iclrtask-yieldtask-method.md)|请求的 CLR 分配处理器时间供其他任务。 CLR 不保证将该任务处于它可以产生的处理时间的状态。|  
  
## <a name="remarks"></a>备注  
 `ICLRTask` CLR 任务的表示形式。 在代码执行期间任何时候，可以描述任务作为运行或等待运行。 在宿主调用`ICLRTask::SwitchIn`方法以通知 CLR 的任务的当前`ICLRTask`实例表示现在处于可操作的状态。 在调用`ICLRTask::SwitchIn`，主机可以在运行时要求线程关联，通过调用指定的位置的情况下除外计划在任何操作系统线程，任务[ihosttaskmanager:: Beginthreadaffinity](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-beginthreadaffinity-method.md)和[Ihosttaskmanager:: Endthreadaffinity](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-endthreadaffinity-method.md)方法。 一段时间后，操作系统可能会决定从线程中删除任务并将其放到非运行状态。 例如，可能发生此错误时任务同步基元上阻塞，或等待 I/O 操作完成。 在宿主调用[SwitchOut](../../../../docs/framework/unmanaged-api/hosting/iclrtask-switchout-method.md)来通知任务表示由当前 CLR`ICLRTask`实例不再处于可操作状态。  
  
 执行代码的结尾通常终止任务。 此时，主机将调用`ICLRTask::ExitTask`销毁关联`ICLRTask`。 但是，任务也都可以通过使用调用回收`ICLRTask::Reset`，它允许`ICLRTask`实例，若要再次使用。 这种方法可以防止反复创建和销毁实例的开销。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** MSCorEE.h  
  
 **库：** 包含为 MSCorEE.dll 中的资源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [ICLRTaskManager 接口](../../../../docs/framework/unmanaged-api/hosting/iclrtaskmanager-interface.md)
- [IHostTask 接口](../../../../docs/framework/unmanaged-api/hosting/ihosttask-interface.md)
- [IHostTaskManager 接口](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-interface.md)
- [承载接口](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
- [ICLRTask2 接口](../../../../docs/framework/unmanaged-api/hosting/iclrtask2-interface.md)
