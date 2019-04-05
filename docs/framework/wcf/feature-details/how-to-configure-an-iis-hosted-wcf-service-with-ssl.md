---
title: 如何：使用 SSL 配置承载 IIS 的 WCF 服务
ms.date: 03/30/2017
ms.assetid: df2fe31f-a4bb-4024-92ca-b74ba055e038
ms.openlocfilehash: ca7343f14215d89b29636776437f5e4a6a8089a1
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54639973"
---
# <a name="how-to-configure-an-iis-hosted-wcf-service-with-ssl"></a>如何：使用 SSL 配置承载 IIS 的 WCF 服务
本主题介绍如何设置 IIS 承载的 WCF 服务以使用 HTTP 传输安全性。 HTTP 传输安全性要求 SSL 证书以便向 IIS 注册。 如果您没有 SSL 证书，则可以使用 IIS 生成测试证书。 接下来，您必须将一个 SSL 绑定添加到网站，并且配置该网站的身份验证属性。 最后，您需要配置 WCF 服务以使用 HTTPS。  
  
### <a name="creating-a-self-signed-certificate"></a>创建自签名证书  
  
1.  打开 Internet 信息服务管理器 (inetmgr.exe)，在左侧树视图中选择您的计算机名称。 在屏幕的右侧选择“服务器证书”  
  
     ![IIS 管理器主屏幕](../../../../docs/framework/wcf/feature-details/media/mg-inetmgrhome.jpg "mg_INetMgrHome")  
  
2.  在服务器证书窗口中单击**创建自签名证书...** 链接。  
  
     ![创建自&#45;签名的证书与 IIS](../../../../docs/framework/wcf/feature-details/media/mg-createselfsignedcert.jpg "mg_CreateSelfSignedCert")  
  
3.  输入的自签名证书的友好名称，然后单击**确定**。  
  
     ![创建自我&#45;签名证书对话框](../../../../docs/framework/wcf/feature-details/media/mg-mycert.jpg "mg_MyCert")  
  
     新创建的自签名的证书的详细信息现在可显示**服务器证书**窗口。  
  
     ![服务器证书窗口](../../../../docs/framework/wcf/feature-details/media/mg-servercertificatewindow.jpg "mg_ServerCertificateWindow")  
  
     生成的证书将安装在“受信任的根证书颁发机构”存储区中。  
  
### <a name="add-ssl-binding"></a>添加 SSL 绑定  
  
1.  仍在 Internet 信息服务管理器中，展开**站点**文件夹，然后**Default Web Site**屏幕左侧树视图中的文件夹。  
  
2.  单击**绑定...** 中的链接**操作**窗口的右上部分中的部分。  
  
     ![添加 SSL 绑定](../../../../docs/framework/wcf/feature-details/media/mg-addsslbinding.jpg "mg_AddSSLBinding")  
  
3.  在网站绑定窗口中单击**添加**按钮。  
  
     ![站点绑定对话框中](../../../../docs/framework/wcf/feature-details/media/mg-sitebindingsdialog.jpg "mg_SiteBindingsDialog")  
  
4.  在中**添加网站绑定**对话框中，选择 https 的类型和您刚的自签名证书的友好名称创建。  
  
     ![站点绑定示例](../../../../docs/framework/wcf/feature-details/media/mg-mycertbinding.jpg "mg_MyCertBinding")  
  
### <a name="configure-virtual-directory-for-ssl"></a>配置 SSL 的虚拟目录  
  
1.  仍在 Internet 信息服务管理器中，选择包含您 WCF 安全服务的虚拟目录。  
  
2.  在窗口的中心窗格中，选择**SSL 设置**的 IIS 部分中。  
  
     ![虚拟目录的 SSL 设置](../../../../docs/framework/wcf/feature-details/media/mg-sslsettingsforvdir.jpg "mg_SSLSettingsForVDir")  
  
3.  在 SSL 设置窗格中，选择**要求 SSL**复选框，单击**应用**中的链接**操作**屏幕的右侧部分。  
  
     ![虚拟目录 SSL 设置](../../../../docs/framework/wcf/feature-details/media/mg-vdirsslsettings.JPG "mg_VDirSSLSettings")  
  
### <a name="configure-wcf-service-for-http-transport-security"></a>为 HTTP 传输安全配置 WCF 服务  
  
1.  在 WCF 服务的 web.config 中，配置 HTTP 绑定以便使用传输安全，如下面的 XML 中所示。  
  
    ```xml  
    <bindings>  
          <basicHttpBinding>  
            <binding name="secureHttpBinding">  
              <security mode="Transport">  
                <transport clientCredentialType="None"/>  
              </security>  
            </binding>  
          </basicHttpBinding>  
    </bindings>  
    ```  
  
2.  指定您的服务和服务终结点，如下面的 XML 中所示。  
  
    ```xml  
    <services>  
          <service name="MySecureWCFService.Service1">  
            <endpoint address=""  
                      binding="basicHttpBinding"  
                      bindingConfiguration="secureHttpBinding"  
                      contract="MySecureWCFService.IService1"/>  
  
            <endpoint address="mex"  
                      binding="mexHttpsBinding"  
                      contract="IMetadataExchange" />  
          </service>  
    </services>  
    ```  
  
## <a name="example"></a>示例  
 以下是使用 HTTP 传输安全的 WCF 服务的 web.config 文件的完整示例  
  
```xml  
<?xml version="1.0"?>  
<configuration>  
  
  <system.web>  
    <compilation debug="true" targetFramework="4.0" />  
  </system.web>  
  <system.serviceModel>  
    <services>  
      <service name="MySecureWCFService.Service1">  
        <endpoint address=""  
                  binding="basicHttpBinding"  
                  bindingConfiguration="secureHttpBinding"  
                  contract="MySecureWCFService.IService1"/>  
  
        <endpoint address="mex"  
                  binding="mexHttpsBinding"  
                  contract="IMetadataExchange" />  
      </service>  
    </services>  
    <bindings>  
      <basicHttpBinding>  
        <binding name="secureHttpBinding">  
          <security mode="Transport">  
            <transport clientCredentialType="None"/>  
          </security>  
        </binding>  
      </basicHttpBinding>  
    </bindings>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <!-- To avoid disclosing metadata information, set the value below to false and remove the metadata endpoint above before deployment -->  
          <serviceMetadata httpsGetEnabled="true"/>  
          <!-- To receive exception details in faults for debugging purposes, set the value below to true.  Set to false before deployment to avoid disclosing exception information -->  
          <serviceDebug includeExceptionDetailInFaults="false"/>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    <serviceHostingEnvironment multipleSiteBindingsEnabled="true" />  
  </system.serviceModel>  
  <system.webServer>  
    <modules runAllManagedModulesForAllRequests="true"/>  
  </system.webServer>  
  
</configuration>  
```  
  
## <a name="see-also"></a>请参阅
- [在 Internet Information Services 中承载](../../../../docs/framework/wcf/feature-details/hosting-in-internet-information-services.md)
- [Internet 信息服务承载说明](../../../../docs/framework/wcf/samples/internet-information-service-hosting-instructions.md)
- [Internet Information Services 承载最佳做法](../../../../docs/framework/wcf/feature-details/internet-information-services-hosting-best-practices.md)
- [使用内联代码的 IIS 承载](../../../../docs/framework/wcf/samples/iis-hosting-using-inline-code.md)
