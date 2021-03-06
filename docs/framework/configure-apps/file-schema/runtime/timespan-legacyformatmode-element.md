---
title: <TimeSpan_LegacyFormatMode>, element
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- <TimeSpan_LegacyFormatMode> element
- TimeSpan_LegacyFormatMode element
ms.assetid: 865e7207-d050-4442-b574-57ea29d5e2d6
ms.openlocfilehash: 9d9eedf52f5d711412e4549e39e6ea23abb68ff3
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2020
ms.locfileid: "73968906"
---
# <a name="timespan_legacyformatmode-element"></a>\<TimeSpan_LegacyFormatMode> Element

Określa, czy środowisko uruchomieniowe zachowuje starsze zachowanie w operacjach formatowania z <xref:System.TimeSpan?displayProperty=nameWithType> wartościami.

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<runtime>**](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<TimeSpan_LegacyFormatMode>**  

## <a name="syntax"></a>Składnia

```xml
<TimeSpan_LegacyFormatMode
   enabled="true|false"/>
```

## <a name="attributes-and-elements"></a>Atrybuty i elementy

W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.

### <a name="attributes"></a>Atrybuty

|Atrybut|Opis|
|---------------|-----------------|
|`enabled`|Atrybut wymagany.<br /><br /> Określa, czy środowisko uruchomieniowe korzysta ze starszego zachowania formatowania z <xref:System.TimeSpan?displayProperty=nameWithType> wartościami.|

## <a name="enabled-attribute"></a>Atrybut włączony

|Wartość|Opis|
|-----------|-----------------|
|`false`|Środowisko uruchomieniowe nie przywraca starszego zachowania formatowania.|
|`true`|Środowisko uruchomieniowe przywraca starsze zachowanie podczas formatowania.|

### <a name="child-elements"></a>Elementy podrzędne

Brak.

### <a name="parent-elements"></a>Elementy nadrzędne

|Element|Opis|
|-------------|-----------------|
|`configuration`|Element główny w każdym pliku konfiguracji używanym przez środowisko uruchomieniowe języka wspólnego i aplikacje programu .NET Framework.|
|`runtime`|Zawiera informacje dotyczące opcji inicjowania środowiska uruchomieniowego.|

## <a name="remarks"></a>Uwagi

Począwszy od .NET Framework 4, <xref:System.TimeSpan?displayProperty=nameWithType> struktura implementuje <xref:System.IFormattable> interfejs i obsługuje operacje formatowania przy użyciu standardowych i niestandardowych ciągów formatu. Jeśli metoda analizy napotka nieobsługiwany specyfikator formatu lub ciąg formatu, zgłasza <xref:System.FormatException> .

W poprzednich wersjach .NET Framework <xref:System.TimeSpan> Struktura nie została zaimplementowana <xref:System.IFormattable> i nie obsługuje ciągów formatu. Jednak w przypadku wielu programistów założono, że program <xref:System.TimeSpan> obsługiwał zestaw ciągów formatu i użył ich w [operacjach formatowania złożonego](../../../../standard/base-types/composite-formatting.md) z metodami takimi jak <xref:System.String.Format%2A?displayProperty=nameWithType> . Zwykle, jeśli typ implementuje <xref:System.IFormattable> i obsługuje ciągi formatowania, wywołania metod formatowania z nieobsługiwanymi ciągami formatu zwykle generują <xref:System.FormatException> . Jednak ponieważ <xref:System.TimeSpan> nie została zaimplementowana <xref:System.IFormattable> , środowisko uruchomieniowe zignorował ciąg formatu i zamiast niego nazywa <xref:System.TimeSpan.ToString?displayProperty=nameWithType> metodę. Oznacza to, że chociaż ciągi formatu nie miały wpływu na operację formatowania, ich obecność nie spowodowało <xref:System.FormatException> .

W przypadkach, w których starszy kod przekazuje metodę formatowania złożonego i nieprawidłowy ciąg formatu, a ten kod nie może zostać ponownie skompilowany, można użyć `<TimeSpan_LegacyFormatMode>` elementu, aby przywrócić starsze <xref:System.TimeSpan> zachowanie. Po ustawieniu `enabled` atrybutu tego elementu na `true` , Metoda formatowania złożonego powoduje wywołanie <xref:System.TimeSpan.ToString?displayProperty=nameWithType> zamiast <xref:System.TimeSpan.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType> i <xref:System.FormatException> nie jest generowane.

## <a name="example"></a>Przykład

Poniższy przykład tworzy wystąpienie <xref:System.TimeSpan> obiektu i próbuje sformatować go za pomocą <xref:System.String.Format%28System.String%2CSystem.Object%29?displayProperty=nameWithType> metody przy użyciu nieobsługiwanego ciągu formatu standardowego.

[!code-csharp[TimeSpan.BreakingChanges#1](../../../../../samples/snippets/csharp/VS_Snippets_CLR/timespan.breakingchanges/cs/legacyformatmode1.cs#1)]
[!code-vb[TimeSpan.BreakingChanges#1](../../../../../samples/snippets/visualbasic/VS_Snippets_CLR/timespan.breakingchanges/vb/legacyformatmode1.vb#1)]

Po uruchomieniu przykładu w .NET Framework 3,5 lub we wcześniejszej wersji zostaną wyświetlone następujące dane wyjściowe:

```console
12:30:45
```

Różni się to od danych wyjściowych w przypadku uruchomienia przykładu w .NET Framework 4 lub jego nowszej wersji:

```console
Invalid Format
```

Jeśli jednak dodasz następujący plik konfiguracji do katalogu przykładu, a następnie uruchomisz przykład w .NET Framework 4 lub nowszej wersji, dane wyjściowe są identyczne z tym, które zostały utworzone przez przykład w przypadku uruchomienia na .NET Framework 3,5.

```xml
<?xml version ="1.0"?>
<configuration>
   <runtime>
      <TimeSpan_LegacyFormatMode enabled="true"/>
   </runtime>
</configuration>
```

## <a name="see-also"></a>Zobacz także

- [Schemat ustawień środowiska uruchomieniowego](index.md)
- [Schemat pliku konfiguracji](../index.md)
