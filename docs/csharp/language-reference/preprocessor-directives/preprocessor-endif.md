---
title: '#endif - C# 参考'
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- '#endif'
helpviewer_keywords:
- '#endif directive [C#]'
ms.assetid: 6a5fca55-5aee-441f-86f6-1c99fbe9ec05
ms.openlocfilehash: 58e29363ca1298966ecf88e6b456f33f43a176b0
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54573041"
---
# <a name="endif-c-reference"></a>#endif（C# 参考）
`#endif` 指定条件指令的末尾，以 [#if](../../../csharp/language-reference/preprocessor-directives/preprocessor-if.md) 指令开头。 例如，应用于对象的  
  
```csharp
#define DEBUG  
// ...  
#if DEBUG  
    Console.WriteLine("Debug version");  
#endif  
```  
  
## <a name="remarks"></a>备注  
 以 `#if` 指令开头的条件指令必须以 `#endif` 指令显式终止。 有关如何使用 `#endif` 的示例，请参阅 [#if](../../../csharp/language-reference/preprocessor-directives/preprocessor-if.md)。  
  
## <a name="see-also"></a>请参阅

- [C# 参考](../../../csharp/language-reference/index.md)
- [C# 编程指南](../../../csharp/programming-guide/index.md)
- [C# 预处理器指令](../../../csharp/language-reference/preprocessor-directives/index.md)
