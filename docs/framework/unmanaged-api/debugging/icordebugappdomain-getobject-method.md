---
title: ICorDebugAppDomain::GetObject 方法
ms.date: 03/30/2017
api_name:
- ICorDebugAppDomain.GetObject
api_location:
- corguids.lib
api_type:
- COM
f1_keywords:
- ICorDebugAppDomain::GetObject
helpviewer_keywords:
- ICorDebugAppDomain::GetObject method [.NET Framework debugging]
- GetObject method, ICorDebugAppDomain interface [.NET Framework debugging]
ms.assetid: 78232e6f-ae18-4cfa-a6cd-e79471cf9d76
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 0ca9792df69f859e20f1d9e40754d1cec138945d
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57480021"
---
# <a name="icordebugappdomaingetobject-method"></a>ICorDebugAppDomain::GetObject 方法
获取对公共语言运行时 (CLR) 应用程序域的接口指针。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT GetObject (  
    [out] ICorDebugValue   **ppObject  
);  
```  
  
## <a name="parameters"></a>参数  
 `ppObject`  
 [out]指向一个 ICorDebugValue 接口对象，表示 CLR 应用程序域的地址的指针。  
  
## <a name="return-value"></a>返回值  
 如果托管<xref:System.AppDomain?displayProperty=nameWithType>尚未为此应用程序域已构造对象，该方法返回`S_FALSE`，并将`NULL`中`*ppObject`。  
  
## <a name="remarks"></a>备注  
 在进程中的每个应用程序域可能具有托管<xref:System.AppDomain?displayProperty=nameWithType>表示它在运行时中的对象。 此函数获取对应于此托管 ICorDebugValue 接口对象<xref:System.AppDomain?displayProperty=nameWithType>对象。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]
