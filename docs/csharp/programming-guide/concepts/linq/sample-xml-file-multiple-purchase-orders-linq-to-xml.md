---
title: 示例 XML 文件：多个采购订单 (LINQ to XML)
ms.date: 07/20/2015
ms.assetid: 2d29fcaa-60df-43d4-8ccc-6cdba7c013e9
ms.openlocfilehash: 232be52bb75c6e07773c79a65f4e8e8f346a65d9
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54747786"
---
# <a name="sample-xml-file-multiple-purchase-orders-linq-to-xml"></a>示例 XML 文件：多个采购订单 (LINQ to XML)
下面的 XML 文件用在 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 文档的很多示例中。 此文件包含多个采购订单。  
  
## <a name="purchaseordersxml"></a>PurchaseOrders.xml  
  
```xml  
<?xml version="1.0"?>  
<PurchaseOrders>  
  <PurchaseOrder PurchaseOrderNumber="99503" OrderDate="1999-10-20">  
    <Address Type="Shipping">  
      <Name>Ellen Adams</Name>  
      <Street>123 Maple Street</Street>  
      <City>Mill Valley</City>  
      <State>CA</State>  
      <Zip>10999</Zip>  
      <Country>USA</Country>  
    </Address>  
    <Address Type="Billing">  
      <Name>Tai Yee</Name>  
      <Street>8 Oak Avenue</Street>  
      <City>Old Town</City>  
      <State>PA</State>  
      <Zip>95819</Zip>  
      <Country>USA</Country>  
    </Address>  
    <DeliveryNotes>Please leave packages in shed by driveway.</DeliveryNotes>  
    <Items>  
      <Item PartNumber="872-AA">  
        <ProductName>Lawnmower</ProductName>  
        <Quantity>1</Quantity>  
        <USPrice>148.95</USPrice>  
        <Comment>Confirm this is electric</Comment>  
      </Item>  
      <Item PartNumber="926-AA">  
        <ProductName>Baby Monitor</ProductName>  
        <Quantity>2</Quantity>  
        <USPrice>39.98</USPrice>  
        <ShipDate>1999-05-21</ShipDate>  
      </Item>  
    </Items>  
  </PurchaseOrder>  
  <PurchaseOrder PurchaseOrderNumber="99505" OrderDate="1999-10-22">  
    <Address Type="Shipping">  
      <Name>Cristian Osorio</Name>  
      <Street>456 Main Street</Street>  
      <City>Buffalo</City>  
      <State>NY</State>  
      <Zip>98112</Zip>  
      <Country>USA</Country>  
    </Address>  
    <Address Type="Billing">  
      <Name>Cristian Osorio</Name>  
      <Street>456 Main Street</Street>  
      <City>Buffalo</City>  
      <State>NY</State>  
      <Zip>98112</Zip>  
      <Country>USA</Country>  
    </Address>  
    <DeliveryNotes>Please notify me before shipping.</DeliveryNotes>  
    <Items>  
      <Item PartNumber="456-NM">  
        <ProductName>Power Supply</ProductName>  
        <Quantity>1</Quantity>  
        <USPrice>45.99</USPrice>  
      </Item>  
    </Items>  
  </PurchaseOrder>  
  <PurchaseOrder PurchaseOrderNumber="99504" OrderDate="1999-10-22">  
    <Address Type="Shipping">  
      <Name>Jessica Arnold</Name>  
      <Street>4055 Madison Ave</Street>  
      <City>Seattle</City>  
      <State>WA</State>  
      <Zip>98112</Zip>  
      <Country>USA</Country>  
    </Address>  
    <Address Type="Billing">  
      <Name>Jessica Arnold</Name>  
      <Street>4055 Madison Ave</Street>  
      <City>Buffalo</City>  
      <State>NY</State>  
      <Zip>98112</Zip>  
      <Country>USA</Country>  
    </Address>  
    <Items>  
      <Item PartNumber="898-AZ">  
        <ProductName>Computer Keyboard</ProductName>  
        <Quantity>1</Quantity>  
        <USPrice>29.99</USPrice>  
      </Item>  
      <Item PartNumber="898-AM">  
        <ProductName>Wireless Mouse</ProductName>  
        <Quantity>1</Quantity>  
        <USPrice>14.99</USPrice>  
      </Item>  
    </Items>  
  </PurchaseOrder>  
</PurchaseOrders>  
```  
  
## <a name="see-also"></a>请参阅

- [示例 XML 文档 (LINQ to XML)](../../../../csharp/programming-guide/concepts/linq/sample-xml-documents-linq-to-xml.md)
