---
title: -pdb（C# 编译器选项）
ms.date: 07/20/2015
f1_keywords:
- /pdb
helpviewer_keywords:
- -pdb compiler option [C#]
- pdb compiler option [C#]
- /pdb compiler option [C#]
ms.assetid: e9d0f96a-5b75-45d6-9765-92538dd5f823
ms.openlocfilehash: b0a566931ac76a3adb191f423a497bc446e280c8
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54575497"
---
# <a name="-pdb-c-compiler-options"></a>-pdb（C# 编译器选项）
-pdb 编译器选项指定调试符号文件的名称和位置。  
  
## <a name="syntax"></a>语法  
  
```console  
-pdb:filename  
```  
  
## <a name="arguments"></a>自变量  
 `filename`  
 调试符号文件的名称和位置。  
  
## <a name="remarks"></a>备注  
 指定 [-debug（C# 编译器选项）](../../../csharp/language-reference/compiler-options/debug-compiler-option.md)后，编译器将在创建输出文件（.exe 或 .dll）的目录中创建 .pdb 文件，且名称与输出文件的名称相同。  
  
 -pdb 允许为 .pdb 文件指定非默认的文件名和位置。  
  
 不能在 Visual Studio 开发环境中设置此编译器选项，也不能以编程方式对其进行更改。  
  
## <a name="example"></a>示例  
 编译 `t.cs` 并创建名为 tt.pdb 的 .pdb 文件：  
  
```console  
csc -debug -pdb:tt t.cs  
```  
  
## <a name="see-also"></a>请参阅

- [C# 编译器选项](../../../csharp/language-reference/compiler-options/index.md)
- [管理项目和解决方案属性](/visualstudio/ide/managing-project-and-solution-properties)
