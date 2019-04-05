---
title: ICorDebugThread::EnumerateChains 方法
ms.date: 03/30/2017
api_name:
- ICorDebugThread.EnumerateChains
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread::EnumerateChains
helpviewer_keywords:
- EnumerateChains method [.NET Framework debugging]
- ICorDebugThread::EnumerateChains method [.NET Framework debugging]
ms.assetid: ec00bc21-117e-4acd-9301-2cfafd5be8d3
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: e01f94e9574ebc032bc45490fd88ff92e9104aa3
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57482855"
---
# <a name="icordebugthreadenumeratechains-method"></a>ICorDebugThread::EnumerateChains 方法
获取包含此 ICorDebugThread 对象中的所有堆栈链的 ICorDebugChainEnum 枚举器的接口指针。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT EnumerateChains (  
    [out] ICorDebugChainEnum **ppChains  
);  
```  
  
## <a name="parameters"></a>参数  
 `ppChains`  
 [out]指向的地址的指针`ICorDebugChainEnum`允许所有堆栈的枚举对象链接在此线程开始活动 （即，最新的） 链中。  
  
## <a name="remarks"></a>备注  
 堆栈链表示在线程的物理调用堆栈。 在以下情况下创建一个堆栈链边界：  
  
-   托管到非托管或非托管到托管的转换。  
  
-   上下文切换。  
  
-   一个调试器用户线程进行的攻击。  
  
 在单一上下文中运行纯托管的代码的线程的简单情况下，线程和堆栈链之间存在一对一的对应关系。  
  
 调试程序可能想要为逻辑调用堆栈中重新排列的所有线程的物理调用堆栈。 这通常需要对所有线程的链由其调用方/被调用方关系进行排序并重新分组。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
