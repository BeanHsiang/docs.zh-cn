---
title: -langversion（C# 编译器选项）
ms.date: 05/14/2018
f1_keywords:
- /langversion
helpviewer_keywords:
- /langversion compiler option [C#]
- -langversion compiler option [C#]
- langversion compiler option [C#]
ms.assetid: 3fb00b05-a0ff-4782-b313-13a4c0f62d94
ms.openlocfilehash: af30095c18a333d5ac3089fe3bf201c32739d9cf
ms.sourcegitcommit: 16aefeb2d265e69c0d80967580365fabf0c5d39a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2019
ms.locfileid: "57846345"
---
# <a name="-langversion-c-compiler-options"></a>-langversion（C# 编译器选项）

使编译器仅接受包含在所选 C# 语言规范中的语法。  
  
## <a name="syntax"></a>语法  

```console
-langversion:option  
```

## <a name="arguments"></a>自变量

 `option`  
 以下为有效值：  
  
|选项|含义|  
|------------|-------------|  
|preview|编译器接受它可支持的最新预览版本中的所有有效语言语法。|
|最新|编译器接受它可支持的最新版本（包括次要版本）中的所有有效语言语法。|
|latestMajor|编译器接受它可支持的最新主版本中的所有有效语言语法。|
|8.0|编译器只接受 C# 8.0 或更低版本中所含的语法。 <sup id="TCS80">[CS80](#FCS80)</sup>|
|7.3|编译器只接受 C# 7.3 或更低版本中所含的语法 <sup id="TCS73">[CS73](#FCS73)</sup>|
|7.2|编译器只接受 C# 7.2 或更低版本中所含的语法 <sup id="TCS72">[CS72](#FCS72)</sup>|
|7.1|编译器只接受 C# 7.1 或更低版本中所含的语法 <sup id="TCS71">[CS71](#FCS71)</sup>|
|7|编译器只接受 C# 7.0 或更低版本中所含的语法 <sup id="TCS7">[CS7](#FCS7)</sup>|
|6|编译器只接受 C# 6.0 或更低版本中所含的语法 <sup id="TCS6">[CS6](#FCS6)</sup>|
|5|编译器只接受 C# 5.0 或更低版本中所含的语法 <sup id="TCS5">[CS5](#FCS5)</sup>|
|4|编译器只接受 C# 4.0 或更低版本中所含的语法 <sup id="TCS4">[CS4](#FCS4)</sup>|
|3|编译器只接受 C# 3.0 或更低版本中所含的语法 <sup id="TCS3">[CS3](#FCS3)</sup>|
|ISO-2|编译器只接受 ISO/IEC 23270:2006 C# (2.0) 中所含的语法 <sup id="TISO2">[ISO2](#FISO2)</sup>|
|ISO-1|编译器只接受 ISO/IEC 23270:2003 C# (1.0/1.2) 中所含的语法 <sup id="TISO1">[ISO1](#FISO1)</sup>|  

## <a name="remarks"></a>备注

 C# 应用程序引用的元数据不受 -langversion 编译器选项约束。  
  
 每个版本的 C# 编译器都包含语言规范的扩展，因此 -langversion 不提供早期版本编译器的同等功能。  

 此外，虽然 C# 版本更新通常与主要的 .NET Framework 版本一致，但新的语法和功能不一定绑定到该特定的 Framework 版本。 虽然新功能肯定需要与 C# 修订版一起发布的新编译器更新，但每项具体功能都有自己的最小 .NET API 或公共语言运行时要求，这些要求通过包括 NuGet 包或其他库允许功能在下层框架上运行。
  
 无论使用哪一项 -langversion 设置，都将使用当前版本的公共语言运行时来创建 .exe 或 .dll。 友元程序集和 [-moduleassemblyname（C# 编译器选项）](../../../csharp/language-reference/compiler-options/moduleassemblyname-compiler-option.md)是一个例外，它们在 -langversion:ISO-1 下工作。  

 若要了解指定 C# 语言版本的其他方式，请参阅[选择 C# 语言版本](../configure-language-version.md)主题。
  
 有关如何以编程方式设置此编译器选项的信息，请参阅 <xref:VSLangProj80.CSharpProjectConfigurationProperties3.LanguageVersion%2A>。  

## <a name="see-also"></a>请参阅

- [C# 编译器选项](index.md)
- [管理项目和解决方案属性](/visualstudio/ide/managing-project-and-solution-properties)

### <a name="c-language-specification"></a>C# 语言规范

|Version|链接|说明|
|-------|----|-----------|
|C# 7.0 和更高版本||当前不可用|
|C# 6.0|[链接](../language-specification/index.md)|C# 语言规范版本 6 - 非官方草稿：.NET Foundation|
|C# 5.0|[下载 PDF](https://www.ecma-international.org/publications/files/ECMA-ST/ECMA-334.pdf)|标准 ECMA-334 第 5 版|
|C# 3.0|[下载 DOC](https://download.microsoft.com/download/3/8/8/388e7205-bc10-4226-b2a8-75351c669b09/CSharp%20Language%20Specification.doc)|C# 语言规范版本 3.0：Microsoft Corporation|
|C# 2.0|[下载 PDF](https://www.ecma-international.org/publications/files/ECMA-ST-ARCH/ECMA-334%204th%20edition%20June%202006.pdf)|标准 ECMA-334 第 4 版|
|C# 1.2|[下载 DOC](https://www.ecma-international.org/publications/files/ECMA-ST-ARCH/ECMA-334%202nd%20edition%20December%202002.pdf)|C# 语言规范版本 1.2：Microsoft Corporation|
|C# 1.0|[下载 DOC](https://www.ecma-international.org/publications/files/ECMA-ST-ARCH/ECMA-334%201st%20edition%20December%202001.pdf)|C# 语言规范版本 1.0：Microsoft Corporation|

### <a name="minimum-compiler-version-needed-to-support-all-language-features"></a>支持所有语言功能所需的最低编译器版本

[↩](#TCS80)<a name="FCS80">CS80</a>：Microsoft Visual Studio/生成工具 2019，版本 16 或 .NET Core 3.0 SDK [↩](#TCS73)<a name="FCS73">CS73</a>：Microsoft Visual Studio/生成工具 2017，版本 15.7  
[↩](#TCS72)<a name="FCS72">CS72</a>：Microsoft Visual Studio/生成工具 2017，版本 15.5  
[↩](#TCS71)<a name="FCS71">CS71</a>：Microsoft Visual Studio/生成工具 2017，版本 15.3  
[↩](#TCS7)<a name="FCS7">CS7</a>：Microsoft Visual Studio/生成工具 2017  
[↩](#TCS6)<a name="FCS6">CS6</a>：Microsoft Visual Studio/生成工具 2015  
[↩](#TCS5)<a name="FCS5">CS5</a>：Microsoft Visual Studio/生成工具 2012 或捆绑的 .NET Framework 4.5 编译器  
[↩](#TCS4)<a name="FCS4">CS4</a>：Microsoft Visual Studio/生成工具 2010 或捆绑的 .NET Framework 4.0 编译器  
[↩](#TCS3)<a name="FCS3">CS3</a>：Microsoft Visual Studio/生成工具 2008 或捆绑的 .NET Framework 3.5 编译器  
[↩](#TISO2)<a name="FISO2">ISO2</a>：Microsoft Visual Studio/生成工具 2005 或捆绑的 .Net Framework 2.0 编译器  
[↩](#TISO1)<a name="FISO1">ISO1</a>：Microsoft Visual Studio/生成工具 .NET 2002 或捆绑的 .Net Framework 1.0 编译器  
