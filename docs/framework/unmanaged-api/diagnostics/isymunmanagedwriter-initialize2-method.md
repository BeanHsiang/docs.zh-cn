---
title: ISymUnmanagedWriter::Initialize2 方法
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.Initialize2
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::Initialize2
helpviewer_keywords:
- ISymUnmanagedWriter::Initialize2 method [.NET Framework debugging]
- Initialize2 method [.NET Framework debugging]
ms.assetid: 93de56b6-4ae8-4cca-acdc-25a434623509
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 71eeeefc594c450d5fb95ebae17e3c1316301278
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57481373"
---
# <a name="isymunmanagedwriterinitialize2-method"></a>ISymUnmanagedWriter::Initialize2 方法
此编写器将与之关联的元数据发射器接口和设置输出文件将写入调试符号的名称。 此方法还允许您设置的程序数据库 (PDB) 文件的最终位置。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT Initialize2(  
    [in] IUnknown     *emitter,  
    [in] const WCHAR  *tempfilename,  
    [in] IStream      *pIStream,  
    [in] BOOL         fFullBuild,  
    [in] const WCHAR  *finalfilename);  
```  
  
## <a name="parameters"></a>参数  
 `emitter`  
 [in]指向元数据发射器接口的指针。  
  
 `tempfilename`  
 [in]一个指向`WCHAR`，其中包含要写入调试符号的文件名称。 如果为不使用文件名的编写器指定文件名，则忽略此参数。  
  
 `pIStream`  
 [in]如果指定，将符号编写器发出符号置于给定<xref:System.Runtime.InteropServices.ComTypes.IStream>而不是文件中指定`filename`参数。 `pIStream` 参数是可选的。  
  
 `fFullBuild`  
 [in]`true`如果这是完全重新生成;`false`如果这是增量编译。  
  
 `finalfilename`  
 [in]一个指向`WCHAR`，它是 PDB 文件的最后一个位置的路径字符串。  
  
## <a name="return-value"></a>返回值  
 如果方法成功，则为 S_OK否则为 E_FAIL 或某些其他错误代码。  
  
## <a name="requirements"></a>要求  
 **标头：** CorSym.idl CorSym.h  
  
## <a name="see-also"></a>请参阅
- [ISymUnmanagedWriter 接口](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-interface.md)
- [Initialize 方法](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-initialize-method.md)
