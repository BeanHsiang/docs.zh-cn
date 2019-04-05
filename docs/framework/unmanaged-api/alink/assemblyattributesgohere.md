---
title: AssemblyAttributesGoHere 类 (System.Runtime.CompilerServices)
ms.date: 03/30/2017
api_name:
- System.Runtime.CompilerServices.AssemblyAttributesGoHere
api_location:
- mscorlib.dll
api_type:
- Assembly
f1_keywords:
- AssemblyAttributesGoHere
helpviewer_keywords:
- AssemblyAttributesGoHere type
- Alink API, AssemblyAttributesGoHere type
ms.assetid: 7b26fcb6-94f4-4f09-933e-b33efe451f4f
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 571c2f6723e827a1b385f77724c33703ae970ae3
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56968109"
---
# <a name="assemblyattributesgohere-class"></a>AssemblyAttributesGoHere 类

由 ALink 用作占位符以存储有关自定义特性的信息。

## <a name="syntax"></a>语法

```csharp
internal sealed class AssemblyAttributesGoHere
```

## <a name="remarks"></a>备注

对此类型的引用可能被嵌入网络模块内，模块的源包含程序集自定义属性。 当从一个或多个包含对这些类型的引用的网络模块生成程序集清单时，ALink 将使用附加到这些引用的信息来发出实际的自定义属性。 因此，此类型永远不会被实例化，而且对它的引用仅用作生成过程的一部分，在最终的程序集中不具有任何用途。

对此类型的引用指示与安全性无关且用途单一的自定义属性。

这些类型标记为"内部".NET Framework 中，并且位于<xref:System.Runtime.CompilerServices>命名空间。

## <a name="requirements"></a>要求

mscorlib.dll

## <a name="see-also"></a>请参阅

- [AssemblyAttributesGoHereM](assemblyattributesgoherem.md)
- [AssemblyAttributesGoHereS](assemblyattributesgoheres.md)
- [AssemblyAttributesGoHereSM](assemblyattributesgoheresm.md)
