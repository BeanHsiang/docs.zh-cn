---
title: 在托管 GDI+ 中使用图像编码器和解码器
ms.date: 03/30/2017
helpviewer_keywords:
- image encoders [Windows Forms], using
- image decoders [Windows Forms], using
ms.assetid: 0e838ea1-4e7e-4334-b882-ab25df607b8b
ms.openlocfilehash: bf0d3a64ce8860d67f0dcfd37c780f03fbd7471a
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57713254"
---
# <a name="using-image-encoders-and-decoders-in-managed-gdi"></a>在托管 GDI+ 中使用图像编码器和解码器
<xref:System.Drawing>命名空间提供<xref:System.Drawing.Image>和<xref:System.Drawing.Bitmap>用于存储和操作图像的类。 通过使用中的图像编码器[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)]，可以将映像从内存写入到磁盘。 通过使用中的图像解码器[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)]，可以将映像从磁盘加载到内存。 编码器中的数据转换<xref:System.Drawing.Image>或<xref:System.Drawing.Bitmap>到指定的磁盘的文件格式的对象。 解码器将转换为所需的格式的磁盘文件中的数据<xref:System.Drawing.Image>和<xref:System.Drawing.Bitmap>对象。  
  
 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 具有内置编码器和解码器支持以下文件类型：  
  
-   BMP  
  
-   GIF  
  
-   JPEG  
  
-   PNG  
  
-   TIFF  
  
 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 此外提供了支持以下文件类型的内置解码器：  
  
-   WMF  
  
-   EMF  
  
-   图标  
  
 以下主题讨论编码器和解码器中更多详细信息：  
  
## <a name="in-this-section"></a>本节内容  
 [如何：列出已安装的编码器](how-to-list-installed-encoders.md)  
 介绍了如何列出计算机上可用的编码器。  
  
 [如何：列出已安装的解码器](how-to-list-installed-decoders.md)  
 介绍了如何列出计算机上可用解码器。  
  
 [如何：确定编码器支持的参数](how-to-determine-the-parameters-supported-by-an-encoder.md)  
 介绍了如何列出<xref:System.Drawing.Imaging.EncoderParameters>编码器支持。  
  
 [如何：将 BMP 图像转换为 PNG 图像](how-to-convert-a-bmp-image-to-a-png-image.md)  
 介绍如何将图像保存在不同的图像格式。  
  
 [如何：设置 JPEG 压缩级别](how-to-set-jpeg-compression-level.md)  
 介绍如何更改图像的质量级别。  
  
## <a name="reference"></a>参考  
 <xref:System.Drawing.Image>  
  
 <xref:System.Drawing.Bitmap>  
  
 <xref:System.Drawing.Imaging.ImageCodecInfo>  
  
 <xref:System.Drawing.Imaging.EncoderParameter>  
  
 <xref:System.Drawing.Imaging.Encoder>  
  
## <a name="related-sections"></a>相关章节  
 [关于 GDI+ 托管代码](about-gdi-managed-code.md)  
  
 [图像、位图和图元文件](images-bitmaps-and-metafiles.md)
