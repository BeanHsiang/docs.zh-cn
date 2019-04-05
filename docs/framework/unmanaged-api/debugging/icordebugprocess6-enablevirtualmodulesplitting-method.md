---
title: ICorDebugProcess6::EnableVirtualModuleSplitting 方法
ms.date: 03/30/2017
ms.assetid: e7733bd3-68da-47f9-82ef-477db5f2e32d
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c6c2a9c806b70ab33f68e3213d82ed96aca47d62
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57484194"
---
# <a name="icordebugprocess6enablevirtualmodulesplitting-method"></a>ICorDebugProcess6::EnableVirtualModuleSplitting 方法
启用或禁用虚拟模块拆分。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT EnableVirtualModuleSplitting(  
   BOOL enableSplitting  
);  
```  
  
## <a name="parameters"></a>参数  
 `enableSplitting`  
 `true` 来启用虚拟模块拆分；`false` 来将其禁用。  
  
## <a name="remarks"></a>备注  
 虚拟模块拆分导致[ICorDebug](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md)识别合并在一起生成的模块处理并将其作为一组单独模块而非单个大型模块呈现。 执行此操作更改的各种行为[ICorDebug](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md)如下所述的方法。  
  
> [!NOTE]
>  此方法仅适用于 .NET Native。  
  
 可随时调用方法并更改 `enableSplitting` 值。 它不会导致任何有状态功能变化[ICorDebug](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md)对象，而非更改中列出的方法的行为[虚拟模块拆分和未托管调试 Api](#APIs)在调用它们的时间部分。 调用那些方法时，使用虚拟模块确实会导致性能显著下降。 此外，重要的内存中缓存的虚拟化的元数据可能需要以正确实现[IMetaDataImport](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)可能保留 Api 和这些缓存，即使虚拟模块拆分已关闭。  
  
## <a name="terminology"></a>术语  
 描述虚拟模块拆分时会用到下列术语：  
  
 容器模块，即容器  
 聚合模块。  
  
 子模块，即虚拟模块  
 在容器中发现的各模块。  
  
 普通模块  
 未在生成过程中合并的模块。 它们既不是容器模块也不是子模块。  
  
 ICorDebugModule 接口对象表示容器模块和子模块。 但是，接口的行为是略有不同每种情况下，作为\<x ref 到部分 > 部分介绍。  
  
## <a name="modules-and-assemblies"></a>模块和程序集  
 在程序集合并的情况下，多模块程序集不受支持，因此模块和程序集之间存在一对一的关系。 每个 icor 调试模块对象，不论其代表容器模块还是子模块，具有相应的 icor 调试程序集对象。 [Icordebugmodule:: Getassembly](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-getassembly-method.md)方法将从模块转换为程序集。 若要在另一个方向中映射[icordebugassembly:: Enumeratemodules](../../../../docs/framework/unmanaged-api/debugging/icordebugassembly-enumeratemodules-method.md)方法枚举仅 1 个模块。 因为在此情况下的程序集和模块形成了一个紧密耦合对，术语程序集和模块变得在很大程度上可以互换。  
  
## <a name="behavioral-differences"></a>行为差异  
 容器模块包含以下行为和特征：  
  
-   所有组成子模块的元数据合并在一起。  
  
-   类型名称可能改变。  
  
-   [Icordebugmodule:: Getname](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-getname-method.md)方法返回的磁盘上的模块的路径。  
  
-   [Icordebugmodule:: Getsize](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-getsize-method.md)方法将返回该映像的大小。  
  
-   ICorDebugAssembly3.EnumerateContainedAssemblies 方法列举子模块。  
  
-   ICorDebugAssembly3.GetContainerAssembly 方法返回 `S_FALSE`。  
  
 子模块包含以下行为和特征：  
  
-   他们具有一套减少的元数据，这些元数据只对应合并的原始程序集。  
  
-   元数据名未改变。  
  
-   元数据令牌经生成过程合并之前，不大可能与原始程序集中的令牌匹配。  
  
-   [Icordebugmodule:: Getname](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-getname-method.md)方法返回程序集名称，而不是文件路径。  
  
-   [Icordebugmodule:: Getsize](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-getsize-method.md)方法将返回原始的未合并的映像大小。  
  
-   ICorDebugModule3.EnumerateContainedAssemblies 方法返回 `S_FALSE`。  
  
-   ICorDebugAssembly3.GetContainerAssembly 方法返回包含模块。  
  
## <a name="interfaces-retrieved-from-modules"></a>从模块恢复的接口  
 模块可恢复或创建多个接口。 其中包括：  
  
-   ICorDebugClass 对象，该返回的对象[icordebugmodule:: Getclassfromtoken](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-getclassfromtoken-method.md)方法。  
  
-   Icor 调试程序集对象，该返回的对象[icordebugmodule:: Getassembly](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-getassembly-method.md)方法。  
  
 这些对象始终由缓存[ICorDebug](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md)，并且它们将具有相同的指针标识，无论它们是创建还是从容器模块还是子模块查询。 子模块提供了这些缓存对象的筛选视图，而非包含各自副本的单独缓存。  
  
<a name="APIs"></a>   
## <a name="virtual-module-splitting-and-the-unmanaged-debugging-apis"></a>虚拟模块拆分和未托管调试 API  
 下表显示了虚拟模块拆分如何影响未托管调试 API 中的其他方法的行为。  
  
|方法|`enableSplitting` = `true`|`enableSplitting` = `false`|  
|------------|---------------------------------|----------------------------------|  
|[ICorDebugFunction::GetModule](../../../../docs/framework/unmanaged-api/debugging/icordebugfunction-getmodule-method.md)|返回最初定义该功能的子模块|返回该功能合并到的容器模块|  
|[ICorDebugClass::GetModule](../../../../docs/framework/unmanaged-api/debugging/icordebugclass-getmodule-method.md)|返回最初定义该类的子模块。|返回该类合并到的容器模块。|  
|ICorDebugModuleDebugEvent::GetModule|返回加载的容器模块。 不管此设置如何，子模块不会收到加载事件。|返回加载的容器模块。|  
|[ICorDebugAppDomain::EnumerateAssemblies](../../../../docs/framework/unmanaged-api/debugging/icordebugappdomain-enumerateassemblies-method.md)|返回一组子程序集和普通程序集；不包含容器程序集。 **注意：** 如果任一容器程序集缺少符号，则其所有的子程序集都不会被枚举。 如果任一普通程序集缺少符号，则其可能被枚举或不枚举。|返回一组子程序集和普通程序集；不包含子程序集。 **注意：** 如果任一普通程序集缺少符号，则其可能被枚举或不枚举。|  
|[Icordebugcode:: Getcode](../../../../docs/framework/unmanaged-api/debugging/icordebugcode-getcode-method.md) （当只指向 IL 代码引用）|返回可能在预合并程序集图像中有效的 IL。 具体来说，当包含 IL 的虚拟模块未定义参考类型时，任一内联元数据令牌都可以作为 TypeRef 或 MemberRef 令牌。 可以查找这些 TypeRef 或 MemberRef 令牌[IMetaDataImport](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)相应虚拟 icor 调试模块对象的对象。|返回预合并程序集图像中的 IL。|  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>请参阅
- [ICorDebugProcess6 接口](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess6-interface.md)
- [调试接口](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
