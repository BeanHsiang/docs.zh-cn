---
title: CoEEShutDownCOM 函数
ms.date: 03/30/2017
api_name:
- CoEEShutDownCOM
api_location:
- mscoree.dll
- clr.dll
- mscorwks.dll
- mscoreei.dll
- mscorsvr.dll
api_type:
- DLLExport
f1_keywords:
- CoEEShutDownCOM
helpviewer_keywords:
- CoEEShutDownCOM function [.NET Framework hosting]
ms.assetid: b634cae2-632f-4737-9be4-92d0652844d7
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d990d63a007240ab0bd0240f7b45fed52e2a2129
ms.sourcegitcommit: 79066169e93d9d65203028b21983574ad9dcf6b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57212243"
---
# <a name="coeeshutdowncom-function"></a>CoEEShutDownCOM 函数
强制公共语言运行时 (CLR) 以释放它在运行时可调用包装 (RCW) 内所持有的所有接口指针。 释放所有 RCW 缓存效果。 中已弃用此全局函数[!INCLUDE[net_v40_long](../../../../includes/net-v40-long-md.md)]。 相反，对于特定的运行时使用的入口点。  
  
## <a name="syntax"></a>语法  
  
```  
void CoEEShutDownCOM ();  
```  
  
## <a name="remarks"></a>备注  
 `CoEEShutDownCOM`函数首先释放所有上下文和所有缓存中的所有 Rcw，并删除现有的安装程序中的任何关闭的通知。 没有 DLL 卸载时发生。  
  
> [!CAUTION]
>  此函数会影响加载到进程的所有运行时。  
  
 从[!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)]，调用此函数在你想要影响的特定运行时的入口点。 若要获取的入口点，请调用[iclrruntimeinfo:: Getprocaddress](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-getprocaddress-method.md)方法并指定"CoEEShutDownCOM"。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** Cor.h  
  
 **库：** 包含为 MsCorEE.dll 中的资源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [元数据全局静态函数](../../../../docs/framework/unmanaged-api/metadata/metadata-global-static-functions.md)
