---
title: 整型表 - C# 参考
ms.custom: seodec18
description: 内置 C# 整型类型的概述
ms.date: 08/20/2018
helpviewer_keywords:
- integral types, C#
- Visual C#, integral types
- types [C#], integral types
- ranges of integral types [C#]
ms.assetid: 62e86126-46ff-40b0-9028-e61d7558268c
ms.openlocfilehash: 7f8e4a9dabb3e24293ae7fcc724e8787dd6d4cf5
ms.sourcegitcommit: 49af435bfdd41faf26d38c20c5b0cc07e87bea60
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2018
ms.locfileid: "53396781"
---
# <a name="integral-types-table-c-reference"></a>整型类型表（C# 参考）

下表显示整型类型的大小和范围，它们构成简单类型的子集。  
  
|类型|范围|大小|  
|----------|-----------|----------|  
|[sbyte](sbyte.md)|-128 到 127|8 位带符号整数|  
|[byte](byte.md)|0 到 255|无符号的 8 位整数|  
|[char](char.md)|U+0000 到 U+ffff|Unicode 16 位字符|  
|[short](short.md)|-32,768 到 32,767|有符号 16 位整数|  
|[ushort](ushort.md)|0 到 65,535|无符号 16 位整数|  
|[int](int.md)|-2,147,483,648 到 2,147,483,647|带符号的 32 位整数|  
|[uint](uint.md)|0 到 4,294,967,295|无符号的 32 位整数|  
|[long](long.md)|-9,223,372,036,854,775,808 到 9,223,372,036,854,775,807|64 位带符号整数|  
|[ulong](ulong.md)|0 到 18,446,744,073,709,551,615|无符号 64 位整数|  

## <a name="remarks"></a>备注
  
如果由整数字面量所表示的值超出了 <xref:System.UInt64.MaxValue?displayProperty=nameWithType>，则将出现编译器错误 [CS1021](../../misc/cs1021.md)。

使用 <xref:System.Numerics.BigInteger?displayProperty=nameWithType> 结构来表示任意大的带符号整数。
  
## <a name="see-also"></a>请参阅

- [C# 参考](../index.md)
- [C# 编程指南](../../programming-guide/index.md)
- [C# 关键字](index.md)
- [类型引用表](reference-tables-for-types.md)
- [浮点型表](floating-point-types-table.md)
- [默认值表](default-values-table.md)
- [设置数值结果表的格式](formatting-numeric-results-table.md)
- [内置类型表](built-in-types-table.md)
- [.NET 中的数字](../../../standard/numerics.md)
