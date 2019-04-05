---
title: 用来控制编码的 SOAP 序列化的属性
ms.date: 03/30/2017
helpviewer_keywords:
- SOAP, XML serialization
- XML serialization, SOAP
- XML serialization, attributes
- attributes [.NET Framework], XML serialization
- serialization, attributes
ms.assetid: 93ee258c-9c0f-4a08-897c-c10db7a00f91
ms.openlocfilehash: 2961d9abc6c32e78b5a61e8f2bbea5cfcf6677bd
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54547185"
---
# <a name="attributes-that-control-encoded-soap-serialization"></a>用来控制编码的 SOAP 序列化的属性

名为 World Wide Web 联合会 (W3C) 文档[简单对象访问协议 (SOAP) 1.1](https://www.w3.org/TR/2000/NOTE-SOAP-20000508/)包含可选章节 （第 5 节），介绍了如何编码 SOAP 参数。 要符合该规范的第 5 节，必须使用在 <xref:System.Xml.Serialization> 命名空间中找到的一组特殊属性。 将这些特性适当应用于类和类的成员，然后使用 <xref:System.Xml.Serialization.XmlSerializer> 序列化一个或多个类的实例。

下表显示属性、属性的应用范围及其作用。 有关使用这些属性控制 XML 序列化的详细信息，请参阅[如何：SOAP 编码的 XML Stream 将对象序列化为](how-to-serialize-an-object-as-a-soap-encoded-xml-stream.md)和[如何：重写编码的 SOAP XML 序列化](how-to-override-encoded-soap-xml-serialization.md)。

有关属性的详细信息，请参阅[属性](../../../docs/standard/attributes/index.md)。

|特性|适用对象|指定|
|---------------|----------------|---------------|
|<xref:System.Xml.Serialization.SoapAttributeAttribute>|公共字段、属性、参数或返回值。|类成员将序列化为 XML 属性。|
|<xref:System.Xml.Serialization.SoapElementAttribute>|公共字段、属性、参数或返回值。|类将序列化为 XML 元素。|
|<xref:System.Xml.Serialization.SoapEnumAttribute>|作为枚举标识符的公共字段。|枚举成员的元素名称。|
|<xref:System.Xml.Serialization.SoapIgnoreAttribute>|公共属性和公共字段。|序列化包含类时，应该忽略属性或字段。|
|<xref:System.Xml.Serialization.SoapIncludeAttribute>|公共的派生类声明，以及 Web 服务描述语言 (WSDL) 文档的公共方法。|生成要在序列化时识别的架构时，应该将该类型包括在内。|
|<xref:System.Xml.Serialization.SoapTypeAttribute>|公共类声明。|类应序列化为 XML 类型。|

## <a name="see-also"></a>请参阅

- [XML 和 SOAP 序列化](xml-and-soap-serialization.md)
- [如何：将对象序列化为 SOAP 编码的 XML Stream](how-to-serialize-an-object-as-a-soap-encoded-xml-stream.md)
- [如何：重写编码的 SOAP XML 序列化](how-to-override-encoded-soap-xml-serialization.md)
- [属性](../../../docs/standard/attributes/index.md)
- <xref:System.Xml.Serialization.XmlSerializer>
- [如何：将对象序列化](how-to-serialize-an-object.md)
- [如何：反序列化对象](how-to-deserialize-an-object.md)
