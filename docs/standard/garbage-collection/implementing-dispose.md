---
title: 实现 Dispose 方法
ms.date: 04/07/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Dispose method
- garbage collection, Dispose method
ms.assetid: eb4e1af0-3b48-4fbc-ad4e-fc2f64138bf9
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 683a71b27d3e3dd1c0db4e49c2c188ccad0fb6d4
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54607116"
---
# <a name="implementing-a-dispose-method"></a>实现 Dispose 方法

通过实现 <xref:System.IDisposable.Dispose%2A> 方法来释放应用程序使用的非托管资源。 .NET 垃圾回收器不分配或释放非托管内存。  
  
对象清理模式（称为[清理模式](../../../docs/standard/design-guidelines/dispose-pattern.md)）对对象生存期强制施加顺序。 释放模式仅用于访问非托管资源的对象，如文件和管道句柄、注册表句柄、等待句柄或指向非托管内存块的指针。 这是因为垃圾回收器在回收不使用的托管对象时非常高效，但无法回收非托管对象。  
  
释放模式有两种变体：  
  
* 你包装类型在安全句柄中（即，在从 <xref:System.Runtime.InteropServices.SafeHandle?displayProperty=nameWithType> 派生的类中）使用的每个非托管资源。 在这种情况下，你可以实现 <xref:System.IDisposable> 接口和额外的 `Dispose(Boolean)` 方法。 这是建议的变体，不要求重写 <xref:System.Object.Finalize%2A?displayProperty=nameWithType> 方法。  
  
  > [!NOTE]
  > <xref:Microsoft.Win32.SafeHandles?displayProperty=nameWithType> 命名空间提供了一组派生自 <xref:System.Runtime.InteropServices.SafeHandle> 的类，[使用安全句柄](#SafeHandles)部分中列出了这些类。 如果找不到适用于释放非托管资源的类，则可实现你自己的 <xref:System.Runtime.InteropServices.SafeHandle> 的子类。  
  
* 你可以实现 <xref:System.IDisposable> 接口和额外的 `Dispose(Boolean)` 方法，还可以重写 <xref:System.Object.Finalize%2A?displayProperty=nameWithType> 方法。 如果类型的使用者未调用你的 <xref:System.Object.Finalize%2A> 实现，则必须重写 <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> 以确保释放非托管资源。 如果使用上一项目符号中讨论的推荐方法，则 <xref:System.Runtime.InteropServices.SafeHandle?displayProperty=nameWithType> 类可代表你执行此操作。  
  
若要帮助确保始终正确地清理资源，<xref:System.IDisposable.Dispose%2A> 方法应该可以多次调用而不引发异常。  
  
为 <xref:System.GC.KeepAlive%2A?displayProperty=nameWithType> 方法提供的代码示例演示了强行垃圾回收如何在回收对象的成员仍在执行时引起终结器运行。 在较长的 <xref:System.GC.KeepAlive%2A> 方法末尾最好调用 <xref:System.IDisposable.Dispose%2A> 方法。  
  
<a name="Dispose2"></a>
## <a name="dispose-and-disposeboolean"></a>Dispose() 和 Dispose(Boolean)  

<xref:System.IDisposable> 接口需要实现单个无参数的方法 <xref:System.IDisposable.Dispose%2A>。 但是，释放模式需要实现两种 `Dispose` 方法：  
  
* 一种没有参数的公共非虚拟的（Visual Basic 中的 `NonInheritable`）<xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> 实现。  
  
* 受保护的虚拟（Visual Basic 中的`Overridable`）`Dispose` 方法，其签名为：  
  
  [!code-csharp[Conceptual.Disposable#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/dispose1.cs#8)]
  [!code-vb[Conceptual.Disposable#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/dispose1.vb#8)]  
  
### <a name="the-dispose-overload"></a>Dispose() 重载

由于公共、非虚拟的（Visual Basic 中的 `NonInheritable`）、无参数 `Dispose` 方法由该类型的使用者调用，因此其用途是释放非托管资源和指示终结器（如果存在）不必运行。 因此，它具有标准实现：  
  
[!code-csharp[Conceptual.Disposable#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/dispose1.cs#7)]
[!code-vb[Conceptual.Disposable#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/dispose1.vb#7)]  
  
`Dispose` 方法执行所有对象清理，使垃圾回收器不再需要调用对象的 <xref:System.Object.Finalize%2A?displayProperty=nameWithType> 重写。 因此，调用 <xref:System.GC.SuppressFinalize%2A> 方法会阻止垃圾回收器运行终结器。 如果类型没有终结器，则对 <xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType> 的调用不起作用。 请注意，释放非托管资源的实际工作是通过第二次重载 `Dispose` 方法执行的。  
  
### <a name="the-disposeboolean-overload"></a>Dispose(Boolean) 重载

在第二个重载中，disposing 参数是 <xref:System.Boolean>，用于指明方法调用是来自 <xref:System.IDisposable.Dispose%2A> 方法（值为 `true`），还是来自终结器（值为 `false`）。  
  
方法的主体包含两个代码块：  
  
* 释放非托管资源的块。 无论 `disposing` 参数的值如何，都会执行此块。  
  
* 释放托管资源的条件块。 如果 `disposing` 的值为 `true`，则执行此块。 它释放的托管资源可包括：  
  
  **实现 <xref:System.IDisposable> 的托管对象。** 可用于调用其 <xref:System.IDisposable.Dispose%2A> 实现的条件块。 如果你已使用安全句柄来包装非托管资源，则应在此处调用 <xref:System.Runtime.InteropServices.SafeHandle.Dispose%28System.Boolean%29?displayProperty=nameWithType> 实现。  
  
  **占用大量内存或使用短缺资源的托管对象。** 在 `Dispose` 方法中显式释放这些对象的速度快于垃圾回收器不确定性回收它们的速度。  
  
如果方法调用来自终结器（即当 disposing 为 `false`），则仅执行释放非托管资源的代码。 由于未定义垃圾回收器在终止期间销毁托管对象的顺序，因此使用 `Dispose` 的值调用此 `false` 重载将阻止终结器尝试释放可能已被回收的托管资源。  
  
## <a name="implementing-the-dispose-pattern-for-a-base-class"></a>实现基类的释放模式

如果实现基类的释放模式，则必须提供以下内容：  
  
> [!IMPORTANT]
> 你应针对实现 <xref:System.IDisposable.Dispose> 并且不是 `sealed`（Visual Basic 中的 `NotInheritable`）的所有基类实现此模式。  
  
* 调用 <xref:System.IDisposable.Dispose%2A> 方法的 `Dispose(Boolean)` 实现。  
  
* 执行释放资源的实际工作的 `Dispose(Boolean)` 方法。  
  
* 从包装非托管资源的 <xref:System.Runtime.InteropServices.SafeHandle> 派生的类（推荐），或对 <xref:System.Object.Finalize%2A?displayProperty=nameWithType> 方法的重写。 <xref:System.Runtime.InteropServices.SafeHandle> 类提供了一个使你无需编写代码的终结器。  
  
以下是一个常规模式，用于实现使用安全句柄的基类的释放模式：  
  
[!code-csharp[System.IDisposable#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.idisposable/cs/base1.cs#3)]
[!code-vb[System.IDisposable#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.idisposable/vb/base1.vb#3)]  
  
> [!NOTE]
> 上一个示例使用 <xref:Microsoft.Win32.SafeHandles.SafeFileHandle> 对象阐释模式；可以使用派生自 <xref:System.Runtime.InteropServices.SafeHandle> 的任何对象来替代。 请注意，该示例不会正确实例化其 <xref:Microsoft.Win32.SafeHandles.SafeFileHandle> 对象。  
  
以下是一个常规模式，用于实现重写 <xref:System.Object.Finalize%2A?displayProperty=nameWithType> 的基类的释放模式。  
  
[!code-csharp[System.IDisposable#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.idisposable/cs/base2.cs#5)]
[!code-vb[System.IDisposable#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.idisposable/vb/base2.vb#5)]  
  
> [!NOTE]
> 在 C# 中，通过定义[析构函数](~/docs/csharp/programming-guide/classes-and-structs/destructors.md)重写 <xref:System.Object.Finalize%2A?displayProperty=nameWithType>。  
  
## <a name="implementing-the-dispose-pattern-for-a-derived-class"></a>实现派生类的释放模式

从实现 <xref:System.IDisposable> 接口的类派生的类不应实现 <xref:System.IDisposable>，因为 <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> 的基类实现由其派生类继承。 相反，若要实现派生类的释放模式，你可提供以下内容：  
  
* `protected Dispose(Boolean)` 方法，用于替代基类方法并执行释放派生类的资源的实际工作。 此方法还应调用基类的 `Dispose(Boolean)` 方法并传递参数的释放状态。  
  
* 从包装非托管资源的 <xref:System.Runtime.InteropServices.SafeHandle> 派生的类（推荐），或对 <xref:System.Object.Finalize%2A?displayProperty=nameWithType> 方法的重写。 <xref:System.Runtime.InteropServices.SafeHandle> 类提供了一个使你无需编写代码的终结器。 如果你提供了终结器，则应调用 *disposing* 参数为 `false` 的 `Dispose(Boolean)` 重载。  
  
以下是一个常规模式，用于实现使用安全句柄的派生类的释放模式：  
  
[!code-csharp[System.IDisposable#4](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.idisposable/cs/derived1.cs#4)]
[!code-vb[System.IDisposable#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.idisposable/vb/derived1.vb#4)]  
  
> [!NOTE]
> 上一个示例使用 <xref:Microsoft.Win32.SafeHandles.SafeFileHandle> 对象阐释模式；可以使用派生自 <xref:System.Runtime.InteropServices.SafeHandle> 的任何对象来替代。 请注意，该示例不会正确实例化其 <xref:Microsoft.Win32.SafeHandles.SafeFileHandle> 对象。  
  
以下是一个常规模式，用于实现重写 <xref:System.Object.Finalize%2A?displayProperty=nameWithType> 的派生类的释放模式：  
  
[!code-csharp[System.IDisposable#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.idisposable/cs/derived2.cs#6)]
[!code-vb[System.IDisposable#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.idisposable/vb/derived2.vb#6)]  
  
> [!NOTE]
> 在 C# 中，通过定义[析构函数](~/docs/csharp/programming-guide/classes-and-structs/destructors.md)重写 <xref:System.Object.Finalize%2A?displayProperty=nameWithType>。  
  
<a name="SafeHandles"></a>   
## <a name="using-safe-handles"></a>使用安全句柄

编写对象终结器的代码是一项复杂的任务，如果处理不好可能会出现问题。 因此，建议你构造 <xref:System.Runtime.InteropServices.SafeHandle?displayProperty=nameWithType> 对象，而非实现终结器。  
  
从 <xref:System.Runtime.InteropServices.SafeHandle?displayProperty=nameWithType> 类派生的类通过无中断地分配和释放句柄来简化对象生存期问题。 它们包含可以保证在卸载应用程序域时运行的重要终结器。 有关使用安全句柄的优势的更多信息，请参见<xref:System.Runtime.InteropServices.SafeHandle?displayProperty=nameWithType>。 <xref:Microsoft.Win32.SafeHandles> 命名空间中的以下派生类提供安全句柄：  
  
* 用于文件、内存映射文件和管道的 <xref:Microsoft.Win32.SafeHandles.SafeFileHandle>、<xref:Microsoft.Win32.SafeHandles.SafeMemoryMappedFileHandle> 和 <xref:Microsoft.Win32.SafeHandles.SafePipeHandle> 类。  
  
* 用于内存视图的 <xref:Microsoft.Win32.SafeHandles.SafeMemoryMappedViewHandle> 类。  
  
* 用于加密构造的 <xref:Microsoft.Win32.SafeHandles.SafeNCryptKeyHandle>、<xref:Microsoft.Win32.SafeHandles.SafeNCryptProviderHandle> 和 <xref:Microsoft.Win32.SafeHandles.SafeNCryptSecretHandle> 类。  
  
* 用于注册表项的 <xref:Microsoft.Win32.SafeHandles.SafeRegistryHandle> 类。  
  
* 用于等待句柄的 <xref:Microsoft.Win32.SafeHandles.SafeWaitHandle> 类。  
  
<a name="base"></a>   
## <a name="using-a-safe-handle-to-implement-the-dispose-pattern-for-a-base-class"></a>使用安全句柄实现基类的释放模式

下面的示例阐释了基类 `DisposableStreamResource` 的释放模式，此模式使用安全句柄封装非托管资源。 它定义 `DisposableResource` 类，该类使用 <xref:Microsoft.Win32.SafeHandles.SafeFileHandle> 包装表示打开的文件的 <xref:System.IO.Stream> 对象。 `DisposableResource` 方法还包含一个属性 `Size`，该属性返回文件流中的总字节数。  
  
[!code-csharp[Conceptual.Disposable#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/base1.cs#9)]
[!code-vb[Conceptual.Disposable#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/base1.vb#9)]  
  
<a name="derived"></a>   
## <a name="using-a-safe-handle-to-implement-the-dispose-pattern-for-a-derived-class"></a>使用安全句柄实现派生类的释放模式

下面的示例阐释派生类 `DisposableStreamResource2` 的释放模式，该类继承自上一个示例中显示的 `DisposableStreamResource` 类。 此类额外添加一种方法（即 `WriteFileInfo`），并使用 <xref:Microsoft.Win32.SafeHandles.SafeFileHandle> 对象包装可写文件的句柄。  
  
[!code-csharp[Conceptual.Disposable#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/derived1.cs#10)]
[!code-vb[Conceptual.Disposable#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/derived1.vb#10)]  
  
## <a name="see-also"></a>请参阅

- <xref:System.GC.SuppressFinalize%2A>
- <xref:System.IDisposable>
- <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType>
- <xref:Microsoft.Win32.SafeHandles>
- <xref:System.Runtime.InteropServices.SafeHandle?displayProperty=nameWithType>
- <xref:System.Object.Finalize%2A?displayProperty=nameWithType>
- [如何：定义和使用类和结构 (C++/CLI)](/cpp/dotnet/how-to-define-and-consume-classes-and-structs-cpp-cli)
- [释放模式](../../../docs/standard/design-guidelines/dispose-pattern.md)
