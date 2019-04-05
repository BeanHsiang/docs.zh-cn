---
title: ICLRTask2 接口
ms.date: 03/30/2017
api_name:
- ICLRTask2
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRTask2
helpviewer_keywords:
- ICLRTask2 interface [.NET Framework hosting]
ms.assetid: b5a22ebc-0582-49de-91f9-97a3d9789290
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 8cbd627eff9318fce38ec238e5fa686cc9d759b8
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54627182"
---
# <a name="iclrtask2-interface"></a>ICLRTask2 接口
提供的所有功能[ICLRTask](../../../../docs/framework/unmanaged-api/hosting/iclrtask-interface.md)接口; 此外，还都提供允许线程中止当前线程上延迟的方法。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[BeginPreventAsyncAbort 方法](../../../../docs/framework/unmanaged-api/hosting/iclrtask2-beginpreventasyncabort-method.md)|延迟的新线程中止当前线程上的请求。|  
|[EndPreventAsyncAbort 方法](../../../../docs/framework/unmanaged-api/hosting/iclrtask2-endpreventasyncabort-method.md)|允许新的或挂起的线程中止请求导致线程中止当前线程上。|  
  
## <a name="remarks"></a>备注  
 `ICLRTask2`接口继承自`ICLRTask`接口，并添加方法，以使宿主延迟线程中止，若要保护的代码必须不发生故障的区域。 调用`BeginPreventAsyncAbort`递增的当前线程和调用的延迟线程中止计数器`EndPreventAsyncAbort`递减它。 调用`BeginPreventAsyncAbort`和`EndPreventAsyncAbort`可以嵌套。 只要该计数器是大于零，则会延迟当前线程的线程中止。  
  
 如果调用`BeginPreventAsyncAbort`和`EndPreventAsyncAbort`不是成对，则可能会进入在哪个线程中止不能传递到当前线程的状态。  
  
 不为线程中止本身采用延迟。  
  
 虚拟机 (VM) 在内部使用此功能公开的功能。 不恰当使用这些方法的可能导致在 VM 中未指定的行为。 例如，调用`EndPreventAsyncAbort`而无需第一个调用`BeginPreventAsyncAbort`VM 先前已增大时，无法设置计数器为零。 同样，内部计数器不会检查溢出。 如果因为加在主机和 VM 超出其不可或缺的限制，所产生的行为是未指定。  
  
 为继承其成员的信息`ICLRTask`和此接口的其他用法，请参阅[ICLRTask](../../../../docs/framework/unmanaged-api/hosting/iclrtask-interface.md)接口。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** MSCorEE.h  
  
 **库：** 包含为 MSCorEE.dll 中的资源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [ICLRTask 接口](../../../../docs/framework/unmanaged-api/hosting/iclrtask-interface.md)
- [ICLRTaskManager 接口](../../../../docs/framework/unmanaged-api/hosting/iclrtaskmanager-interface.md)
- [IHostTask 接口](../../../../docs/framework/unmanaged-api/hosting/ihosttask-interface.md)
- [IHostTaskManager 接口](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-interface.md)
- [承载接口](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
