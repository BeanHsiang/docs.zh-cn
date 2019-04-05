---
title: 从命令行生成 (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- builds [Visual Basic], command-line
- Visual Basic compiler, about Visual Basic compiler
- command line [Visual Basic], compilers
- command line [Visual Basic], building from
- command line [Visual Basic], builds
- compilers [Visual Basic], invoking from command line
- command-line builds
- compiling source code
- command-line compilers [Visual Basic], Visual Basic
- command line [Visual Basic], Visual Basic
ms.assetid: e61947e9-a42e-4717-a699-5f70a98cdd03
ms.openlocfilehash: 798baa90308c83e42b335635fb23a9983f5180fb
ms.sourcegitcommit: facefcacd7ae2e5645e463bc841df213c505ffd4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/05/2019
ms.locfileid: "55739470"
---
# <a name="building-from-the-command-line-visual-basic"></a>从命令行生成 (Visual Basic)
Visual Basic 项目由一个或多个单独的源代码文件组成。 在名为编译过程中，这些文件被集中到一个包，可以为应用程序运行的单个可执行文件。  
  
 Visual Basic 提供命令行编译器作为从 Visual Studio 集成的开发环境 (IDE) 中编译程序的替代方法。 命令行编译器专为不需要完整的 IDE 中的功能集的情况下，例如，当您是使用或编写具有有限的系统内存或存储空间的计算机。  
  
  若要编译源文件从 Visual Studio IDE 中的，选择**构建**命令**生成**菜单。  
  
> [!TIP]
>  通过使用 Visual Studio IDE 生成项目文件时，可以显示有关关联的信息**vbc**命令和输出窗口中的其开关。 若要显示此信息，请打开[选项对话框、 项目和解决方案、 生成和运行](/visualstudio/ide/reference/options-dialog-box-projects-and-solutions-build-and-run)，然后设置**MSBuild 项目生成输出详细级别**到**正常**或更高级别的详细级别。 有关详细信息，请参阅[如何：查看、 保存和配置生成日志文件](/visualstudio/ide/how-to-view-save-and-configure-build-log-files)。  
  
 可以通过使用 MSBuild 编译在命令提示符下的项目 (.vbproj) 文件。 有关详细信息，请参阅[命令行参考](/visualstudio/msbuild/msbuild-command-line-reference)和[演练：使用 MSBuild](/visualstudio/msbuild/walkthrough-using-msbuild)。  
  
## <a name="in-this-section"></a>本节内容  
 [如何：调用命令行编译器](../../../visual-basic/reference/command-line-compiler/how-to-invoke-the-command-line-compiler.md)  
 介绍如何调用命令行编译器在 MS-DOS 提示符处或从特定的子目录。  
  
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)  
 提供了一系列可以修改供自己使用的示例命令行。  
  
## <a name="related-sections"></a>相关章节  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)  
 提供编译器选项，按字母顺序或按目的组织的列表。  
  
 [条件编译](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)  
 描述如何编译代码的特定部分。  
  
 [在 Visual Studio 中生成和清理项目和解决方案](/visualstudio/ide/building-and-cleaning-projects-and-solutions-in-visual-studio)  
 说明如何组织什么将包含在不同版本中，选择项目属性中，并确保以正确的顺序生成项目。
