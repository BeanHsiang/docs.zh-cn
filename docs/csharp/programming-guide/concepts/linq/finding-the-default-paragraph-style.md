---
title: 查找默认段落样式 (C#)
ms.date: 07/20/2015
ms.assetid: be102177-8ab0-444a-b671-7023e555ffdb
ms.openlocfilehash: 052accf31007001c0fa0d46870ee6e4cd30f6bb8
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54674071"
---
# <a name="finding-the-default-paragraph-style-c"></a>查找默认段落样式 (C#)
在 WordprocessingML 文档中操作信息教程中的第一项任务是在文档中查找默认段落样式。  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>说明  
 下面的示例打开一个 Office Open XML WordprocessingML 文档，查找文档和包的样式部分，然后执行查找默认样式名称的查询。 有关 Office Open XML 文档包及其构成包的信息，请参阅 [Office Open XML WordprocessingML 文档的详细信息 (C#)](../../../../csharp/programming-guide/concepts/linq/details-of-office-open-xml-wordprocessingml-documents.md)。  
  
 查询将查找名为 `w:style` 的节点，该节点具有值为“paragraph”的名为 `w:type` 的属性和值为“1”的名为 `w:default` 的属性。 由于将只有一个 XML 节点具有这些属性，因此查询使用 <xref:System.Linq.Enumerable.First%2A?displayProperty=nameWithType> 运算符将集合转换为单一实例。 然后，它获取名为 `w:styleId` 的属性的值。  
  
 本示例使用 WindowsBase 程序集中的类。 它使用 <xref:System.IO.Packaging?displayProperty=nameWithType> 命名空间中的类型。  
  
### <a name="code"></a>代码  
  
```csharp  
const string fileName = "SampleDoc.docx";  
  
const string documentRelationshipType =  
  "http://schemas.openxmlformats.org/officeDocument/2006/relationships/officeDocument";  
const string stylesRelationshipType =  
  "http://schemas.openxmlformats.org/officeDocument/2006/relationships/styles";  
const string wordmlNamespace =  
  "http://schemas.openxmlformats.org/wordprocessingml/2006/main";  
XNamespace w = wordmlNamespace;  
  
XDocument xDoc = null;  
XDocument styleDoc = null;  
  
using (Package wdPackage = Package.Open(fileName, FileMode.Open, FileAccess.Read))  
{  
    PackageRelationship docPackageRelationship =  
      wdPackage.GetRelationshipsByType(documentRelationshipType).FirstOrDefault();  
    if (docPackageRelationship != null)  
    {  
        Uri documentUri = PackUriHelper.ResolvePartUri(new Uri("/", UriKind.Relative),  
          docPackageRelationship.TargetUri);  
        PackagePart documentPart = wdPackage.GetPart(documentUri);  
  
        //  Load the document XML in the part into an XDocument instance.  
        xDoc = XDocument.Load(XmlReader.Create(documentPart.GetStream()));  
  
        //  Find the styles part. There will only be one.  
        PackageRelationship styleRelation =  
          documentPart.GetRelationshipsByType(stylesRelationshipType).FirstOrDefault();  
        if (styleRelation != null)  
        {  
            Uri styleUri = PackUriHelper.ResolvePartUri(documentUri, styleRelation.TargetUri);  
            PackagePart stylePart = wdPackage.GetPart(styleUri);  
  
            //  Load the style XML in the part into an XDocument instance.  
            styleDoc = XDocument.Load(XmlReader.Create(stylePart.GetStream()));  
        }  
    }  
}  
  
// The following query finds all the paragraphs that have the default style.  
string defaultStyle =   
    (string)(  
        from style in styleDoc.Root.Elements(w + "style")  
        where (string)style.Attribute(w + "type") == "paragraph"&&  
              (string)style.Attribute(w + "default") == "1"  
              select style  
    ).First().Attribute(w + "styleId");  
  
Console.WriteLine("The default style is: {0}", defaultStyle);  
```  
  
### <a name="comments"></a>注释  
 该示例产生下面的输出：  
  
```  
The default style is: Normal  
```  
  
## <a name="next-steps"></a>后续步骤  
 下一个示例中将创建一个类似的查询，查找文档中的所有段落及其样式：  
  
-   [检索段落及其样式 (C#)](../../../../csharp/programming-guide/concepts/linq/retrieving-the-paragraphs-and-their-styles.md)  
  
## <a name="see-also"></a>请参阅

- [教程：操作 WordprocessingML 文档中的内容](../../../../csharp/programming-guide/concepts/linq/tutorial-manipulating-content-in-a-wordprocessingml-document.md)
