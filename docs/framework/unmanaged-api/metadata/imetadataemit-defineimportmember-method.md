---
title: IMetaDataEmit::DefineImportMember 方法
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.DefineImportMember
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::DefineImportMember
helpviewer_keywords:
- DefineImportMember method [.NET Framework metadata]
- IMetaDataEmit::DefineImportMember method [.NET Framework metadata]
ms.assetid: c7dd94c6-335b-46ff-9dfe-505056db5673
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 7ac44d29dd99e0205c515905f9846263033babf3
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57479292"
---
# <a name="imetadataemitdefineimportmember-method"></a>IMetaDataEmit::DefineImportMember 方法
创建对指定成员的类型或模块的当前作用域之外定义，并定义该引用的令牌的引用。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT DefineImportMember (   
    [in]  IMetaDataAssemblyImport  *pAssemImport,   
    [in]  const void               *pbHashValue,   
    [in]  ULONG                    cbHashValue,  
    [in]  IMetaDataImport          *pImport,   
    [in]  mdToken                  mbMember,   
    [in]  IMetaDataAssemblyEmit    *pAssemEmit,   
    [in]  mdToken                  tkParent,   
    [out] mdMemberRef              *pmr   
);  
```  
  
## <a name="parameters"></a>参数  
 `pAssemImport`  
 [in][IMetaDataAssemblyImport](../../../../docs/framework/unmanaged-api/metadata/imetadataassemblyimport-interface.md)表示从中导入的目标成员的程序集的接口。  
  
 `pbHashValue`  
 [in]一个数组，包含由指定的程序集的哈希`pAssemImport`。  
  
 `cbHashValue`  
 [in] `pbHashValue` 数组中的字节数。  
  
 `pImport`  
 [in][IMetaDataImport](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)表示从中导入的目标成员的元数据范围的接口。  
  
 `mbMember`  
 [in]指定目标成员的元数据标记。 标记可以是`mdMethodDef`（适用于成员方法）， `mdProperty` （适用于成员属性），或`mdFieldDef`（适用于成员字段） 令牌。  
  
 `pAssemEmit`  
 [in][IMetaDataAssemblyEmit](../../../../docs/framework/unmanaged-api/metadata/imetadataassemblyemit-interface.md)表示目标成员导入的程序集的接口。  
  
 `tkParent`  
 [in]`mdTypeRef`或`mdModuleRef`令牌类型或模块，分别，拥有的目标成员。  
  
 `pmr`  
 [out]`mdMemberRef`在成员引用的当前作用域中定义的令牌。  
  
## <a name="remarks"></a>备注  
 `DefineImportMember`方法查找由指定的成员`mbMember`，即定义另一个作用域中指定的`pImport`，并检索其属性。 使用此信息来调用[imetadataemit:: Definememberref](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-definememberref-method.md)要创建成员引用的当前作用域中的方法。  
  
 通常情况下，使用之前`DefineImportMember`方法，您必须创建，在当前作用域、 类型引用或目标成员的父类、 接口或模块的模块参考。 然后传入此引用的元数据标记`tkParent`参数。 不需要创建对目标成员的父级的引用，如果将在解决更高版本的编译器或链接器。 总结：  
  
-   如果目标成员是字段或方法，可以使用两种[imetadataemit:: Definetyperefbyname](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-definetyperefbyname-method.md)或[imetadataemit:: Defineimporttype](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-defineimporttype-method.md)方法为创建的类型引用，在当前范围内，成员的父类或父接口。  
  
-   如果目标成员的全局变量或全局函数 （即，不是成员的类或接口），请使用[imetadataemit:: Definemoduleref](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-definemoduleref-method.md)方法中成员的父级的当前范围，创建模块引用模块。  
  
-   如果目标成员的父级将由编译器或链接器的更高版本解析，则传递`mdTokenNil`在`tkParent`。 此应用的唯一情况是全局函数或全局变量从最终将链接到当前模块的.obj 文件导入和合并的元数据。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** Cor.h  
  
 **库：** 用作 MSCorEE.dll 中的资源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [IMetaDataEmit Interface](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md)
- [IMetaDataEmit2 Interface](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-interface.md)
