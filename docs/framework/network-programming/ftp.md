---
title: FTP - .NET
ms.date: 03/30/2017
helpviewer_keywords:
- FTP
ms.assetid: 9b43f8b4-89d7-46a7-89fc-71aca916dd32
ms.openlocfilehash: d945f03077a863d9e1baa6b59fe8a908566aba5a
ms.sourcegitcommit: 90775b20343b6ad831af6f5380f8ab7553abb16b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2019
ms.locfileid: "54186145"
---
# <a name="ftp"></a>FTP

.NET Framework 通过 <xref:System.Net.FtpWebRequest> 和 <xref:System.Net.FtpWebResponse> 类为 FTP 协议提供全面支持。 这些类派生自 <xref:System.Net.WebRequest> 和 <xref:System.Net.WebResponse>。 大多数情况下，<xref:System.Net.WebRequest> 和 <xref:System.Net.WebResponse> 类提供发出请求所需的所有事项，但如果需要访问作为属性公开的 FTP 特定功能，可以将这两个类转换为 <xref:System.Net.FtpWebRequest> 或 <xref:System.Net.FtpWebResponse>。

## <a name="examples"></a>示例

有关详细信息，请参阅下列主题：[如何：使用 FTP 下载文件](how-to-download-files-with-ftp.md)，[如何：使用 FTP 上传文件](how-to-upload-files-with-ftp.md)和[如何：使用 FTP 列出目录内容](how-to-list-directory-contents-with-ftp.md)。

## <a name="ftp-and-proxies"></a>FTP 和代理

如果代理（由 <xref:System.Net.FtpWebRequest.Proxy%2A> 属性指定）为 HTTP 代理，则仅支持 <xref:System.Net.WebRequestMethods.Ftp.DownloadFile>、<xref:System.Net.WebRequestMethods.Ftp.ListDirectory> 和 <xref:System.Net.WebRequestMethods.Ftp.ListDirectoryDetails> 命令。

## <a name="see-also"></a>请参阅

- [通过代理访问 Internet](accessing-the-internet-through-a-proxy.md)
- [网络编程示例](network-programming-samples.md)
- [使用应用程序协议](using-application-protocols.md)
