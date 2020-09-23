---
title: 'Przykładowy plik XML: dane liczbowe w przestrzeni nazw — LINQ to XML'
description: Ten plik XML — który jest używany w przykładach — zawiera dane liczbowe w przestrzeni nazw.
ms.date: 07/20/2015
ms.assetid: 51750cab-3c66-4511-90fb-b9d211308d31
ms.openlocfilehash: 11e0d15ebd0bd0e34d76f78ed4f9980b05d1a47a
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/08/2020
ms.locfileid: "89553592"
---
# <a name="sample-xml-file-numerical-data-in-a-namespace-linq-to-xml"></a><span data-ttu-id="97d99-103">Przykładowy plik XML: dane liczbowe w przestrzeni nazw (LINQ to XML)</span><span class="sxs-lookup"><span data-stu-id="97d99-103">Sample XML file: Numerical data in a namespace (LINQ to XML)</span></span>

<span data-ttu-id="97d99-104">Poniższy plik XML jest używany w różnych przykładach w dokumentacji LINQ to XML.</span><span class="sxs-lookup"><span data-stu-id="97d99-104">The following XML file is used in various examples in the LINQ to XML documentation.</span></span> <span data-ttu-id="97d99-105">Ten plik zawiera dane liczbowe dla sumowania, uśredniania i grupowania.</span><span class="sxs-lookup"><span data-stu-id="97d99-105">This file contains numerical data for summing, averaging, and grouping.</span></span> <span data-ttu-id="97d99-106">KOD XML znajduje się w przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="97d99-106">The XML is in a namespace.</span></span>

## <a name="data"></a><span data-ttu-id="97d99-107">Dane</span><span class="sxs-lookup"><span data-stu-id="97d99-107">Data</span></span>

```xml
<Root xmlns='http://www.adatum.com'>
  <TaxRate>7.25</TaxRate>
  <Data>
    <Category>A</Category>
    <Quantity>3</Quantity>
    <Price>24.50</Price>
  </Data>
  <Data>
    <Category>B</Category>
    <Quantity>1</Quantity>
    <Price>89.99</Price>
  </Data>
  <Data>
    <Category>A</Category>
    <Quantity>5</Quantity>
    <Price>4.95</Price>
  </Data>
  <Data>
    <Category>A</Category>
    <Quantity>3</Quantity>
    <Price>66.00</Price>
  </Data>
  <Data>
    <Category>B</Category>
    <Quantity>10</Quantity>
    <Price>.99</Price>
  </Data>
  <Data>
    <Category>A</Category>
    <Quantity>15</Quantity>
    <Price>29.00</Price>
  </Data>
  <Data>
    <Category>B</Category>
    <Quantity>8</Quantity>
    <Price>6.99</Price>
  </Data>
</Root>
```