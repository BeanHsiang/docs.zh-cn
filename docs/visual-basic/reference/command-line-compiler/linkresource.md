---
title: -linkresource (Visual Basic)
ms.date: 03/10/2018
helpviewer_keywords:
- /linkresource compiler option [Visual Basic]
- -linkresource compiler option [Visual Basic]
- linkresource compiler option [Visual Basic]
- /linkres compiler option [Visual Basic]
- linkres compiler option [Visual Basic]
- -linkres compiler option [Visual Basic]
ms.assetid: cf4dcad8-17b7-404c-9184-29358aa05b15
ms.openlocfilehash: 5555f83107a40b40c7f05c7cc5729f721727f67c
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54729991"
---
# <a name="-linkresource-visual-basic"></a>-linkresource (Visual Basic)
创建指向托管资源的链接。  
  
## <a name="syntax"></a>语法  
  
```  
-linkresource:filename[,identifier[,public|private]]  
' -or-  
-linkres:filename[,identifier[,public|private]]  
```  
  
## <a name="arguments"></a>自变量  
 `filename`  
 必需。 要链接到程序集的资源文件。 如果文件名包含空格，将名称括在引号 ("")。  
  
 `identifier`  
 可选。 资源的逻辑名称。 用于加载资源名称。 默认值是文件的名称。 或者，可以指定文件是否是公共或私有程序集清单，例如： `-linkres:filename.res,myname.res,public`。 默认情况下，`filename`在程序集是公共的。  
  
## <a name="remarks"></a>备注  
 `-linkresource`选项不会将资源文件嵌入到输出文件中; 使用`-resource`选项来执行此操作。  
  
 `-linkresource`选项要求之一`-target`不是选项`-target:module`。  
  
 如果`filename`是[!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)]创建的资源文件，例如，通过[Resgen.exe （资源文件生成器）](../../../framework/tools/resgen-exe-resource-file-generator.md)或在开发环境中，则可以使用来访问中的成员<xref:System.Resources>命名空间。 （有关详细信息，请参阅 <xref:System.Resources.ResourceManager>。）若要在运行时访问所有其他资源，使用的方法的开头`GetManifestResource`在<xref:System.Reflection.Assembly>类。  
  
 文件名称可以是任何文件格式。 例如，你可能希望生成程序集的本机 DLL 部分，从而可将它安装到全局程序集缓存中，并且可从该程序集中的托管代码访问它。  
  
 `-linkresource` 的缩写形式是 `-linkres`。  
  
> [!NOTE]
>  `-linkresource`选项不适用于从 Visual Studio 开发环境，便可仅在编译时从命令行。  
  
## <a name="example"></a>示例  
 下面的代码编译`in.vb`并链接到资源文件`rf.resource`。  
  
```console  
vbc -linkresource:rf.resource in.vb  
```  
  
## <a name="see-also"></a>请参阅

- [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)
- [-目标 (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)
- [-资源 (Visual Basic)](../../../visual-basic/reference/command-line-compiler/resource.md)
- [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
