---
title: 在类和结构之间选择
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- class library design guidelines [.NET Framework], structures
- class library design guidelines [.NET Framework], classes
- structures [.NET Framework], vs. classes
- classes [.NET Framework], design guidelines
- type design guidelines, structures
- structures [.NET Framework], design guidelines
- classes [.NET Framework], vs. structures
- type design guidelines, classes
ms.assetid: f8b8ec9b-0ba7-4dea-aadf-a93395cd804f
author: KrzysztofCwalina
ms.openlocfilehash: a47e43b2387362500d46c8e531f16d004d823c4c
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54565860"
---
# <a name="choosing-between-class-and-struct"></a>在类和结构之间选择
每个框架设计者面临的基本设计决策之一是将类型设计为类（引用类型）还是结构（值类型）。 要做出合适的选择，深入理解引用类型和值类型的行为差异非常重要。  
  
 我们要考虑的第一个引用类型和值类型之间的区别是引用类型在堆上分配并进行垃圾回收，而值类型在堆栈中分配并在堆栈展开时被释放，或内联包含类型并在它们的包含类型被释放时被释放。 因此，值类型的分配和释放通常比引用类型的分配和释放开销更低。  
  
 其次，引用类型数组是乱序分配的，这意味着数组元素只是对驻留在堆上的引用类型的实例的引用。 值类型数组是内联分配的，这意味着数组元素是值类型的实际实例。 因此，值类型数组的分配和释放比引用类型数组的分配和释放开销更低。 此外，在大多数情况下，值类型数组具有更好的引用地址。  
  
 下一个区别与内存使用有关。 当值类型转换为引用类型或它们实现的接口之一时，该值类型会被装箱。 它们在转回值类型时会被拆箱。 因为箱是在堆上分配的对象并会被垃圾回收，所以过多的装箱和拆箱会对堆、垃圾回收器以及最终应用程序的性能产生负面影响。  相反，在转换引用类型时不会发生这样的装箱。 （有关详细信息，请参阅[装箱和取消装箱](../../csharp/programming-guide/types/boxing-and-unboxing.md)）。
  
 再次，引用类型的赋值复制引用，而值类型的赋值复制整个值。 因此，大型引用类型的赋值比大型值类型的赋值开销更低。  
  
 最后，引用类型通过引用传递，而值类型通过值传递。 对引用类型实例的更改会影响指向该实例的所有引用。 值类型实例在按值传递时被复制。 当更改值类型的实例时，它当然不会影响其任何副本。 由于副本并非由用户显式创建，而是在传递参数或返回返回值时隐式创建，因此可以更改的值类型可能会让许多用户感到困惑。 所以，值类型应不可变。  
  
 一般来说，框架中的大多数类型应该是类。 但是，在某些情况下，值类型的特征使得其更适合使用结构。  
  
 **✓ 考虑**如果类型的实例比较小并且通常生存期较短或者通常嵌入在其他对象中，则定义结构而不是类。  
  
 **X 避免**定义一个结构，除非该类型具有所有以下特征：  
  
-   它逻辑上表示单个值，类似于基元类型（`int`， `double`，等等）。  
  
-   它的实例大小小于 16 字节。  
  
-   它是不可变的。  
  
-   它不会频繁装箱。  
  
 在所有其他情况下，应将类型定义为类。  
  
 *部分版权 © 2005, 2009 Microsoft Corporation。保留所有权利。*  
  
 *经 Pearson Education, Inc 授权，转载自[框架设计准则：可重用的 .NET 库的约定、习惯用语和模式，第 2 版](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 作者：Krzysztof Cwalina 和 Brad Abrams，由 Addison Wesley Professional 于 2008 年 10 月 22 日印发，作为 Microsoft Windows 开发系列的一部分。*  
  
## <a name="see-also"></a>请参阅

- [类型设计准则](../../../docs/standard/design-guidelines/type.md)
- [框架设计指南](../../../docs/standard/design-guidelines/index.md)
