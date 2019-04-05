---
title: 在 FileName 中指定的文件不是有效的 XML 文件
ms.date: 07/20/2015
ms.assetid: c4c30bf3-e0ad-4bc8-89e0-2c3e49e9793b
ms.openlocfilehash: ffa39653c20127bb6af5e85654fee940a191fe5b
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54603517"
---
# <a name="file-specified-in-filename-is-not-a-valid-xml-file"></a>在 FileName 中指定的文件不是有效的 XML 文件
所提供的文件名称不是有效的 XML 文件。 若要指定允许的 XML 文档的结构和内容，可使用文档类型定义 (DTD)、Microsoft XML 数据缩减 (XDR) 架构或 XML 架构定义语言 (XSD) 架构。 XSD 架构是用于指定 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)]中的 XML 语法的首选方式。

> [!NOTE]
>  在某些较早版本的 Visual Studio 中，“XML 设计器”  是针对类型化数据集和 XML 架构的设计器。 “XML 设计器”  仍可用于创建和编辑 XML 架构文件。 但是，在 Visual Studio 2012 中，用于创建和编辑类型化数据集设计器是**数据集设计器**。 有关详细信息，请参阅[创建和编辑类型化数据集](/visualstudio/data-tools/creating-and-editing-typed-datasets)。

## <a name="to-correct-this-error"></a>更正此错误

-   检查你所提供的文件名是否正确。

-   通过将你想要检查的 XML 文件加载到“XML 设计器” 中，检查指定文件是否包含有效的 XML。 从“XML”  菜单上，单击“验证 XML” 。 错误都显示在“输出列表” 中。

-   如果 XML 文件具有关联的 XML 架构，请检查显示在已定义结构中的元素，以及单个元素的内容是否符合架构中指定的已声明的数据类型。

## <a name="see-also"></a>请参阅

- <xref:System.Xml>
- [如何：分析文件路径](../../visual-basic/developing-apps/programming/drives-directories-files/how-to-parse-file-paths.md)