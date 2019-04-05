---
title: IMetaDataDispenserEx::SetOption 方法
ms.date: 03/30/2017
api_name:
- IMetaDataDispenserEx.SetOption
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataDispenserEx::SetOption
helpviewer_keywords:
- IMetaDataDispenserEx::SetOption method [.NET Framework metadata]
- SetOption method [.NET Framework metadata]
ms.assetid: 9f1c7ccd-7fb2-41d8-aa00-24b823376527
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: f9e9d7a66f37759e6f62ddae2c5af989cee57e3b
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57470645"
---
# <a name="imetadatadispenserexsetoption-method"></a>IMetaDataDispenserEx::SetOption 方法
将指定的选项设置为当前元数据范围的给定值。 选项，可以控制如何处理对当前元数据范围的调用。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT SetOption (  
    [in] REFGUID optionId,   
    [in] const VARIANT *pValue  
);  
```  
  
## <a name="parameters"></a>参数  
 `optionId`  
 [in]一个指向指定要设置的选项的 GUID。  
  
 `pValue`  
 [in]要用于设置选项的值。 此值的类型必须是类型的指定的选项的变体。  
  
## <a name="remarks"></a>备注  
 下表列出了可用的 Guid，`optionId`参数可以指向和相应的有效值`pValue`参数。  
  
|GUID|描述|`pValue` 参数|  
|----------|-----------------|------------------------|  
|MetaDataCheckDuplicatesFor|控制哪些项检查重复项。 每次调用[IMetaDataEmit](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md)创建一个新项的方法，可以要求检查该项是否已存在于当前作用域的方法。 例如，可以检查是否存在`mdMethodDef`项; 在这种情况下，当调用[imetadataemit:: Definemethod](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-definemethod-method.md)，它将检查，该方法不存在当前作用域中。 此检查使用唯一标识给定的方法的密钥： 父类型、 名称和签名。|必须为类型 UI4 的变体，必须包含的值的组合[CorCheckDuplicatesFor](../../../../docs/framework/unmanaged-api/metadata/corcheckduplicatesfor-enumeration.md)枚举。|  
|MetaDataRefToDefCheck|控制将哪些引用项转换为的定义。 默认情况下，元数据引擎将通过将被引用的项转换为其定义，如果在当前作用域中实际定义被引用的项优化的代码。|必须为类型 UI4 的变体，必须包含的值的组合[CorRefToDefCheck](../../../../docs/framework/unmanaged-api/metadata/correftodefcheck-enumeration.md)枚举。|  
|MetaDataNotificationForTokenMovement|控制哪些标记重新映射发生在元数据合并过程会生成回调。 使用[imetadataemit:: Sethandler](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-sethandler-method.md)方法以建立您[IMapToken](../../../../docs/framework/unmanaged-api/metadata/imaptoken-interface.md)接口。|必须为类型 UI4 的变体，必须包含的值的组合[CorNotificationForTokenMovement](../../../../docs/framework/unmanaged-api/metadata/cornotificationfortokenmovement-enumeration.md)枚举。|  
|MetaDataSetENC|控制编辑并继续 (ENC) 的行为。 可以一次设置只有一种模式的行为。|必须为类型 UI4 的变体，必须包含的值[CorSetENC](../../../../docs/framework/unmanaged-api/metadata/corsetenc-enumeration.md)枚举。 值不是一个位掩码。|  
|MetaDataErrorIfEmitOutOfOrder|控制哪些发出-的无序错误生成回调。 发出元数据不按顺序不是致命错误;但是，如果发出元数据引擎，则前者的顺序的元数据，元数据将是更紧凑，因此可以更有效地搜索。 使用`IMetaDataEmit::SetHandler`方法以建立您[IMetaDataError](../../../../docs/framework/unmanaged-api/metadata/imetadataerror-interface.md)接口。|必须为类型 UI4 的变体，必须包含的值的组合[CorErrorIfEmitOutOfOrder](../../../../docs/framework/unmanaged-api/metadata/corerrorifemitoutoforder-enumeration.md)枚举。|  
|MetaDataImportOption|控制哪些类型的在 ENC 期间删除的项检索枚举器。|必须为类型 UI4 的变体，必须包含的值的组合[CorImportOptions 枚举](../../../../docs/framework/unmanaged-api/metadata/corimportoptions-enumeration.md)枚举。|  
|MetaDataThreadSafetyOptions|控制元数据引擎是否获取读取器/编写器锁，从而确保线程安全。 默认情况下，则引擎将假定，访问是单线程的调用方，因此会不获取任何锁。 客户端负责维护适当的线程同步时使用元数据 API。|必须为类型 UI4 的变体，必须包含的值[CorThreadSafetyOptions](../../../../docs/framework/unmanaged-api/metadata/corthreadsafetyoptions-enumeration.md)枚举。 值不是一个位掩码。|  
|MetaDataGenerateTCEAdapters|控件类型库导入程序是否应生成 COM 连接点容器的紧密耦合的事件 (TCE) 适配器。|必须为类型 BOOL 的变体。 如果`pValue`设置为`true`，类型库导入程序将生成 TCE 适配器。|  
|MetaDataTypeLibImportNamespace|指定要导入的类型库的非默认命名空间。|必须为 null 值或 BSTR 类型的变体。 如果`pValue`是一个 null 值，当前命名空间设置为 null; 否则为在当前命名空间设置为保存在变量的 BSTR 类型的字符串。|  
|MetaDataLinkerOptions|控制链接器是否应生成程序集或.NET Framework 模块文件。|必须为类型 UI4 的变体，必须包含的值的组合[CorLinkerOptions](../../../../docs/framework/unmanaged-api/metadata/corlinkeroptions-enumeration.md)枚举。|  
|MetaDataRuntimeVersion|指定公共语言运行时生成此映像时针对的版本。 版本存储为一个字符串，例如"v1.0.3705"。|必须为 null 值、 VT_EMPTY 值或 BSTR 类型的变体。 如果`pValue`是运行时版本设置为 null，为 null。 如果`pValue`是 VT_EMPTY，版本设置为默认值，从版本的 Mscorwks.dll 在其中运行的元数据代码绘制。 否则，运行时版本设置为保存在变量的 BSTR 类型的字符串。|  
|MetaDataMergerOptions|指定合并元数据的选项。|必须为类型 UI4 的变体，必须包含的值的组合`MergeFlags`枚举，它在 CorHdr.h 文件中所述。|  
|MetaDataPreserveLocalRefs|禁用优化到定义的本地引用。|必须包含的值的组合[CorLocalRefPreservation](../../../../docs/framework/unmanaged-api/metadata/corlocalrefpreservation-enumeration.md)枚举。|  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** Cor.h  
  
 **库：** 用作 MsCorEE.dll 中的资源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅
- [IMetaDataDispenserEx 接口](../../../../docs/framework/unmanaged-api/metadata/imetadatadispenserex-interface.md)
- [IMetaDataDispenser 接口](../../../../docs/framework/unmanaged-api/metadata/imetadatadispenser-interface.md)
