---
title: 如何：使用 CodeDOM 创建 XML 文档文件
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- CodeDOM, generating XML documentation
- XML documentation, creating using CodeDOM
- Code Document Object Model, generating XML documentation
ms.assetid: e3b80484-36b9-41dd-9d21-a2f9a36381dc
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 8086a512d117767127260bcf779fc11555cd67dd
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54632824"
---
# <a name="how-to-create-an-xml-documentation-file-using-codedom"></a>如何：使用 CodeDOM 创建 XML 文档文件
可使用 CodeDOM 创建生成 XML 文档的代码。 该进程包括创建包含 XML 文档注释的 CodeDOM 图、生成代码和通过创建 XML 文档输出的编译器选项编译生成的代码。  
  
### <a name="to-create-a-codedom-graph-that-contains-xml-documentation-comments"></a>创建包含 XML 文档注释的 CodeDOM 图  
  
1.  为示例应用程序创建包含 CodeDOM 图的 <xref:System.CodeDom.CodeCompileUnit>。  
  
2.  使用 <xref:System.CodeDom.CodeCommentStatement.%23ctor%2A> 构造函数（`docComment` 参数设置为 `true`）创建 XML 文档注释元素和文本。  
  
     [!code-csharp[CodeDomHelloWorldSample#4](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomHelloWorldSample/cs/program.cs#4)]
     [!code-vb[CodeDomHelloWorldSample#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomHelloWorldSample/vb/program.vb#4)]  
  
### <a name="to-generate-the-code-from-the-codecompileunit"></a>从 CodeCompileUnit 生成代码  
  
1.  使用 <xref:System.CodeDom.Compiler.CodeDomProvider.GenerateCodeFromCompileUnit%2A> 方法生成代码并创建要编译的源文件。  
  
     [!code-csharp[CodeDomHelloWorldSample#5](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomHelloWorldSample/cs/program.cs#5)]
     [!code-vb[CodeDomHelloWorldSample#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomHelloWorldSample/vb/program.vb#5)]  
  
### <a name="to-compile-the-code-and-generate-the-documentation-file"></a>编译代码并生成文档文件  
  
1.  将 /doc 编译器选项添加到 <xref:System.CodeDom.Compiler.CompilerParameters> 对象的 <xref:System.CodeDom.Compiler.CompilerParameters.CompilerOptions%2A> 属性中，然后将该对象传递给 <xref:System.CodeDom.Compiler.CodeDomProvider.CompileAssemblyFromFile%2A> 方法，以便在编译代码时创建 XML 文档文件。  
  
     [!code-csharp[CodeDomHelloWorldSample#6](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomHelloWorldSample/cs/program.cs#6)]
     [!code-vb[CodeDomHelloWorldSample#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomHelloWorldSample/vb/program.vb#6)]  
  
## <a name="example"></a>示例  
 以下代码示例创建一个包含文档注释的 CodeDOM 图，从该图生成一个代码文件，然后编译该文件并创建一个关联的 XML 文档文件。  
  
 [!code-csharp[CodeDomHelloWorldSample#1](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomHelloWorldSample/cs/program.cs#1)]
 [!code-vb[CodeDomHelloWorldSample#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomHelloWorldSample/vb/program.vb#1)]  
  
 该代码示例在 HelloWorldDoc.xml 文件中创建以下 XML 文档。  
  
```xml  
<?xml version="1.0" ?>   
<doc>  
  <assembly>  
    <name>HelloWorld</name>   
  </assembly>  
  <members>  
    <member name="T:Samples.Class1">  
      <summary>  
        Create a Hello World application.   
        <seealso cref="M:Samples.Class1.Main" />   
      </summary>  
    </member>  
    <member name="M:Samples.Class1.Main">  
      <summary>  
        Main method for HelloWorld application.   
        <para>Add a new paragraph to the description.</para>   
      </summary>  
    </member>  
  </members>  
</doc>  
```  
  
## <a name="compiling-the-code"></a>编译代码  
  
-   需要 `FullTrust` 权限集才可成功执行此代码示例。  
  
## <a name="see-also"></a>请参阅
- [使用 XML 记录代码](~/docs/visual-basic/programming-guide/program-structure/documenting-your-code-with-xml.md)
- [XML 文档注释](~/docs/csharp/programming-guide/xmldoc/xml-documentation-comments.md)
- [XML 文档](/cpp/ide/xml-documentation-visual-cpp)
