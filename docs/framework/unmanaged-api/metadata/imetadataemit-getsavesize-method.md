---
title: IMetaDataEmit::GetSaveSize 方法
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.GetSaveSize
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::GetSaveSize
helpviewer_keywords:
- IMetaDataEmit::GetSaveSize method [.NET Framework metadata]
- GetSaveSize method [.NET Framework metadata]
ms.assetid: 8aea2e2c-23a3-4cda-9a06-e19f97383830
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 16984fe108abd1cfc01c471bcfc091a805b28e83
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57501498"
---
# <a name="imetadataemitgetsavesize-method"></a>IMetaDataEmit::GetSaveSize 方法
获取当前作用域中的程序集和其元数据的估计二进制大小。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT GetSaveSize (  
    [in]  CorSaveSize fSave,  
    [out] DWORD       *pdwSaveSize  
);  
```  
  
## <a name="parameters"></a>参数  
 `fSave`  
 [in]值为[CorSaveSize](../../../../docs/framework/unmanaged-api/metadata/corsavesize-enumeration.md)枚举，用于指定是否要获取的准确或近似大小。 只有三个值都有效： cssAccurate，cssQuick，和 cssDiscardTransientCAs:  
  
-   cssAccurate 返回确切的存储大小，但花费的时间来计算。  
  
-   cssQuick 返回大小，为安全起见，填充，但需要更少的时间来计算。  
  
-   cssDiscardTransientCAs 告知`GetSaveSize`，它可以丢弃可放弃的自定义属性。  
  
 `pdwSaveSize`  
 [out]一个指向保存该文件所需的大小。  
  
## <a name="remarks"></a>备注  
 `GetSaveSize` 计算所需的空间，以字节为单位，以将该程序集和其元数据保存在当前作用域。 (调用[imetadataemit:: Savetostream](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-savetostream-method.md)方法将发出此数目的字节数。)  
  
 如果调用方实现[IMapToken](../../../../docs/framework/unmanaged-api/metadata/imaptoken-interface.md)接口 (通过[imetadataemit:: Sethandler](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-sethandler-method.md)或[imetadataemit:: Merge](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-merge-method.md))，`GetSaveSize`将执行两个阶段通过优化并将其压缩的元数据。 否则，不执行任何优化。  
  
 如果执行优化，则第一步只需进行排序来优化性能的导入时搜索的元数据结构。 此步骤通常会记录移动，并且其副作用，保留供将来参考工具的令牌都无效。 元数据不会通知调用方之前这些令牌更改后的第二个过程，但是。 在第二个阶段中，各种优化的执行，旨在减少的元数据，例如优化去除 （早期绑定） 的总体大小`mdTypeRef`和`mdMemberRef`令牌的类型或成员声明中的引用时当前元数据范围。 在此阶段中，会发生另一轮标记映射。 之后此阶段中，元数据引擎通知调用方，通过其`IMapToken`接口的任何更改令牌值。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** Cor.h  
  
 **库：** 用作 MSCorEE.dll 中的资源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v11plus](../../../../includes/net-current-v11plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [IMetaDataEmit Interface](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md)
- [IMetaDataEmit2 Interface](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-interface.md)
