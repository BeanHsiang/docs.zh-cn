---
title: IMetaDataAssemblyEmit::DefineManifestResource 方法
ms.date: 03/30/2017
api_name:
- IMetaDataAssemblyEmit.DefineManifestResource
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataAssemblyEmit::DefineManifestResource
helpviewer_keywords:
- DefineManifestResource method [.NET Framework metadata]
- IMetaDataAssemblyEmit::DefineManifestResource method [.NET Framework metadata]
ms.assetid: 27f6d295-0fe9-4cda-b77e-6e7d5c53df09
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 06cac833ada1b642a7036f4b7cccbd167d91ecf9
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57487872"
---
# <a name="imetadataassemblyemitdefinemanifestresource-method"></a>IMetaDataAssemblyEmit::DefineManifestResource 方法
创建包含指定清单资源的元数据的 `ManifestResource` 结构，并返回关联的元数据标记。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT DefineManifestResource (  
    [in] LPCWSTR                szName,   
    [in] mdToken                tkImplementation,   
    [in] DWORD                  dwOffset,   
    [in] DWORD                  dwResourceFlags,  
    [out] mdManifestResource    *pmdmr  
);  
```  
  
## <a name="parameters"></a>参数  
 `szName`  
 [in]资源的名称。  
  
 `tkImplementation`  
 [in]类型的元数据令牌`mdtFile`或`mdtAssemblyRef`，它映射到资源提供程序。 NULL 值指示在其中嵌入的元数据文件为资源提供程序。  
  
 `dwOffset`  
 [in]到文件中资源的开头的偏移量。 对于独立文件中的资源，这将始终为零。 如果 PE （可移植可执行文件） 文件中嵌入资源，这是资源 BLOB，cor.h 标头文件中指定的位置开始的偏移量。  
  
 `dwResourceFlags`  
 [in]指定资源定义的属性设置的标志值的按位组合。  
  
 `pmdmr`  
 [out]指向返回的元数据标记的指针。  
  
## <a name="remarks"></a>备注  
 一个`ManifestResource`必须为每个程序集的文件中实现每个资源定义元数据结构。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** Cor.h  
  
 **库：** 用作 MsCorEE.dll 中的资源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [IMetaDataAssemblyEmit 接口](../../../../docs/framework/unmanaged-api/metadata/imetadataassemblyemit-interface.md)
