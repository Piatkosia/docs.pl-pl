---
title: Przykład, który wyprowadza fragmenty dokumentu Office Open XML — LINQ to XML
description: Dowiedz się, jak otworzyć dokument pakietu Office Open XML i uzyskać dostęp do jego części.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 6cd37055-89b4-42e8-bf27-5a29717e35f3
ms.openlocfilehash: 68ecdc573eaafd706c3082c736243874cb8dcc30
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/08/2020
ms.locfileid: "89552915"
---
# <a name="example-that-outputs-office-open-xml-document-parts-linq-to-xml"></a>Przykład, w którym są wyprowadzane części dokumentu Office Open XML (LINQ to XML)

W tym artykule przedstawiono sposób otwierania dokumentu Office Open XML i uzyskiwania dostępu do jego części.

## <a name="example-print-the-document-and-style-parts-of-an-office-open-xml-document"></a>Przykład: Drukuj elementy Document i style dokumentu Office Open XML

Poniższy przykład otwiera dokument Office Open XML i drukuje części dokumentu i stylów.

W tym przykładzie zastosowano klasy z zestawu 'Windowsbase oraz typy z <xref:System.IO.Packaging?displayProperty=nameWithType> przestrzeni nazw.

```csharp
const string fileName = "SampleDoc.docx";

const string documentRelationshipType =
  "http://schemas.openxmlformats.org/officeDocument/2006/relationships/officeDocument";
const string stylesRelationshipType =
  "http://schemas.openxmlformats.org/officeDocument/2006/relationships/styles";
const string wordmlNamespace =
  "http://schemas.openxmlformats.org/wordprocessingml/2006/main";
XNamespace w = wordmlNamespace;

using (Package wdPackage = Package.Open(fileName, FileMode.Open, FileAccess.Read))
{
    PackageRelationship docPackageRelationship =
      wdPackage.GetRelationshipsByType(documentRelationshipType).FirstOrDefault();
    if (docPackageRelationship != null)
    {
        Uri documentUri = PackUriHelper.ResolvePartUri(new Uri("/", UriKind.Relative),
          docPackageRelationship.TargetUri);
        PackagePart documentPart = wdPackage.GetPart(documentUri);

        //  Load the document XML in the part into an XDocument instance.
        XDocument xdoc = XDocument.Load(XmlReader.Create(documentPart.GetStream()));

        Console.WriteLine("TargetUri:{0}", docPackageRelationship.TargetUri);
        Console.WriteLine("==================================================================");
        Console.WriteLine(xdoc.Root);
        Console.WriteLine();

        //  Find the styles part. There will only be one.
        PackageRelationship styleRelation =
          documentPart.GetRelationshipsByType(stylesRelationshipType).FirstOrDefault();
        if (styleRelation != null)
        {
            Uri styleUri = PackUriHelper.ResolvePartUri(documentUri, styleRelation.TargetUri);
            PackagePart stylePart = wdPackage.GetPart(styleUri);

            //  Load the style XML in the part into an XDocument instance.
            XDocument styleDoc = XDocument.Load(XmlReader.Create(stylePart.GetStream()));

            Console.WriteLine("TargetUri:{0}", styleRelation.TargetUri);
            Console.WriteLine("==================================================================");
            Console.WriteLine(styleDoc.Root);
            Console.WriteLine();
        }
    }
}
```

```vb
Const fileName As String = "SampleDoc.docx"

Const documentRelationshipType As String = _
  "http://schemas.openxmlformats.org/officeDocument/2006/relationships/officeDocument"
Const stylesRelationshipType As String = _
  "http://schemas.openxmlformats.org/officeDocument/2006/relationships/styles"
Const wordmlNamespace As String = _
  "http://schemas.openxmlformats.org/wordprocessingml/2006/main"
Dim w As XNamespace = wordmlNamespace

Using wdPackage As Package = Package.Open(fileName, FileMode.Open, FileAccess.Read)
    Dim docPackageRelationship As PackageRelationship = _
      wdPackage.GetRelationshipsByType(documentRelationshipType).FirstOrDefault()
    If docPackageRelationship IsNot Nothing Then
        Dim documentUri As Uri = PackUriHelper.ResolvePartUri(New Uri("/", UriKind.Relative), _
          docPackageRelationship.TargetUri)
        Dim documentPart As PackagePart = wdPackage.GetPart(documentUri)

        ' Load the document XML in the part into an XDocument instance.
        Dim xdoc As XDocument = XDocument.Load(XmlReader.Create(documentPart.GetStream()))

        Console.WriteLine("TargetUri:{0}", docPackageRelationship.TargetUri)
        Console.WriteLine("==================================================================")
        Console.WriteLine(xdoc.Root)
        Console.WriteLine()

        ' Find the styles part. There will only be one.
        Dim styleRelation As PackageRelationship = _
          documentPart.GetRelationshipsByType(stylesRelationshipType).FirstOrDefault()
        If styleRelation IsNot Nothing Then
            Dim styleUri As Uri = _
              PackUriHelper.ResolvePartUri(documentUri, styleRelation.TargetUri)
            Dim stylePart As PackagePart = wdPackage.GetPart(styleUri)

            ' Load the style XML in the part into an XDocument instance.
            Dim styleDoc As XDocument = XDocument.Load(XmlReader.Create(stylePart.GetStream()))

            Console.WriteLine("TargetUri:{0}", styleRelation.TargetUri)
            Console.WriteLine("==================================================================")
            Console.WriteLine(styleDoc.Root)
            Console.WriteLine()
        End If
    End If
End Using
```
