---
title: LINQ to SQL
ms.date: 03/30/2017
ms.assetid: 73d13345-eece-471a-af40-4cc7a2f11655
ms.openlocfilehash: 532813f68c0996337ce3bed8172a826425db1ec0
ms.sourcegitcommit: d2ccb199ae6bc5787b4762e9ea6d3f6fe88677af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56092223"
---
# <a name="linq-to-sql"></a>LINQ to SQL
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 是 [!INCLUDE[dnprdnshort](../../../../../../includes/dnprdnshort-md.md)] 3.5 版的一个组件，提供了用于将关系数据作为对象管理的运行时基础结构。  
  
> [!NOTE]
>  关系数据显示为由二维表（关系或平面文件）组成的集合，其中公共列将表互相关联起来。 若要有效地使用 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]，您必须略为熟悉关系数据库的基本原理。  
  
 在 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 中，关系数据库的数据模型映射到用开发人员所用的编程语言表示的对象模型。 当应用程序运行时，[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 会将对象模型中的语言集成查询转换为 SQL，然后将它们发送到数据库进行执行。 当数据库返回结果时，[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 会将它们转换回您可以用您自己的编程语言处理的对象。  
  
 通常使用 Visual Studio 的开发人员使用[!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)]，它提供用于实现许多功能的用户界面[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]。  
  
 此版本的 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 附带的文档介绍了生成 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 应用程序所需的基本构造块、流程和技术。 您还可以搜索 Microsoft Docs 特定问题，并且可以参与[LINQ 论坛](https://go.microsoft.com/fwlink/?LinkId=76488)，可以与专家们讨论更复杂的主题的详细信息。 最后， [LINQ to SQL： 关系数据的.net 语言集成查询](https://go.microsoft.com/fwlink/?LinkId=93205)白皮书详细介绍[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]技术并包含 Visual Basic 和 C# 代码示例。  
  
## <a name="in-this-section"></a>本节内容  
 [入门](../../../../../../docs/framework/data/adonet/sql/linq/getting-started.md)  
 提供对 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 的简要概述以及有关如何开始使用 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 的信息。  
  
 [编程指南](../../../../../../docs/framework/data/adonet/sql/linq/programming-guide.md)  
 提供映射、查询、更新、调试及类似任务的步骤。  
  
 [引用](../../../../../../docs/framework/data/adonet/sql/linq/reference.md)  
 提供有关 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 的多个方面的参考信息。 相关主题包括“SQL-CLR 类型映射”、“标准查询运算符转换”等。  
  
 [示例](../../../../../../docs/framework/data/adonet/sql/linq/samples.md)  
 提供指向 Visual Basic 和 C# 示例。  
  
## <a name="related-sections"></a>相关章节  
 [语言集成查询 (LINQ)-C#](../../../../../csharp/programming-guide/concepts/linq/index.md)\
 中的 LINQ 技术概述了C#。
 
 [语言集成查询 (LINQ) 的 Visual Basic](../../../../../visual-basic/programming-guide/concepts/linq/index.md)  
 提供了在 Visual Basic 中的 LINQ 技术的概述。
  
 [LINQ](../../../../../visual-basic/programming-guide/language-features/linq/index.md)  
 介绍[!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)]技术，可用于 Visual Basic 用户。  
  
 [LINQ 和 ADO.NET](../../../../../../docs/framework/data/adonet/linq-and-ado-net.md)  
 链接到 [!INCLUDE[vstecado](../../../../../../includes/vstecado-md.md)] 门户。  
  
 [LINQ to SQL 演练](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/bb386295(v=vs.90))  
 列出可用于 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 的演练。  
  
 [下载示例数据库](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md)  
 介绍如何下载文档中使用的示例数据库。  
  
 [LinqDataSource Web 服务器控件概述](https://docs.microsoft.com/previous-versions/aspnet/bb547113(v=vs.100))  
 介绍 <xref:System.Web.UI.WebControls.LinqDataSource> 控件如何通过 [!INCLUDE[vbteclinqext](../../../../../../includes/vbteclinqext-md.md)] 数据源控件结构向 Web 开发人员公开 [!INCLUDE[vstecasp](../../../../../../includes/vstecasp-md.md)]。
