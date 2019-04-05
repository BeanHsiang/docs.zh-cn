---
title: ICLRTask::Reset 方法
ms.date: 03/30/2017
api_name:
- ICLRTask.Reset
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRTask::Reset
helpviewer_keywords:
- ICLRTask::Reset method [.NET Framework hosting]
- Reset method, ICLRTask interface [.NET Framework hosting]
ms.assetid: 1bfb5d3a-0ffd-4bb4-9bf6-aec00cb675b7
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ae0a2a3af532b81d7b346cdd17da1712dfa3cba8
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57499922"
---
# <a name="iclrtaskreset-method"></a>ICLRTask::Reset 方法
通知公共语言运行时 (CLR)，主机具有完成某项任务，并使 CLR 能够重复使用当前[ICLRTask](../../../../docs/framework/unmanaged-api/hosting/iclrtask-interface.md)实例来表示另一个任务。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT Reset (  
    [in] BOOL fFull  
);  
```  
  
## <a name="parameters"></a>参数  
 `fFull`  
 [in]`true`，如果在运行时应重置与当前相关的安全和区域设置信息的补充所有相关的帖子的静态值`ICLRTask`实例; 否则为`false`。  
  
 如果值为`true`，运行时将使用存储的数据重置<xref:System.Threading.Thread.AllocateDataSlot%2A>或<xref:System.Threading.Thread.AllocateNamedDataSlot%2A>。  
  
## <a name="return-value"></a>返回值  
  
|HRESULT|描述|  
|-------------|-----------------|  
|S_OK|`Reset` 已成功返回。|  
|HOST_E_CLRNOTAVAILABLE|CLR 尚未加载到进程中，或处于不能运行托管的代码或处理调用的状态。 已成功|  
|HOST_E_TIMEOUT|呼叫已超时。|  
|HOST_E_NOT_OWNER|调用方不拥有该锁。|  
|HOST_E_ABANDONED|事件已取消时被阻塞的线程或纤程正在等待它。|  
|E_FAIL|发生未知的灾难性故障。 如果某方法返回 E_FAIL，CLR 不再在进程内可用。 对托管方法的后续调用返回 HOST_E_CLRNOTAVAILABLE。|  
  
## <a name="remarks"></a>备注  
 CLR 可以回收之前创建`ICLRTask`实例，以避免重复创建新实例，每次需要新任务时的系统开销。 主机启用此功能通过调用`ICLRTask::Reset`而不是[iclrtask:: Exittask](../../../../docs/framework/unmanaged-api/hosting/iclrtask-exittask-method.md)时它已完成一个任务。 以下列表总结了正常的生命周期的`ICLRTask`实例：  
  
1.  在运行时创建一个新`ICLRTask`实例。  
  
2.  运行时调用[ihosttaskmanager:: Getcurrenttask](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-getcurrenttask-method.md)获取与当前主机任务的引用。  
  
3.  运行时调用[ihosttask:: Setclrtask](../../../../docs/framework/unmanaged-api/hosting/ihosttask-setclrtask-method.md)要与主机任务关联的新实例。  
  
4.  该任务执行，并完成。  
  
5.  宿主通过调用销毁任务`ICLRTask::ExitTask`。  
  
 `Reset` 更改此方案的两种方法。 在上面的步骤 5，宿主调用`Reset`将任务重置为空白状态，然后将分离`ICLRTask`实例及其关联[IHostTask](../../../../docs/framework/unmanaged-api/hosting/ihosttask-interface.md)实例。 如果需要，也可以缓存主机`IHostTask`以供重复使用的实例。 在上述步骤 1 中，运行时提取回收`ICLRTask`从缓存而不是创建一个新实例。  
  
 此方法适用于主机也有一个可重用工作线程任务的池。 主机时销毁其中一个其`IHostTask`情况下，它将销毁相应`ICLRTask`通过调用`ExitTask`。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** MSCorEE.h  
  
 **库：** 包含为 MSCorEE.dll 中的资源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [ICLRTask 接口](../../../../docs/framework/unmanaged-api/hosting/iclrtask-interface.md)
- [ICLRTaskManager 接口](../../../../docs/framework/unmanaged-api/hosting/iclrtaskmanager-interface.md)
- [IHostTask 接口](../../../../docs/framework/unmanaged-api/hosting/ihosttask-interface.md)
- [IHostTaskManager 接口](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-interface.md)
