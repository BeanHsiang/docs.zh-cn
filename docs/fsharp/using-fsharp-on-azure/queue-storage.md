---
title: 使用 Azure 队列存储入门F#
description: Azure 队列提供可靠、 异步消息传送应用程序组件之间。 云消息传送使应用程序组件可单独缩放。
author: sylvanc
ms.date: 09/20/2016
ms.openlocfilehash: 58a46dfe905a32be77a13d11df8f0544546ea0ed
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56974271"
---
# <a name="get-started-with-azure-queue-storage-using-f"></a>开始使用 Azure 队列存储中使用 F\#

Azure 队列存储提供了云应用程序组件之间的消息传送。 在设计时缩放的应用程序，应用程序组件通常被分离，以便它们可以独立缩放。 队列存储可实现异步消息传送应用程序组件之间的通信是否在云中、 在桌面上、 在本地服务器上，或在移动设备上运行。 队列存储还支持管理异步任务以及构建过程工作流。

### <a name="about-this-tutorial"></a>有关本教程

本教程演示如何编写F#使用 Azure 队列存储一些常见任务的代码。 涉及的任务包括创建和删除队列以及添加、 读取和删除队列消息。

有关队列存储的概念性概述，请参阅[队列存储.NET 指南](/azure/storage/storage-dotnet-how-to-use-queues)。

## <a name="prerequisites"></a>系统必备

若要使用本指南，您必须首先[创建 Azure 存储帐户](/azure/storage/storage-create-storage-account)。
此外需要为此帐户存储访问密钥。

## <a name="create-an-f-script-and-start-f-interactive"></a>创建F#脚本并启动F#交互式

这篇文章中的示例可在F#应用程序或F#脚本。 若要创建F#脚本，创建的文件`.fsx`扩展，例如`queues.fsx`，在你F#开发环境。

接下来，使用[程序包管理器](package-management.md)如[paket 依存](https://fsprojects.github.io/Paket/)或[NuGet](https://www.nuget.org/)安装`WindowsAzure.Storage`程序包和引用`WindowsAzure.Storage.dll`使用在脚本中`#r`指令。

### <a name="add-namespace-declarations"></a>添加命名空间声明

添加以下`open`顶部的语句`queues.fsx`文件：

[!code-fsharp[QueueStorage](../../../samples/snippets/fsharp/azure/queue-storage.fsx#L1-L3)]

### <a name="get-your-connection-string"></a>获取连接字符串

对于本教程需要 Azure 存储连接字符串。 有关连接字符串的详细信息，请参阅[配置存储连接字符串](/azure/storage/storage-configure-connection-string)。

本教程中，将在脚本中，此类输入你的连接字符串：

[!code-fsharp[QueueStorage](../../../samples/snippets/fsharp/azure/queue-storage.fsx#L9-L9)]

但是，这是**不建议这样做**为实际项目。 你的存储帐户密钥是类似于你的存储帐户的根密码。 始终要小心保护存储帐户密钥。 避免将其分发给其他用户，硬编码，或将其保存在其他人可以访问的纯文本格式的文件。 您可以重新生成你使用 Azure 门户，如果你认为可能已泄露的密钥。

为实际的应用程序，维护存储连接字符串的最佳方法是在配置文件中。 若要从配置文件中提取的连接字符串，可以执行此操作：

[!code-fsharp[QueueStorage](../../../samples/snippets/fsharp/azure/queue-storage.fsx#L11-L13)]

使用 Azure 配置管理器是可选的。 此外可以使用诸如.NET Framework 的 API`ConfigurationManager`类型。

### <a name="parse-the-connection-string"></a>分析连接字符串

若要分析的连接字符串，请使用：

[!code-fsharp[QueueStorage](../../../samples/snippets/fsharp/azure/queue-storage.fsx#L19-L20)]

这将返回`CloudStorageAccount`。

### <a name="create-the-queue-service-client"></a>创建队列服务客户端

`CloudQueueClient`类使您能够检索存储在队列中的队列存储。 下面是创建服务客户端的一种方法：

[!code-fsharp[QueueStorage](../../../samples/snippets/fsharp/azure/queue-storage.fsx#L26-L26)]

现在已准备好编写代码，读取数据并将数据写入到队列存储。

## <a name="create-a-queue"></a>创建队列

此示例演示如何创建队列，如果它尚不存在：

[!code-fsharp[QueueStorage](../../../samples/snippets/fsharp/azure/queue-storage.fsx#L32-L36)]

## <a name="insert-a-message-into-a-queue"></a>队列中插入一条消息

若要将消息插入现有队列，先创建一个新`CloudQueueMessage`。 接下来，调用`AddMessage`方法。 一个`CloudQueueMessage`可以创建从字符串 （utf-8 格式） 或`byte`数组，如下：

[!code-fsharp[QueueStorage](../../../samples/snippets/fsharp/azure/queue-storage.fsx#L42-L44)]

## <a name="peek-at-the-next-message"></a>扫视下一条消息

可以扫视队列前面的消息，但不从队列中移除它通过调用`PeekMessage`方法。

[!code-fsharp[QueueStorage](../../../samples/snippets/fsharp/azure/queue-storage.fsx#L50-L52)]

## <a name="get-the-next-message-for-processing"></a>获取下一条消息的处理

可以通过调用来检索消息的处理队列的前部`GetMessage`方法。

[!code-fsharp[QueueStorage](../../../samples/snippets/fsharp/azure/queue-storage.fsx#L58-L59)]

更高版本通过使用指示成功处理了消息的`DeleteMessage`。

## <a name="change-the-contents-of-a-queued-message"></a>更改已排队消息的内容

你可以检索的消息中现有的队列中的内容。 如果消息表示工作任务，可以使用此功能来更新该工作任务的状态。 以下代码使用新内容更新队列消息，并设置可见性超时延长 60 秒。 这会保存与消息关联的工作状态并为客户端提供了一分钟的时间来继续处理该消息。 可以使用此方法在队列消息中，跟踪多步骤工作流，而无需从头开始，如果一个处理步骤因硬件或软件故障而失败。 通常，你还可以保留重试计数，并且如果消息重试次数超过几次，则会将其删除。 这可避免每次处理它时将触发应用程序错误的消息。

[!code-fsharp[QueueStorage](../../../samples/snippets/fsharp/azure/queue-storage.fsx#L65-L69)]

## <a name="de-queue-the-next-message"></a>取消下一条消息的排队

你的代码来取消队列的消息从队列中两个步骤。 当您调用`GetMessage`，您将获得队列中下一条消息。 从返回的消息`GetMessage`变得对从此队列读取消息的任何其他代码不可见。 默认情况下，此消息将保持不可见 30 秒。 若要完成从队列中删除消息，还必须调用`DeleteMessage`。 删除消息的此两步过程可确保你的代码无法处理消息，因为硬件或软件故障，如果你的代码的另一个实例可以获取同一消息并重试。 你的代码调用`DeleteMessage`处理消息后。

[!code-fsharp[QueueStorage](../../../samples/snippets/fsharp/azure/queue-storage.fsx#L75-L76)]

## <a name="use-async-workflows-with-common-queue-storage-apis"></a>使用具有公用队列存储 Api 的异步工作流

此示例演示如何使用公用队列存储 Api 的异步工作流。

[!code-fsharp[QueueStorage](../../../samples/snippets/fsharp/azure/queue-storage.fsx#L82-L91)]

## <a name="additional-options-for-de-queuing-messages"></a>其他方法取消排队消息

有两种方法可以自定义队列中的消息检索。
首先，您可以获取一批消息 （最多 32)。 其次，您可以设置更长或更短的不可见超时，从而允许代码使用更多或更少的时间来彻底处理每条消息。 下面的代码示例使用`GetMessages`获取 20 中其中一个的消息调用，然后再处理每条消息。 它还设置为 5 分钟内为每个消息的不可见超时时间。 请注意，对于所有消息在 5 分钟内开始在同一时间，因此 5 分钟后传递自调用`GetMessages`，尚未删除的任何消息将再次变得可见。

[!code-fsharp[QueueStorage](../../../samples/snippets/fsharp/azure/queue-storage.fsx#L97-L99)]

## <a name="get-the-queue-length"></a>获取队列长度

您可以获得队列中的消息数的估计值。 `FetchAttributes`方法要求队列服务检索队列属性，包括消息计数。 `ApproximateMessageCount`属性返回检索到的最后一个值`FetchAttributes`方法，而不会调用队列服务。

[!code-fsharp[QueueStorage](../../../samples/snippets/fsharp/azure/queue-storage.fsx#L105-L106)]

## <a name="delete-a-queue"></a>删除队列

若要删除队列及其包含的所有消息，调用`Delete`对队列对象的方法。

[!code-fsharp[QueueStorage](../../../samples/snippets/fsharp/azure/queue-storage.fsx#L112-L113)]

## <a name="next-steps"></a>后续步骤

现在，你已了解队列存储的基础知识，单击下面的链接可了解更复杂的存储任务。

- [用于.NET 的 azure 存储 Api](/dotnet/api/overview/azure/storage)
- [Azure 存储类型提供程序](https://github.com/fsprojects/AzureStorageTypeProvider)
- [Azure 存储团队博客](https://blogs.msdn.microsoft.com/windowsazurestorage/)
- [配置 Azure 存储连接字符串](/azure/storage/common/storage-configure-connection-string)
- [Azure 存储服务 REST API 参考](/rest/api/storageservices/Azure-Storage-Services-REST-API-Reference)
