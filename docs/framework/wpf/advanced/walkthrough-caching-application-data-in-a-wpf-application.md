---
title: 演练：缓存在 WPF 应用程序的应用程序数据
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- walkthroughs [WPF], caching
- caching [.NET Framework]
- caching [WPF]
ms.assetid: dac2c9ce-042b-4d23-91eb-28f584415cef
ms.openlocfilehash: 886a436f845aa4ba9662e75cbc9e534e915a4cfa
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57361169"
---
# <a name="walkthrough-caching-application-data-in-a-wpf-application"></a>演练：缓存在 WPF 应用程序的应用程序数据
缓存可以将数据存储在内存中以便快速访问。 再次访问数据时，应用程序可以从缓存获取数据，而不是从原始源检索数据。 这可改善性能和可伸缩性。 此外，数据源暂时不可用时，缓存可提供数据。

 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]提供了使你能够使用缓存中的类[!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]应用程序。 这些类都位于<xref:System.Runtime.Caching>命名空间。

> [!NOTE]
>  <xref:System.Runtime.Caching>命名空间是中的新增功能[!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)]。 此命名空间使缓存可供所有[!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]应用程序。 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 以前的版本中，缓存仅在 <xref:System.Web> 命名空间可用，因此，需要 ASP.NET 类上的一个依赖项。

 本演练演示如何使用缓存功能，现已推出[!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]作为的一部分[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]应用程序。 在本演练中，你将缓存的文本文件的内容。

 本演练演示以下任务：

-   创建 WPF 应用程序项目。

-   添加对引用[!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)]。

-   正在初始化缓存。

-   正在添加的缓存项的包含文本文件的内容。

-   提供的缓存项的逐出策略。

-   监视缓存的文件的路径和通知的缓存实例更改为受监视的项目。

## <a name="prerequisites"></a>系统必备
 若要完成本演练，你将需要：

-   Microsoft Visual Studio 2010。

-   包含少量的文本的文本文件。 （您将显示文本文件的内容在消息框中。）在本演练中所示的代码假定正在使用以下文件：

     `c:\cache\cacheText.txt`

     但是，可以使用任何文本文件，并为本演练中的代码进行微小的更改。

## <a name="creating-a-wpf-application-project"></a>创建 WPF 应用程序项目
 您将首先创建一个 WPF 应用程序项目。

#### <a name="to-create-a-wpf-application"></a>创建 WPF 应用程序

1.  启动 Visual Studio。

2.  在中**文件**菜单上，单击**新建**，然后单击**新项目**。

     随即显示“新建项目”对话框。

3.  下**已安装的模板**，选择你想要使用的编程语言 (**Visual Basic**或**Visual C#**)。

4.  在中**新的项目**对话框中，选择**WPF 应用程序**。

    > [!NOTE]
    >  如果没有看到**WPF 应用程序**模板，请确保您的目标版本的[!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]支持 WPF。 在中**新的项目**对话框中，选择[!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)]从列表中。

5.  在中**名称**文字框中，输入你的项目的名称。 例如，可以输入**WPFCaching**。

6.  选择“为解决方案创建目录”复选框。

7.  单击 **“确定”**。

     WPF 设计器中打开**设计**查看，并显示 MainWindow.xaml 文件。 Visual Studio 将创建**我的项目**文件夹、 Application.xaml 文件和 MainWindow.xaml 文件。

## <a name="targeting-the-net-framework-and-adding-a-reference-to-the-caching-assemblies"></a>面向.NET Framework 并添加对缓存程序集的引用
 默认情况下，WPF 应用程序目标[!INCLUDE[net_client_v40_long](../../../../includes/net-client-v40-long-md.md)]。 若要使用<xref:System.Runtime.Caching>WPF 应用程序中的命名空间，该应用程序必须面向[!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)](不[!INCLUDE[net_client_v40_long](../../../../includes/net-client-v40-long-md.md)])，并且必须包括对命名空间的引用。

 因此下, 一步将更改.NET Framework 目标，并添加对引用<xref:System.Runtime.Caching>命名空间。

> [!NOTE]
>  .NET Framework 目标更改的过程是不同的 Visual Basic 项目中并在 Visual C# 项目中。

#### <a name="to-change-the-target-net-framework-in-visual-basic"></a>若要更改的目标在 Visual Basic 中的.NET Framework

1.  在中**解决方案资源管理器**，右键单击项目名称，然后单击**属性**。

     显示应用程序的属性窗口。

2.  单击“编译”选项卡。

3.  在窗口的底部，单击**高级编译选项...**.

     **高级编译器设置**显示对话框。

4.  在中**目标框架 （所有配置）** 列表中，选择[!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)]。 (不要选择[!INCLUDE[net_client_v40_long](../../../../includes/net-client-v40-long-md.md)]。)

5.  单击 **“确定”**。

     随即显示“目标框架更改”对话框。

6.  在中**目标 Framework 更改**对话框中，单击**是**。

     项目已关闭，然后重新打开它。

7.  通过执行以下步骤添加对缓存程序集的引用：

    1.  在中**解决方案资源管理器**，右键单击项目的名称，然后单击**添加引用**。

    2.  选择 **.NET**选项卡上，选择`System.Runtime.Caching`，然后单击**确定**。

#### <a name="to-change-the-target-net-framework-in-a-visual-c-project"></a>若要更改 Visual C# 项目中的目标.NET Framework

1.  在中**解决方案资源管理器**，右键单击项目名称，然后单击**属性**。

     显示应用程序的属性窗口。

2.  单击“应用程序”  选项卡。

3.  在中**目标框架**列表中，选择[!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)]。 (不要选择 **.NET Framework 4 Client Profile**。)

4.  通过执行以下步骤添加对缓存程序集的引用：

    1.  右键单击**引用**文件夹，然后单击**添加引用**。

    2.  选择 **.NET**选项卡上，选择`System.Runtime.Caching`，然后单击**确定**。

## <a name="adding-a-button-to-the-wpf-window"></a>将按钮添加到 WPF 窗口
 接下来，您将添加一个按钮控件，并创建为按钮的事件处理程序`Click`事件。 更高版本将添加代码，以便当单击按钮时，缓存并显示文本文件的内容。

#### <a name="to-add-a-button-control"></a>若要添加一个按钮控件

1.  在中**解决方案资源管理器**，双击 MainWindow.xaml 文件以将其打开。

2.  从**工具箱**下**常用 WPF 控件**，将`Button`控制对`MainWindow`窗口。

3.  在中**属性**窗口中，将`Content`的属性`Button`控制对**获取缓存**。

## <a name="initializing-the-cache-and-caching-an-entry"></a>正在初始化缓存和缓存条目
 接下来，将添加代码以执行以下任务：

-   创建缓存类的实例 — 也就是说，您将实例化一个新<xref:System.Runtime.Caching.MemoryCache>对象。

-   指定缓存使用<xref:System.Runtime.Caching.HostFileChangeMonitor>对象来监视在文本文件中的更改。

-   读取该文本文件并缓存其内容作为缓存项。

-   显示缓存的文本文件的内容。

#### <a name="to-create-the-cache-object"></a>若要创建缓存对象

1.  双击您只是为了在 MainWindow.xaml.cs 或 MainWindow.Xaml.vb 文件创建一个事件处理程序添加的按钮。

2.  （在类声明中） 的文件的顶部添加以下`Imports`(Visual Basic) 或`using`(C#) 语句：

    ```csharp
    using System.Runtime.Caching;
    using System.IO;
    ```

    ```vb
    Imports System.Runtime.Caching
    Imports System.IO
    ```

3.  事件处理程序中，添加以下代码以实例化的缓存对象：

    ```csharp
    ObjectCache cache = MemoryCache.Default;
    ```

    ```vb
    Dim cache As ObjectCache = MemoryCache.Default
    ```

     <xref:System.Runtime.Caching.ObjectCache>类是一个内置的类，提供内存中对象缓存。

4.  添加以下代码以读取内容的名为某个缓存项`filecontents`:

    ```vb
    Dim fileContents As String = TryCast(cache("filecontents"), String)
    ```

    ```csharp
    string fileContents = cache["filecontents"] as string;
    ```

5.  添加以下代码以检查是否为命名的缓存项`filecontents`存在：

    ```vb
    If fileContents Is Nothing Then

    End If
    ```

    ```csharp
    if (fileContents == null)
    {

    }
    ```

     如果指定的缓存条目不存在，必须读取该文本文件并将其作为某个缓存项添加到缓存。

6.  在中`if/then`块中，添加以下代码以创建一个新<xref:System.Runtime.Caching.CacheItemPolicy>对象，它指定缓存项将在 10 秒后过期。

    ```vb
    Dim policy As New CacheItemPolicy()
    policy.AbsoluteExpiration = DateTimeOffset.Now.AddSeconds(10.0)
    ```

    ```csharp
    CacheItemPolicy policy = new CacheItemPolicy();
    policy.AbsoluteExpiration = DateTimeOffset.Now.AddSeconds(10.0);
    ```

     如果未不提供任何逐出或过期的信息，默认值是<xref:System.Runtime.Caching.ObjectCache.InfiniteAbsoluteExpiration>，这意味着缓存项永远不会过期时间取决于只有一个绝对时间。 相反，缓存条目过期仅当内存压力时。 作为最佳做法，应始终显式提供绝对或可调到期。

7.  内部`if/then`阻止和上一步中添加的代码，添加以下代码以创建你想要监视，并将文本文件的路径添加到集合的文件路径的集合：

    ```vb
    Dim filePaths As New List(Of String)()
    filePaths.Add("c:\cache\cacheText.txt")
    ```

    ```csharp
    List<string> filePaths = new List<string>();
    filePaths.Add("c:\\cache\\cacheText.txt");
    ```

    > [!NOTE]
    >  如果不是你想要使用的文本文件`c:\cache\cacheText.txt`，指定的文本文件是你想要使用的路径。

8.  在上一步骤中，添加的代码后面添加以下代码以添加新<xref:System.Runtime.Caching.HostFileChangeMonitor>到更改的集合对象监视缓存项：

    ```vb
    policy.ChangeMonitors.Add(New HostFileChangeMonitor(filePaths))
    ```

    ```csharp
    policy.ChangeMonitors.Add(new HostFileChangeMonitor(filePaths));
    ```

     <xref:System.Runtime.Caching.HostFileChangeMonitor>对象可监视文本文件的路径并通知缓存，如果在发生更改。 在此示例中，如果文件的内容发生更改，将过期的缓存项。

9. 在上一步中添加该代码之后添加以下代码以读取文本文件的内容：

    ```vb
    fileContents = File.ReadAllText("c:\cache\cacheText.txt") & vbCrLf & DateTime.Now.ToString()
    ```

    ```csharp
    fileContents = File.ReadAllText("c:\\cache\\cacheText.txt") + "\n" + DateTime.Now;
    ```

     以便你将能够看到该缓存项过期时添加的日期和时间的时间戳。

10. 在上一步骤中，添加的代码后面添加以下代码以将该文件的内容插入到缓存对象作为<xref:System.Runtime.Caching.CacheItem>实例：

    ```vb
    cache.Set("filecontents", fileContents, policy)
    ```

    ```csharp
    cache.Set("filecontents", fileContents, policy);
    ```

     指定有关如何通过将传递逐出缓存项的信息<xref:System.Runtime.Caching.CacheItemPolicy>作为参数前面创建的对象。

11. 之后`if/then`块中，添加以下代码以在消息框中显示缓存的文件内容：

    ```vb
    MessageBox.Show(fileContents)
    ```

    ```csharp
    MessageBox.Show(fileContents);
    ```

12. 在中**构建**菜单上，单击**生成 WPFCaching**生成项目。

## <a name="testing-caching-in-the-wpf-application"></a>测试在缓存中的 WPF 应用程序
 现在可以测试应用程序。

#### <a name="to-test-caching-in-the-wpf-application"></a>若要测试的 WPF 应用程序中的缓存

1.  按 Ctrl+F5 运行应用程序。

     `MainWindow`显示窗口。

2.  单击**中获取缓存**。

     在消息框中显示文本文件中缓存的内容。 请注意，该文件上的时间戳。

3.  关闭消息框，然后单击**获取缓存**试。

     时间戳保持不变。 这将指示显示缓存的内容。

4.  等待 10 秒或更长，然后单击**获取缓存**试。

     此时将显示新时间戳。 这表示该策略允许缓存项过期，并且将显示新缓存的内容。

5.  在文本编辑器中，打开您创建的文本文件。 不进行任何更改。

6.  关闭消息框，然后单击**获取缓存**试。

     请再次注意时间戳。

7.  对文本文件进行更改，然后保存该文件。

8.  关闭消息框，然后单击**获取缓存**试。

     此消息框包含中的文本文件和新的时间戳的已更新的内容。 这指示主文件的更改监视器逐出缓存项后更改该文件，将立即即使绝对超时时间尚未过期。

    > [!NOTE]
    >  可以增加到 20 秒或更多用于允许更多时间，以便在文件中进行更改的逐出时间。

## <a name="code-example"></a>代码示例
 完成本演练后，你创建的项目的代码将类似于下面的示例。

 [!code-csharp[CachingWPFApplications#1](~/samples/snippets/csharp/VS_Snippets_Wpf/CachingWPFApplications/CSharp/MainWindow.xaml.cs#1)]
 [!code-vb[CachingWPFApplications#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CachingWPFApplications/VisualBasic/MainWindow.xaml.vb#1)]

## <a name="see-also"></a>请参阅

- <xref:System.Runtime.Caching.MemoryCache>
- <xref:System.Runtime.Caching.ObjectCache>
- <xref:System.Runtime.Caching>
- [在 .NET Framework 应用程序中缓存](../../performance/caching-in-net-framework-applications.md)
