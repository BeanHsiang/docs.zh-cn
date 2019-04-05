---
title: 从 XML 生成数据类型类
ms.date: 03/30/2017
ms.assetid: e4e5e4e8-527f-44d1-92fa-8904a08784ea
ms.openlocfilehash: a6666f1ba23dd563bd7a005d458cd7fe8253c3af
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2019
ms.locfileid: "57679081"
---
# <a name="generating-data-type-classes-from-xml"></a>从 XML 生成数据类型类
[!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 包括用于从 XML 生成数据类型类的新功能。 本主题介绍如何为.NET 博客 RSS 源自动生成的数据类型。  
  
### <a name="obtaining-the-xml-from-the-net-blog-rss-feed"></a>获取从.NET 博客 RSS XML 源  
  
1.  在 Internet Explorer 中，导航到[.NET 博客 RSS 源](https://devblogs.microsoft.com/dotnet/feed/)。  
  
2.  右键单击页并选择**查看源**。  
  
3.  通过按复制的源文本**Ctrl + A**以选择所有文本，并**Ctrl + C**复制。  
  
### <a name="creating-the-data-types"></a>创建数据类型  
  
1.  打开要使用代理的代码文件。 此文件应为 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 项目的一部分。  
  
2.  将游标放置于该文件中任何现有类之外的位置中。  
  
3.  选择**编辑**，**选择性粘贴**，**将 XML 粘贴为类**。  
  
4.  类名为`link`， `rss`， `rssChannel`， `rssChannelImage`，`rssChannelItem`和`rssChannelItemGuid`用于访问 RSS 源中的元素创建使用所需成员。  
  
### <a name="using-the-generated-classes"></a>使用生成的类  
  
1.  一旦生成了类，这些类就可以像任何其他类一样在代码中使用。 下面的代码示例返回 `rssChannelImage` 类的新实例。  
  
    ```  
    var channelImage = new rssChannelImage()   
    {   
        title = "MyImage",   
        link = "http://www.contoso.com/images/channelImage.jpg",   
        url = "http://www.contoso.com/entries/myEntry.html"   
    };  
    ```
