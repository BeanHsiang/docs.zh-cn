---
title: 如何：修改 XML 文本 (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- XML axis [Visual Basic], Value
- XML literals [Visual Basic]
- XML literals [Visual Basic], modifying
ms.assetid: 4e864522-a37a-43a2-8236-af80277c5482
ms.openlocfilehash: 003715b04f3a5c0fb41e846beb189f117378ea58
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2019
ms.locfileid: "57675324"
---
# <a name="how-to-modify-xml-literals-visual-basic"></a>如何：修改 XML 文本 (Visual Basic)

Visual Basic 提供方便的方式来修改 XML 文本。 可以添加或删除元素和属性，并还可以使用新的 XML 元素来替换现有元素。 本主题提供如何修改现有 XML 文本的几个示例。

### <a name="to-modify-the-value-of-an-xml-literal"></a>若要修改的 XML 文本值

1. 若要修改的 XML 文本的值，获取对 XML 文本，并且已设置的引用`Value`属性设置为所需的值。

    以下代码示例将更新的所有值\<价格 > XML 文档中的元素。

    [!code-vb[VbXmlSamples2#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXmlSamples2/VB/Module2.vb#4)]

    下面显示了示例源为 XML 并修改此代码示例中的 XML。

    源 XML:

    ```xml
    <?xml version="1.0"?>
    <Catalog>
      <Book id="bk101">
        <Author>Garghentini, Davide</Author>
        <Title>XML Developer's Guide</Title>
        <Price>44.95</Price>
      </Book>
      <Book id="bk331">
        <Author>Spencer, Phil</Author>
        <Title>Developing Applications with Visual Basic .NET</Title>
        <Price>45.95</Price>
      </Book>
    </Catalog>
    ```

    修改后的 XML:

    ```xml
    <?xml version="1.0"?>
    <Catalog>
      <Book id="bk101">
        <Author>Garghentini, Davide</Author>
        <Title>XML Developer's Guide</Title>
        <Price>47.20</Price>
      </Book>
      <Book id="bk331">
        <Author>Spencer, Phil</Author>
        <Title>Developing Applications with Visual Basic .NET</Title>
        <Price>48.25</Price>
      </Book>
    </Catalog>
    ```

    > [!NOTE]
    > `Value`属性是指集合中的第一个 XML 元素。 如果不存在具有相同的名称在集合中的多个元素，则将设置`Value`属性会影响仅在集合中的第一个元素。

### <a name="to-add-an-attribute-to-an-xml-literal"></a>将属性添加到 XML 文本

1. 若要将属性添加到 XML 文本，首先获取对 XML 文本的引用。 然后可以通过添加新的 XML 特性轴属性添加一个属性。 您还可以添加一个新<xref:System.Xml.Linq.XAttribute>对象与 XML 文本使用<xref:System.Xml.Linq.XContainer.Add%2A>方法。 下面的示例显示了这两个选项。

    [!code-vb[VbXmlSamples2#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXmlSamples2/VB/Module2.vb#5)]

    下面显示了示例源为 XML 并修改此代码示例中的 XML。

    源 XML:

    ```xml
    <?xml version="1.0"?>
    <Catalog>
      <Book id="bk101" >
        <Author>Garghentini, Davide</Author>
        <Title>XML Developer's Guide</Title>
        <Price>44.95</Price>
      </Book>
      <Book id="bk331">
        <Author>Spencer, Phil</Author>
        <Title>Developing Applications with Visual Basic .NET</Title>
        <Price>45.95</Price>
      </Book>
    </Catalog>
    ```

    修改后的 XML:

    ```xml
    <?xml version="1.0"?>
    <Catalog>
      <Book id="bk101" genre="Computer" editorEmail="someone@example.com">
        <Author>Garghentini, Davide</Author>
        <Title>XML Developer's Guide</Title>
        <Price>44.95</Price>
      </Book>
      <Book id="bk331" genre="Computer" editorEmail="someone@example.com">
        <Author>Spencer, Phil</Author>
        <Title>Developing Applications with Visual Basic .NET</Title>
        <Price>45.95</Price>
      </Book>
    </Catalog>
    ```

    有关 XML 特性轴属性的详细信息，请参阅[XML 特性轴属性](../../../../visual-basic/language-reference/xml-axis/xml-attribute-axis-property.md)。

### <a name="to-add-an-element-to-an-xml-literal"></a>若要将元素添加到 XML 文本

1. 若要将元素添加到 XML 文本，首先获取对 XML 文本的引用。 然后，可以添加一个新<xref:System.Xml.Linq.XElement>对象使用的元素的最后一个子元素作为<xref:System.Xml.Linq.XContainer.Add%2A>方法。 您可以添加一个新<xref:System.Xml.Linq.XElement>对象使用的第一个子元素作为<xref:System.Xml.Linq.XContainer.AddFirst%2A>方法。

    若要在特定位置相对于其他子元素添加一个新的元素，请首先获取对相邻的子元素的引用。 然后，可以添加新<xref:System.Xml.Linq.XElement>对象使用相邻的子元素之前的<xref:System.Xml.Linq.XNode.AddBeforeSelf%2A>方法。 您还可以添加新<xref:System.Xml.Linq.XElement>通过使用相邻的子元素之后的对象<xref:System.Xml.Linq.XNode.AddAfterSelf%2A>方法。

    下面的示例显示了每种技术的示例。

    [!code-vb[VbXmlSamples2#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXmlSamples2/VB/Module2.vb#6)]

    下面显示了示例源为 XML 并修改此代码示例中的 XML。

    源 XML:

    ```xml
    <?xml version="1.0"?>
    <Catalog>
      <Book id="bk101" >
        <Author>Garghentini, Davide</Author>
        <Title>XML Developer's Guide</Title>
        <Price>44.95</Price>
      </Book>
      <Book id="bk331">
        <Author>Spencer, Phil</Author>
        <Title>Developing Applications with Visual Basic .NET</Title>
        <Price>45.95</Price>
      </Book>
    </Catalog>
    ```

    修改后的 XML:

    ```xml
    <?xml version="1.0"?>
    <Catalog>
      <Book id="bk101" >
        <Author>Garghentini, Davide</Author>
        <Title>XML Developer's Guide</Title>
        <Price>44.95</Price>
      </Book>
      <Book id="bk000"></Book>
      <Book id="bk331">
        <Publisher>Microsoft Press</Publisher>
        <Author>Spencer, Phil</Author>
        <Title>Developing Applications with Visual Basic .NET</Title>
        <Price>45.95</Price>
        <PublishDate>2005-2-14</PublishDate>
      </Book>
      <Book id="bk999"></Book>
    </Catalog>
    ```

### <a name="to-remove-an-element-or-attribute-from-an-xml-literal"></a>若要从 XML 文本中移除的元素或属性

1. 若要从 XML 文本中删除一个元素或属性，请获取对元素或属性与调用的引用`Remove`方法，如以下示例所示。

    [!code-vb[VbXmlSamples2#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXmlSamples2/VB/Module2.vb#7)]

    下面显示了示例源为 XML 并修改此代码示例中的 XML。

    源 XML:

    ```xml
    <?xml version="1.0"?>
    <Catalog>
      <Book id="bk101" genre="Computer" editorEmail="someone@example.com">
        <Author>Garghentini, Davide</Author>
        <Title>XML Developer's Guide</Title>
        <Price>44.95</Price>
      </Book>
      <Book id="bk000"></Book>
      <Book id="bk331" genre="Computer" editorEmail="someone@example.com">
        <Author>Spencer, Phil</Author>
        <Title>Developing Applications with Visual Basic .NET</Title>
        <Price>45.95</Price>
      </Book>
      <Book id="bk999"></Book>
    </Catalog>
    ```

    修改后的 XML:

    ```xml
    <?xml version="1.0"?>
    <Catalog>
      <Book id="bk101" editorEmail="someone@example.com">
        <Author>Garghentini, Davide</Author>
        <Title>XML Developer's Guide</Title>
        <Price>44.95</Price>
      </Book>
      <Book id="bk000"></Book>
      <Book id="bk331" editorEmail="someone@example.com">
        <Author>Spencer, Phil</Author>
        <Title>Developing Applications with Visual Basic .NET</Title>
        <Price>45.95</Price>
      </Book></Catalog>
    ```

    若要从 XML 文本中移除所有元素或属性，获取对 XML 文本的引用，并调用<xref:System.Xml.Linq.XElement.RemoveAll%2A>方法。

### <a name="to-modify-an-xml-literal"></a>若要修改 XML 文本

1. 若要更改的 XML 元素的名称，首先获取对元素的引用。 然后创建一个新<xref:System.Xml.Linq.XElement>有一个新的命名并传递新的对象<xref:System.Xml.Linq.XElement>对象传递给<xref:System.Xml.Linq.XNode.ReplaceWith%2A>方法的现有<xref:System.Xml.Linq.XElement>对象。

    如果要替换的元素具有必须保留的子元素，将新的值设置<xref:System.Xml.Linq.XElement>对象传递给<xref:System.Xml.Linq.XContainer.Nodes%2A>现有元素的属性。 这会将新元素的值设置为现有元素的内部 XML。 另外，可以将新元素的值设置`Value`现有元素的属性。

    下面的代码示例替换所有\<说明 > 的元素\<抽象 > 元素。 内容\<说明 > 元素保留在新\<抽象 > 元素中的使用<xref:System.Xml.Linq.XContainer.Nodes%2A>的属性\<说明 ><xref:System.Xml.Linq.XElement>对象。

    [!code-vb[VbXmlSamples2#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXmlSamples2/VB/Module2.vb#8)]

    下面显示了示例源为 XML 并修改此代码示例中的 XML。

    源 XML:

    ```xml
    <?xml version="1.0"?>
    <Catalog>
      <Book id="bk101">
        <Author>Garghentini, Davide</Author>
        <Title>XML Developer's Guide</Title>
        <Price>44.95</Price>
        <Description>
          An in-depth look at creating applications
          with <technology>XML</technology>. For
          <audience>beginners</audience> or
          <audience>advanced</audience> developers.
        </Description>
      </Book>
      <Book id="bk331">
        <Author>Spencer, Phil</Author>
        <Title>Developing Applications with Visual Basic .NET</Title>
        <Price>45.95</Price>
        <Description>
          Get the expert insights, practical code samples, and best
          practices you need to advance your expertise with
          <technology>Visual Basic .NET</technology>.
          Learn how to create faster, more reliable applications
          based on professional, pragmatic guidance by today's top
          <audience>developers</audience>.
        </Description>
      </Book>
    </Catalog>
    ```

    修改后的 XML:

    ```xml
    <?xml version="1.0"?>
    <Catalog>
      <Book id="bk101">
        <Author>Garghentini, Davide</Author>
        <Title>XML Developer's Guide</Title>
        <MSRP>44.95</MSRP>    <Abstract>
          An in-depth look at creating applications
          with <technology>XML</technology>. For
          <audience>beginners</audience> or
          <audience>advanced</audience> developers.
        </Abstract>
      </Book>
      <Book id="bk331">
        <Author>Spencer, Phil</Author>
        <Title>Developing Applications with Visual Basic .NET</Title>
        <MSRP>45.95</MSRP>    <Abstract>
          Get the expert insights, practical code samples, and best
          practices you need to advance your expertise with
          <technology>Visual Basic .NET</technology>.
          Learn how to create faster, more reliable applications
          based on professional, pragmatic guidance by today's top
          <audience>developers</audience>.
        </Abstract>
      </Book>
    </Catalog>
    ```

## <a name="see-also"></a>请参阅

- [在 Visual Basic 中操控 XML](../../../../visual-basic/programming-guide/language-features/xml/manipulating-xml.md)
- [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)
- [如何：从文件、 字符串或 Stream 加载 XML](../../../../visual-basic/programming-guide/language-features/xml/how-to-load-xml-from-a-file-string-or-stream.md)
- [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)
- [Visual Basic 中的 LINQ 简介](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)
