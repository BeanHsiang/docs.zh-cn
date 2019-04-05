---
title: 在 Visual Basic 中编写查询
ms.date: 07/20/2015
helpviewer_keywords:
- queries [LINQ in Visual Basic], writing
- LINQ [Visual Basic], walkthroughs
- LINQ [Visual Basic], writing queries
- writing LINQ queries [Visual Basic]
ms.assetid: f0045808-b9fe-4d31-88d1-473d9957211e
ms.openlocfilehash: 3c1087f1ea260b61a51126f42703a32075884e54
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56971281"
---
# <a name="walkthrough-writing-queries-in-visual-basic"></a>演练：在 Visual Basic 中编写查询
本演练演示如何使用 Visual Basic 语言功能编写[!INCLUDE[vbteclinqext](~/includes/vbteclinqext-md.md)]查询表达式。 本演练演示如何在列表中的学生对象创建查询、 运行查询，以及如何对其进行修改。 查询将合并多个功能，包括对象初始值设定项、 局部类型推理和匿名类型。  
  
 完成此演练后，您将随时可以转到示例和文档的特定[!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)]感兴趣的提供程序。 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 提供程序包括[!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)]， [!INCLUDE[linq_dataset](~/includes/linq-dataset-md.md)]，和[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]。  
  
## <a name="create-a-project"></a>创建项目  
  
#### <a name="to-create-a-console-application-project"></a>若要创建控制台应用程序项目  
  
1.  启动 Visual Studio。  
  
2.  在 **“文件”** 菜单上，指向 **“新建”**，然后单击 **“项目”**。  
  
3.  在中**已安装的模板**列表中，单击**Visual Basic**。  
  
4.  在项目类型列表中，单击**控制台应用程序**。 在中**名称**框中，键入项目的名称，然后单击**确定**。  
  
     创建一个项目。 默认情况下，它包含对 system.core.dll 的引用。 此外，**导入命名空间**上列出[，项目设计器 (Visual Basic) 引用页](/visualstudio/ide/reference/references-page-project-designer-visual-basic)包括<xref:System.Linq?displayProperty=nameWithType>命名空间。  
  
5.  上[编译页，项目设计器 (Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic)，确保**Option infer**设置为**上**。  
  
## <a name="add-an-in-memory-data-source"></a>添加的内存中数据源  
 在本演练中的查询的数据源是一系列`Student`对象。 每个`Student`对象包含名字、 姓氏、 一类和学术排名学生正文中的。  
  
#### <a name="to-add-the-data-source"></a>添加数据源  
  
-   定义`Student`类，并创建类的实例的列表。  
  
    > [!IMPORTANT]
    >  定义所需的代码`Student`类，并创建使用的列表在本演练中提供示例[如何：创建的项列表](../../../../visual-basic/programming-guide/concepts/linq/how-to-create-a-list-of-items.md)。 可以在此处复制并将其粘贴到你的项目。 新代码将替换在创建项目时出现的代码。  
  
#### <a name="to-add-a-new-student-to-the-students-list"></a>若要向学生列表添加新学生  
  
-   请按照中的模式`getStudents`方法中添加的另一个实例`Student`到列表的类。 添加学生将介绍对象初始值设定项。 有关详细信息，请参阅[对象初始值设定项：命名和匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)。  
  
## <a name="create-a-query"></a>创建查询  
 执行时，在本部分中添加查询将生成其学术排名将其放入前十个学生列表。 因为该查询用于选择完整`Student`对象每次查询结果的类型是`IEnumerable(Of Student)`。 但是，查询类型通常是未指定在查询定义中。 相反，编译器使用局部类型推理来确定的类型。 有关详细信息，请参阅[本地类型推断](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)。 查询的范围变量`currentStudent`，可作为对每个引用`Student`在源中的实例`students`，提供对中的每个对象的属性访问`students`。  
  
#### <a name="to-create-a-simple-query"></a>创建简单查询  
  
1.  查找中的位置`Main`方法的项目的标记，如下所示：  
  
     [!code-vb[VbLINQWalkthrough#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQWalkthrough/VB/Class1.vb#1)]  
  
     将以下代码复制并粘贴到此位置。  
  
     [!code-vb[VbLINQWalkthrough#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQWalkthrough/VB/Class1.vb#2)]  
  
2.  将鼠标指针停留在`studentQuery`若要验证编译器分配的类型是在代码中`IEnumerable(Of Student)`。  
  
## <a name="run-the-query"></a>运行查询  
 该变量`studentQuery`包含定义的查询，而不运行查询的结果。 用于运行查询的典型机制是`For Each`循环。 返回序列中的每个元素的循环迭代变量可通过访问。 有关执行查询的详细信息，请参阅[编写你的第一个 LINQ 查询](../../../../visual-basic/programming-guide/concepts/linq/writing-your-first-linq-query.md)。  
  
#### <a name="to-run-the-query"></a>若要运行查询  
  
1.  以下代码添加到`For Each`循环在项目中查询的下面。  
  
     [!code-vb[VbLINQWalkthrough#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQWalkthrough/VB/Class1.vb#3)]  
  
2.  将鼠标指针停留在循环控制变量`studentRecord`以查看其数据类型。 类型`studentRecord`被推断为`Student`，因为`studentQuery`返回的集合`Student`实例。  
  
3.  生成并通过按 CTRL + F5 运行该应用程序。 请注意控制台窗口中的结果。  
  
## <a name="modify-the-query"></a>修改查询  
 它是更轻松地扫描查询结果，如果它们在指定的顺序。 可以对基于任何可用字段返回的序列进行排序。  
  
#### <a name="to-order-the-results"></a>对结果进行排序  
  
1.  添加以下`Order By`子句之间`Where`语句和`Select`查询语句。 `Order By`子句将排序结果按字母顺序从 A 到 Z、 的最后一个根据每个学生的名字。  
  
    ```  
    Order By currentStudent.Last Ascending   
    ```  
  
2.  若要按姓氏，然后按名字排序，请将这两个字段添加到查询：  
  
    ```  
    Order By currentStudent.Last Ascending, currentStudent.First Ascending   
    ```  
  
     此外可以指定`Descending`顺序从 Z 到 a。  
  
3.  生成并通过按 CTRL + F5 运行该应用程序。 请注意控制台窗口中的结果。  
  
#### <a name="to-introduce-a-local-identifier"></a>引入本地标识符  
  
1.  将代码添加在本部分介绍在查询表达式中的本地标识符。 本地标识符将用于保存中间结果。 在以下示例中，`name`是包含学生的串联的标识符的名字和姓氏。 为方便起见，可以使用的本地标识符或也可以通过将存储的一个表达式，否则将计算多次结果来提高性能。  
  
     [!code-vb[VbLINQWalkthrough#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQWalkthrough/VB/Class1.vb#4)]  
  
2.  生成并通过按 CTRL + F5 运行该应用程序。 请注意控制台窗口中的结果。  
  
#### <a name="to-project-one-field-in-the-select-clause"></a>投影在 Select 子句中的一个字段  
  
1.  添加查询和`For Each`来创建查询，以生成一个序列，其元素与不同源中元素的此部分中的循环。 在以下示例中，源是一系列`Student`返回对象，但只有一个成员的每个对象： 其姓氏为 Garcia 学生的名字。 因为`currentStudent.First`是一个字符串，返回的序列的数据类型`studentQuery3`是`IEnumerable(Of String)`，一个字符串序列。 如前面的示例中所示分配的数据类型为`studentQuery3`留给编译器通过使用局部类型推理来确定。  
  
     [!code-vb[VbLINQWalkthrough#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQWalkthrough/VB/Class1.vb#5)]  
  
2.  将鼠标指针停留在`studentQuery3`以验证是否已分配的类型在代码中`IEnumerable(Of String)`。  
  
3.  生成并通过按 CTRL + F5 运行该应用程序。 请注意控制台窗口中的结果。  
  
#### <a name="to-create-an-anonymous-type-in-the-select-clause"></a>若要在 Select 子句中创建一个匿名类型  
  
1.  添加查询中使用此部分，以查看如何匿名类型中的代码。 如果您使用它们在查询中你想要从数据源而不是完整记录返回多个字段 (`currentStudent`前面的示例中的记录) 或单个字段 (`First`前面部分中)。 而不是定义新的命名的类型包含你想要在结果中包含的字段，你可以指定在字段`Select`子句和编译器创建一个匿名类型与这些字段作为其属性。 有关详细信息，请参阅[匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)。  
  
     以下示例创建的查询返回的名称和的高年级学生其学术排名是介于 1 和 10，学术排名的顺序。 在此示例中，类型`studentQuery4`必须推断，因为`Select`子句将返回一个匿名类型的实例和匿名类型已没有可用的名称。  
  
     [!code-vb[VbLINQWalkthrough#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQWalkthrough/VB/Class1.vb#6)]  
  
2.  生成并通过按 CTRL + F5 运行该应用程序。 请注意控制台窗口中的结果。  
  
## <a name="additional-examples"></a>其他示例  
 现在，你已了解基础知识，下面是其他示例来演示灵活的列表，以及利用[!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)]查询。 每个示例被前面其用途的简短说明。 将鼠标指针停留在每个查询，以查看推断出的类型的查询结果变量。 使用`For Each`循环生成的结果。  
  
 [!code-vb[VbLINQWalkthrough#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQWalkthrough/VB/Class1.vb#7)]  
  
## <a name="additional-information"></a>其他信息  
 了解如何使用查询的基本概念后，已准备好读取的特定类型的文档和示例[!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)]感兴趣的提供程序：  
  
 [LINQ to Objects](../../../../visual-basic/programming-guide/concepts/linq/linq-to-objects.md)  
  
 [LINQ to SQL](../../../../framework/data/adonet/sql/linq/index.md)  
  
 [LINQ to XML](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml.md)  
  
 [LINQ to DataSet](../../../../framework/data/adonet/linq-to-dataset.md)  
  
## <a name="see-also"></a>请参阅

- [语言集成查询 (LINQ) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/index.md)
- [Visual Basic 中的 LINQ 入门](../../../../visual-basic/programming-guide/concepts/linq/getting-started-with-linq.md)
- [局部类型推理](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)
- [对象初始值设定项：命名和匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)
- [匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)
- [Visual Basic 中的 LINQ 简介](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)
- [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)
- [查询](../../../../visual-basic/language-reference/queries/index.md)
