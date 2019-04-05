---
title: '#pragma checksum - C# 参考'
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- '#pragma checksum'
helpviewer_keywords:
- '#pragma checksum [C#]'
ms.assetid: 3673e4ca-6098-4ec1-890f-8fceb2a794a2
ms.openlocfilehash: ec215517cd667a6333137d0c7e51fe2ac58f5bcf
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57499819"
---
# <a name="pragma-checksum-c-reference"></a>#pragma checksum（C# 参考）
为源文件生成校验和，以帮助调试校验 [!INCLUDE[vstecasp](~/includes/vstecasp-md.md)] 页。  
  
## <a name="syntax"></a>语法  
  
```csharp
#pragma checksum "filename" "{guid}" "checksum bytes"  
```  
  
## <a name="parameters"></a>参数  
 `"filename"`  
 需要监视更改或更新的文件的名称。  
  
 `"{guid}"`  
 哈希算法的全局唯一标识符 (GUID)。  
  
 `"checksum_bytes"`  
 表示校验和字节的十六进制数字的字符串。 必须是偶数个十六进制数字。 奇数个十六进制数字会导致编译时警告出现，且指令遭忽略。  
  
## <a name="remarks"></a>备注  
 Visual Studio 调试器使用校验和确保它可始终找到正确的源。 编译器为源文件计算校验和，然后将输出发出到程序数据库 (PDB) 文件。 调试器随后使用 PDB 针对它为源文件计算的校验和进行比较。  
  
 此解决方案不适合 [!INCLUDE[vstecasp](~/includes/vstecasp-md.md)] 项目，因为计算的校验和用于生成的源文件，而不是 .aspx 文件。 为了解决此问题，`#pragma checksum` 为 [!INCLUDE[vstecasp](~/includes/vstecasp-md.md)] 页提供了校验和支持。  
  
 在 Visual C# 中创建 [!INCLUDE[vstecasp](~/includes/vstecasp-md.md)] 项目时，生成的源文件包含从其生成源的 .aspx 文件的校验和。 编译器随后将此信息写入 PDB 文件中。  
  
 如果编译器在文件中未遇到 `#pragma checksum` 指令，则它会计算校验和并将值写入 PDB 文件中。  
  
## <a name="example"></a>示例  
  
```csharp
class TestClass  
{  
    static int Main()  
    {  
        #pragma checksum "file.cs" "{406EA660-64CF-4C82-B6F0-42D48172A799}" "ab007f1d23d9" // New checksum  
    }  
}  
```  
  
## <a name="see-also"></a>请参阅

- [C# 参考](../../../csharp/language-reference/index.md)
- [C# 编程指南](../../../csharp/programming-guide/index.md)
- [C# 预处理器指令](../../../csharp/language-reference/preprocessor-directives/index.md)
