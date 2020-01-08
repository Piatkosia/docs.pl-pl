---
ms.openlocfilehash: 7c0930f6606aa96d2863dc740aef8e9cab724b37
ms.sourcegitcommit: 30a558d23e3ac5a52071121a52c305c85fe15726
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/25/2019
ms.locfileid: "75344879"
---
### <a name="change-in-default-value-of-useshellexecute"></a>Zmień wartość domyślną UseShellExecute

<xref:System.Diagnostics.ProcessStartInfo.UseShellExecute?displayProperty=nameWithType> ma wartość domyślną `false` na platformie .NET Core. Na .NET Framework wartość domyślna to `true`.

#### <a name="change-description"></a>Opis zmiany

<xref:System.Diagnostics.Process.Start%2A?displayProperty=nameWithType> umożliwia bezpośrednie uruchamianie aplikacji, na przykład przy użyciu kodu, takiego jak `Process.Start("mspaint.exe")`, który uruchamia program Paint. Umożliwia ona również pośrednio uruchomienie skojarzonej aplikacji, jeśli <xref:System.Diagnostics.ProcessStartInfo.UseShellExecute?displayProperty=nameWithType> jest ustawiona na `true`. Na .NET Framework wartość domyślna <xref:System.Diagnostics.ProcessStartInfo.UseShellExecute?displayProperty=nameWithType> jest `true`, co oznacza, że kod taki jak `Process.Start("mytextfile.txt")` zostałby uruchomiony Notatnik, jeśli masz skojarzone pliki *txt* z tym edytorem. Aby zapobiec pośredniemu uruchamianiu aplikacji na .NET Framework, musisz jawnie ustawić <xref:System.Diagnostics.ProcessStartInfo.UseShellExecute?displayProperty=nameWithType> do `false`. W przypadku platformy .NET Core wartość domyślna dla <xref:System.Diagnostics.ProcessStartInfo.UseShellExecute?displayProperty=nameWithType> jest `false`. Oznacza to, że domyślnie skojarzone aplikacje nie są uruchamiane podczas wywoływania `Process.Start`.

Ta zmiana została wprowadzona w programie .NET Core ze względu na wydajność. Zazwyczaj <xref:System.Diagnostics.Process.Start%2A?displayProperty=nameWithType> jest używany do bezpośredniego uruchamiania aplikacji. Bezpośrednie uruchamianie aplikacji nie wymaga ponoszenia powłoki systemu Windows i wiąże się z powiązanymi kosztami wydajności. Aby ten przypadek domyślny był szybszy, program .NET Core zmieni wartość domyślną <xref:System.Diagnostics.ProcessStartInfo.UseShellExecute?displayProperty=nameWithType> na `false`. Jeśli potrzebujesz, możesz zrezygnować z wolniejszej ścieżki.

#### <a name="version-introduced"></a>Wprowadzona wersja

2.1

> [!NOTE]
> We wcześniejszych wersjach programu .NET Core `UseShellExecute` nie została zaimplementowana dla systemu Windows.

#### <a name="recommended-action"></a>Zalecane działanie

Jeśli aplikacja korzysta ze starego zachowania, wywołaj <xref:System.Diagnostics.Process.Start(System.Diagnostics.ProcessStartInfo)?displayProperty=nameWithType> z <xref:System.Diagnostics.ProcessStartInfo.UseShellExecute> ustawionym na `true` na obiekcie <xref:System.Diagnostics.ProcessStartInfo>.

#### <a name="category"></a>Kategoria

CoreFx

#### <a name="affected-apis"></a>Dotyczy interfejsów API

- <xref:System.Diagnostics.Process.Start%2A?displayProperty=nameWithType>
- <xref:System.Diagnostics.ProcessStartInfo?displayProperty=nameWithType>

<!--

### Affected APIs

- `Overload:System.Diagnostics.Process.Start`
- `M:System.Diagnostics.ProcessStartInfo`

-->