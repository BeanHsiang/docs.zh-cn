---
title: 开始使用 Azure Blob 存储使用F#
description: 使用 Azure Blob 存储在云中存储非结构化的数据。
author: sylvanc
ms.date: 09/20/2016
ms.openlocfilehash: 62178edf22ad48d0388f34488b68d135068d50a2
ms.sourcegitcommit: 69bf8b719d4c289eec7b45336d0b933dd7927841
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/14/2019
ms.locfileid: "57846423"
---
# <a name="get-started-with-azure-blob-storage-using-f"></a>开始使用 Azure Blob 存储中使用 F\#

Azure Blob 存储是将非结构化数据作为对象/blob 存储在云中的服务。 Blob 存储可以存储任何类型的文本或二进制数据（如文档、媒体文件或应用程序安装程序）。 Blob 存储也称为对象存储。

本文介绍如何使用 Blob 存储执行常见任务。 相关示例是使用F#使用用于.NET 的 Azure 存储客户端库。 涉及的任务包括如何上传、 列出、 下载和删除 blob。

有关 blob 存储的概念概述，请参阅[适用于 blob 存储的.NET 指南](/azure/storage/storage-dotnet-how-to-use-blobs)。

## <a name="prerequisites"></a>系统必备

若要使用本指南，您必须首先[创建 Azure 存储帐户](/azure/storage/storage-create-storage-account)。 为此帐户还需要存储访问密钥。

## <a name="create-an-f-script-and-start-f-interactive"></a>创建F#脚本并启动F#交互式

这篇文章中的示例可在F#应用程序或F#脚本。 若要创建F#脚本，创建的文件`.fsx`扩展，例如`blobs.fsx`，在你F#开发环境。

接下来，使用[程序包管理器](package-management.md)如[paket 依存](https://fsprojects.github.io/Paket/)或[NuGet](https://www.nuget.org/)安装`WindowsAzure.Storage`并`Microsoft.WindowsAzure.ConfigurationManager`包和引用`WindowsAzure.Storage.dll`和`Microsoft.WindowsAzure.Configuration.dll`脚本使用`#r`指令。

### <a name="add-namespace-declarations"></a>添加命名空间声明

添加以下`open`顶部的语句`blobs.fsx`文件：

[!code-fsharp[BlobStorage](../../../samples/snippets/fsharp/azure/blob-storage.fsx#L1-L5)]

### <a name="get-your-connection-string"></a>获取连接字符串

对于本教程需要 Azure 存储连接字符串。 有关连接字符串的详细信息，请参阅[配置存储连接字符串](/azure/storage/storage-configure-connection-string)。

本教程中，在脚本中，此类输入连接字符串：

[!code-fsharp[BlobStorage](../../../samples/snippets/fsharp/azure/blob-storage.fsx#L11-L11)]

但是，这是**不建议这样做**为实际项目。 你的存储帐户密钥是类似于你的存储帐户的根密码。 始终要小心保护存储帐户密钥。 避免将其分发给其他用户，硬编码，或将其保存在其他人可以访问的纯文本格式的文件。 您可以重新生成你使用 Azure 门户，如果你认为可能已泄露的密钥。

为实际的应用程序，维护存储连接字符串的最佳方法是在配置文件中。 若要从配置文件中提取的连接字符串，可以执行此操作：

[!code-fsharp[BlobStorage](../../../samples/snippets/fsharp/azure/blob-storage.fsx#L13-L15)]

使用 Azure 配置管理器是可选的。 此外可以使用诸如.NET Framework 的 API`ConfigurationManager`类型。

### <a name="parse-the-connection-string"></a>分析连接字符串

若要分析的连接字符串，请使用：

[!code-fsharp[BlobStorage](../../../samples/snippets/fsharp/azure/blob-storage.fsx#L21-L22)]

这将返回`CloudStorageAccount`。

### <a name="create-some-local-dummy-data"></a>创建一些本地虚拟数据

在开始之前，请在我们的脚本的目录中创建一些虚拟的本地数据。 稍后您将此数据上传。

[!code-fsharp[BlobStorage](../../../samples/snippets/fsharp/azure/blob-storage.fsx#L28-L30)]

### <a name="create-the-blob-service-client"></a>创建 Blob 服务客户端

`CloudBlobClient`类型使你能够检索存储在 Blob 存储中容器和 blob。 下面是创建服务客户端的一种方法：

[!code-fsharp[BlobStorage](../../../samples/snippets/fsharp/azure/blob-storage.fsx#L36-L36)]

现在已准备好编写代码，读取数据并将数据写入到 Blob 存储。

## <a name="create-a-container"></a>创建容器

此示例演示如何创建一个容器，如果尚不存在：

[!code-fsharp[BlobStorage](../../../samples/snippets/fsharp/azure/blob-storage.fsx#L42-L46)]

默认情况下，新容器是私有的这意味着，必须指定存储访问密钥才能从该容器下载 blob。 如果你想要让容器中的文件可供所有人，你可以将容器设置为公共使用以下代码：

[!code-fsharp[BlobStorage](../../../samples/snippets/fsharp/azure/blob-storage.fsx#L48-L49)]

在 Internet 上的任何人都可以看到公共容器中的 blob，但您可以修改或删除它们仅在具有相应的帐户访问密钥或共享的访问签名。

## <a name="upload-a-blob-into-a-container"></a>一个 blob 上传到容器

Azure Blob 存储支持块 blob 和页 blob。 在大多数情况下，块 blob 是要使用的建议的类型。

若要将文件上载到块 blob，获取容器引用，并使用它获取块 blob 引用。 Blob 引用后，您可以将任何数据流上载的数据到它通过调用`UploadFromFile`方法。 如果以前不存在，或者覆盖它，如果存在，此操作将创建 blob。

[!code-fsharp[BlobStorage](../../../samples/snippets/fsharp/azure/blob-storage.fsx#L55-L59)]

## <a name="list-the-blobs-in-a-container"></a>列出容器中的 blob

若要列出容器中的 blob，首先获取容器引用。 然后，可以使用容器的`ListBlobs`方法来检索其中的 blob 和/或目录。 若要访问的属性和方法返回丰富`IListBlobItem`，你必须将其转换为`CloudBlockBlob`， `CloudPageBlob`，或`CloudBlobDirectory`对象。 如果类型未知，可以使用类型检查来确定要将其转换为。 下面的代码演示如何检索和输出中的每个项的 URI`mydata`容器：

[!code-fsharp[BlobStorage](../../../samples/snippets/fsharp/azure/blob-storage.fsx#L67-L80)]

您还可以包含在其名称中的路径信息的名称 blob。 这将创建一个虚拟目录结构，您可以组织和遍历像传统文件系统一样。 请注意，目录结构仅仅是虚拟-可在 Blob 存储的唯一资源是容器和 blob。 但是，存储客户端库提供`CloudBlobDirectory`对象来引用虚拟目录，并简化过程的这种方式组织的 blob 的使用。

例如，考虑名为的容器的块 blob 的下面一`photos`:

*photo1.jpg*\
*2015/architecture/description.txt*\
*2015/architecture/photo3.jpg*\
*2015/architecture/photo4.jpg*\
*2016/architecture/photo5.jpg*\
*2016/architecture/photo6.jpg*\
*2016/architecture/description.txt*\
*2016/photo7.jpg*\

当您调用`ListBlobs`上 （如上面的示例中） 的容器，将返回一个层次结构列表。 如果它同时包含`CloudBlobDirectory`和`CloudBlockBlob`对象，分别表示目录和 blob 容器中的，则生成的输出显示类似于下面：

```console
Directory: https://<accountname>.blob.core.windows.net/photos/2015/
Directory: https://<accountname>.blob.core.windows.net/photos/2016/
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

或者，可以设置`UseFlatBlobListing`的参数`ListBlobs`方法`true`。 在这种情况下，每个 blob 容器中的返回作为`CloudBlockBlob`对象。 对调用`ListBlobs`返回一个平面列表如下所示：

[!code-fsharp[BlobStorage](../../../samples/snippets/fsharp/azure/blob-storage.fsx#L82-L89)]

而且，具体取决于你的容器的当前内容，结果如下所示：

```console
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2015/architecture/description.txt
Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2015/architecture/photo3.jpg
Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2015/architecture/photo4.jpg
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2016/architecture/description.txt
Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2016/architecture/photo5.jpg
Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2016/architecture/photo6.jpg
Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2016/photo7.jpg
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

## <a name="download-blobs"></a>下载 blob

若要下载 blob，首先检索 blob 引用，然后调用`DownloadToStream`方法。 下面的示例使用`DownloadToStream`方法将 blob 内容传输到稍后可以保存到本地文件的流对象。

[!code-fsharp[BlobStorage](../../../samples/snippets/fsharp/azure/blob-storage.fsx#L95-L101)]

此外可以使用`DownloadToStream`方法下载文本字符串形式将 blob 的内容。

[!code-fsharp[BlobStorage](../../../samples/snippets/fsharp/azure/blob-storage.fsx#L103-L106)]

## <a name="delete-blobs"></a>删除 blob

若要删除 blob，首先请获取 blob 引用，然后调用`Delete`方法。

[!code-fsharp[BlobStorage](../../../samples/snippets/fsharp/azure/blob-storage.fsx#L112-L116)]

## <a name="list-blobs-in-pages-asynchronously"></a>以异步方式列出页中的 blob

如果要列出大量 blob，或者你想要控制在一个列表操作返回的结果数，可以列出页结果中的 blob。 此示例演示如何在页中以异步方式返回结果，以便等待返回大量结果时不阻止执行。

此示例演示平面 blob 列表，但还可以执行分层列表中，通过设置`useFlatBlobListing`的参数`ListBlobsSegmentedAsync`方法`false`。

此示例定义一个异步方法，使用`async`块。 ``let!``关键字将挂起示例方法的执行，直至列表任务完成。

[!code-fsharp[BlobStorage](../../../samples/snippets/fsharp/azure/blob-storage.fsx#L122-L160)]

我们现在可以使用此异步例程，如下所示。 首先您将上传一些虚拟数据 （使用在本教程前面创建的本地文件）。

[!code-fsharp[BlobStorage](../../../samples/snippets/fsharp/azure/blob-storage.fsx#L162-L166)]

现在，调用该例程。 您使用`Async.RunSynchronously`以强制执行异步操作。

[!code-fsharp[BlobStorage](../../../samples/snippets/fsharp/azure/blob-storage.fsx#L168-L168)]

## <a name="writing-to-an-append-blob"></a>写入追加 blob

追加 blob 针对追加操作，例如日志记录优化。 块 blob，相似的追加 blob 块组成，但当将新的块添加到追加 blob，始终追加到 blob 的末尾。 无法更新或删除追加 blob 中的现有块。 追加 blob 的块 Id 不公开，因为它们是用于块 blob。

追加 blob 中的每个块可以是不同的大小，最大为 4 MB，并追加 blob 可以包含 50,000 个块的最大值。 因此，追加 blob 的最大大小是稍微大于 195 GB （4 MB X 50,000 块）。

以下示例创建新的追加 blob，并将一些数据追加到其中，模拟一个简单的日志记录操作。

[!code-fsharp[BlobStorage](../../../samples/snippets/fsharp/azure/blob-storage.fsx#L174-L203)]

请参阅[了解块 Blob、 页 Blob 和追加 Blob](https://msdn.microsoft.com/library/azure/ee691964.aspx)有关三种 blob 之间的差异的详细信息。

## <a name="concurrent-access"></a>并发访问

若要允许从多个客户端或多个进程实例并发访问到某一 blob，可以使用**Etag**或**租约**。

* **Etag** -提供用于检测 blob 或容器已被另一个进程修改

* **租约**-提供了一种方法来获取独占式可续订写入或删除的一段时间内对 blob 的访问

有关详细信息，请参阅[在 Microsoft Azure 存储管理并发](https://azure.microsoft.com/blog/managing-concurrency-in-microsoft-azure-storage-2/)。

## <a name="naming-containers"></a>命名容器

在 Azure 存储中的每个 blob 必须驻留在一个容器。 该容器构成 blob 名称的一部分。 例如，`mydata`是这些示例 blob Uri 中的容器的名称：

    https://storagesample.blob.core.windows.net/mydata/blob1.txt
    https://storagesample.blob.core.windows.net/mydata/photos/myphoto.jpg

容器名称必须是有效的 DNS 名称，符合以下命名规则：

1. 容器名称必须以字母或数字开头，并且可以包含字母、 数字和短划线 （-） 字符。
1. 必须立即前面和后面以字母或数字; 每个短划线 （-） 字符容器名称中不允许使用连续划线。
1. 容器名称中的所有字母都必须小写。
1. 容器名称必须介于 3 到 63 个字符。

请注意，容器的名称必须始终为小写。 如果在容器名称，包括大写字母或其他方式违反了容器命名规则，可能会收到 400 错误 （错误请求）。

## <a name="managing-security-for-blobs"></a>管理 blob 安全性

默认情况下，Azure 存储器随时满足你的数据安全通过限制对帐户所有者，拥有帐户访问密钥访问。 当需要共享存储帐户中的 blob 数据时，务必为此，不会影响你的帐户访问密钥的安全性。 此外，可以加密 blob 数据，以确保其安全会在网络传输和 Azure 存储中。

### <a name="controlling-access-to-blob-data"></a>控制对 blob 数据的访问权限

默认情况下，你的存储帐户中的 blob 数据是仅供存储帐户所有者访问。 默认情况下，针对 Blob 存储的请求进行身份验证需要帐户访问密钥。 但是，你可能想要向其他用户提供特定的 blob 数据。

### <a name="encrypting-blob-data"></a>加密 blob 数据

Azure 存储支持加密 blob 数据在客户端和服务器上。

## <a name="next-steps"></a>后续步骤

现在，你已了解 Blob 存储的基础知识，单击以下链接了解详细信息。

### <a name="tools"></a>工具

- [F# AzureStorageTypeProvider](https://fsprojects.github.io/AzureStorageTypeProvider/)\
F#类型提供程序可用于浏览 Blob、 表和队列的 Azure 存储资产并轻松地将应用对它们的 CRUD 操作。

- [FSharp.Azure.Storage](https://github.com/fsprojects/FSharp.Azure.Storage)\
F#使用 Microsoft Azure 表存储服务 API

- [Microsoft Azure 存储资源管理器 (MASE)](/azure/vs-azure-tools-storage-manage-with-storage-explorer)\
使您能够以可视方式处理 Azure 存储的数据在 Windows、 OS X 和 Linux 上的 microsoft 免费提供的独立应用。

### <a name="blob-storage-reference"></a>Blob 存储参考

- [用于.NET 的 azure 存储 Api](/dotnet/api/overview/azure/storage)
- [Azure 存储服务 REST API 参考](/rest/api/storageservices/Azure-Storage-Services-REST-API-Reference)

### <a name="related-guides"></a>相关的指南

- [使用 C# 中的 Azure Blob 存储入门](https://azure.microsoft.com/resources/samples/storage-blob-dotnet-getting-started/)
- [使用 AzCopy 命令行实用工具 on Windows 传输数据](/azure/storage/common/storage-use-azcopy)
- [使用 AzCopy 命令行实用工具 on Linux 传输数据](/azure/storage/common/storage-use-azcopy-linux)
- [配置 Azure 存储连接字符串](/azure/storage/common/storage-configure-connection-string)
- [Azure 存储团队博客](https://blogs.msdn.microsoft.com/windowsazurestorage/)
- [快速入门：使用.NET 在对象存储中创建 blob](/azure/storage/blobs/storage-quickstart-blobs-dotnet)
