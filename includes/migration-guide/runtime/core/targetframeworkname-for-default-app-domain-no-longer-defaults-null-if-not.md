---
ms.openlocfilehash: 4e685722271a8079e727ea9c2e0e501f68b30fc9
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/05/2020
ms.locfileid: "89497403"
---
### <a name="targetframeworkname-for-default-app-domain-no-longer-defaults-to-null-if-not-set"></a>TargetFrameworkName dla domyślnej domeny aplikacji nie ma już wartości null, jeśli nie jest ustawiona

#### <a name="details"></a>Szczegóły

<xref:System.AppDomainSetup.TargetFrameworkName?displayProperty=fullName>Program był wcześniej pusty w domenie aplikacji domyślnej, chyba że został jawnie ustawiony. Począwszy od 4,6, <xref:System.AppDomainSetup.TargetFrameworkName?displayProperty=fullName> Właściwość domyślnej domeny aplikacji będzie mieć wartość domyślną pochodzącą z TargetFrameworkAttribute (jeśli istnieje). Domeny aplikacji innych niż domyślne będą nadal dziedziczyć <xref:System.AppDomainSetup.TargetFrameworkName?displayProperty=fullName> z domyślnej domeny aplikacji (która nie ma wartości null w 4,6), chyba że zostanie jawnie przesłonięty.

#### <a name="suggestion"></a>Sugestia

Kod powinien zostać zaktualizowany, aby nie zależał <xref:System.AppDomainSetup.TargetFrameworkName> domyślnego ustawienia wartości null. Jeśli jest wymagane, aby ta właściwość kontynuowała szacowanie do wartości null, może być jawnie ustawiona na tę wartość.

| Nazwa    | Wartość       |
|:--------|:------------|
| Zakres   |Edge|
|Wersja|4,6|
|Typ|Środowisko uruchomieniowe|

#### <a name="affected-apis"></a>Dotyczy interfejsów API

- <xref:System.AppDomainSetup.TargetFrameworkName?displayProperty=nameWithType>

<!--

#### Affected APIs

- `P:System.AppDomainSetup.TargetFrameworkName`

-->
