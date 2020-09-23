---
title: Część stylu dokumentu WordprocessingML — LINQ to XML
description: Zapoznaj się z przykładem XML, który stanowi część stylu dokumentu Office Open XML WordprocessingML.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 5458bccf-3898-4661-904b-7d280c9239a9
ms.openlocfilehash: 9283a62014b8d035f717f506dcf8a5850981abb5
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/08/2020
ms.locfileid: "89553251"
---
# <a name="style-part-of-a-wordprocessingml-document-linq-to-xml"></a><span data-ttu-id="f4347-103">Część stylu dokumentu WordprocessingML (LINQ to XML)</span><span class="sxs-lookup"><span data-stu-id="f4347-103">Style part of a WordprocessingML document (LINQ to XML)</span></span>

<span data-ttu-id="f4347-104">W tym artykule przedstawiono przykładowy kod XML, który stanowi część stylu dokumentu Office Open XML WordprocessingML.</span><span class="sxs-lookup"><span data-stu-id="f4347-104">This article shows an example of the XML that makes up the style part of an Office Open XML WordprocessingML document.</span></span>

## <a name="example-the-xml-that-makes-up-the-style-part-of-a-document"></a><span data-ttu-id="f4347-105">Przykład: kod XML, który stanowi część stylu dokumentu</span><span class="sxs-lookup"><span data-stu-id="f4347-105">Example: The XML that makes up the style part of a document</span></span>

<span data-ttu-id="f4347-106">Poniższy przykład to kod XML, który stanowi część stylu dokumentu Office Open XML WordprocessingML.</span><span class="sxs-lookup"><span data-stu-id="f4347-106">The following example is the XML that makes up the style part of an Office Open XML WordprocessingML document.</span></span>

<span data-ttu-id="f4347-107">Domyślny styl akapitu ma element z następującym tagiem otwierającym:</span><span class="sxs-lookup"><span data-stu-id="f4347-107">The default paragraph style has an element with the following opening tag:</span></span>

```xml
<w:style w:type="paragraph" w:default="1" w:styleId="Normal">
```

<span data-ttu-id="f4347-108">Musisz znać te informacje podczas pisania zapytania, aby znaleźć domyślny identyfikator stylu, aby zapytanie mogło identyfikować styl akapitów, które mają styl domyślny.</span><span class="sxs-lookup"><span data-stu-id="f4347-108">You need to know this information when you write the query to find the default style identifier, so that the query can identify the style of paragraphs that have the default style.</span></span>

<span data-ttu-id="f4347-109">Należy pamiętać, że te dokumenty są bardzo proste w porównaniu z typowymi dokumentami wygenerowanymi przez program Microsoft Word.</span><span class="sxs-lookup"><span data-stu-id="f4347-109">Note that these documents are very simple when compared to typical documents that Microsoft Word generates.</span></span> <span data-ttu-id="f4347-110">W wielu przypadkach program Word zapisuje znaczną część dodatkowych informacji, dodatkowego formatowania i metadanych.</span><span class="sxs-lookup"><span data-stu-id="f4347-110">In many cases, Word saves a great deal of additional information, additional formatting, and metadata.</span></span> <span data-ttu-id="f4347-111">Ponadto program Word nie sformatuje wierszy, aby można je było łatwo odczytać, jak w tym przykładzie. Zamiast tego, kod XML jest zapisywany bez wcięcia.</span><span class="sxs-lookup"><span data-stu-id="f4347-111">Furthermore, Word doesn't format the lines to be easily readable as in this example; instead, the XML is saved without indentation.</span></span> <span data-ttu-id="f4347-112">Jednak wszystkie dokumenty WordprocessingML korzystają z tego samego podstawowego kształtu XML.</span><span class="sxs-lookup"><span data-stu-id="f4347-112">However, all WordprocessingML documents share the same basic XML shape.</span></span> <span data-ttu-id="f4347-113">Z tego powodu zapytania przedstawione w tej sekcji będą działały z bardziej skomplikowanymi dokumentami.</span><span class="sxs-lookup"><span data-stu-id="f4347-113">Because of this, the queries presented in this section will work with more complicated documents.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<w:styles
    xmlns:r="http://schemas.openxmlformats.org/officeDocument/2006/relationships"
    xmlns:w="http://schemas.openxmlformats.org/wordprocessingml/2006/main">
  <w:docDefaults>
    <w:rPrDefault>
      <w:rPr>
        <w:rFonts
            w:ascii="Times New Roman"
            w:eastAsia="Times New Roman"
            w:hAnsi="Times New Roman"
            w:cs="Times New Roman" />
        <w:sz w:val="22" />
        <w:szCs w:val="22" />
        <w:lang w:val="en-US" w:eastAsia="en-US" w:bidi="ar-SA" />
      </w:rPr>
    </w:rPrDefault>
    <w:pPrDefault />
  </w:docDefaults>
  <w:style w:type="paragraph" w:default="1" w:styleId="Normal">
    <w:name w:val="Normal" />
    <w:qFormat />
    <w:rPr>
      <w:sz w:val="24" />
      <w:szCs w:val="24" />
    </w:rPr>
  </w:style>
  <w:style w:type="paragraph" w:styleId="Heading1">
    <w:name w:val="heading 1" />
    <w:basedOn w:val="Normal" />
    <w:next w:val="Normal" />
    <w:link w:val="Heading1Char" />
    <w:uiPriority w:val="99" />
    <w:qFormat />
    <w:rsid w:val="006027C7" />
    <w:pPr>
      <w:keepNext />
      <w:spacing w:before="240" w:after="60" />
      <w:outlineLvl w:val="0" />
    </w:pPr>
    <w:rPr>
      <w:rFonts w:ascii="Arial" w:hAnsi="Arial" w:cs="Arial" />
      <w:b />
      <w:bCs />
      <w:kern w:val="32" />
      <w:sz w:val="32" />
      <w:szCs w:val="32" />
    </w:rPr>
  </w:style>
  <w:style w:type="character" w:default="1" w:styleId="DefaultParagraphFont">
    <w:name w:val="Default Paragraph Font" />
    <w:uiPriority w:val="99" />
    <w:semiHidden />
  </w:style>
  <w:style w:type="table" w:default="1" w:styleId="TableNormal">
    <w:name w:val="Normal Table" />
    <w:uiPriority w:val="99" />
    <w:semiHidden />
    <w:unhideWhenUsed />
    <w:qFormat />
    <w:tblPr>
      <w:tblInd w:w="0" w:type="dxa" />
      <w:tblCellMar>
        <w:top w:w="0" w:type="dxa" />
        <w:left w:w="108" w:type="dxa" />
        <w:bottom w:w="0" w:type="dxa" />
        <w:right w:w="108" w:type="dxa" />
      </w:tblCellMar>
    </w:tblPr>
  </w:style>
  <w:style w:type="numbering" w:default="1" w:styleId="NoList">
    <w:name w:val="No List" />
    <w:uiPriority w:val="99" />
    <w:semiHidden />
    <w:unhideWhenUsed />
  </w:style>
  <w:style w:type="character" w:customStyle="1" w:styleId="Heading1Char">
    <w:name w:val="Heading 1 Char" />
    <w:basedOn w:val="DefaultParagraphFont" />
    <w:link w:val="Heading1" />
    <w:uiPriority w:val="9" />
    <w:rsid w:val="009765E3" />
    <w:rPr>
      <w:rFonts
          w:asciiTheme="majorHAnsi"
          w:eastAsiaTheme="majorEastAsia"
          w:hAnsiTheme="majorHAnsi"
          w:cstheme="majorBidi" />
      <w:b />
      <w:bCs />
      <w:kern w:val="32" />
      <w:sz w:val="32" />
      <w:szCs w:val="32" />
    </w:rPr>
  </w:style>
  <w:style w:type="paragraph" w:customStyle="1" w:styleId="Code">
    <w:name w:val="Code" />
    <w:aliases w:val="c" />
    <w:uiPriority w:val="99" />
    <w:rsid w:val="006027C7" />
    <w:pPr>
      <w:spacing w:after="60" w:line="300" w:lineRule="exact" />
    </w:pPr>
    <w:rPr>
      <w:rFonts w:ascii="Courier New" w:hAnsi="Courier New" />
      <w:noProof />
      <w:color w:val="000080" />
      <w:sz w:val="20" />
      <w:szCs w:val="20" />
    </w:rPr>
  </w:style>
</w:styles>
```