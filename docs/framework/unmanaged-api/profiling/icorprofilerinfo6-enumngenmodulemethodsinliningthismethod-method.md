---
title: ICorProfilerInfo6::EnumNgenModuleMethodsInliningThisMethod 方法
ms.date: 03/30/2017
ms.assetid: b933dfe6-7833-40cb-aad8-40842dc3034f
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 67ae413ae8944757fc90bcde752b9a5fe53cc68f
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57365316"
---
# <a name="icorprofilerinfo6enumngenmodulemethodsinliningthismethod-method"></a>ICorProfilerInfo6::EnumNgenModuleMethodsInliningThisMethod 方法

为给定的 NGen 模块和内联给定方法中定义的所有方法返回一个枚举器。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumNgenModuleMethodsInliningThisMethod(
        [in] ModuleID inlinersModuleId,
        [in] ModuleID inlineeModuleId,
        [in] mdMethodDef inlineeMethodId,
        [out] BOOL *incompleteData,
        [out] ICorProfilerMethodEnum** ppEnum
);
```

## <a name="parameters"></a>参数

`inlinersModuleId`\
[in]NGen 模块的标识符。

`inlineeModuleId`\
[in]定义的模块标识符`inlineeMethodId`。 有关详细信息，请参阅备注部分。

`inlineeMethodId`\
[in]内联方法的标识符。 有关详细信息，请参阅备注部分。

`incompleteData`\
[out]一个标志，指示是否`ppEnum`包含给定的方法的内联的所有方法。  有关详细信息，请参阅备注部分。

`ppEnum`\
[out]一个指向枚举器的地址

## <a name="remarks"></a>备注

`inlineeModuleId` 和`inlineeMethodId`一起构成了可能会进行内联方法的完整标识符。 例如，假定模块`A`定义的方法`Simple.Add`:

```csharp
Simple.Add(int a, int b)
{ return a + b; }
```

和模块 B 定义`Fancy.AddTwice`:

```csharp
Fancy.AddTwice(int a, int b)
{ return Simple.Add(a,b) + Simple.Add(a,b); }
```

允许并假设`Fancy.AddTwice`内嵌元素调用到`SimpleAdd`。 探查器可以使用此枚举器来查找模块 B 中哪些以内联方式定义的所有方法`Simple.Add`，并枚举结果会`AddTwice`。  `inlineeModuleId` 是的模块标识符`A`，并`inlineeMethodId`是标识符`Simple.Add(int a, int b)`。

如果`incompleteData`函数的后面是 true，将返回枚举器不包含内联的所有方法的给定的方法。 这可能会在一个或多直接或间接依赖关系的内联模块尚未尚未加载。 如果探查器需要准确的数据，它应稍后重试多个模块加载时，最好是在每个模块加载。

`EnumNgenModuleMethodsInliningThisMethod`方法可用于解决限制为 ReJIT 内联。 ReJIT 允许探查器更改方法的实现，然后动态为其创建新的代码。 例如，我们可能会更改`Simple.Add`，如下所示：

```csharp
Simple.Add(int a, int b)
{ return 42; }
```

但是由于`Fancy.AddTwice`具有已内联`Simple.Add`，它将继续像以前一样具有相同的行为。 若要解决这一限制，调用方必须搜索所有方法的所有模块中内联`Simple.Add`，并使用`ICorProfilerInfo5::RequestRejit`上的每个这些方法。 重新编译方法时，它们将具有新行为的`Simple.Add`而不是这一旧行为。

## <a name="requirements"></a>要求

**平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。

**标头：** CorProf.idl, CorProf.h

**库：** CorGuids.lib

**.NET Framework 版本：**[!INCLUDE[net_current_v46plus](../../../../includes/net-current-v46plus-md.md)]

## <a name="see-also"></a>请参阅

- [ICorProfilerInfo6 接口](icorprofilerinfo6-interface.md)