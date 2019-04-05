---
title: LoadTypeLibWithResolver 函数
ms.date: 03/30/2017
api_name:
- LoadTypeLibWithResolver
api_location:
- TlbRef.dll
api_type:
- DLLExport
f1_keywords:
- LoadTypeLibWithResolver
helpviewer_keywords:
- LoadTypeLibWithResolver function [.NET Framework]
ms.assetid: 7123a89b-eb9b-463a-a552-a081e33b0a3a
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a7187076eb338d5a57388d19f62e79af041ee774
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57501040"
---
# <a name="loadtypelibwithresolver-function"></a>LoadTypeLibWithResolver 函数
加载类型库并使用所提供[ITypeLibResolver 接口](../../../../docs/framework/unmanaged-api/tlbexp/itypelibresolver-interface.md)若要解决任何内部引用的类型库。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT LoadTypeLibWithResolver(  
    [in]  LPCOLESTR           szFile,  
    [in]  REGKIND             regkind,  
    [in]  ITypeLibResolver   *pTlbResolver,  
    [out] ITypeLib          **pptlib);  
```  
  
## <a name="parameters"></a>参数  
 `szFile`  
 [in]类型库文件路径。  
  
 `regkind`  
 [in]一个[REGKIND 枚举](https://docs.microsoft.com/previous-versions/windows/desktop/api/oleauto/ne-oleauto-tagregkind)标志，用于控制如何注册类型库。 其可能的值为：  
  
-   `REGKIND_DEFAULT`：使用默认注册行为。  
  
-   `REGKIND_REGISTER`：注册此类型库。  
  
-   `REGKIND_NONE`：未注册此类型库。  
  
 `pTlbResolver`  
 [in]实现的指针[ITypeLibResolver 接口](../../../../docs/framework/unmanaged-api/tlbexp/itypelibresolver-interface.md)。  
  
 `pptlib`  
 [out]对要加载的类型库的引用。  
  
## <a name="return-value"></a>返回值  
 下表中列出的 HRESULT 值之一。  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|成功。|  
|`E_OUTOFMEMORY`|内存不足。|  
|`E_POINTER`|一个或多个指针均无效。|  
|`E_INVALIDARG`|一个或多个参数均无效。|  
|`TYPE_E_IOERROR`|该函数无法写入到文件。|  
|`TYPE_E_REGISTRYACCESS`|无法打开系统注册数据库。|  
|`TYPE_E_INVALIDSTATE`|无法打开类型库。|  
|`TYPE_E_CANTLOADLIBRARY`|无法加载类型库或 DLL。|  
  
## <a name="remarks"></a>备注  
 [Tlbexp.exe （类型库导出程序）](../../../../docs/framework/tools/tlbexp-exe-type-library-exporter.md)调用`LoadTypeLibWithResolver`在程序集到类型库转换过程中的函数。  
  
 此函数将加载指定的类型库具有对注册表的最低访问权限。 然后，该函数将检查内部引用的类型库，其中每个必须加载和添加到父类型库的类型库。  
  
 可以加载引用的类型库之前，必须将其引用文件路径解析为完整文件路径。 这通过实现[ResolveTypeLib 方法](../../../../docs/framework/unmanaged-api/tlbexp/resolvetypelib-method.md)由提供[ITypeLibResolver 接口](../../../../docs/framework/unmanaged-api/tlbexp/itypelibresolver-interface.md)，其中传入`pTlbResolver`参数。  
  
 如果已知引用的类型库的完整文件路径，`LoadTypeLibWithResolver`函数都会加载并将引用的类型库添加到父类型库，创建合并的主类型库。  
  
 该函数解析并加载了所有内部引用的类型库后，它将返回到主解析的类型库中的引用`pptlib`参数。  
  
 `LoadTypeLibWithResolver`通常调用函数[Tlbexp.exe （类型库导出程序）](../../../../docs/framework/tools/tlbexp-exe-type-library-exporter.md)，其中提供其自身内部[ITypeLibResolver 接口](../../../../docs/framework/unmanaged-api/tlbexp/itypelibresolver-interface.md)中的实现`pTlbResolver`参数。  
  
 如果您调用`LoadTypeLibWithResolver`直接，您必须提供你自己[ITypeLibResolver 接口](../../../../docs/framework/unmanaged-api/tlbexp/itypelibresolver-interface.md)实现。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** TlbRef.h  
  
 **库：** TlbRef.lib  
  
 **.NET framework 版本：** 3.5, 3.0, 2.0  
  
## <a name="see-also"></a>请参阅
- [Tlbexp Helper 函数](../../../../docs/framework/unmanaged-api/tlbexp/index.md)
- [LoadTypeLibEx 函数](https://docs.microsoft.com/previous-versions/windows/desktop/api/oleauto/nf-oleauto-loadtypelibex)
