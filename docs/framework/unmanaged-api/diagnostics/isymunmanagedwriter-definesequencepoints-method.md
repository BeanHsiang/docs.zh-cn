---
title: ISymUnmanagedWriter::DefineSequencePoints 方法
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.DefineSequencePoints
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::DefineSequencePoints
helpviewer_keywords:
- DefineSequencePoints method [.NET Framework debugging]
- ISymUnmanagedWriter::DefineSequencePoints method [.NET Framework debugging]
ms.assetid: 64202baf-be6b-40ba-8162-8cc6c0c9b8e1
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 4210dedd77c6ab041189fa287e192bb7038080b2
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57491397"
---
# <a name="isymunmanagedwriterdefinesequencepoints-method"></a>ISymUnmanagedWriter::DefineSequencePoints 方法
在当前方法内定义一组序列点。 每个起始行和起始列定义一种方法中的语句的开始。 每个结束行和结束列定义一种方法中的语句的结束。 数组应以偏移量的升序进行排序。 偏移量始终是从开始处的方法，以字节为单位度量的。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT DefineSequencePoints(  
    [in] ISymUnmanagedDocumentWriter*  document,  
    [in] ULONG32 spCount,  
    [in, size_is(spCount)] ULONG32     offsets[],  
    [in, size_is(spCount)] ULONG32     lines[],  
    [in, size_is(spCount)] ULONG32     columns[],  
    [in, size_is(spCount)] ULONG32     endLines[],  
    [in, size_is(spCount)] ULONG32     endColumns[]);  
```  
  
## <a name="parameters"></a>参数  
 `document`  
 [in]要为其定义序列点的文档对象。  
  
 `spCount`  
 [in]一个`ULONG32`，该值指示每个的大小`offsets`， `lines`， `columns`， `endLines`，并`endColumns`缓冲区。  
  
 `offsets`  
 [in]从方法开始测量的序列点的偏移量。  
  
 `lines`  
 [in]序列点的起始行号。  
  
 `columns`  
 [in]序列点的起始列号。  
  
 `endLines`  
 [in]序列点的结束行号。 此参数可选。  
  
 `endColumns`  
 [in]序列点的结束列号。 此参数可选。  
  
## <a name="return-value"></a>返回值  
 如果方法成功，则为 S_OK否则为 E_FAIL 或某些其他错误代码。  
  
## <a name="requirements"></a>要求  
 **标头：** CorSym.idl CorSym.h  
  
## <a name="see-also"></a>请参阅
- [ISymUnmanagedWriter 接口](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-interface.md)
