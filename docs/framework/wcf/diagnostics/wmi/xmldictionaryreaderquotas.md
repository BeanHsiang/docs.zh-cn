---
title: XmlDictionaryReaderQuotas
ms.date: 03/30/2017
ms.assetid: 9b4ca8b4-0a89-4758-97ab-528a8ce18f07
ms.openlocfilehash: f24865fb0affa7b4516a14fc05b905995826e82e
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54597666"
---
# <a name="xmldictionaryreaderquotas"></a>XmlDictionaryReaderQuotas
XmlDictionaryReaderQuotas  
  
## <a name="syntax"></a>语法  
  
```csharp
class XmlDictionaryReaderQuotas  
{  
  sint32 MaxArrayLength;  
  sint32 MaxBytesPerRead;  
  sint32 MaxDepth;  
  sint32 MaxNameTableCharCount;  
  sint32 MaxStringContentLength;  
};  
```  
  
## <a name="methods"></a>方法  
 XmlDictionaryReaderQuotas 类不定义任何方法。  
  
## <a name="properties"></a>Properties  
 XmlDictionaryReaderQuotas 类具有以下属性：  
  
### <a name="maxarraylength"></a>MaxArrayLength  
 数据类型：sint32  
  
 访问类型：只读  
  
 允许的最大数组长度。  
  
### <a name="maxbytesperread"></a>MaxBytesPerRead  
 数据类型：sint32  
  
 访问类型：只读  
  
 允许为每次读取返回的最大字节数。  
  
### <a name="maxdepth"></a>MaxDepth  
 数据类型：sint32  
  
 访问类型：只读  
  
 每次读取的最大嵌套节点深度。  
  
### <a name="maxnametablecharcount"></a>MaxNameTableCharCount  
 数据类型：sint32  
  
 访问类型：只读  
  
 表名称中允许的最大字符数。  
  
### <a name="maxstringcontentlength"></a>MaxStringContentLength  
 数据类型：sint32  
  
 访问类型：只读  
  
 XML 元素内容中允许包含的最大字符数。  
  
## <a name="requirements"></a>要求  
  
|MOF|已在 Servicemodel.mof 中声明。|  
|---------|-----------------------------------|  
|命名空间|已在 root\ServiceModel 中定义|  
  
## <a name="see-also"></a>请参阅
- <xref:System.Xml.XmlDictionaryReaderQuotas>
- <xref:System.ServiceModel.Configuration.XmlDictionaryReaderQuotasElement>
