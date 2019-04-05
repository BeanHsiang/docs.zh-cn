---
title: IMetaDataEmit::SetClassLayout 方法
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.SetClassLayout
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::SetClassLayout
helpviewer_keywords:
- IMetaDataEmit::SetClassLayout method [.NET Framework metadata]
- SetClassLayout method [.NET Framework metadata]
ms.assetid: 2576c449-388d-4434-a0e1-9f53991e11b6
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: b629f5fd461da23aa1d55519d371a70f9f1128ab
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57471844"
---
# <a name="imetadataemitsetclasslayout-method"></a>IMetaDataEmit::SetClassLayout 方法
完成已由调用之前定义的类的字段的布局[DefineTypeDef 方法](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-definetypedef-method.md)。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT SetClassLayout (  
    [in]  mdTypeDef           td,   
    [in]  DWORD               dwPackSize,   
    [in]  COR_FIELD_OFFSET    rFieldOffsets[],   
    [in]  ULONG               ulClassSize   
);  
```  
  
## <a name="parameters"></a>参数  
 `td`  
 [in]`mdTypeDef`标记，用于指定要进行布局的类。  
  
 `dwPackSize`  
 [in]封装大小：1、 2、 4、 8 或 16 个字节。 封装大小为相邻的域之间的字节数。  
  
 `rFieldOffsets`  
 [in]一个数组[COR_FIELD_OFFSET](../../../../docs/framework/unmanaged-api/metadata/cor-field-offset-structure.md)结构，其中每个指定的类的字段和字段的偏移量的类中。 终止与数组`mdTokenNil`。  
  
 `ulClassSize`  
 [in]以字节为单位，类的大小。  
  
## <a name="remarks"></a>备注  
 通过调用最初定义该类[imetadataemit:: Definetypedef](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-definetypedef-method.md)方法，并指定三种布局的类的字段之一： 自动、 连续的或显式。 通常情况下，将使用自动布局，并让运行时选择最佳的方式进行布局的字段。  
  
 但是，您可能希望根据非托管代码使用的排列方式布局的字段。 在这种情况下，选择连续或显式布局，并调用`SetClassLayout`完成字段的布局：  
  
-   顺序布局：指定封装大小。 字段对齐根据自然大小或包装大小，在较小的偏移量字段的任何结果。 设置`rFieldOffsets`和`ulClassSize`为零。  
  
-   显式布局：指定每个字段的偏移量，或者指定类的大小和封装大小。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** Cor.h  
  
 **库：** 用作 MSCorEE.dll 中的资源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [IMetaDataEmit Interface](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md)
- [IMetaDataEmit2 Interface](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-interface.md)
