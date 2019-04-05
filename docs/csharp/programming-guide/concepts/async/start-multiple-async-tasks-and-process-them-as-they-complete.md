---
title: 在异步任务完成时对其进行处理
ms.date: 09/12/2018
ms.assetid: 25331850-35a7-43b3-ab76-3908e4346b9d
ms.openlocfilehash: ec5729eaa8d63eb18b1ac4dea5820cbf834d001b
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53152353"
---
# <a name="start-multiple-async-tasks-and-process-them-as-they-complete-c"></a>启动多个异步任务并在其完成时进行处理 (C#)

通过使用 <xref:System.Threading.Tasks.Task.WhenAny%2A?displayProperty=nameWithType>，可以同时启动多个任务，并在它们完成时逐个对它们进行处理，而不是按照它们的启动顺序进行处理。

下面的示例使用查询来创建一组任务。 每个任务都下载指定网站的内容。 在对 while 循环的每次迭代中，对 `WhenAny` 的等待调用返回任务集合中首先完成下载的任务。 此任务从集合中删除并进行处理。 循环重复进行，直到集合中不包含任何任务。

> [!NOTE]
> 若要运行示例，计算机上必须安装有 Visual Studio（2012 或更高版本）和 .NET Framework 4.5 或更高版本。

## <a name="download-an-example-solution"></a>下载示例解决方案

若要下载完整的 Windows Presentation Foundation (WPF) 项目，请参阅 [Async Sample: Fine Tuning Your Application](https://code.msdn.microsoft.com/Async-Fine-Tuning-Your-a676abea)（异步示例：微调应用程序），然后遵循以下步骤。

> [!TIP]
> 如果不想下载项目，可在本主题末尾处查看 MainWindow.xaml.cs 文件。

1.  从 .zip 文件中提取已下载的文件，然后启动 Visual Studio。

2.  在菜单栏上，依次选择“文件” > “打开” > “项目/解决方案”。

3.  在“打开项目”对话框中，打开保存已下载的示例代码的文件夹，然后打开 AsyncFineTuningCS 的解决方案 (.sln) 文件。

4.  在“解决方案资源管理器”中，打开“ProcessTasksAsTheyFinish”项目的快捷菜单，选择“设为启动项目”。

5.  选择 F5 键以运行此程序（或按 Ctrl+F5 键以运行此程序，而不对其进行调试）。

6.  多次运行此项目以验证并不总是以相同顺序显示已下载的长度。

## <a name="create-the-program-yourself"></a>自行创建程序

本示例对[在一个任务完成后取消剩余异步任务 (C#)](../../../../csharp/programming-guide/concepts/async/cancel-remaining-async-tasks-after-one-is-complete.md) 中开发的代码进行了补充，并使用了相同的 UI。

若要自行生成示例，请按[下载示例](../../../../csharp/programming-guide/concepts/async/cancel-remaining-async-tasks-after-one-is-complete.md#downloading-the-example)部分的说明逐步操作，但将“CancelAfterOneTask”设置为“启动项目”。 将此主题中的更改添加到项目中的 `AccessTheWebAsync` 方法。 这些更改标有星号。

**CancelAfterOneTask** 项目已包含一个查询，执行此查询时，将创建任务集合。 每次对以下代码中的 `ProcessURLAsync` 进行调用都会返回 <xref:System.Threading.Tasks.Task%601>，其中 `TResult` 是一个整数：

```csharp
IEnumerable<Task<int>> downloadTasksQuery = from url in urlList select ProcessURL(url, client, ct);
```

在项目的 MainWindow.xaml.cs 文件中，对 `AccessTheWebAsync` 方法进行以下更改。

-   通过应用 <xref:System.Linq.Enumerable.ToList%2A?displayProperty=nameWithType> 而非 <xref:System.Linq.Enumerable.ToArray%2A> 执行查询。

    ```csharp
    List<Task<int>> downloadTasks = downloadTasksQuery.ToList();
    ```

-   添加 `while` 循环，针对集合中的每个任务执行以下步骤：

    1.  等待调用 `WhenAny`，以标识集合中首个完成下载的任务。

        ```csharp
        Task<int> firstFinishedTask = await Task.WhenAny(downloadTasks);
        ```

    2.  从集合中移除任务。

        ```csharp
        downloadTasks.Remove(firstFinishedTask);
        ```

    3.  等待 `firstFinishedTask`，由对 `ProcessURLAsync` 的调用返回。 `firstFinishedTask` 变量是 <xref:System.Threading.Tasks.Task%601>，其中 `TReturn` 是整数。 任务已完成，但需等待它检索已下载网站的长度，如以下示例所示。

        ```csharp
        int length = await firstFinishedTask;
        resultsTextBox.Text += $"\r\nLength of the download:  {length}";
        ```

多次运行此程序以验证并不总是以相同顺序显示已下载的长度。

> [!CAUTION]
> 如示例所示，可以在循环中使用 `WhenAny` 来解决涉及少量任务的问题。 但是，如果要处理大量任务，可以采用其他更高效的方法。 有关详细信息和示例，请参阅 [Processing tasks as they complete](https://blogs.msdn.microsoft.com/pfxteam/2012/08/02/processing-tasks-as-they-complete/)（在任务完成时处理它们）。

## <a name="complete-example"></a>完整示例

下列代码是示例的 MainWindow.xaml.cs 文件的完整文本。 对添加到此示例的元素进行了星号标记。 另请注意，必须为 <xref:System.Net.Http> 添加引用。

可以从 [Async Sample: Fine Tuning Your Application](https://code.msdn.microsoft.com/Async-Fine-Tuning-Your-a676abea)（异步示例：微调应用程序）下载这些项目。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;

// Add a using directive and a reference for System.Net.Http.
using System.Net.Http;

// Add the following using directive.
using System.Threading;

namespace ProcessTasksAsTheyFinish
{
    public partial class MainWindow : Window
    {
        // Declare a System.Threading.CancellationTokenSource.
        CancellationTokenSource cts;

        public MainWindow()
        {
            InitializeComponent();
        }

        private async void startButton_Click(object sender, RoutedEventArgs e)
        {
            resultsTextBox.Clear();

            // Instantiate the CancellationTokenSource.
            cts = new CancellationTokenSource();

            try
            {
                await AccessTheWebAsync(cts.Token);
                resultsTextBox.Text += "\r\nDownloads complete.";
            }
            catch (OperationCanceledException)
            {
                resultsTextBox.Text += "\r\nDownloads canceled.\r\n";
            }
            catch (Exception)
            {
                resultsTextBox.Text += "\r\nDownloads failed.\r\n";
            }

            cts = null;
        }

        private void cancelButton_Click(object sender, RoutedEventArgs e)
        {
            if (cts != null)
            {
                cts.Cancel();
            }
        }

        async Task AccessTheWebAsync(CancellationToken ct)
        {
            HttpClient client = new HttpClient();

            // Make a list of web addresses.
            List<string> urlList = SetUpURLList();

            // ***Create a query that, when executed, returns a collection of tasks.
            IEnumerable<Task<int>> downloadTasksQuery =
                from url in urlList select ProcessURL(url, client, ct);

            // ***Use ToList to execute the query and start the tasks.
            List<Task<int>> downloadTasks = downloadTasksQuery.ToList();

            // ***Add a loop to process the tasks one at a time until none remain.
            while (downloadTasks.Count > 0)
            {
                    // Identify the first task that completes.
                    Task<int> firstFinishedTask = await Task.WhenAny(downloadTasks);

                    // ***Remove the selected task from the list so that you don't
                    // process it more than once.
                    downloadTasks.Remove(firstFinishedTask);

                    // Await the completed task.
                    int length = await firstFinishedTask;
                    resultsTextBox.Text += $"\r\nLength of the download:  {length}";
            }
        }

        private List<string> SetUpURLList()
        {
            List<string> urls = new List<string>
            {
                "https://msdn.microsoft.com",
                "https://msdn.microsoft.com/library/windows/apps/br211380.aspx",
                "https://msdn.microsoft.com/library/hh290136.aspx",
                "https://msdn.microsoft.com/library/dd470362.aspx",
                "https://msdn.microsoft.com/library/aa578028.aspx",
                "https://msdn.microsoft.com/library/ms404677.aspx",
                "https://msdn.microsoft.com/library/ff730837.aspx"
            };
            return urls;
        }

        async Task<int> ProcessURL(string url, HttpClient client, CancellationToken ct)
        {
            // GetAsync returns a Task<HttpResponseMessage>.
            HttpResponseMessage response = await client.GetAsync(url, ct);

            // Retrieve the website contents from the HttpResponseMessage.
            byte[] urlContents = await response.Content.ReadAsByteArrayAsync();

            return urlContents.Length;
        }
    }
}

// Sample Output:

// Length of the download:  226093
// Length of the download:  412588
// Length of the download:  175490
// Length of the download:  204890
// Length of the download:  158855
// Length of the download:  145790
// Length of the download:  44908
// Downloads complete.
```

## <a name="see-also"></a>请参阅

- <xref:System.Threading.Tasks.Task.WhenAny%2A>
- [微调异步应用程序 (C#)](../../../../csharp/programming-guide/concepts/async/fine-tuning-your-async-application.md)
- [使用 Async 和 Await 的异步编程 (C#)](../../../../csharp/programming-guide/concepts/async/index.md)
- [异步示例：微调应用程序](https://code.msdn.microsoft.com/Async-Fine-Tuning-Your-a676abea)