---
ms.openlocfilehash: 48d2f1b5fa2eced30d3c9fb65804268904f11ab8
ms.sourcegitcommit: a69d548f90a03e105ee6701236c38390ecd9ccd1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/14/2020
ms.locfileid: "90065070"
---
### <a name="unicode-category-changed-for-some-latin-1-characters"></a>Zmieniono kategorię Unicode dla niektórych znaków łacińskich 1

<xref:System.Char> Metody teraz zwracają poprawną kategorię Unicode dla znaków w zakresie łaciński-1. Kategoria jest zgodna z normą standardu Unicode.

#### <a name="change-description"></a>Zmień opis

W poprzednich wersjach .NET, <xref:System.Char> metody używały ustalonej listy kategorii Unicode dla znaków w zakresie łaciński-1. Jednak standard Unicode zmienił kategorie niektórych z tych znaków, ponieważ te interfejsy API zostały zaimplementowane, tworząc niezgodność. Ponadto istnieje również rozbieżność między <xref:System.Char> i <xref:System.Globalization.CharUnicodeInfo> interfejsami API, które są zgodne ze standardem Unicode. W programie .NET 5,0 i jego nowszych wersjach <xref:System.Char> metody używają i zwracają kategorię Unicode zgodną ze standardem Unicode dla wszystkich znaków.

W poniższej tabeli przedstawiono znaki, których kategorie Unicode zostały zmienione w programie .NET 5,0:

| Znak    | Kategoria Unicode<br>w poprzednich wersjach programu .NET | Kategoria Unicode<br>w programie .NET 5,0 i jego nowszych wersjach |
|:------------:|:---------------------------------------------:|:--------------------------------------------------:|
| § (\u00a7)   | `OtherSymbol`                                 | `OtherPunctuation`                                 |
| ª (\u00aa)   | `LowercaseLetter`                             | `OtherLetter`                                      |
| LUBISZ (\u00ad) | `DashPunctuation`                             | `Format`                                           |
| ¶ (\u00b6)   | `OtherSymbol`                                 | `OtherPunctuation`                                 |
| € (\u00ba)   | `LowercaseLetter`                             | `OtherLetter`                                      |

#### <a name="version-introduced"></a>Wprowadzona wersja

.NET 5,0 RC1

#### <a name="recommended-action"></a>Zalecana akcja

Jeśli masz kod, który pobiera kategorię znaku Unicode przy użyciu <xref:System.Char> klasy i zakłada, że Kategoria nigdy nie ulegnie zmianie, może być konieczne jej zaktualizowanie.

#### <a name="reason-for-change"></a>Przyczyna zmiany

Ta zmiana została wprowadzona w taki sposób, aby kategorie zwracane przez <xref:System.Char> Typ były zgodne ze standardem Unicode i <xref:System.Globalization.CharUnicodeInfo> typem.

#### <a name="category"></a>Kategoria

- Podstawowe biblioteki platformy .NET
- Globalizacja

#### <a name="affected-apis"></a>Dotyczy interfejsów API

- <xref:System.Char.GetUnicodeCategory%2A?displayProperty=fullName>
- <xref:System.Char.IsLetter%2A?displayProperty=fullName>
- <xref:System.Char.IsPunctuation%2A?displayProperty=fullName>
- <xref:System.Char.IsSymbol%2A?displayProperty=fullName>
- <xref:System.Char.IsLower%2A?displayProperty=fullName>

Ponadto ta zmiana ma wpływ na każdą klasę, która jest zależna od elementu w <xref:System.Char> celu uzyskania kategorii znaków Unicode, na przykład <xref:System.Text.RegularExpressions.Regex> .

<!--

#### Affected APIs

- `Overload:System.Char.GetUnicodeCategory`
- `Overload:System.Char.IsLetter`
- `Overload:System.Char.IsPunctuation`
- `Overload:System.Char.IsSymbol`
- `Overload:System.Char.IsLower`

-->
