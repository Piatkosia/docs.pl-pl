---
title: <add>element dla NameValueSectionHandler i DictionarySectionHandler
ms.date: 05/01/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/sectionName/add
helpviewer_keywords:
- add Element
- <add> Element
ms.assetid: 0d4ddb53-eb2b-49c0-9c33-a8dec5c39b46
ms.openlocfilehash: 57722f3518fad12cb8e6e35d68f40bb8465bdd86
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2020
ms.locfileid: "77215439"
---
# <a name="add-element-for-namevaluesectionhandler-and-dictionarysectionhandler"></a>\<add>element dla NameValueSectionHandler i DictionarySectionHandler

Dodaje niestandardowe ustawienia aplikacji. Każdy **\<add>** tag zawiera parę klucz/wartość.

[**\<configuration>**](configuration-element.md)\
&nbsp;&nbsp;[**\<sectionName>**](custom-element-2.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<add>**

## <a name="syntax"></a>Składnia

```xml
<add key="key" value="value" />
```

## <a name="attributes"></a>Atrybuty

| Atrybut | Opis |
| --------- | ----------- |
| **głównych**   | Atrybut wymagany.<br><br>Określa nazwę ustawienia. |
| **wartościami** | Atrybut wymagany.<br><br>Określa wartość ustawienia. |

## <a name="parent-element"></a>Element nadrzędny

| Element | Opis |
| ------- | ------------|
| [**\<sectionName>** Postaci](custom-element-2.md) | Definiuje ustawienia niestandardowych sekcji konfiguracji, które używają <xref:System.Configuration.NameValueSectionHandler> klas i <xref:System.Configuration.DictionarySectionHandler> . |

## <a name="child-elements"></a>Elementy podrzędne

Brak

## <a name="example"></a>Przykład

Poniższy przykład pokazuje, jak zdefiniować sekcję konfiguracji niestandardowej i użyć **\<add>** elementu, aby umieścić ustawienia w sekcji:

```xml
<configuration>
  <configSections>
    <section name="dictionarySample" type="System.Configuration.DictionarySectionHandler,System" />
  </configSections>
  <dictionarySample>
    <add key="myKey" value="myValue" />
  </dictionarySample>
</configuration>
```

## <a name="configuration-file"></a>Plik konfiguracji

Tego elementu można użyć w pliku konfiguracyjnym aplikacji, pliku konfiguracji komputera (*Machine. config*) i plikach *Web. config* , które nie znajdują się na poziomie katalogu aplikacji.

## <a name="see-also"></a>Zobacz także

- [Schemat pliku konfiguracji dla .NET Framework](index.md)
