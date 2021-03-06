---
title: Jak sortować elementy w wielu kluczach — LINQ to XML
description: Dowiedz się, jak sortować elementy XML dla wielu kluczy.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 3b2760b6-d607-4ac7-b784-5c6524e2a0e0
ms.openlocfilehash: 161f354192b3bc5cecec7e7e1b457b23c415c073
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90550129"
---
# <a name="how-to-sort-elements-on-multiple-keys-linq-to-xml"></a>Jak sortować elementy w wielu kluczach (LINQ to XML)

W tym artykule przedstawiono sposób sortowania wielu kluczy w języku C# i Visual Basic.

## <a name="example-sort-xml-elements-on-multiple-keys"></a>Przykład: Sortuj elementy XML w wielu kluczach

Ten przykład sortuje w dwóch kluczach: kod pocztowy (podstawowy) i Data zamówienia. Używa [przykładowego pliku XML dokumentu XML: klienci i zamówienia](sample-xml-file-customers-orders.md).

```csharp
XElement co = XElement.Load("CustomersOrders.xml");
var sortedElements =
    from c in co.Element("Orders").Elements("Order")
    orderby (string)c.Element("ShipInfo").Element("ShipPostalCode"),
            (DateTime)c.Element("OrderDate")
    select new {
        CustomerID = (string)c.Element("CustomerID"),
        EmployeeID = (string)c.Element("EmployeeID"),
        ShipPostalCode = (string)c.Element("ShipInfo").Element("ShipPostalCode"),
        OrderDate = (DateTime)c.Element("OrderDate")
    };
foreach (var r in sortedElements)
    Console.WriteLine("CustomerID:{0} EmployeeID:{1} ShipPostalCode:{2} OrderDate:{3:d}",
        r.CustomerID, r.EmployeeID, r.ShipPostalCode, r.OrderDate);
```

```vb
Dim co As XElement = XElement.Load("CustomersOrders.xml")
Dim result = _
    From c In co.<Orders>.<Order> _
    Order By c.<ShipInfo>.<ShipPostalCode>.Value, Convert.ToDateTime(c.<OrderDate>.Value) _
    Select New With { _
        .CustomerID = c.<CustomerID>.Value, _
        .EmployeeID = c.<EmployeeID>.Value, _
        .ShipPostalCode = c.<ShipInfo>.<ShipPostalCode>.Value, _
        .OrderDate = Convert.ToDateTime(c.<OrderDate>.Value) _
    }
For Each r In result
    Console.WriteLine("CustomerID:{0} EmployeeID:{1} ShipPostalCode:{2} OrderDate:{3:d}", _
                r.CustomerID, r.EmployeeID, r.ShipPostalCode, r.OrderDate)
Next
```

Ten przykład generuje następujące wyniki:

```output
CustomerID:LETSS EmployeeID:1 ShipPostalCode:94117 OrderDate:6/25/1997
CustomerID:LETSS EmployeeID:8 ShipPostalCode:94117 OrderDate:10/27/1997
CustomerID:LETSS EmployeeID:6 ShipPostalCode:94117 OrderDate:11/10/1997
CustomerID:LETSS EmployeeID:4 ShipPostalCode:94117 OrderDate:2/12/1998
CustomerID:GREAL EmployeeID:6 ShipPostalCode:97403 OrderDate:5/6/1997
CustomerID:GREAL EmployeeID:8 ShipPostalCode:97403 OrderDate:7/4/1997
CustomerID:GREAL EmployeeID:1 ShipPostalCode:97403 OrderDate:7/31/1997
CustomerID:GREAL EmployeeID:4 ShipPostalCode:97403 OrderDate:7/31/1997
CustomerID:GREAL EmployeeID:6 ShipPostalCode:97403 OrderDate:9/4/1997
CustomerID:GREAL EmployeeID:3 ShipPostalCode:97403 OrderDate:9/25/1997
CustomerID:GREAL EmployeeID:4 ShipPostalCode:97403 OrderDate:1/6/1998
CustomerID:GREAL EmployeeID:3 ShipPostalCode:97403 OrderDate:3/9/1998
CustomerID:GREAL EmployeeID:3 ShipPostalCode:97403 OrderDate:4/7/1998
CustomerID:GREAL EmployeeID:4 ShipPostalCode:97403 OrderDate:4/22/1998
CustomerID:GREAL EmployeeID:4 ShipPostalCode:97403 OrderDate:4/30/1998
CustomerID:HUNGC EmployeeID:3 ShipPostalCode:97827 OrderDate:12/6/1996
CustomerID:HUNGC EmployeeID:1 ShipPostalCode:97827 OrderDate:12/25/1996
CustomerID:HUNGC EmployeeID:3 ShipPostalCode:97827 OrderDate:1/15/1997
CustomerID:HUNGC EmployeeID:4 ShipPostalCode:97827 OrderDate:7/16/1997
CustomerID:HUNGC EmployeeID:8 ShipPostalCode:97827 OrderDate:9/8/1997
CustomerID:LAZYK EmployeeID:1 ShipPostalCode:99362 OrderDate:3/21/1997
CustomerID:LAZYK EmployeeID:8 ShipPostalCode:99362 OrderDate:5/22/1997
```

## <a name="example-sort-xml-thats-in-a-namespace"></a>Przykład: Sortuj kod XML, który znajduje się w przestrzeni nazw

Ten przykład wykonuje takie samo sortowanie jak pierwszy, ale dla XML, który znajduje się w przestrzeni nazw. Używa [przykładowego pliku XML dokumentu XML: klienci i zamówienia w przestrzeni nazw](sample-xml-file-customers-orders-namespace.md).

Aby uzyskać więcej informacji, zobacz [Omówienie przestrzeni nazw](namespaces-overview.md).

```csharp
XElement co = XElement.Load("CustomersOrdersInNamespace.xml");
XNamespace aw = "http://www.adventure-works.com";
var sortedElements =
    from c in co.Element(aw + "Orders").Elements(aw + "Order")
    orderby (string)c.Element(aw + "ShipInfo").Element(aw + "ShipPostalCode"),
            (DateTime)c.Element(aw + "OrderDate")
    select new
    {
        CustomerID = (string)c.Element(aw + "CustomerID"),
        EmployeeID = (string)c.Element(aw + "EmployeeID"),
        ShipPostalCode = (string)c.Element(aw + "ShipInfo").Element(aw + "ShipPostalCode"),
        OrderDate = (DateTime)c.Element(aw + "OrderDate")
    };
foreach (var r in sortedElements)
    Console.WriteLine("CustomerID:{0} EmployeeID:{1} ShipPostalCode:{2} OrderDate:{3:d}",
        r.CustomerID, r.EmployeeID, r.ShipPostalCode, r.OrderDate);
```

```vb
Imports <xmlns='http://www.adventure-works.com'>

Module Module1
    Sub Main()
        Dim co As XElement = XElement.Load("CustomersOrdersInNamespace.xml")
        Dim result = _
            From c In co.<Orders>.<Order> _
            Order By c.<ShipInfo>.<ShipPostalCode>.Value, Convert.ToDateTime(c.<OrderDate>.Value) _
            Select New With { _
                .CustomerID = c.<CustomerID>.Value, _
                .EmployeeID = c.<EmployeeID>.Value, _
                .ShipPostalCode = c.<ShipInfo>.<ShipPostalCode>.Value, _
                .OrderDate = Convert.ToDateTime(c.<OrderDate>.Value) _
            }
        For Each r In result
            Console.WriteLine("CustomerID:{0} EmployeeID:{1} ShipPostalCode:{2} OrderDate:{3:d}", _
                        r.CustomerID, r.EmployeeID, r.ShipPostalCode, r.OrderDate)
        Next
    End Sub
End Module
```

Ten przykład generuje następujące wyniki:

```output
CustomerID:LETSS EmployeeID:1 ShipPostalCode:94117 OrderDate:6/25/1997
CustomerID:LETSS EmployeeID:8 ShipPostalCode:94117 OrderDate:10/27/1997
CustomerID:LETSS EmployeeID:6 ShipPostalCode:94117 OrderDate:11/10/1997
CustomerID:LETSS EmployeeID:4 ShipPostalCode:94117 OrderDate:2/12/1998
CustomerID:GREAL EmployeeID:6 ShipPostalCode:97403 OrderDate:5/6/1997
CustomerID:GREAL EmployeeID:8 ShipPostalCode:97403 OrderDate:7/4/1997
CustomerID:GREAL EmployeeID:1 ShipPostalCode:97403 OrderDate:7/31/1997
CustomerID:GREAL EmployeeID:4 ShipPostalCode:97403 OrderDate:7/31/1997
CustomerID:GREAL EmployeeID:6 ShipPostalCode:97403 OrderDate:9/4/1997
CustomerID:GREAL EmployeeID:3 ShipPostalCode:97403 OrderDate:9/25/1997
CustomerID:GREAL EmployeeID:4 ShipPostalCode:97403 OrderDate:1/6/1998
CustomerID:GREAL EmployeeID:3 ShipPostalCode:97403 OrderDate:3/9/1998
CustomerID:GREAL EmployeeID:3 ShipPostalCode:97403 OrderDate:4/7/1998
CustomerID:GREAL EmployeeID:4 ShipPostalCode:97403 OrderDate:4/22/1998
CustomerID:GREAL EmployeeID:4 ShipPostalCode:97403 OrderDate:4/30/1998
CustomerID:HUNGC EmployeeID:3 ShipPostalCode:97827 OrderDate:12/6/1996
CustomerID:HUNGC EmployeeID:1 ShipPostalCode:97827 OrderDate:12/25/1996
CustomerID:HUNGC EmployeeID:3 ShipPostalCode:97827 OrderDate:1/15/1997
CustomerID:HUNGC EmployeeID:4 ShipPostalCode:97827 OrderDate:7/16/1997
CustomerID:HUNGC EmployeeID:8 ShipPostalCode:97827 OrderDate:9/8/1997
CustomerID:LAZYK EmployeeID:1 ShipPostalCode:99362 OrderDate:3/21/1997
CustomerID:LAZYK EmployeeID:8 ShipPostalCode:99362 OrderDate:5/22/1997
```

## <a name="see-also"></a>Zobacz także

- [Zapytania podstawowe (LINQ to XML) (Visual Basic)](./find-element-specific-attribute.md)
