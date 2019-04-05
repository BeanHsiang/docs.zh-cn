---
title: GetHistoryFileDirectory 函数
ms.date: 03/30/2017
api_name:
- GetHistoryFileDirectory
api_location:
- fusion.dll
api_type:
- DLLExport
f1_keywords:
- GetHistoryFileDirectory
helpviewer_keywords:
- GetHistoryFileDirectory function [.NET Framework fusion]
ms.assetid: 93232222-926e-42ac-b85d-8a6d33977672
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 21742881c5aef7384be318297aa3432411c3d57c
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57479276"
---
# <a name="gethistoryfiledirectory-function"></a>GetHistoryFileDirectory 函数
检索应用程序历史记录目录的路径。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT GetHistoryFileDirectory (  
    [in]      LPWSTR      wzDir,  
    [in,out]  LPCWSTR  *pdwsize,  
);  
```  
  
## <a name="parameters"></a>参数  
 `wzDir`  
 [out]一个缓冲区来存放到应用程序历史记录目录的路径。  
  
 `pdwSize`  
 [in、 out]缓冲区的长度。  
  
## <a name="return-value"></a>返回值  
 除了以下值在 WinError.h 文件中定义，此方法将返回标准 COM 错误代码。  
  
|返回代码|描述|  
|-----------------|-----------------|  
|S_OK|该方法已成功完成。|  
|E_INVALIDARG|`wzDir` 或`pdwSize`是 null 或版本字符串不正确。|  
  
## <a name="remarks"></a>备注  
 成功完成后，`pdwSize`参数设置为路径字符串的长度。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** Fusion.h  
  
 **库：** Fusion.dll 和 Mscorwks.dll。 使用而不是 Mscorwks.dll Fusion.dll 确保面向.NET Framework 的正确版本。  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v11plus](../../../../includes/net-current-v11plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [CreateHistoryReader 函数](../../../../docs/framework/unmanaged-api/fusion/createhistoryreader-function.md)
- [NukeDownloadedCache 函数](../../../../docs/framework/unmanaged-api/fusion/nukedownloadedcache-function.md)
- [合成全局静态函数](../../../../docs/framework/unmanaged-api/fusion/fusion-global-static-functions.md)
