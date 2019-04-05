---
title: ICLRDebuggingLibraryProvider::ProvideLibrary 方法
ms.date: 03/30/2017
api_name:
- ICLRDebuggingLibraryProvider.ProvideLibrary Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRDebuggingLibraryProvider::ProvideLibrary
helpviewer_keywords:
- ProvideLibrary method [.NET Framework debugging]
- ICLRDebuggingLibraryProvider::ProvideLibrary method [.NET Framework debugging]
ms.assetid: 86f06245-9517-49be-8d8c-ca5deaf34c02
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 3dd1038fdc8b22b99e1c8c7b753b46b9ce877355
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57496438"
---
# <a name="iclrdebugginglibraryproviderprovidelibrary-method"></a>ICLRDebuggingLibraryProvider::ProvideLibrary 方法
获取一个库提供程序允许公共语言运行时 (CLR) 特定于版本的调试库定位和加载根据需要的回调接口。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT ProvideLibrary(  
     [in] const WCHAR* pwszFileName,  
     [in] DWORD dwTimestamp,  
     [in] DWORD dwSizeOfImage,  
     [out] HMODULE* hModule);  
```  
  
## <a name="parameters"></a>参数  
 `pwszFilename`  
 [in]请求的模块的名称。  
  
 `dwTimestamp`  
 [in]日期时间戳存储在 PE 文件的 COFF 文件标头中。  
  
 `pLibraryProvider`  
 [in]`SizeOfImage` COFF 可选文件标头的 PE 文件中存储的字段。  
  
 `hModule`  
 [out]请求的模块句柄。  
  
## <a name="return-value"></a>返回值  
 此方法返回以下特定 HRESULT 以及表示方法失败的 HRESULT 错误。  
  
|HRESULT|描述|  
|-------------|-----------------|  
|S_OK|该方法已成功完成。|  
  
## <a name="exceptions"></a>Exceptions  
  
## <a name="remarks"></a>备注  
 `ProvideLibrary` 使调试器能够提供所需的调试特定 CLR 文件，如 mscordbi.dll 和 mscordacwks.dll 的模块。 模块句柄必须在调用之前保持有效[iclrdebugging:: Canunloadnow](../../../../docs/framework/unmanaged-api/debugging/iclrdebugging-canunloadnow-method.md)方法指示，它们可能会被释放，此时它是调用方负责释放句柄。  
  
 调试器可能会使用任何可用的方式来定位或获得调试模块。  
  
> [!IMPORTANT]
>  此功能允许 API 调用方提供的包含可执行文件，并可能是恶意的代码模块。 作为安全预防措施，调用方不应使用`ProvideLibrary`分发不愿意执行本身的任何代码。  
>   
>  如果在已发布的库中，如 mscordbi.dll 或 mscordacwks.dll，发现了严重的安全问题可以修补该填充程序来识别错误版本的文件。 填充程序可以然后修补版本的文件中的发出请求并拒绝不适用的版本，如果响应任何请求中提供了它们。 这可能仅当用户已修补到填充程序的新版本。 未安装修补程序的版本仍易受攻击。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [调试接口](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
- [调试](../../../../docs/framework/unmanaged-api/debugging/index.md)
