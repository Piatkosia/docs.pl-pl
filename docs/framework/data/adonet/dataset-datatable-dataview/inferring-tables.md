---
title: Wnioskowanie tabel
ms.date: 03/30/2017
ms.assetid: 74a288d4-b8e9-4f1a-b2cd-10df92c1ed1f
ms.openlocfilehash: 4a3d7b239dbc405cf2acae967b5be401dc772e38
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91177556"
---
# <a name="inferring-tables"></a>Wnioskowanie tabel

Gdy wywnioskowano schemat dla programu <xref:System.Data.DataSet> z dokumentu XML, ADO.net najpierw określa, które elementy XML reprezentują tabele. Poniższe struktury XML powodują powstanie tabeli dla schematu **zestawu danych** :  
  
- Elementy z atrybutami  
  
- Elementy z elementami podrzędnymi  
  
- Powtarzające się elementy  
  
## <a name="elements-with-attributes"></a>Elementy z atrybutami  

 Elementy, które mają określone atrybuty, powodują wywnioskowane tabele. Rozważmy na przykład następujący kod XML:  
  
```xml  
<DocumentElement>  
  <Element1 attr1="value1"/>  
  <Element1 attr1="value2">Text1</Element1>  
</DocumentElement>  
```  
  
 Proces wnioskowania tworzy tabelę o nazwie "element1".  
  
 **Zestaw danych:** DocumentElement  
  
 **Tabela:** Element1  
  
|attr1|Element1_Text|  
|-----------|--------------------|  
|sekwencj||  
|wartość2|Organizacji1|  
  
## <a name="elements-with-child-elements"></a>Elementy z elementami podrzędnymi  

 Elementy, które mają elementy podrzędne, powodują wywnioskowane tabele. Rozważmy na przykład następujący kod XML:  
  
```xml  
<DocumentElement>  
  <Element1>  
    <ChildElement1>Text1</ChildElement1>  
  </Element1>  
</DocumentElement>  
```  
  
 Proces wnioskowania tworzy tabelę o nazwie "element1".  
  
 **Zestaw danych:** DocumentElement  
  
 **Tabela:** Element1  
  
|ChildElement1|  
|-------------------|  
|Organizacji1|  
  
 Dokument lub element główny, wynik w tabeli wywnioskowanej, jeśli ma atrybuty lub elementy podrzędne, które są wywnioskowane jako kolumny. Jeśli element dokumentu nie ma żadnych atrybutów i żadne elementy podrzędne, które zostałyby wywnioskowane jako kolumny, element jest wywnioskowany jako **zestaw danych**. Rozważmy na przykład następujący kod XML:  
  
```xml  
<DocumentElement>  
  <Element1>Text1</Element1>  
  <Element2>Text2</Element2>  
</DocumentElement>  
```  
  
 Proces wnioskowania tworzy tabelę o nazwie "DocumentElement".  
  
 **Zestaw danych:** NewDataSet  
  
 **Tabela:** DocumentElement  
  
|Element1|Element2|  
|--------------|--------------|  
|Organizacji1|Text2|  
  
 Alternatywnie należy wziąć pod uwagę następujące elementy XML:  
  
```xml  
<DocumentElement>  
  <Element1 attr1="value1" attr2="value2"/>  
</DocumentElement>  
```  
  
 Proces wnioskowania generuje **zestaw danych** o nazwie "DocumentElement", który zawiera tabelę o nazwie "element1".  
  
 **Zestaw danych:** DocumentElement  
  
 **Tabela:** Element1  
  
|attr1|attr2|  
|-----------|-----------|  
|sekwencj|wartość2|  
  
## <a name="repeating-elements"></a>Powtarzające się elementy  

 Elementy powtarzające się powodują powstanie pojedynczej tabeli wywnioskowanej. Rozważmy na przykład następujący kod XML:  
  
```xml  
<DocumentElement>  
  <Element1>Text1</Element1>  
  <Element1>Text2</Element1>  
</DocumentElement>  
```  
  
 Proces wnioskowania tworzy tabelę o nazwie "element1".  
  
 **Zestaw danych:** DocumentElement  
  
 **Tabela:** Element1  
  
|Element1_Text|  
|--------------------|  
|Organizacji1|  
|Text2|  
  
## <a name="see-also"></a>Zobacz też

- [Wnioskowanie relacyjnej struktury elementu DataSet z pliku XML](inferring-dataset-relational-structure-from-xml.md)
- [Ładowanie elementu DataSet z pliku XML](loading-a-dataset-from-xml.md)
- [Ładowanie informacji o schemacie elementu DataSet z pliku XML](loading-dataset-schema-information-from-xml.md)
- [Używanie języka XML w elemencie DataSet](using-xml-in-a-dataset.md)
- [Elementy DataSet, DataTable i DataView](index.md)
- [Omówienie ADO.NET](../ado-net-overview.md)
