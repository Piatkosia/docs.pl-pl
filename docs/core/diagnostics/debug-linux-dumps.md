---
title: Debuguj zrzuty systemu Linux
description: W tym artykule dowiesz się, jak zbierać i analizować zrzuty ze środowisk systemu Linux.
ms.date: 08/27/2020
ms.openlocfilehash: d62295e165f56e32ef73ab628ca9ebd77a4435d1
ms.sourcegitcommit: 43d5aca3fda42bad8843f6c4e72f6bd52daa55f1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/09/2020
ms.locfileid: "89598356"
---
# <a name="debug-linux-dumps"></a>Debuguj zrzuty systemu Linux

**Ten artykuł ma zastosowanie do: ✔️** .net Core 3,0 SDK i nowszych wersjach

## <a name="collect-dumps-on-linux"></a>Zbieraj zrzuty w systemie Linux

Dwa zalecane sposoby zbierania zrzutów w systemie Linux to [`dotnet-dump`](dotnet-dump.md) [`createdump`](https://github.com/dotnet/runtime/blob/master/docs/design/coreclr/botr/xplat-minidump-generation.md) Narzędzia lub.

### <a name="managed-dumps-with-dotnet-dump"></a>Zarządzane zrzuty z `dotnet-dump`

[`dotnet-dump`](dotnet-dump.md)Narzędzie jest proste w użyciu i nie jest zależne od żadnych natywnych debugerów. `dotnet-dump` działa na wielu platformach systemu Linux (takich jak Alpine lub ARM32/ARM64), gdzie tradycyjne narzędzia debugowania mogą być niedostępne. Jednak `dotnet-dump` tylko przechwytuje stan zarządzany, dlatego nie można go używać do debugowania w kodzie natywnym. Zrzuty zbierane przez program `dotnet-dump` są analizowane w środowisku z tym samym systemem operacyjnym i architekturą, w której został utworzony zrzut. [`dotnet-gcdump`](dotnet-gcdump.md)Narzędzie może służyć jako alternatywa, która przechwytuje informacje o stercie GC, ale tworzy zrzuty, które można analizować w systemie Windows.

### <a name="core-dumps-with-createdump"></a>Zrzuty rdzeniowe z `createdump`

Alternatywnym rozwiązaniem `dotnet-dump` jest utworzenie zrzutów, które [`createdump`](https://github.com/dotnet/runtime/blob/master/docs/design/coreclr/botr/xplat-minidump-generation.md) są przeznaczone tylko do zarządzania, jest zalecanym narzędziem do tworzenia podstawowych zrzutów w systemie Linux zawierających zarówno dane natywne, jak i zarządzane. Można również użyć innych narzędzi, takich jak GDB lub gcore, w celu utworzenia zrzutów podstawowych, ale może brakować stanu wymaganego do debugowania zarządzanego, co powoduje "Nieznane" nazwy typu lub funkcji podczas analizy.

`createdump`Narzędzia są instalowane przy użyciu środowiska uruchomieniowego .NET Core i można je znaleźć obok libcoreclr.so (zazwyczaj w "/usr/share/dotnet/Shared/Microsoft.NETCore.App/[wersja]"). Narzędzie Pobiera identyfikator procesu w celu zebrania zrzutu z jako argumentu podstawowego i może również przyjmować parametry opcjonalne określające rodzaj zrzutu do zebrania (wartość domyślna to minizrzutu z stertą). Dostępne są następujące opcje:

- **`<input-filename>`**

  Wejściowy plik śledzenia do przekonwertowania. Wartość domyślna to *Trace. Trace*.

### <a name="options"></a>Opcje

- **`-f|--name <output-filename>`**

  Plik, w którym ma zostać zapisany zrzut. Wartość domyślna to "/tmp/CoreDump.%p", gdzie% p jest IDENTYFIKATORem procesu docelowego.

- **`-n|--normal`**

  Utwórz element minizrzutu.

- **`-h|--withheap`**

  Utwórz element minizrzutu z stertą (domyślnie).

- **`-t|--triage`**

  Utwórz element Klasyfikacja minizrzutu.

- **`-u|--full`**

  Utwórz pełny zrzut rdzenia.

- **`-d|--diag`**

  Włącz komunikaty diagnostyczne.

Należy pamiętać, że zbieranie podstawowych zrzutów wymaga `SYS_PTRACE` możliwości lub `createdump` uruchomienia z sudo lub su.

## <a name="analyze-dumps-on-linux"></a>Analizowanie zrzutów w systemie Linux

Zarówno zarządzane zrzuty zebrane z `dotnet-dump` i rdzenie podstawowe zbierane z programem `createdump` można analizować za pomocą `dotnet-dump` Narzędzia przy użyciu `dotnet-dump analyze` polecenia. `dotnet dump`Wymaga, aby środowisko analizuje zrzut ma ten sam system operacyjny i architekturę co środowisko, w którym został przechwycony zrzut.

Alternatywnie, [LLDB](https://lldb.llvm.org/) może służyć do analizowania zrzutów rdzeni w systemie Linux, co umożliwia analizę zarówno ramek zarządzanych, jak i natywnych. LLDB używa rozszerzenia SOS do debugowania kodu zarządzanego. [`dotnet-sos`](dotnet-sos.md)Narzędzia interfejsu wiersza polecenia można użyć do instalacji sos, która zawiera [wiele przydatnych poleceń](https://github.com/dotnet/diagnostics/blob/master/documentation/sos-debugging-extension.md) debugowania kodu zarządzanego. W celu przeanalizowania zrzutów programu .NET Core LLDB i SOS wymagają następujących plików binarnych platformy .NET Core ze środowiska, w którym został utworzony zrzut:

1. libmscordaccore.so
2. libcoreclr.so
3. dotnet (host używany do uruchamiania aplikacji)

W większości przypadków te pliki binarne można pobrać przy użyciu [`dotnet-symbol`](dotnet-symbol.md) Narzędzia. Jeśli nie można pobrać niezbędnych plików binarnych z `dotnet-symbol` (na przykład jeśli prywatna wersja platformy .NET Core oparta na źródle była w użyciu), może być konieczne skopiowanie plików wymienionych powyżej ze środowiska, w którym został utworzony. Jeśli pliki nie znajdują się obok pliku zrzutu, można użyć polecenia LLDB/SOS, `setclrpath <path>` Aby ustawić ścieżkę, z której mają zostać załadowane, i `setsymbolserver -directory <path>` ustawić ścieżkę do wyszukiwania dla plików symboli.

Gdy wymagane pliki są dostępne, zrzut może zostać załadowany w LLDB, określając hosta dotnet jako plik wykonywalny do debugowania:

```console
lldb --core <dump-file> <host-program>
```

W powyższym wierszu polecenia `<dump-file>` jest ścieżką do analizy zrzutu i `<host-program>` jest programem macierzystym, który uruchomił aplikację .NET Core. Jest to zazwyczaj `dotnet` plik binarny, chyba że aplikacja jest niezależna. w takim przypadku jest to nazwa aplikacji bez rozszerzenia biblioteki DLL.

Po rozpoczęciu LLDB może być konieczne użycie polecenia, `setsymbolserver` Aby wskazać prawidłową lokalizację symboli ( `setsymbolserver -ms` do użycia serwera symboli firmy Microsoft lub `setsymbolserver -directory <path>` określić ścieżkę lokalną). Symbole natywne mogą być ładowane przez uruchomienie `loadsymbols` . W tym momencie [polecenia sos](https://github.com/dotnet/diagnostics/blob/master/documentation/sos-debugging-extension.md) mogą służyć do analizowania zrzutu.

## <a name="see-also"></a>Zobacz też

- [dotnet-sos](dotnet-sos.md) , aby uzyskać więcej informacji na temat instalowania rozszerzenia sos.
- Program [dotnet — symbol](dotnet-symbol.md) , aby uzyskać więcej informacji na temat instalowania i używania narzędzia do pobierania symboli.
- [Repozytorium diagnostyki .NET Core](https://github.com/dotnet/diagnostics/blob/master/documentation/) , aby uzyskać więcej informacji na temat debugowania, w tym przydatnych często zadawanych pytań.
- [Instalowanie programu LLDB](https://github.com/dotnet/diagnostics/blob/master/documentation/sos.md#getting-lldb) w celu uzyskania instrukcji dotyczących instalowania LLDB w systemie Linux lub Mac.
