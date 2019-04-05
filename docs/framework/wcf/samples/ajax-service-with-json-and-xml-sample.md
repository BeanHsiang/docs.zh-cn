---
title: 具有 JSON 和 XML 的 AJAX 服务示例
ms.date: 03/30/2017
ms.assetid: 8ea5860d-0c42-4ae9-941a-e07efdd8e29c
ms.openlocfilehash: f8e112a75d537927d7a099d2988c1219515e2c1a
ms.sourcegitcommit: 0069cb3de8eed4e92b2195d29e5769a76111acdd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/16/2019
ms.locfileid: "56332334"
---
# <a name="ajax-service-with-json-and-xml-sample"></a>具有 JSON 和 XML 的 AJAX 服务示例
此示例演示如何使用 Windows Communication Foundation (WCF) 创建异步 JavaScript 和 XML (AJAX) 服务返回 JavaScript 对象表示法 (JSON) 或 XML 数据。 可以从 Web 浏览器客户端使用 JavaScript 代码来访问 AJAX 服务。 此示例是基于[基本 AJAX 服务](../../../../docs/framework/wcf/samples/basic-ajax-service.md)示例。  
  
 与其他 AJAX 示例不同的是，此示例不使用 ASP.NET AJAX 和 <xref:System.Web.UI.ScriptManager> 控件。 使用某些其他配置时，WCF AJAX 服务可以从任何 HTML 页面通过 JavaScript，访问和此方案如下所示。 使用 ASP.NET AJAX 使用 WCF 的示例，请参阅[AJAX 示例](ajax.md)。
  
 此示例演示如何在 JSON 和 XML 之间切换操作的响应类型。 无论服务是配置为由 ASP.NET AJAX 访问还是由 HTML/JavaScript 客户端页面访问，此功能均可用。  
  
> [!NOTE]
> 本主题的最后介绍了此示例的设置过程和生成说明。
  
为了启用非 ASP.NET AJAX 客户端，请在 .svc 文件中使用 <xref:System.ServiceModel.Activation.WebServiceHostFactory>（而不是 <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory>）。 <xref:System.ServiceModel.Activation.WebServiceHostFactory> 将 <xref:System.ServiceModel.Description.WebHttpEndpoint> 标准终结点添加到服务中。 相对于.svc 文件中; 的空地址处配置的终结点这意味着该服务的地址是`http://localhost/ServiceModelSamples/service.svc`，除了操作名以外没有其他后缀。  
  
```svc
<%@ServiceHost language="c#" Debug="true" Service="Microsoft.Samples.XmlAjaxService.CalculatorService" Factory="System.ServiceModel.Activation.WebServiceHostFactory" %>  
```  
  
 可以使用 Web.config 中的以下节对终结点进行其他配置更改。 如果不需要额外更改，则可以移除该节。  
  
```xml  
<system.serviceModel>  
  <standardEndpoints>  
    <webHttpEndpoint>  
      <!-- Use this element to configure the endpoint -->  
      <standardEndpoint name="" />  
    </webHttpEndpoint>  
  </standardEndpoints>  
</system.serviceModel>  
```  
  
 默认数据格式<xref:System.ServiceModel.Description.WebHttpEndpoint>时的默认数据格式为 XML，<xref:System.ServiceModel.Description.WebScriptEndpoint>是 JSON。 有关详细信息，请参阅[不使用 ASP.NET 创建 WCF AJAX 服务](../../../../docs/framework/wcf/feature-details/creating-wcf-ajax-services-without-aspnet.md)。  
  
 下面的示例中的服务是具有两个操作的标准 WCF 服务。 这两个操作都需要针对 <xref:System.ServiceModel.Web.WebMessageBodyStyle.Wrapped> 或 <xref:System.ServiceModel.Web.WebGetAttribute> 属性使用 <xref:System.ServiceModel.Web.WebInvokeAttribute> 正文样式，该样式特定于 `webHttp` 行为，对于 JSON/XML 数据格式开关没有任何影响。  

```csharp
[OperationContract]  
[WebInvoke(ResponseFormat = WebMessageFormat.Xml, BodyStyle = WebMessageBodyStyle.Wrapped)]  
MathResult DoMathXml(double n1, double n2);  
```

 该操作的响应格式指定为 XML，这是默认值设置为[ \<webHttp >](../../../../docs/framework/configure-apps/file-schema/wcf/webhttp.md)行为。 但是，最好显式指定响应格式。  
  
 另一个操作使用 `WebInvokeAttribute` 属性并显式指定响应的 JSON（而不是 XML）。  

```csharp
[OperationContract]  
[WebInvoke(ResponseFormat = WebMessageFormat.Json, BodyStyle = WebMessageBodyStyle.Wrapped)]  
MathResult DoMathJson(double n1, double n2);  
```

 请注意，在这两种情况下操作返回复杂类型， `MathResult`，这是标准的 WCF 数据协定类型。  
  
 客户端网页 XmlAjaxClientPage.htm 包含 JavaScript 代码在用户单击时调用上述两个操作之一**执行计算 (返回 JSON)** 或**执行计算 (返回 XML)** 页上的按钮。 用来调用服务的代码将构造 JSON 正文并使用 HTTP POST 发送它。 该请求用 JavaScript 手动创建，与不同[基本 AJAX 服务](../../../../docs/framework/wcf/samples/basic-ajax-service.md)的示例，并使用 ASP.NET AJAX 的其他示例。  

```csharp
// Create HTTP request  
var xmlHttp;  
// Request instantiation code omitted…  
// Result handler code omitted…  
  
// Build the operation URL  
var url = "service.svc/ajaxEndpoint/";  
url = url + operation;  
  
// Build the body of the JSON message  
var body = '{"n1":';  
body = body + document.getElementById("num1").value + ',"n2":';  
body = body + document.getElementById("num2").value + '}';  
  
// Send the HTTP request  
xmlHttp.open("POST", url, true);  
xmlHttp.setRequestHeader("Content-type", "application/json");  
xmlHttp.send(body);  
```

 当服务进行响应时，响应将显示出来，而不会在页面上的文本框中进一步执行任何处理。 这是为了进行演示而实现的，您可以直接遵循所使用的 XML 和 JSON 数据格式。  

```javascript
// Create result handler   
xmlHttp.onreadystatechange=function(){  
     if(xmlHttp.readyState == 4){  
          document.getElementById("result").value = xmlHttp.responseText;  
     }  
}  
```

> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。 在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请转到[Windows Communication Foundation (WCF) 和.NET Framework 4 的 Windows Workflow Foundation (WF) 示例](https://go.microsoft.com/fwlink/?LinkId=150780)若要下载所有 Windows Communication Foundation (WCF) 和[!INCLUDE[wf1](../../../../includes/wf1-md.md)]示例。 此示例位于以下目录：  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\AJAX\XmlAjaxService`  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>设置、生成和运行示例  
  
1.  请确保您具有执行[的 Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2.  如中所述生成解决方案 XmlAjaxService.sln[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)。  
  
3.  导航到`http://localhost/ServiceModelSamples/XmlAjaxClientPage.htm`（不要打开 XmlAjaxClientPage.htm 在浏览器中从项目目录中）。  
  
## <a name="see-also"></a>请参阅
- [使用 HTTP POST 的 AJAX 服务](../../../../docs/framework/wcf/samples/ajax-service-using-http-post.md)
