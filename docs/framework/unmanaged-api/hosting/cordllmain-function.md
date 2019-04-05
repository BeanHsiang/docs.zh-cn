---
title: _CorDllMain 函数
ms.date: 03/30/2017
api_name:
- _CorDllMain
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- _CorDllMain
helpviewer_keywords:
- _CorDllMain function [.NET Framework hosting]
ms.assetid: bc7b51cf-39d3-48ec-a5cb-2f179fbefff8
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c509f475d5bf0105ece9791ee3e51d21c298a31f
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2019
ms.locfileid: "57679302"
---
# <a name="cordllmain-function"></a>\_CorDllMain 函数

初始化公共语言运行时 (CLR) 中，查找托管的入口点 DLL 程序集 CLR 头中，并开始执行。  
  
## <a name="syntax"></a>语法  
  
```  
BOOL STDMETHODCALLTYPE _CorDllMain (  
   [in] HINSTANCE hInst,  
   [in] DWORD     dwReason,  
   [in] LPVOID    lpReserved  
);  
```  
  
## <a name="parameters"></a>参数  
 `hInst`  
 [in]已加载的模块实例句柄。  
  
 `dwReason`  
 [in]指示调用 DLL 入口点函数。 此参数可以是下列值之一：DLL\_PROCESS_ATTACH、 DLL\_线程\_附加、 DLL\_线程\_附加或 DLL\_过程\_分离。 有关这些值的说明，请参阅`DllMain`Platform SDK 中的文档。  
  
 `lpReserved`  
 [in]未使用。  
  
## <a name="return-value"></a>返回值  
 此方法返回`true`成功和`false`如果发生错误。  
  
## <a name="remarks"></a>备注  
 DLL 程序集由操作系统加载程序调用此函数。 对于可执行程序集，加载程序将调用[ \_CorExeMain](../../../../docs/framework/unmanaged-api/hosting/corexemain-function.md)函数。  
  
 操作系统加载程序调用此方法而不考虑 DLL 文件中指定的入口点。  
  
`_CorDllMain`由操作系统加载程序直接调用函数。
  
 有关其他信息，请参阅中的备注部分[ \_CorValidateImage](../../../../docs/framework/unmanaged-api/hosting/corvalidateimage-function.md)主题。  
  
## <a name="requirements"></a>要求  

 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** Cor.h  
  
 **库：** 包含为 MsCorEE.dll 中的资源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅

- [元数据全局静态函数](../../../../docs/framework/unmanaged-api/metadata/metadata-global-static-functions.md)
