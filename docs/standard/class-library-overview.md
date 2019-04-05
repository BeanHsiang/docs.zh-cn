---
title: .NET 类库概述
ms.date: 02/08/2018
ms.technology: dotnet-standard
helpviewer_keywords:
- classes [.NET Framework], library overview
- classes [.NET Core], library overview
- .NET, library overview
- class objects value type
- naming conventions [.NET Framework]
- types, .NET Framework
- user-defined types
- Visual Basic, data types
- data types [.NET Framework], C++
- Visual C#, data types
- libraries, .NET Framework class library
- data types [.NET Framework], F#
- System namespace
- F#, data types
- .NET Framework, class library
- type system [.NET Framework]
- data types [.NET Framework]
- value types
- data types [.NET Framework], Visual Basic
- Common Language Specification
- namespaces [.NET Framework]
- floating point value type
- class library [.NET Framework]
- CLS
- logical value type
- .NET Framework class library, about
- built-in types
- namespaces [.NET Framework], about namespaces
- Visual C++, data types
- members [.NET Framework], type
- data types [.NET Framework], C#
- integer value type
- base types, class library
ms.assetid: 7e4c5921-955d-4b06-8709-101873acf157
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 82854b87f922f9937e593d0936fb1b29e6380ec0
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56970566"
---
# <a name="net-class-library-overview"></a>.NET 类库概述

.NET 实现包括可加快和优化开发过程并提供对系统功能的访问的类、接口、委托和值类型。 为了便于语言之间进行交互操作，大多数 .NET 类型都符合 CLS，因而可在编译器符合公共语言规范 (CLS) 的任何编程语言中使用。  
  
 .NET 类型是生成 .NET 应用程序、组件和控件的基础。 .NET 实现包括的类型可执行下列功能：  
  
-   表示基础数据类型和异常。  
  
-   封装数据结构。  
  
-   执行 I/O。  
  
-   访问关于加载类型的信息。  
  
-   调用 .NET Framework 安全检查。  
  
-   提供数据访问、多客户端 GUI 和服务器控制的客户端 GUI。  
  
 .NET 提供了一组丰富的接口以及抽象类和具体（非抽象）类。 可以按原样使用这些具体的类，或者在多数情况下从这些类派生您自己的类。 若要使用接口的功能，既可以创建实现接口的类，也可以从某个实现接口的 .NET 类中派生类。  
  
## <a name="naming-conventions"></a>命名约定

 .NET 类型使用点语法命名方案，该方案隐含了层次结构的意思。 此技术将相关类型分为不同的命名空间组，以便可以更容易地搜索和引用它们。 全名的第一部分（最右边的点之前的内容）是命名空间名。 全名的最后一部分是类型名。 例如，`System.Collections.Generic.List<T>` 表示 `List<T>` 类型，属于 `System.Collections.Generic` 命名空间。 可使用 <xref:System.Collections.Generic> 中的类型使用泛型集合。  
  
 此命名方案使扩展 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 的库开发人员可以轻松创建分层类型组，并用一致的、带有提示性的方式对其进行命名。 它还允许用全名（即命名空间和类型名称）明确地标识类型，这样可以防止类型名称发生冲突。 库开发人员在创建其命名空间的名称时应使用以下约定：  
  
 CompanyName.TechnologyName  
  
 例如，`Microsoft.Word` 命名空间就符合此原则。  
  
 利用命名模式将相关类型分组为命名空间是生成和记录类库的一种非常有用的方式。 但是，此命名方案对可见性、成员访问、继承、安全性或绑定无效。 一个命名空间可以被划分在多个程序集中，而单个程序集可以包含来自多个命名空间的类型。 程序集为公共语言运行时中的版本控制、部署、安全性、加载和可见性提供外形结构。  
  
 有关命名空间和类型名的更多信息，请参阅[通用类型系统](../../docs/standard/base-types/common-type-system.md)。  
  
## <a name="system-namespace"></a>系统命名空间

 <xref:System> 命名空间是 .NET 中基本类型的根命名空间。 此命名空间包括表示由所有应用程序使用的基本数据类型的类：<xref:System.Object>（继承层次结构的根）、<xref:System.Byte>、<xref:System.Char>、<xref:System.Array>、<xref:System.Int32>、<xref:System.String> 等。 在这些类型中，有许多与编程语言所使用的基元数据类型相对应。 当使用 .NET Framework 类型编写代码时，可以在应使用 .NET Framework 基础数据类型时使用编程语言的相应关键字。  
  
 下表列出了 .NET 提供的基类型，并对每种类型进行了简单描述，同时指出了 Visual Basic、C#、C++ 和 F# 中的相应类型。  
  
|类别|类名|说明|Visual Basic 数据类型|C# 数据类型|C++/CLI 数据类型|F# 数据类型|  
|--------------|----------------|-----------------|----------------------------|-------------------|---------------------|-----------------------|  
|整数|<xref:System.Byte>|8 位无符号整数。|**Byte**|**byte**|**unsigned char**|**byte**|  
||<xref:System.SByte>|8 位有符号整数。<br /><br /> 不符合 CLS。|**SByte**|**sbyte**|**char**<br /> 或<br /> signed char|**sbyte**|  
||<xref:System.Int16>|16 位带符号整数。|**Short**|**short**|**short**|**int16**|  
||<xref:System.Int32>|32 位带符号整数。|**Integer**|**int**|**int**<br /><br /> 或<br /><br /> **long**|**int**|  
||<xref:System.Int64>|64 位带符号整数。|**Long**|**long**|**__int64**|**int64**|  
||<xref:System.UInt16>|16 位无符号整数。<br /><br /> 不符合 CLS。|**UShort**|**ushort**|**unsigned short**|**uint16**|  
||<xref:System.UInt32>|32 位无符号整数。<br /><br /> 不符合 CLS。|**UInteger**|**uint**|**unsigned int**<br /> 或<br /> **unsigned long**|**uint32**|  
||<xref:System.UInt64>|64 位无符号整数。<br /><br /> 不符合 CLS。|**ULong**|**ulong**|unsigned __int64|**uint64**|  
|浮点|<xref:System.Single>|单精度（32 位）浮点数字。|**单精度**|**float**|**float**|**float32**<br> or<br>**single**|  
||<xref:System.Double>|双精度（64 位）浮点数字。|**双精度**|**double**|**double**|**float**<br> or <br> **double**|  
|逻辑运算|<xref:System.Boolean>|布尔值（真或假）。|**布尔值**|**bool**|**bool**|**bool**|  
|其他|<xref:System.Char>|Unicode（16 位）字符。|**Char**|**char**|**wchar_t**|**char**|  
||<xref:System.Decimal>|十进制（128 位）值。|**小数**|**decimal**|**小数**|**decimal**|  
||<xref:System.IntPtr>|大小取决于基础平台（32 位平台上为 32 位值，64 位平台上为 64 位值）的有符号整数。|**IntPtr**<br /><br /> 无内置类型。|**IntPtr**<br /><br /> 无内置类型。|**IntPtr**<br /><br /> 无内置类型。|**unativeint**|  
||<xref:System.UIntPtr>|大小取决于基础平台的无符号整数（32 位平台上为 32 位值，64 位平台上为 64 位值）。<br /><br /> 不符合 CLS。|**UIntPtr**<br /><br /> 无内置类型。|**UIntPtr**<br /><br /> 无内置类型。|**UIntPtr**<br /><br /> 无内置类型。|**unativeint**|  
||<xref:System.Object>|对象层次结构的根。|**对象**|**object**|**Object^**|**obj**|  
||<xref:System.String>|Unicode 字符的不变的定长串。|**字符串**|**string**|**String^**|**string**|  
  
 除了基本数据类型外，<xref:System> 命名空间还包含 100 多个类，范围从处理异常的类到处理核心运行时概念的类，如应用程序域和垃圾回收器。 
  <xref:System> 命名空间还包含许多二级命名空间。  
  
 有关命名空间的详细信息，请使用 [.NET API 浏览器](https://docs.microsoft.com/dotnet/api)来浏览 .NET 类库。 API 参考文档提供了有关每个名称空间及其类型和每个成员的文档。  
  
## <a name="see-also"></a>请参阅

- [常规类型系统](../../docs/standard/base-types/common-type-system.md)
- [.NET API 浏览器](../../api/index.md)
- [概述](../../docs/framework/get-started/overview.md)
