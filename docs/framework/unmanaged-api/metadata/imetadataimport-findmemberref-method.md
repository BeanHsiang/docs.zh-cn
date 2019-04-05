---
title: IMetaDataImport::FindMemberRef 方法
ms.date: 03/30/2017
api_name:
- IMetaDataImport.FindMemberRef
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::FindMemberRef
helpviewer_keywords:
- IMetaDataImport::FindMemberRef method [.NET Framework metadata]
- FindMemberRef method [.NET Framework metadata]
ms.assetid: 1ccda329-d752-4d89-abe8-511af3c3f4c9
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 2a58cba0ce4672a479cf5af9467d024a1b1562fc
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57474283"
---
# <a name="imetadataimportfindmemberref-method"></a>IMetaDataImport::FindMemberRef 方法
获取指向成员的 MemberRef 标记的指针，它是引用包含由指定<xref:System.Type>并具有指定的名称和元数据签名。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT FindMemberRef (  
   [in]  mdTypeRef          td,  
   [in]  LPCWSTR            szName,   
   [in]  PCCOR_SIGNATURE    pvSigBlob,   
   [in]  ULONG              cbSigBlob,   
   [out] mdMemberRef        *pmr  
);  
```  
  
## <a name="parameters"></a>参数  
 `td`  
 [in]对类或接口，包含要搜索的成员引用的 TypeRef 标记。 如果此值为`mdTokenNil`，在执行查找的全局变量或全局函数引用。  
  
 `szName`  
 [in]要搜索的成员引用的名称。  
  
 `pvSigBlob`  
 [in]指向成员引用的二进制元数据签名的指针。  
  
 `cbSigBlob`  
 [in]以字节为单位的大小`pvSigBlob`。  
  
 `pmr`  
 [out]指向匹配的 MemberRef 标记的指针。  
  
## <a name="remarks"></a>备注  
 指定使用封闭类或接口的成员 (`td`)，其名称 (`szName`)，并根据需要它的签名 (`pvSigBlob`)。  
  
 签名传递给`FindMemberRef`必须已生成在当前范围内，因为这些签名将绑定到特定的作用域。 签名可以嵌入令牌，用于标识封闭类或值类型。 令牌的本地 TypeDef 表中的索引。 无法生成上下文的当前作用域外部的运行时签名并使用该签名作为输入`FindMemberRef`。  
  
 `FindMemberRef` 查找仅直接在类或接口; 中定义的成员引用找不到继承的成员的引用。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** Cor.h  
  
 **库：** 包含为 MsCorEE.dll 中的资源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [IMetaDataImport 接口](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
- [IMetaDataImport2 接口](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
