---
title: 开始使用 Azure 文件存储使用F#
description: 使用 Azure 文件存储在云中存储文件数据和从 Azure 虚拟机 (VM) 装载云文件共享或从本地应用程序运行 Windows。
author: sylvanc
ms.date: 09/20/2016
ms.openlocfilehash: fa6dadc863bb9116cfac5afd7cd22a724bc7afe2
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56969591"
---
# <a name="get-started-with-azure-file-storage-using-f"></a>Azure 文件存储使用 F 入门\#

Azure 文件存储是一种服务，提供在云中使用标准文件共享[服务器消息块 (SMB) 协议](https://msdn.microsoft.com/library/windows/desktop/aa365233.aspx)。 支持 SMB 2.1 和 SMB 3.0。 使用 Azure 文件存储，你可以迁移依赖文件共享到 Azure，快速且无成本高昂的重写的旧版应用程序。 在 Azure 虚拟机或云服务或从本地客户端运行的应用程序可以装载文件共享在云中，就像桌面应用程序装载典型 SMB 共享一样。 任意数量的应用程序组件可以然后装载并同时访问文件存储共享。

有关文件存储的概念概述，请参阅[文件存储的.NET 指南](/azure/storage/storage-dotnet-how-to-use-files)。

## <a name="prerequisites"></a>系统必备

若要使用本指南，您必须首先[创建 Azure 存储帐户](/azure/storage/storage-create-storage-account)。
此外需要为此帐户存储访问密钥。

## <a name="create-an-f-script-and-start-f-interactive"></a>创建F#脚本并启动F#交互式

这篇文章中的示例可在F#应用程序或F#脚本。 若要创建F#脚本，创建的文件`.fsx`扩展，例如`files.fsx`，在你F#开发环境。

接下来，使用[程序包管理器](package-management.md)如[paket 依存](https://fsprojects.github.io/Paket/)或[NuGet](https://www.nuget.org/)安装`WindowsAzure.Storage`程序包和引用`WindowsAzure.Storage.dll`使用在脚本中`#r`指令。

### <a name="add-namespace-declarations"></a>添加命名空间声明

添加以下`open`顶部的语句`files.fsx`文件：

[!code-fsharp[FileStorage](../../../samples/snippets/fsharp/azure/file-storage.fsx#L1-L5)]

### <a name="get-your-connection-string"></a>获取连接字符串

对于本教程需要 Azure 存储连接字符串。 有关连接字符串的详细信息，请参阅[配置存储连接字符串](/azure/storage/storage-configure-connection-string)。

本教程中，将在脚本中，此类输入你的连接字符串：

[!code-fsharp[FileStorage](../../../samples/snippets/fsharp/azure/file-storage.fsx#L11-L11)]

但是，这是**不建议这样做**为实际项目。 你的存储帐户密钥是类似于你的存储帐户的根密码。 始终要小心保护存储帐户密钥。 避免将其分发给其他用户，硬编码，或将其保存在其他人可以访问的纯文本格式的文件。 您可以重新生成你使用 Azure 门户，如果你认为可能已泄露的密钥。

为实际的应用程序，维护存储连接字符串的最佳方法是在配置文件中。 若要从配置文件中提取的连接字符串，可以执行此操作：

[!code-fsharp[FileStorage](../../../samples/snippets/fsharp/azure/file-storage.fsx#L13-L15)]

使用 Azure 配置管理器是可选的。 此外可以使用诸如.NET Framework 的 API`ConfigurationManager`类型。

### <a name="parse-the-connection-string"></a>分析连接字符串

若要分析的连接字符串，请使用：

[!code-fsharp[FileStorage](../../../samples/snippets/fsharp/azure/file-storage.fsx#L21-L22)]

这将返回`CloudStorageAccount`。

### <a name="create-the-file-service-client"></a>创建文件服务客户端

`CloudFileClient`类型可让你以编程方式使用文件存储中存储的文件。 下面是创建服务客户端的一种方法：

[!code-fsharp[FileStorage](../../../samples/snippets/fsharp/azure/file-storage.fsx#L28-L28)]

现在已准备好编写代码，读取数据并将数据写入到文件存储。

## <a name="create-a-file-share"></a>创建文件共享

此示例演示如何创建文件共享，如果尚不存在：

[!code-fsharp[FileStorage](../../../samples/snippets/fsharp/azure/file-storage.fsx#L34-L35)]

## <a name="create-a-root-directory-and-a-subdirectory"></a>创建根目录和子目录

在此，您将获取的根目录，并获取根目录的子目录。 如果它们尚不存在，则创建两者。

[!code-fsharp[FileStorage](../../../samples/snippets/fsharp/azure/file-storage.fsx#L41-L43)]

## <a name="upload-text-as-a-file"></a>将文本作为一个文件上传

此示例演示如何将文本作为一个文件上传。

[!code-fsharp[FileStorage](../../../samples/snippets/fsharp/azure/file-storage.fsx#L49-L50)]

### <a name="download-a-file-to-a-local-copy-of-the-file"></a>将文件下载到文件的本地副本

此处您下载刚创建的文件将内容追加到本地文件。

[!code-fsharp[FileStorage](../../../samples/snippets/fsharp/azure/file-storage.fsx#L56-L56)]

### <a name="set-the-maximum-size-for-a-file-share"></a>设置文件共享的最大大小

以下示例演示如何检查共享当前使用情况以及如何设置共享的配额。 `FetchAttributes` 必须调用来填充的共享`Properties`，和`SetProperties`传播到 Azure 文件存储的本地更改。

[!code-fsharp[FileStorage](../../../samples/snippets/fsharp/azure/file-storage.fsx#L62-L72)]

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a>生成共享的访问签名的文件或文件共享

可以生成共享的访问签名 (SAS) 文件共享或单个文件。 此外可以用于管理共享的访问签名的文件共享上创建共享的访问策略。 创建共享的访问策略建议，因为它提供了它在受到威胁时撤消 SAS 的一种方式。

在这里，创建共享访问策略在共享上，并将该策略以便提供对共享中文件的 SAS 的约束。

[!code-fsharp[FileStorage](../../../samples/snippets/fsharp/azure/file-storage.fsx#L78-L94)]

有关创建和使用共享的访问签名的详细信息，请参阅[使用共享访问签名 (SAS)](/azure/storage/storage-dotnet-shared-access-signature-part-1)并[创建并将 SAS 用于 Blob 存储](/azure/storage/storage-dotnet-shared-access-signature-part-2)。

### <a name="copy-files"></a>将文件复制

您可以将文件复制到另一个文件或 blob 或将一个 blob 到文件。 如果要将 blob 复制到一个文件或某个文件到一个 blob，你*必须*使用共享的访问签名 (SAS) 进行身份验证的源对象，即使相同的存储帐户内进行复制。

### <a name="copy-a-file-to-another-file"></a>将文件复制到另一个文件

在这里，您将文件复制到同一共享中的另一个文件。 因为此复制操作在相同的存储帐户中的文件之间进行复制，可以使用共享密钥身份验证来执行复制。

[!code-fsharp[FileStorage](../../../samples/snippets/fsharp/azure/file-storage.fsx#L100-L101)]

### <a name="copy-a-file-to-a-blob"></a>将文件复制到 blob

在这里，创建一个文件并将其复制到同一存储帐户内的 blob。 创建源文件，该服务用于在复制操作期间验证源文件的访问权限的 SAS。

[!code-fsharp[FileStorage](../../../samples/snippets/fsharp/azure/file-storage.fsx#L107-L120)]

相同的方式，可以将 blob 复制到一个文件。 如果源对象是一个 blob，然后创建一个 SAS 以复制操作期间对该 blob 的访问进行身份验证。

## <a name="troubleshooting-file-storage-using-metrics"></a>故障排除的文件存储使用指标

Azure 存储分析针对文件存储支持的指标。 使用指标数据，可以跟踪请求和诊断问题。

可以启用对从文件存储的指标[Azure 门户](https://portal.azure.com)，也可以从F#如下所示：

[!code-fsharp[FileStorage](../../../samples/snippets/fsharp/azure/file-storage.fsx#L126-L140)]

## <a name="next-steps"></a>后续步骤

请参阅以下链接详细了解 Azure 文件存储。

### <a name="conceptual-articles-and-videos"></a>概念性文章和视频

- [Azure 文件存储： 顺畅的云 SMB 文件系统适用于 Windows 和 Linux](https://azure.microsoft.com/resources/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
- [如何通过 Linux 使用 Azure 文件存储](/azure/storage/storage-how-to-use-files-linux)

### <a name="tooling-support-for-file-storage"></a>文件存储的工具支持

- [对 Azure 存储使用 Azure PowerShell](/azure/storage/storage-powershell-guide-full)
- [如何使用 Microsoft Azure 存储 AzCopy](/azure/storage/storage-use-azcopy)
- [使用 Azure CLI 与 Azure 存储](/azure/storage/storage-azure-cli#create-and-manage-file-shares)

### <a name="reference"></a>参考

- [存储客户端库.NET 参考](https://msdn.microsoft.com/library/azure/mt347887.aspx)
- [文件服务 REST API 参考](/rest/api/storageservices/fileservices/File-Service-REST-API)

### <a name="blog-posts"></a>博客文章

- [Azure 文件存储现已公开发布](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
- [Azure 文件存储内部](https://azure.microsoft.com/blog/inside-azure-file-storage/) 
- [Microsoft Azure 文件服务简介](https://blogs.msdn.microsoft.com/windowsazurestorage/2014/05/12/introducing-microsoft-azure-file-service/)
- [将连接保存到 Microsoft Azure 文件](https://blogs.msdn.microsoft.com/windowsazurestorage/2014/05/26/persisting-connections-to-microsoft-azure-files/)
