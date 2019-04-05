---
title: 如何：使用 XAML 定义表
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [WPF], defining tables
- documents [WPF], defining tables with XAML
- tables [WPF], defining with XAML
ms.assetid: 83f2dc58-437e-4cdc-b5dd-0019810c7a85
ms.openlocfilehash: 7398af6fddae56238e1af3ee4e726420c01ab7ea
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57376918"
---
# <a name="how-to-define-a-table-with-xaml"></a>如何：使用 XAML 定义表
下面的示例演示如何定义<xref:System.Windows.Documents.Table>使用[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]。  示例表有四个列 (由<xref:System.Windows.Documents.TableColumn>元素) 和若干行 (由<xref:System.Windows.Documents.TableRow>元素) 包含数据以及标题、 页眉和页脚信息。  行必须包含在<xref:System.Windows.Documents.TableRowGroup>元素。  表中的每个行组成的一个或多个单元格 (由<xref:System.Windows.Documents.TableCell>元素)。  在表单元的内容必须包含在<xref:System.Windows.Documents.Block>元素; 在这种情况下<xref:System.Windows.Documents.Paragraph>使用元素。  该表还承载一个超链接 (由<xref:System.Windows.Documents.Hyperlink>元素) 中的脚注行。  
  
## <a name="example"></a>示例  
 [!code-xaml[TableSnippetsXAML#_TableXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippetsXAML/CS/Window1.xaml#_tablexaml)]  
  
 下图显示了此示例中定义的表的呈现效果。  
  
 ![呈现的表。](./media/tableeg.png "TableEG")
