---
title: -keycontainer（C# 编译器选项）
ms.date: 05/16/2018
f1_keywords:
- /keycontainer
helpviewer_keywords:
- /keycontainer compiler option [C#]
- keycontainer compiler option [C#]
- -keycontainer compiler option [C#]
ms.assetid: b3982b6d-2382-4f7e-bebd-ce98eaa30763
ms.openlocfilehash: 06a714bf9140ac793e8d853183047ca7255d565e
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54728981"
---
# <a name="-keycontainer-c-compiler-options"></a>-keycontainer（C# 编译器选项）
指定加密密钥容器的名称。  
  
## <a name="syntax"></a>语法  
  
```console  
-keycontainer:string  
```  
  
## <a name="arguments"></a>自变量  
 `string`  
 强名称密钥容器的名称。  
  
## <a name="remarks"></a>备注  
 当使用“-keycontainer”选项时，编译器将创建一个可共享的组件。 编译器在程序集清单中插入指定容器的公钥，然后使用私钥对最终的程序集进行签名。 若要生成密钥文件，请在命令行键入 `sn -k file`。 `sn -i` 将密钥对安装到容器中。 编译器在 CoreCLR 上运行时，不支持此选项。 在生成 CoreCLR 时对程序集进行签名，请使用 [-keyfile](keyfile-compiler-option.md) 选项。
  
 如果使用 [-target:module](../../../csharp/language-reference/compiler-options/target-module-compiler-option.md) 进行编译，当使用 [-addmodule](../../../csharp/language-reference/compiler-options/addmodule-compiler-option.md) 将此模块编译到程序集时，密钥文件的名称将保存在模块中，且会并入程序集。  
  
 还可以将此选项指定为任何 Microsoft 中间语言 (MSIL) 模块的源代码中的自定义特性 (<xref:System.Reflection.AssemblyKeyNameAttribute?displayProperty=nameWithType>)。  
  
 此外，可使用 [-keyfile](../../../csharp/language-reference/compiler-options/keyfile-compiler-option.md) 将加密信息传递给编译器。 如果希望将公钥添加到程序集清单，但希望测试完程序集后再对其签名，请使用 [-delaysign](../../../csharp/language-reference/compiler-options/delaysign-compiler-option.md)。  
  
 有关详细信息，请参阅[创建和使用具有强名称的程序集](../../../framework/app-domains/create-and-use-strong-named-assemblies.md)和[延迟为程序集签名](../../../framework/app-domains/delay-sign-assembly.md)。  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 开发环境中设置此编译器选项  
  
1.  Visual Studio 开发环境中尚未提供此编译器选项。  
  
 可通过 <xref:VSLangProj.ProjectProperties.AssemblyKeyContainerName%2A> 以编程方式访问此编译器选项。  
  
## <a name="see-also"></a>请参阅

- [C# 编译器 -keyfile 选项](keyfile-compiler-option.md)
- [C# 编译器选项](index.md)
- [管理项目和解决方案属性](/visualstudio/ide/managing-project-and-solution-properties)
