---
title: 编译器警告 CS3024
ms.date: 07/20/2015
f1_keywords:
- CS3024
helpviewer_keywords:
- CS3024
ms.assetid: fef9db31-9a7f-42d5-ad37-3e7faf661f95
ms.openlocfilehash: e49c131328f132ae6372167818d084df51ef6c78
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "56797352"
---
# <a name="compiler-warning-cs3024"></a>编译器警告 CS3024
约束类型“'type”不符合 CLS。  
  
 编译器发出此警告是因为：将不符合 CLS 的类型用作泛型类型约束会导致用某些语言编写的代码无法使用泛型类。  
  
### <a name="to-eliminate-this-warning"></a>消除此警告  
  
1.  对类型约束使用符合 CLS 的类型。  
  
## <a name="example"></a>示例  
 下面的示例在几个位置生成 CS3024：  
  
```csharp  
// cs3024.cs  
// Compile with: /target:library  
 [assembly: System.CLSCompliant(true)]  
  
[type: System.CLSCompliant(false)]  
public class TestClass // CS3024  
{  
    public ushort us;  
}  
[type: System.CLSCompliant(false)]  
public interface ITest // CS3024  
{}  
public interface I<T> where T : TestClass  
{}  
public class TestClass_2<T> where T : ITest  
{}  
public class TestClass_3<T> : I<T> where T : TestClass  
{}  
public class TestClass_4<T> : TestClass_2<T> where T : ITest  
{}  
public class Test  
{  
    public static int Main()  
    {  
        return 0;  
    }  
}  
```  
  
## <a name="see-also"></a>请参阅

- [类型参数的约束](../../csharp/programming-guide/generics/constraints-on-type-parameters.md)
