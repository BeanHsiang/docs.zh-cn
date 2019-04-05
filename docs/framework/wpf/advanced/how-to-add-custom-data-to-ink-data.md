---
title: 如何：向墨迹数据添加自定义数据
ms.date: 03/30/2017
helpviewer_keywords:
- ink data [WPF], adding custom data
- InkCanvas [WPF], displaying
ms.assetid: f02aac6f-3436-4f7c-b6ea-0452cba5332c
ms.openlocfilehash: c524e30943a21426e2e5e8fe6ae009999924fead
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57361663"
---
# <a name="how-to-add-custom-data-to-ink-data"></a>如何：向墨迹数据添加自定义数据
可以将自定义数据添加到手写内容保存为墨迹序列化格式 (ISF) 时将保存的墨迹。  您可以自定义将数据保存到<xref:System.Windows.Ink.DrawingAttributes>，则<xref:System.Windows.Ink.StrokeCollection>，或<xref:System.Windows.Ink.Stroke>。  能够将自定义数据保存在三个对象上使你能够决定保存数据的最佳位置。  所有三个类使用类似的方法来存储和访问自定义数据。  
  
 只能使用以下类型可以另存为自定义数据：  
  
-   <xref:System.Boolean>  
  
-   <xref:System.Boolean>[]  
  
-   <xref:System.Byte>  
  
-   <xref:System.Byte>[]  
  
-   <xref:System.Char>  
  
-   <xref:System.Char>[]  
  
-   <xref:System.DateTime>  
  
-   <xref:System.DateTime>[]  
  
-   <xref:System.Decimal>  
  
-   <xref:System.Decimal>[]  
  
-   <xref:System.Double>  
  
-   <xref:System.Double>[]  
  
-   <xref:System.Int16>  
  
-   <xref:System.Int16>[]  
  
-   <xref:System.Int32>  
  
-   <xref:System.Int32>[]  
  
-   <xref:System.Int64>  
  
-   <xref:System.Int64>[]  
  
-   <xref:System.Single>  
  
-   <xref:System.Single>[]  
  
-   <xref:System.String>  
  
-   <xref:System.UInt16>  
  
-   <xref:System.UInt16>[]  
  
-   <xref:System.UInt32>  
  
-   <xref:System.UInt32>[]  
  
-   <xref:System.UInt64>  
  
-   <xref:System.UInt64>[]  
  
## <a name="example"></a>示例  
 下面的示例演示如何添加和检索自定义数据<xref:System.Windows.Ink.StrokeCollection>。  
  
 [!code-csharp[HowToAddCustomDataToInk#1](~/samples/snippets/csharp/VS_Snippets_Wpf/HowToAddCustomDataToInk/CSharp/Window1.xaml.cs#1)]  
  
 下面的示例创建一个显示应用程序<xref:System.Windows.Controls.InkCanvas>和两个按钮。  按钮， `switchAuthor`，使两个笔使用由两个不同的作者。  按钮`changePenColors`上的更改的每个笔画颜色<xref:System.Windows.Controls.InkCanvas>根据作者。  应用程序定义了两个<xref:System.Windows.Ink.DrawingAttributes>对象，并将自定义属性添加到指示哪个作者绘制每个<xref:System.Windows.Ink.Stroke>。  当用户单击`changePenColors`，应用程序更改自定义属性的值根据笔画的外观。  
  
 [!code-xaml[HowToAddCustomDataToInk#2](~/samples/snippets/csharp/VS_Snippets_Wpf/HowToAddCustomDataToInk/CSharp/Window1.xaml#2)]  
  
 [!code-csharp[HowToAddCustomDataToInk#3](~/samples/snippets/csharp/VS_Snippets_Wpf/HowToAddCustomDataToInk/CSharp/Window1.xaml.cs#3)]
