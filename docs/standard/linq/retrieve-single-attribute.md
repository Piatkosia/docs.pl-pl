---
title: Jak pobrać pojedynczy atrybut-LINQ to XML
description: Pobierz pojedynczy atrybut elementu pod nazwą atrybutu.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 1b6b07b9-933f-47e9-874e-e790cab49dc5
ms.openlocfilehash: a8a56ec62275f2376d19d7fc9090414b74fc77ad
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/08/2020
ms.locfileid: "89553660"
---
# <a name="how-to-retrieve-a-single-attribute-linq-to-xml"></a><span data-ttu-id="135f8-103">Pobieranie pojedynczego atrybutu (LINQ to XML)</span><span class="sxs-lookup"><span data-stu-id="135f8-103">How to retrieve a single attribute (LINQ to XML)</span></span>

<span data-ttu-id="135f8-104">W tym artykule wyjaśniono, jak pobrać pojedynczy atrybut elementu, pod nazwą atrybutu.</span><span class="sxs-lookup"><span data-stu-id="135f8-104">This article explains how to retrieve a single attribute of an element, given the attribute name.</span></span> <span data-ttu-id="135f8-105">Jest to przydatne w przypadku pisania wyrażeń zapytania, gdzie chcesz znaleźć element, który ma określony atrybut.</span><span class="sxs-lookup"><span data-stu-id="135f8-105">This is useful for writing query expressions where you want to find an element that has a particular attribute.</span></span>

<span data-ttu-id="135f8-106"><xref:System.Xml.Linq.XElement.Attribute%2A>Metoda <xref:System.Xml.Linq.XElement> klasy zwraca <xref:System.Xml.Linq.XAttribute> z określoną nazwą.</span><span class="sxs-lookup"><span data-stu-id="135f8-106">The <xref:System.Xml.Linq.XElement.Attribute%2A> method of the <xref:System.Xml.Linq.XElement> class returns the <xref:System.Xml.Linq.XAttribute> with the specified name.</span></span>

## <a name="example-retrieve-attribute-values-given-the-element-and-attribute-names"></a><span data-ttu-id="135f8-107">Przykład: pobieranie wartości atrybutów, z uwzględnieniem nazw elementów i atrybutów</span><span class="sxs-lookup"><span data-stu-id="135f8-107">Example: Retrieve attribute values, given the element and attribute names</span></span>

<span data-ttu-id="135f8-108">Poniższy przykład używa <xref:System.Xml.Linq.XElement> metody do utworzenia elementu o nazwie `PhoneNumbers` .</span><span class="sxs-lookup"><span data-stu-id="135f8-108">The following example uses the <xref:System.Xml.Linq.XElement> method to create an element named `PhoneNumbers`.</span></span> <span data-ttu-id="135f8-109">Następnie znajduje wszystkie elementy podrzędne o nazwie `Phone` i, dla każdego, używa <xref:System.Xml.Linq.XElement.Attribute%2A> metody do uzyskania i wyprowadzenia wartości atrybutu o nazwie `type` :</span><span class="sxs-lookup"><span data-stu-id="135f8-109">It then finds all the descendant elements named `Phone` and, for each, uses the <xref:System.Xml.Linq.XElement.Attribute%2A> method to obtain and output the value of the attribute named `type`:</span></span>

```csharp
XElement cust = new XElement("PhoneNumbers",
    new XElement("Phone",
        new XAttribute("type", "home"),
        "555-555-5555"),
    new XElement("Phone",
        new XAttribute("type", "work"),
        "555-555-6666")
);
IEnumerable<XElement> elList =
    from el in cust.Descendants("Phone")
    select el;
foreach (XElement el in elList)
    Console.WriteLine((string)el.Attribute("type"));
```

```vb
Dim cust As XElement = <PhoneNumbers>
                           <Phone type="home">555-555-5555</Phone>
                           <Phone type="work">555-555-6666</Phone>
                       </PhoneNumbers>
Dim elList = From el In cust...<Phone>
For Each e As XElement In elList
    Console.WriteLine(e.@type)
Next
```

<span data-ttu-id="135f8-110">Ten przykład generuje następujące wyniki:</span><span class="sxs-lookup"><span data-stu-id="135f8-110">This example produces the following output:</span></span>

```output
home
work
```

## <a name="example-retrieve-an-attribute-value-with-a-cast"></a><span data-ttu-id="135f8-111">Przykład: pobieranie wartości atrybutu z rzutowania</span><span class="sxs-lookup"><span data-stu-id="135f8-111">Example: Retrieve an attribute value with a cast</span></span>

<span data-ttu-id="135f8-112">Możesz pobrać wartość atrybutu poprzez jego rzutowanie, tak jak w przypadku <xref:System.Xml.Linq.XElement> obiektów.</span><span class="sxs-lookup"><span data-stu-id="135f8-112">You can retrieve the value of an attribute by casting it, just as you do for with <xref:System.Xml.Linq.XElement> objects.</span></span> <span data-ttu-id="135f8-113">Poniższy przykład ilustruje:</span><span class="sxs-lookup"><span data-stu-id="135f8-113">The following example demonstrates this:</span></span>

```csharp
XElement cust = new XElement("PhoneNumbers",
    new XElement("Phone",
        new XAttribute("type", "home"),
        "555-555-5555"),
    new XElement("Phone",
        new XAttribute("type", "work"),
        "555-555-6666")
);
IEnumerable<XElement> elList =
    from el in cust.Descendants("Phone")
    select el;
foreach (XElement el in elList)
    Console.WriteLine((string)el.Attribute("type"));
```

```vb
Dim cust As XElement = <PhoneNumbers>
                           <Phone type="home">555-555-5555</Phone>
                           <Phone type="work">555-555-6666</Phone>
                       </PhoneNumbers>
Dim elList As IEnumerable(Of XElement) = _
    From el In cust...<Phone> _
    Select el
For Each el As XElement In elList
    Console.WriteLine(el.@type)
Next
```

<span data-ttu-id="135f8-114">Ten przykład generuje następujące wyniki:</span><span class="sxs-lookup"><span data-stu-id="135f8-114">This example produces the following output:</span></span>

```output
home
work
```

<span data-ttu-id="135f8-115">LINQ to XML zapewnia jawne Operatory rzutowania dla klasy do,,,,,,,,, <xref:System.Xml.Linq.XAttribute> `string` `bool` `bool?` `int` `int?` `uint` `uint?` `long` `long?` `ulong` , `ulong?` , `float` , `float?` `double` `double?` `decimal` `decimal?` `DateTime` `DateTime?` `TimeSpan` `TimeSpan?` `GUID` `GUID?` ,,,,,,,,,, i.</span><span class="sxs-lookup"><span data-stu-id="135f8-115">LINQ to XML provides explicit cast operators for the <xref:System.Xml.Linq.XAttribute> class to `string`, `bool`, `bool?`, `int`, `int?`, `uint`, `uint?`, `long`, `long?`, `ulong`, `ulong?`, `float`, `float?`, `double`, `double?`, `decimal`, `decimal?`, `DateTime`, `DateTime?`, `TimeSpan`, `TimeSpan?`, `GUID`, and `GUID?`.</span></span>

## <a name="example-cast-for-an-attribute-in-a-namespace"></a><span data-ttu-id="135f8-116">Przykład: Rzutowanie atrybutu w przestrzeni nazw</span><span class="sxs-lookup"><span data-stu-id="135f8-116">Example: Cast for an attribute in a namespace</span></span>

<span data-ttu-id="135f8-117">Poniższy przykład pokazuje ten sam kod dla atrybutu, który znajduje się w przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="135f8-117">The following example shows the same code for an attribute that's in a namespace.</span></span> <span data-ttu-id="135f8-118">Aby uzyskać więcej informacji, zobacz [Omówienie przestrzeni nazw](namespaces-overview.md).</span><span class="sxs-lookup"><span data-stu-id="135f8-118">For more information, see [Namespaces overview](namespaces-overview.md).</span></span>

```csharp
XNamespace aw = "http://www.adventure-works.com";
XElement cust = new XElement(aw + "PhoneNumbers",
    new XElement(aw + "Phone",
        new XAttribute(aw + "type", "home"),
        "555-555-5555"),
    new XElement(aw + "Phone",
        new XAttribute(aw + "type", "work"),
        "555-555-6666")
);
IEnumerable<XElement> elList =
    from el in cust.Descendants(aw + "Phone")
    select el;
foreach (XElement el in elList)
    Console.WriteLine((string)el.Attribute(aw + "type"));
```

```vb
Imports <xmlns:aw="http://www.adventure-works.com">

Module Module1
    Sub Main()
        Dim cust As XElement = _
            <aw:PhoneNumbers>
                <aw:Phone aw:type="home">555-555-5555</aw:Phone>
                <aw:Phone aw:type="work">555-555-6666</aw:Phone>
            </aw:PhoneNumbers>
        Dim elList As IEnumerable(Of XElement) = _
            From el In cust...<aw:Phone> _
            Select el
        For Each el As XElement In elList
            Console.WriteLine(el.@aw:type)
        Next
    End Sub
End Module
```

<span data-ttu-id="135f8-119">Ten przykład generuje następujące wyniki:</span><span class="sxs-lookup"><span data-stu-id="135f8-119">This example produces the following output:</span></span>

```output
home
work
```

## <a name="see-also"></a><span data-ttu-id="135f8-120">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="135f8-120">See also</span></span>

- [<span data-ttu-id="135f8-121">Przegląd osi LINQ to XML</span><span class="sxs-lookup"><span data-stu-id="135f8-121">LINQ to XML axes overview</span></span>](linq-xml-axes-overview.md)