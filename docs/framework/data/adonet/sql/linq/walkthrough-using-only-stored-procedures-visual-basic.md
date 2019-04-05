---
title: 演练：仅使用存储过程 (Visual Basic)
ms.date: 03/30/2017
dev_langs:
- vb
ms.assetid: 5a736a30-ba66-4adb-b87c-57d19476e862
ms.openlocfilehash: 7c696d24dd84aee568706200389839dea080d7b4
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54577374"
---
# <a name="walkthrough-using-only-stored-procedures-visual-basic"></a>演练：仅使用存储过程 (Visual Basic)
本演练提供了通过仅使用存储过程来访问数据的 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 基本端对端方案。 数据库管理员经常使用此方法来限制数据存储的访问方式。  
  
> [!NOTE]
>  您还可以在 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 应用程序中使用存储过程来重写默认行为，尤其是 `Create`、`Update` 和 `Delete` 进程的默认行为。 有关详细信息，请参阅[自定义插入、 更新和删除操作](../../../../../../docs/framework/data/adonet/sql/linq/customizing-insert-update-and-delete-operations.md)。  
  
 对于本演练的目的，你将使用已映射到 Northwind 示例数据库中的存储过程的两种方法：CustOrdersDetail 和 CustOrderHist。 此映射发生在运行 SqlMetal 命令行工具生成的 Visual Basic 文件。 有关更多信息，请参见本演练后面的“先决条件”一节。  
  
 本演练不依赖于[!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)]。 使用 Visual Studio 的开发人员还可以使用[!INCLUDE[vs_ordesigner_short](../../../../../../includes/vs-ordesigner-short-md.md)]实现存储的过程功能。 请参阅[LINQ to SQL 工具在 Visual Studio 中](/visualstudio/data-tools/linq-to-sql-tools-in-visual-studio2)。  
  
 [!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]  
  
 本演练是使用 Visual Basic 开发设置编写的。  
  
## <a name="prerequisites"></a>系统必备  
 本演练需要如下内容：  
  
-   本演练使用专用文件夹（“c:\linqtest3”）来保存文件。 请在开始本演练前创建此文件夹。  
  
-   Northwind 示例数据库。  
  
     如果您的开发计算机上没有此数据库，您可以从 Microsoft 下载网站下载它。 有关说明，请参阅[下载示例数据库](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md)。 下载此数据库后，请将 northwnd.mdf 文件复制到 c:\linqtest3 文件夹。  
  
-   从 Northwind 数据库生成的 Visual Basic 代码文件。  
  
     本演练是通过使用 SqlMetal 工具以及如下命令行编写的：  
  
     **sqlmetal /code:"c:\linqtest3\northwind.vb" /language:vb "c:\linqtest3\northwnd.mdf" /sprocs /functions /pluralize**  
  
     有关详细信息，请参阅 [SqlMetal.exe（代码生成工具）](../../../../../../docs/framework/tools/sqlmetal-exe-code-generation-tool.md)。  
  
## <a name="overview"></a>概述  
 本演练由六项主要任务组成：  
  
-   设置[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]Visual Studio 中的解决方案。  
  
-   将 System.Data.Linq 程序集添加到项目中。  
  
-   向项目添加数据库代码文件。  
  
-   创建与数据库的连接。  
  
-   设置用户界面。  
  
-   运行和测试应用程序。  
  
## <a name="creating-a-linq-to-sql-solution"></a>创建 LINQ to SQL 解决方案  
 在此第一个任务中，创建一个包含必要的引用，生成并运行的 Visual Studio 解决方案[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]项目。  
  
#### <a name="to-create-a-linq-to-sql-solution"></a>创建 LINQ to SQL 解决方案  
  
1.  在 Visual Studio**文件**菜单上，单击**新项目**。  
  
2.  在 **“新建项目”** 对话框中的 **“项目类型”** 窗格中，展开 **“Visual Basic”**，然后单击 **“Windows”**。  
  
3.  在 **“模板”** 窗格中，单击 **“Windows 窗体应用程序”**。  
  
4.  在中**名称**框中，键入**SprocOnlyApp**。  
  
5.  单击 **“确定”**。  
  
     Windows 窗体设计器即会打开。  
  
## <a name="adding-the-linq-to-sql-assembly-reference"></a>添加 LINQ to SQL 程序集引用  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 程序集未包含在标准的 Windows 窗体应用程序模板中。 您将需要按照以下步骤中的说明自行添加此程序集：  
  
#### <a name="to-add-systemdatalinqdll"></a>添加 System.Data.Linq.dll  
  
1.  在中**解决方案资源管理器**，单击**显示所有文件**。  
  
2.  在中**解决方案资源管理器**，右键单击**引用**，然后单击**添加引用**。  
  
3.  在中**添加引用**对话框中，单击 **.NET**，单击 System.Data.Linq 程序集，然后单击**确定**。  
  
     此程序集即被添加到项目中。  
  
## <a name="adding-the-northwind-code-file-to-the-project"></a>将 Northwind 代码文件添加到项目  
 此步骤假定您已使用 SqlMetal 工具从 Northwind 示例数据库生成代码文件。 有关更多信息，请参见本演练前面部分的“先决条件”一节。  
  
#### <a name="to-add-the-northwind-code-file-to-the-project"></a>将 northwind 代码文件添加到项目  
  
1.  上**项目**菜单上，单击**添加现有项**。  
  
2.  在中**添加现有项**对话框中，移动到 c:\linqtest3\northwind.vb，然后依次**添加**。  
  
     northwind.vb 文件即被添加到项目中。  
  
## <a name="creating-a-database-connection"></a>创建数据库连接  
 在此步骤中，您要定义与 Northwind 示例数据库的连接。 本演练使用“c:\linqtest3\northwnd.mdf”作为路径。  
  
#### <a name="to-create-the-database-connection"></a>创建数据库连接  
  
1.  在中**解决方案资源管理器**，右键单击**Form1.vb**，然后单击**查看代码**。  
  
     `Class Form1` 将显示在代码编辑器中。  
  
2.  在 `Form1` 代码块中键入如下代码：  
  
     [!code-vb[DLinqWalk4VB#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk4VB/vb/Form1.vb#1)]  
  
## <a name="setting-up-the-user-interface"></a>设置用户界面  
 在此任务中，您要创建用户界面，供用户执行存储过程以访问数据库中的数据之用。 在您按照本演练开发的应用程序中，用户可以只使用嵌入在此应用程序中的存储过程来访问数据库中的数据。  
  
#### <a name="to-set-up-the-user-interface"></a>设置用户界面  
  
1.  返回 Windows 窗体设计器 (**Form1.vb[Design]**)。  
  
2.  在 **“视图”** 菜单上单击 **“工具箱”**。  
  
     工具箱即会打开。  
  
    > [!NOTE]
    >  单击**自动隐藏**图钉，以使工具箱保持打开状态，而执行的其余步骤在本部分中。  
  
3.  将两个按钮、 两个文本框和两个标签拖从工具箱中拖动**Form1**。  
  
     按照附图排列这些控件。 展开**Form1** ，以便控件更便于显示。  
  
4.  右键单击**Label1**，然后单击**属性**。  
  
5.  更改**文本**属性从**Label1**到**Enter OrderID:**。  
  
6.  在相同的方式对**Label2**，更改**文本**属性从**Label2**到**Enter CustomerID:**。  
  
7.  同样，在更改**文本**属性**Button1**到**订单详细信息**。  
  
8.  更改**文本**属性**Button2**到**订单历史记录**。  
  
     将这些按钮控件加宽，以使所有文本均可见。  
  
#### <a name="to-handle-button-clicks"></a>处理按钮单击  
  
1.  双击**订单详细信息**上**Form1**创建`Button1`事件处理程序并打开代码编辑器。  
  
2.  将如下代码键入到 `Button1` 处理程序中：  
  
     [!code-vb[DLinqWalk4VB#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk4VB/vb/Form1.vb#2)]  
  
3.  现在双击**Button2**若要创建的 Form1 上`Button2`事件处理程序并打开代码编辑器。  
  
4.  将如下代码键入到 `Button2` 处理程序中：  
  
     [!code-vb[DLinqWalk4VB#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk4VB/vb/Form1.vb#3)]  
  
## <a name="testing-the-application"></a>测试应用程序  
 现在，可以开始测试您的应用程序了。 请注意，您可对数据存储施加的影响仅限于这两个存储过程能够执行的操作。 这些操作是要根据您输入的所有 orderID 返回相应订单包括的产品，或根据您输入的所有 CustomerID 返回相应客户的产品订购历史记录。  
  
#### <a name="to-test-the-application"></a>测试应用程序  
  
1.  按 F5 开始调试。  
  
     此时将显示 Form1。  
  
2.  在中**Enter OrderID**框中，键入**10249** ，然后单击**Order Details**。  
  
     随即会显示一个消息框，其中列出了 10249 号订单中所包括的产品。  
  
     单击**确定**以关闭消息框。  
  
3.  在中**输入 CustomerID**框中，键入`ALFKI`，然后单击**订单历史记录**。  
  
     随即会显示一个消息框，其中列出了 ALFKI 客户的订单历史记录。  
  
     单击**确定**以关闭消息框。  
  
4.  在中**Enter OrderID**框中，键入`123`，然后单击**订单详细信息**。  
  
     随即会显示一个消息框，其中显示“无结果”。  
  
     单击**确定**以关闭消息框。  
  
5.  上**调试**菜单上，单击**停止调试**。  
  
     调试会话即会关闭。  
  
6.  如果您已试验完毕，则可以单击**关闭项目**上**文件**菜单中，并在提示时保存你的项目。  
  
## <a name="next-steps"></a>后续步骤  
 您可以通过做一些更改来增强此项目的功能。 例如，您可以在列表框中列出可用的存储过程，供用户选择要执行哪些过程。 您还可以将报告的输出以流的方式传输到文本文件。  
  
## <a name="see-also"></a>请参阅
- [通过演练学习](../../../../../../docs/framework/data/adonet/sql/linq/learning-by-walkthroughs.md)
- [存储过程](../../../../../../docs/framework/data/adonet/sql/linq/stored-procedures.md)
