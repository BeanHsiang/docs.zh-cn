---
title: ICLRDebugManager 接口
ms.date: 03/30/2017
api_name:
- ICLRDebugManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRDebugManager
helpviewer_keywords:
- ICLRDebugManager interface [.NET Framework hosting]
ms.assetid: e835062c-c7d6-4945-8a44-2de7ebf3928e
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 515eb0633c82c3e1386487d1866de79c9898c9cd
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54654602"
---
# <a name="iclrdebugmanager-interface"></a>ICLRDebugManager 接口
提供允许主机以将一组任务标识符和友好名称与相关联的方法。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[BeginConnection 方法](../../../../docs/framework/unmanaged-api/hosting/iclrdebugmanager-beginconnection-method.md)|建立新连接来将任务与标识符和友好名称相关联的主机与调试器之间。|  
|[EndConnection 方法](../../../../docs/framework/unmanaged-api/hosting/iclrdebugmanager-endconnection-method.md)|删除任务列表和标识符和友好名称之间的关联。|  
|[GetDacl 方法](../../../../docs/framework/unmanaged-api/hosting/iclrdebugmanager-getdacl-method.md)|未实现此方法。|  
|[IsDebuggerAttached 方法](../../../../docs/framework/unmanaged-api/hosting/iclrdebugmanager-isdebuggerattached-method.md)|获取一个值，它指示调试器是否已附加到进程。|  
|[SetConnectionTasks 方法](../../../../docs/framework/unmanaged-api/hosting/iclrdebugmanager-setconnectiontasks-method.md)|将一组相关联[ICLRTask](../../../../docs/framework/unmanaged-api/hosting/iclrtask-interface.md)实例标识符和友好名称。|  
|[SetDacl 方法](../../../../docs/framework/unmanaged-api/hosting/iclrdebugmanager-setdacl-method.md)|未实现此方法。|  
|[SetSymbolReadingPolicy 方法](../../../../docs/framework/unmanaged-api/hosting/iclrdebugmanager-setsymbolreadingpolicy-method.md)|设置用于读取程序数据库 (PDB) 文件的策略。 策略将确定是否在调用堆栈中包括行号和文件相关信息。|  
  
## <a name="remarks"></a>备注  
 在调试方案中，主机可能需要根据其自己的编程逻辑组任务。 例如，一组将允许开发人员若要查看仅由开发人员的 Api，而不是查看在进程中运行的每项任务所需的任务。 `ICLRDebugManager` 允许主机来实现这种类型的分组。  
  
> [!IMPORTANT]
>  三个`ICLRDebugManager`方法， `BeginConnection`，`SetConnectionTasks`和`EndConnection`，依赖于彼此。 按给定的顺序按预期方式工作，必须调用它们。  
  
 分组的标识符和友好名称的主机分配给分组，具有对公共语言运行时 (CLR) 没有意义。 CLR 只是将信息传递到调试器。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** MSCorEE.h  
  
 **库：** 包含为 MSCorEE.dll 中的资源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [承载接口](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
