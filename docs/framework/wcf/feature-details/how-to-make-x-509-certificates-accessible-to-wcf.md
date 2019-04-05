---
title: 如何：使 X.509 证书可由 WCF 访问
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- X.509 certificates [WCF]
- certificates [WCF], making X.509 certificates accessible to WCF
- X.509 certificates [WCF], making accessible to WCF
ms.assetid: a54e407c-c2b5-4319-a648-60e43413664b
ms.openlocfilehash: 7c90d5b0541edfc11145d9373c2554ee4595a7b1
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54741871"
---
# <a name="how-to-make-x509-certificates-accessible-to-wcf"></a>如何：使 X.509 证书可由 WCF 访问
若要使 X.509 证书对 Windows Communication Foundation (WCF) 访问，应用程序代码必须指定证书存储区名称和位置。 在某些情况下，进程标识必须具有对包含私钥的文件的访问权限，此私钥与 X.509 证书相关联。 若要获取与证书存储区中的 X.509 证书关联的私钥，WCF 必须有权执行此操作。 默认情况下，只有所有者和“系统”帐户才可以访问证书的私钥。  
  
### <a name="to-make-x509-certificates-accessible-to-wcf"></a>使 X.509 证书可由 WCF 访问  
  
1.  为提供的 WCF 的运行的帐户读取访问权限到包含与 X.509 证书关联的私钥的文件。  
  
    1.  确定是否 WCF 需要读取访问权限的私钥的 X.509 证书。  
  
         下表详细描述在使用某个 X.509 证书时是否必须提供私钥。  
  
        |X.509 证书用途|私钥|  
        |---------------------------|-----------------|  
        |对出站 SOAP 消息进行数字签名。|是|  
        |验证入站 SOAP 消息的签名。|否|  
        |对出站 SOAP 消息进行加密。|否|  
        |对入站 SOAP 消息进行解密。|是|  
  
    2.  确定在其中存储证书的存储区的位置和名称。  
  
         在其中存储证书的证书存储区要么在应用程序代码中指定，要么在配置中指定。 例如，下面的示例指定证书位于名为 `CurrentUser` 的 `My` 证书存储区中。  
  
         [!code-csharp[x509Accessible#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/x509accessible/cs/source.cs#1)]
         [!code-vb[x509Accessible#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/x509accessible/vb/source.vb#1)]  
  
    3.  确定证书的私钥在计算机上位于通过[FindPrivateKey](../../../../docs/framework/wcf/samples/findprivatekey.md)工具。  
  
         [FindPrivateKey](../../../../docs/framework/wcf/samples/findprivatekey.md)工具需要证书存储区名称、 证书存储区位置和内容可唯一标识的证书。 此工具接受将证书的主题名称或其指纹作为唯一标识符。 有关如何确定证书的指纹的详细信息，请参阅[如何：检索证书的指纹](../../../../docs/framework/wcf/feature-details/how-to-retrieve-the-thumbprint-of-a-certificate.md)。  
  
         下面的代码示例使用[FindPrivateKey](../../../../docs/framework/wcf/samples/findprivatekey.md)工具来确定的位置中的证书的私钥`My`将存储在`CurrentUser`指纹为`46 dd 0e 7a ed 0b 7a 31 9b 02 a3 a0 43 7a d8 3f 60 40 92 9d`。  
  
        ```  
        findprivatekey.exe My CurrentUser -t "46 dd 0e 7a ed 0b 7a 31 9b 02 a3 a0 43 7a d8 3f 60 40 92 9d" -a  
        ```  
  
    4.  确定 WCF 下运行的帐户。  
  
         下表详细说明 WCF 运行在给定方案的帐户。  
  
        |方案|进程标识|  
        |--------------|----------------------|  
        |客户端（控制台或 WinForms 应用程序）。|当前登录的用户。|  
        |自承载服务。|当前登录的用户。|  
        |在 IIS 6.0 ([!INCLUDE[ws2003](../../../../includes/ws2003-md.md)]) 或 IIS 7.0 ([!INCLUDE[wv](../../../../includes/wv-md.md)]) 中承载的服务。|NETWORK SERVICE|  
        |在 IIS 5.X ([!INCLUDE[wxp](../../../../includes/wxp-md.md)]) 中承载的服务。|由 Machine.config 文件中的 `<processModel>` 元素控制。 默认帐户为 ASPNET。|  
  
    5.  授予对包含到 WCF 运行时所使用 icacls.exe 之类的工具的帐户的私钥的文件的读取访问权限。  
  
         下面的代码示例编辑的自由访问控制列表 (DACL) 授予 NETWORK SERVICE 帐户读取指定的文件 (: R) 对文件的访问。  
  
        ```  
        icacls.exe "C:\Documents and Settings\All Users\Application Data\Microsoft\Crypto\RSA\MachineKeys\8aeda5eb81555f14f8f9960745b5a40d_38f7de48-5ee9-452d-8a5a-92789d7110b1" /grant "NETWORK SERVICE":R  
        ```  
  
## <a name="see-also"></a>请参阅
- [FindPrivateKey](../../../../docs/framework/wcf/samples/findprivatekey.md)
- [如何：检索证书的指纹](../../../../docs/framework/wcf/feature-details/how-to-retrieve-the-thumbprint-of-a-certificate.md)
- [使用证书](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)
