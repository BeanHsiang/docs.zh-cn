---
title: 可互操作的对象引用
ms.date: 03/30/2017
ms.assetid: cb8da4c8-08ca-4220-a16b-e04c8f527f1b
ms.openlocfilehash: 5d2f7d93544cafab7cfe5d8dcbb8a4c5d5c5b576
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54582412"
---
# <a name="interoperable-object-references"></a>可互操作的对象引用
默认情况下，<xref:System.Runtime.Serialization.DataContractSerializer> 按值序列化对象。 可以使用 <xref:System.Runtime.Serialization.DataContractAttribute.IsReference%2A> 属性指示数据协定序列化程序在序列化类型的对象时保留对象引用。  
  
## <a name="generated-xml"></a>生成的 XML  
 例如，请考虑下面的对象：  
  
```  
[DataContract]  
public class X  
{  
    SomeClass someInstance = new SomeClass();  
    [DataMember]  
    public SomeClass A = someInstance;  
    [DataMember]  
    public SomeClass B = someInstance;  
}  
  
public class SomeClass   
{  
}  
```  
  
 当 <xref:System.Runtime.Serialization.DataContractSerializer.PreserveObjectReferences%2A> 设置为 `false`（默认值）时，会生成下面的 XML：  
  
```xml  
<X>  
   <A>contents of someInstance</A>  
   <B>contents of someInstance</B>  
</X>  
```  
  
 当 <xref:System.Runtime.Serialization.DataContractSerializer.PreserveObjectReferences%2A> 设置为 `true` 时，会生成下面的 XML：  
  
```xml  
<X>  
   <A id="1">contents of someInstance</A>  
   <B ref="1" />  
</X>  
```  
  
 但是，<xref:System.Runtime.Serialization.XsdDataContractExporter> 不在其架构中描述 `id` 和 `ref` 属性 (Attribute)，即使在 `preserveObjectReferences` 属性 (Property) 设置为 `true` 时也如此。  
  
## <a name="using-isreference"></a>使用 IsReference  
 若要生成对象引用信息并使该信息对于描述它的架构有效，请将 <xref:System.Runtime.Serialization.DataContractAttribute> 特性应用于类型，并将 <xref:System.Runtime.Serialization.DataContractAttribute.IsReference%2A> 标志设置为 `true`。 在前面的示例类 `IsReference` 中使用 `X`：  
  
 `[DataContract(IsReference=true)] public class X`  
  
 `{`  
  
 `SomeClass someInstance = new SomeClass();`  
  
 `[DataMember]`  
  
 `public SomeClass A = someInstance;`  
  
 `[DataMember]`  
  
 `public SomeClass B = someInstance;`  
  
 `}`  
  
 `public class SomeClass`  
  
 `{`  
  
 `}`  
  
 生成的 XML 如下：  
  
 `<X>`  
  
 `<A id="1">`  
  
 `<Value>contents of A</Value>`  
  
 `</A>`  
  
 `<B ref="1">`  
  
 `</B>`  
  
 `</X>`  
  
 使用 `IsReference` 可确保消息往返时遵从架构要求。 如果未使用该属性，则从架构生成某个类型时，为该类型发回的 XML 不一定与架构最初设定的内容一致。 换言之，虽然 `id` 和 `ref` 属性进行了序列化，但原始架构可能禁止这些属性（或所有属性）在 XML 中出现。 在将 `IsReference` 应用于某个数据成员时，该成员在往返时会继续被识别为“可引用”。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Runtime.Serialization.DataContractAttribute>
- <xref:System.Runtime.Serialization.CollectionDataContractAttribute>
- <xref:System.Runtime.Serialization.DataContractAttribute.IsReference%2A>
- <xref:System.Runtime.Serialization.CollectionDataContractAttribute.IsReference%2A>
