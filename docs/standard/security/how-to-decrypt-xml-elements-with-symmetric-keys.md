---
title: 如何：使用对称密钥解密 XML 元素
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- symmetric keys
- System.Security.Cryptography.EncryptedXml class
- System.Security.Cryptography.RijndaelManaged class
- XML encryption
- Rijndael
- decryption
ms.assetid: 6038aff0-f92c-4e29-a618-d793410410d8
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 19ee0e3244d9a9bf7d7eddc9be4eb7c50b467cf5
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54502619"
---
# <a name="how-to-decrypt-xml-elements-with-symmetric-keys"></a>如何：使用对称密钥解密 XML 元素
可以使用 <xref:System.Security.Cryptography.Xml> 命名空间中的类加密 XML 文档内的元素。  XML 加密可用于存储或传输敏感 XML，而无需担心数据被轻易读取。  此代码示例使用高级加密标准 (AES) 算法（也称为 Rijndael）对 XML 元素进行解密。  
  
 有关如何加密 XML 元素使用此过程的信息，请参阅[如何：使用对称密钥加密 XML 元素](../../../docs/standard/security/how-to-encrypt-xml-elements-with-symmetric-keys.md)。  
  
 当使用对称算法（如 AES）来加密 XML 数据时，必须使用相同的密钥来加密和解密 XML 数据。  此过程中的示例假定加密的 XML 是使用相同的密钥进行加密的，且加密方和解密方对要使用的算法和密钥达成一致。  此示例不对加密的 XML 内的 AES 密钥进行存储或加密。  
  
 此示例适用于以下情况：单个应用程序需要根据内存中存储的会话密钥加密数据，或根据从密码派生而来的加密型强密钥进行加密。  对于两个或多个应用程序需要共享加密的 XML 数据的情况，请考虑使用基于非对称算法或 X.509 证书的加密方案。  
  
### <a name="to-decrypt-an-xml-element-with-a-symmetric-key"></a>若要使用对称密钥解密 XML 元素  
  
1.  使用以前生成的密钥使用中所述的技术加密 XML 元素[如何：使用对称密钥加密 XML 元素](../../../docs/standard/security/how-to-encrypt-xml-elements-with-symmetric-keys.md)。  
  
2.  在包含加密的 XML 的 <xref:System.Xml.XmlDocument> 对象中查找 <`EncryptedData`> 元素（由 XML 加密标准定义），然后创建一个新的 <xref:System.Xml.XmlElement> 对象来表示该元素。  
  
     [!code-csharp[HowToEncryptXMLElementSymmetric#10](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/cs/sample.cs#10)]
     [!code-vb[HowToEncryptXMLElementSymmetric#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/vb/sample.vb#10)]  
  
3.  通过从之前创建的 <xref:System.Xml.XmlElement> 对象加载原始 XML 数据来创建 <xref:System.Security.Cryptography.Xml.EncryptedData> 对象。  
  
     [!code-csharp[HowToEncryptXMLElementSymmetric#11](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/cs/sample.cs#11)]
     [!code-vb[HowToEncryptXMLElementSymmetric#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/vb/sample.vb#11)]  
  
4.  创建一个新的 <xref:System.Security.Cryptography.Xml.EncryptedXml> 对象并使用它对使用与加密相同密钥的 XML 数据进行解密。  
  
     [!code-csharp[HowToEncryptXMLElementSymmetric#12](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/cs/sample.cs#12)]
     [!code-vb[HowToEncryptXMLElementSymmetric#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/vb/sample.vb#12)]  
  
5.  将加密的元素替换为 XML 文档内的新解密的纯文本元素。  
  
     [!code-csharp[HowToEncryptXMLElementSymmetric#13](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/cs/sample.cs#13)]
     [!code-vb[HowToEncryptXMLElementSymmetric#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/vb/sample.vb#13)]  
  
## <a name="example"></a>示例  
 此示例假定名为 `"test.xml"` 的文件与已编译程序存在于同一目录中。  它还假定 `"test.xml"` 包含 `"creditcard"` 元素。  可以将以下 XML 放在名为 `test.xml` 的文件，并将其用于以下示例。  
  
```xml  
<root>  
    <creditcard>  
        <number>19834209</number>  
        <expiry>02/02/2002</expiry>  
    </creditcard>  
</root>  
```  
  
 [!code-csharp[HowToEncryptXMLElementSymmetric#1](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/cs/sample.cs#1)]
 [!code-vb[HowToEncryptXMLElementSymmetric#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/vb/sample.vb#1)]  
  
## <a name="compiling-the-code"></a>编译代码  
  
-   若要编译此示例，需要包含对 `System.Security.dll` 的引用。  
  
-   包括以下命名空间：<xref:System.Xml>、<xref:System.Security.Cryptography> 和 <xref:System.Security.Cryptography.Xml>。  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 永远不要以纯文本形式存储加密密钥，也不要以纯文本形式在计算机之间传输密钥。  
  
 当你完成使用对称加密密钥后，通过将每个字节设置为零或通过调用托管加密类的 <xref:System.Security.Cryptography.SymmetricAlgorithm.Clear%2A> 方法来将它从内存中清除。  
  
## <a name="see-also"></a>请参阅

- <xref:System.Security.Cryptography.Xml>
- [如何：使用对称密钥加密 XML 元素](../../../docs/standard/security/how-to-encrypt-xml-elements-with-symmetric-keys.md)
