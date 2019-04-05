---
title: IMetaDataEmit::MergeEnd 方法
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.MergeEnd
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::MergeEnd
helpviewer_keywords:
- MergeEnd method [.NET Framework metadata]
- IMetaDataEmit::MergeEnd method [.NET Framework metadata]
ms.assetid: 2d64315a-1af1-4c60-aedf-f8a781914aea
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: a8602405a743f1ced6485d84a34a267771716d9b
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57469009"
---
# <a name="imetadataemitmergeend-method"></a>IMetaDataEmit::MergeEnd 方法
合并到当前作用域指定一个或多个以前调用的所有元数据作用域[imetadataemit:: Merge](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-merge-method.md)。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT MergeEnd ();  
```  
  
## <a name="parameters"></a>参数  
 此方法需要任何参数。  
  
## <a name="remarks"></a>备注  
 此例程将触发实际合并的元数据，所有的导入以前调用指定作用域`IMetaDataEmit::Merge`，到当前的输出范围。  
  
 以下特殊条件适用于合并：  
  
-   永远不会导入的模块版本标识符 （mvid） 发生，因为它是唯一的导入作用域中的元数据。  
  
-   将不覆盖任何现有模块范围内的属性。  
  
     如果已为当前作用域设置模块属性，导不入任何模块属性。 但是，如果尚未在当前作用域中设置模块属性，它们是导入后仅当其首先出现。 如果再次遇到这些模块属性，它们是重复项。 如果 （除了 mvid） 发生的所有模块属性的值进行比较并且找到了没有重复项，将引发错误。  
  
-   有关类型定义 (`TypeDef`)，没有重复项将合并到当前作用域。 `TypeDef` 检查对象是否已对每个重复项*完全限定对象名称* + *GUID* + *版本号*。 如果没有匹配名称或 GUID，并且任何其他两个元素则不同，将引发错误。 否则为如果所有三个项匹配，`MergeEnd`执行粗略检查以确保这些项确实重复项; 如果没有，将引发错误。 此粗略的检查是查找：  
  
    -   相同的成员声明中的相同顺序出现。 标记为成员`mdPrivateScope`(请参阅[CorMethodAttr](../../../../docs/framework/unmanaged-api/metadata/cormethodattr-enumeration.md)枚举) 不包含在此检查; 特别合并。  
  
    -   相同的类布局。  
  
     这意味着，`TypeDef`对象必须始终完全且一致地定义每个元数据范围内声明它; 如果其成员的实现 （类） 分布在多个编译单元中，假定的完整定义为存在于每个范围内，不是增量对每个作用域。 例如，如果参数名称与协定相关，它们必须发出相同的方式引入每个作用域;如果它们不相关，它们不应将发送到元数据。  
  
     例外情况是，`TypeDef`对象可以具有标记为增量成员`mdPrivateScope`。 在遇到这些，`MergeEnd`以增量方式将其添加到当前作用域而不考虑重复项。 由于编译器能够识别专用作用域，编译器必须负责强制执行规则。  
  
-   不导入或合并; 相对虚拟地址 (Rva)编译器会重新发出此信息。  
  
-   仅当合并附加到的项时，将合并自定义属性。 例如，当第一次遇到此类合并与类关联的自定义属性。 如果与之关联的自定义特性`TypeDef`或`MemberDef`这就是特定于编译单元 （例如成员编译的时间戳），它们将不会合并，并将由编译器删除或更新此类元数据。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** Cor.h  
  
 **库：** 用作 MSCorEE.dll 中的资源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v11plus](../../../../includes/net-current-v11plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [IMetaDataEmit Interface](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md)
- [IMetaDataEmit2 Interface](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-interface.md)
