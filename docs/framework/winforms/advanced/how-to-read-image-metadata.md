---
title: 如何：读取图像元数据
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- metadata [Windows Forms], property item
- metadata [Windows Forms], reading image
ms.assetid: 72ec0b31-0be7-444a-9575-1dbcb864e0be
ms.openlocfilehash: eba21519e6ea6cf4a2a412750fd305d7af620c1b
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57720783"
---
# <a name="how-to-read-image-metadata"></a>如何：读取图像元数据
某些图像文件包含元数据可以读取来确定映像的功能。 例如，数字照片中可能包含您可以读取以确定品牌和型号的照相机用于捕获映像的元数据。 使用[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)]，可以读取现有的元数据，并还可以将新的元数据写入图像文件。  
  
 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 存储元数据中的个别<xref:System.Drawing.Imaging.PropertyItem>对象。 可以读取<xref:System.Drawing.Image.PropertyItems%2A>属性的<xref:System.Drawing.Image>要从文件检索的元数据对象。 <xref:System.Drawing.Image.PropertyItems%2A>属性返回的数组<xref:System.Drawing.Imaging.PropertyItem>对象。  
  
 一个<xref:System.Drawing.Imaging.PropertyItem>对象具有以下四个属性： `Id`， `Value`， `Len`，和`Type`。  
  
## <a name="id"></a>Id  
 一个标识元数据项的标记。 可以分配给某些值<xref:System.Drawing.Imaging.PropertyItem.Id%2A>下表中所示。  
  
|十六进制值|描述|  
|-----------------------|-----------------|  
|0x0320<br /><br /> 0x010F<br /><br /> 0x0110<br /><br /> 0x9003<br /><br /> 0x829A<br /><br /> 0x5090<br /><br /> 0x5091|图像标题<br /><br /> 设备制造商<br /><br /> 设备模型<br /><br /> ExifDTOriginal<br /><br /> Exif 暴露时间<br /><br /> 亮度表<br /><br /> 色度表|  
  
## <a name="value"></a>值  
 值的数组。 值的格式由<xref:System.Drawing.Imaging.PropertyItem.Type%2A>属性。  
  
## <a name="len"></a>Len  
 指向的值数组的长度 （以字节为单位）<xref:System.Drawing.Imaging.PropertyItem.Value%2A>属性。  
  
## <a name="type"></a>类型  
 指向数组中的值的数据类型`Value`属性。 通过指示的格式`Type`下表中显示属性值  
  
|数字值|描述|  
|-------------------|-----------------|  
|1|一个 `Byte`|  
|2|一个数组`Byte`对象编码为 ASCII|  
|3|16 位整数|  
|4|一个 32 位整数|  
|5|两个数组`Byte`代表有理数的对象|  
|6|未使用|  
|7|未定义|  
|8|未使用|  
|9|`SLong`|  
|10|`SRational`|  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>描述  
 下面的代码示例读取并显示文件中的元数据的七个部分`FakePhoto.jpg`。 在列表中的第二个 （索引 1） 属性项<xref:System.Drawing.Imaging.PropertyItem.Id%2A>0x010F （设备制造商） 和<xref:System.Drawing.Imaging.PropertyItem.Type%2A>2 （ASCII 编码的字节数组）。 此代码示例显示该属性项的值。  
  
 此代码生成类似于以下输出：  
  
 `Property Item 0`  
  
 `id: 0x320`  
  
 `type: 2`  
  
 `length: 16 bytes`  
  
 `Property Item 1`  
  
 `id: 0x10f`  
  
 `type: 2`  
  
 `length: 17 bytes`  
  
 `Property Item 2`  
  
 `id: 0x110`  
  
 `type: 2`  
  
 `length: 7 bytes`  
  
 `Property Item 3`  
  
 `id: 0x9003`  
  
 `type: 2`  
  
 `length: 20 bytes`  
  
 `Property Item 4`  
  
 `id: 0x829a`  
  
 `type: 5`  
  
 `length: 8 bytes`  
  
 `Property Item 5`  
  
 `id: 0x5090`  
  
 `type: 3`  
  
 `length: 128 bytes`  
  
 `Property Item 6`  
  
 `id: 0x5091`  
  
 `type: 3`  
  
 `length: 128 bytes`  
  
 `The equipment make is Northwind Camera.`  
  
### <a name="code"></a>代码  
 [!code-csharp[System.Drawing.WorkingWithImages#51](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/CS/Class1.cs#51)]
 [!code-vb[System.Drawing.WorkingWithImages#51](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/VB/Class1.vb#51)]  
  
## <a name="compiling-the-code"></a>编译代码  
 前面的示例专用于 Windows 窗体，它需要 <xref:System.Windows.Forms.PaintEventArgs> `e`，后者是 <xref:System.Windows.Forms.Control.Paint> 事件处理程序的参数。 处理窗体的<xref:System.Windows.Forms.Control.Paint>事件并将此代码粘贴到 paint 事件处理程序。 必须替换`FakePhoto.jpg`用的映像名称和路径上您的系统和导入有效`System.Drawing.Imaging`命名空间。  
  
## <a name="see-also"></a>请参阅
- [图像、位图和图元文件](images-bitmaps-and-metafiles.md)
- [使用图像、位图、图标和图元文件](working-with-images-bitmaps-icons-and-metafiles.md)
