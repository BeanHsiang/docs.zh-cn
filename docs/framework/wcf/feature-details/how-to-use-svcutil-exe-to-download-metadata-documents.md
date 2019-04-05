---
title: 如何：使用 Svcutil.exe 下载元数据文档
ms.date: 03/30/2017
ms.assetid: 15524274-3167-4627-b722-d6cedb9fa8c6
ms.openlocfilehash: dc3a1d402a9f6ffb69c1f692800698609f9fa84b
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54603269"
---
# <a name="how-to-use-svcutilexe-to-download-metadata-documents"></a>如何：使用 Svcutil.exe 下载元数据文档
您可以使用 Svcutil.exe 从正在运行的服务中下载元数据并将元数据保存到本地文件。 对于 HTTP 和 HTTPS URL 方案，Svcutil.exe 会尝试使用 Ws-metadataexchange 检索元数据和[XML Web 服务发现](https://go.microsoft.com/fwlink/?LinkId=94950)。 对于所有其他 URL 架构，Svcutil.exe 仅使用 WS-MetadataExchange。  
  
 默认情况下，Svcutil.exe 使用 <xref:System.ServiceModel.Description.MetadataExchangeBindings> 类中定义的绑定。 若要配置用于 WS-MetadataExchange 的绑定，必须在 Svcutil.exe 的配置文件 (svcutil.exe.config) 中定义一个客户端终结点，使该终结点使用 `IMetadataExchange` 约定，并具有与元数据终结点地址的统一资源标识符 (URI) 架构相同的名称。  
  
> [!CAUTION]
> 当运行 Svcutil.exe 以获取公开两个不同的服务的服务的元数据协定，每个包含具有相同名称的操作时，Svcutil.exe 将显示"无法获取元数据从..."的错误消息，例如，如果你具有公开名为服务协定的服务`ICarService`有一个操作`Get(Car c)`，并在同一个服务公开名为服务协定`IBookService`有一个操作`Get(Book b)`。 若要解决此问题，请执行下列操作之一：
>
> - 重命名其中的一项操作。
> - 将 <xref:System.ServiceModel.OperationContractAttribute.Name%2A> 设置为其他名称。
> - 使用 <xref:System.ServiceModel.ServiceContractAttribute.Namespace%2A> 属性将其中一项操作的命名空间设置为其他命名空间。
  
## <a name="to-download-metadata-using-svcutilexe"></a>使用 Svcutil.exe 下载元数据  
  
1.  在以下位置找到 Svcutil.exe 工具：  
  
     C:\Program Files\Microsoft SDKs\Windows\v1.0.\bin  
  
2.  在命令提示符处，使用下面的格式启动该工具。  
  
    ```  
    svcutil.exe /t:metadata  <url>* | <epr>  
    ```  
  
     您必须指定 `/t:metadata` 选项才能下载元数据。 否则，会生成客户端代码和配置。  
  
3.  <`url`> 参数指定到提供的元数据的服务终结点或联机承载的元数据文档的 URL。 <`epr`> 参数指定的 XML 文件包含与 Ws-addressing 路径`EndpointAddress`支持 Ws-metadataexchange 的服务终结点。  
  
 有关元数据下载并使用此工具的更多选项，请参阅[ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)。  
  
## <a name="example"></a>示例  
 下面的命令从正在运行的服务中下载元数据文档。  
  
```  
svcutil /t:metadata http://service/metadataEndpoint  
```  
  
## <a name="see-also"></a>请参阅
- [ServiceModel 元数据实用工具 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)
