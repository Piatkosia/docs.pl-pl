---
title: Jak używać klas kodowania znaków w programie .NET
description: Dowiedz się, jak używać klas kodowania znaków w programie .NET.
ms.date: 12/22/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- encoding, understanding
- encoding, choosing
- encoding, fallback strategy
ms.assetid: bf6d9823-4c2d-48af-b280-919c5af66ae9
ms.openlocfilehash: c626e79e7bbcd71c90775df8ee8c4d6570c29125
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/02/2020
ms.locfileid: "84290581"
---
# <a name="how-to-use-character-encoding-classes-in-net"></a>Jak używać klas kodowania znaków w programie .NET

W tym artykule wyjaśniono, jak używać klas, które platforma .NET zapewnia do kodowania i dekodowania tekstu przy użyciu różnych schematów kodowania. W instrukcjach przyjęto założenie, że wprowadzono [wprowadzenie do kodowania znaków w programie .NET](character-encoding-introduction.md).

## <a name="encoders-and-decoders"></a>Kodery i dekodery

Platforma .NET udostępnia klasy kodowania, które kodują i dekodują tekst przy użyciu różnych systemów kodowania. Na przykład <xref:System.Text.UTF8Encoding> Klasa opisuje reguły kodowania do i dekodowania z, UTF-8. Platforma .NET używa kodowania UTF-16 (reprezentowanego przez <xref:System.Text.UnicodeEncoding> klasę) dla `string` wystąpień. Kodery i dekodery są dostępne dla innych schematów kodowania.

Kodowanie i dekodowanie może również obejmować walidację. Na przykład <xref:System.Text.UnicodeEncoding> Klasa sprawdza wszystkie `char` wystąpienia w zakresie surogatu, aby upewnić się, że znajdują się one w prawidłowych parach zastępczych. Strategia rezerwowa określa, jak koder obsługuje nieprawidłowe znaki lub jak dekoder obsługuje nieprawidłowe bajty.

> [!WARNING]
> Klasy kodowania .NET umożliwiają przechowywanie i konwertowanie danych znakowych. Nie powinny być używane do przechowywania danych binarnych w postaci ciągów. W zależności od użytego kodowania Konwertowanie danych binarnych na format ciągu z klasami kodowania może spowodować nieoczekiwane zachowanie i generować niedokładne lub uszkodzone dane. Aby przekonwertować dane binarne na postać ciągu, użyj <xref:System.Convert.ToBase64String%2A?displayProperty=nameWithType> metody.

Wszystkie klasy kodowania znaków w programie .NET dziedziczą z <xref:System.Text.Encoding?displayProperty=nameWithType> klasy, która jest klasą abstrakcyjną, która definiuje funkcje wspólne dla wszystkich kodowań znaków. Aby uzyskać dostęp do poszczególnych obiektów kodowania wdrożonych w programie .NET, wykonaj następujące czynności:

- Użyj właściwości statycznych <xref:System.Text.Encoding> klasy, które zwracają obiekty reprezentujące standardowe kodowanie znaków dostępne w .NET (ASCII, UTF-7, UTF-8, UTF-16 i UTF-32). Na przykład <xref:System.Text.Encoding.Unicode%2A?displayProperty=nameWithType> Właściwość zwraca <xref:System.Text.UnicodeEncoding> obiekt. Każdy obiekt używa powrotu zamiennej do obsługi ciągów, których nie można kodować, i bajtów, których nie można zdekodować. Aby uzyskać więcej informacji, zobacz [rezerwowe zastąpienie](character-encoding.md#Replacement).

- Wywołaj konstruktora klasy kodowania. W ten sposób można utworzyć wystąpienie obiektów dla kodowania ASCII, UTF-7, UTF-8, UTF-16 i UTF-32. Domyślnie każdy obiekt używa powrotu zamiennej do obsługi ciągów, których nie można kodować, i bajtów, których nie można zdekodować, ale można określić, że zamiast tego ma zostać zgłoszony wyjątek. Aby uzyskać więcej informacji, zobacz rezerwowe [rezerwy](character-encoding.md#Replacement) i [wyjątki](character-encoding.md#Exception).

- Wywołaj <xref:System.Text.Encoding.%23ctor%28System.Int32%29> konstruktora i przekaż go do liczby całkowitej, która reprezentuje kodowanie. Obiekty kodowania standardowego używają rezerw zamiennych, a strony kodowej i dwubajtowego zestawu znaków (DBCS) używają najlepiej dopasowanej rezerwy do obsługi ciągów, których nie można kodować, i bajtów, których nie można zdekodować. Aby uzyskać więcej informacji, zobacz [najlepiej dopasowany powrotu](character-encoding.md#BestFit).

- Wywołaj <xref:System.Text.Encoding.GetEncoding%2A?displayProperty=nameWithType> metodę, która zwraca dowolne kodowanie standardowe, strony kodowej lub DBCS dostępne w programie .NET. Przeciążenia umożliwiają określenie obiektu rezerwowego dla kodera i dekodera.

Możesz pobrać informacje o wszystkich kodowaniach dostępnych w programie .NET, wywołując <xref:System.Text.Encoding.GetEncodings%2A?displayProperty=nameWithType> metodę. Platforma .NET obsługuje schematy kodowania znaków wymienione w poniższej tabeli.

|Klasa kodowania|Opis|
|--------------|-----------|
|[ASCII](xref:System.Text.ASCIIEncoding)|Koduje ograniczony zakres znaków przy użyciu krótszych siedmiu bitów bajtu. Ponieważ to kodowanie obsługuje tylko wartości znakowe z U + 0000 za pośrednictwem U + 007F, w większości przypadków nie jest to wystarczające dla międzynarodowych aplikacji.|
|[UTF-7](xref:System.Text.UTF7Encoding)|Reprezentuje znaki jako sekwencje 7-bitowego znaków ASCII. Znaki Unicode inne niż ASCII są reprezentowane przez sekwencję ucieczki znaków ASCII. UTF-7 obsługuje protokoły takie jak wiadomości e-mail i grupy dyskusyjne. Jednak kodowanie UTF-7 nie jest szczególnie bezpieczne ani niezawodne. W niektórych przypadkach zmiana jednego bitu może radykalnie zmienić interpretację całego ciągu UTF-7. W innych przypadkach, różne ciągi UTF-7 mogą kodować ten sam tekst. W przypadku sekwencji, które zawierają znaki inne niż ASCII, UTF-7 wymaga więcej miejsca niż UTF-8, a Kodowanie/dekodowanie jest wolniejsze. W związku z tym należy zamiast tego użyć formatu UTF-8, jeśli jest to możliwe.|
|[UTF-8](xref:System.Text.UTF8Encoding)|Reprezentuje każdy punkt kodu Unicode jako sekwencję od 1 do 4 bajtów. UTF-8 obsługuje 8-bitowe rozmiary danych i współpracuje z wieloma istniejącymi systemami operacyjnymi. W przypadku zakresu znaków ASCII UTF-8 jest taka sama jak kodowanie ASCII i umożliwia szerszego zestawu znaków. Jednak w przypadku skryptów języka chińskiego-japońskiego (CJK) UTF-8 może wymagać trzech bajtów dla każdego znaku i może spowodować większe rozmiary danych niż UTF-16. Czasami ilość danych ASCII, takich jak tagi HTML, uzasadnia zwiększony rozmiar dla zakresu CJK.|
|[UTF-16](xref:System.Text.UnicodeEncoding)|Reprezentuje każdy punkt kodu Unicode jako sekwencję jednej lub 2 16-bitowej liczby całkowitej. Najpopularniejsze znaki Unicode wymagają tylko jednego punktu kodu UTF-16, chociaż znaki dodatkowe Unicode (U + 10000 i nowsze) wymagają dwóch zastępczych punktów kodowych w formacie UTF-16. Obsługiwane są zarówno kolejność bajtów little-endian, jak i big-endian. Kodowanie UTF-16 jest używane przez środowisko uruchomieniowe języka wspólnego do reprezentowania <xref:System.Char> i <xref:System.String> wartości, i jest używane przez system operacyjny Windows do reprezentowania `WCHAR` wartości.|
|[UTF-32](xref:System.Text.UTF32Encoding)|Reprezentuje każdy punkt kodu Unicode jako 32-bitową liczbę całkowitą. Obsługiwane są zarówno kolejność bajtów little-endian, jak i big-endian. Kodowanie UTF-32 jest używane, gdy aplikacje chcą uniknąć zachowania surogatu kodu UTF-16 w systemach operacyjnych, w których zakodowane miejsce jest zbyt ważne. Pojedyncze glify renderowane na ekranie mogą wciąż być kodowane przy użyciu więcej niż jednego znaku UTF-32.|
|Kodowanie ANSI/ISO|Zapewnia obsługę różnych stron kodowych. W systemach operacyjnych Windows strony kodowe są używane do obsługi określonego języka lub grupy języków. W przypadku tabeli, która wyświetla listę stron kodowych obsługiwanych przez platformę .NET, zobacz <xref:System.Text.Encoding> Klasa. Można pobrać obiekt kodowania dla konkretnej strony kodowej, wywołując <xref:System.Text.Encoding.GetEncoding%28System.Int32%29?displayProperty=nameWithType> metodę. Strona kodowa zawiera 256 punktów kodu i jest zależna od zera. W większości stron kodowych od 0 do 127 reprezentuje zestaw znaków ASCII, a punkty kodów 128 przez 255 różnią się znacząco między stronami kodowymi. Na przykład strona kodowa 1252 zawiera znaki dla systemów pisania łacińskiego, w tym angielski, niemiecki i francuski. Ostatnie 128 punktów kodowych na stronie kodowej 1252 zawierają znaki akcentu. Strona kodowa 1253 zawiera kody znaków, które są wymagane w greckim systemie pisania. Ostatnie 128 punktów kodu na stronie kodowej 1253 zawierają znaki greckie. W związku z tym aplikacja, która opiera się na stronach kodowych ANSI, nie może przechowywać greckich i niemieckich w tym samym strumieniu tekstowym, chyba że zawiera identyfikator, który wskazuje na stronę kodową, do której się odwołuje.|
|Kodowanie zestawów znaków dwubajtowych (DBCS)|Obsługuje języki, takie jak chiński, japoński i koreański, które zawierają więcej niż 256 znaków. W DBCS para punktów kodu (dwubajtowy) reprezentuje każdy znak. <xref:System.Text.Encoding.IsSingleByte%2A?displayProperty=nameWithType>Właściwość zwraca `false` dla kodowań DBCS. Można pobrać obiekt kodowania dla określonego zestawu DBCS, wywołując <xref:System.Text.Encoding.GetEncoding%28System.Int32%29?displayProperty=nameWithType> metodę. Gdy aplikacja obsługuje dane DBCS, pierwszy bajt znaku dwubajtowego (bajt wiodący) jest przetwarzany w połączeniu z bajtem końcowym, który natychmiast następuje po nim. Ponieważ pojedyncza para dwubajtowych punktów kodowych może reprezentować różne znaki w zależności od strony kodowej, schemat ten nadal nie pozwala na połączenie dwóch języków, takich jak japoński i chiński, w tym samym strumieniu danych.|

Te kodowania umożliwiają współdziałanie z znakami Unicode, a także z kodowaniem najczęściej używanym w starszych aplikacjach. Ponadto można utworzyć niestandardowe kodowanie, definiując klasę, która dziedziczy z <xref:System.Text.Encoding> i zastępując jej składowe.

## <a name="net-core-encoding-support"></a>Obsługa kodowania .NET Core

Domyślnie platforma .NET Core nie udostępnia żadnych kodowań stron kodowych innych niż strona kodowa 28591 i kodowanie Unicode, takie jak UTF-8 i UTF-16. Można jednak dodać kodowanie stron kodowych Znalezione w standardowych aplikacjach systemu Windows, które są przeznaczone dla platformy .NET dla aplikacji. Aby uzyskać więcej informacji, zobacz <xref:System.Text.CodePagesEncodingProvider> temat.

<a name="Selecting"></a>

## <a name="selecting-an-encoding-class"></a>Wybieranie klasy kodowania

Jeśli masz możliwość wybrania kodowania, które ma być używane przez aplikację, użyj kodowania Unicode, najlepiej <xref:System.Text.UTF8Encoding> lub <xref:System.Text.UnicodeEncoding> . (Platforma .NET obsługuje także trzecie kodowanie Unicode, <xref:System.Text.UTF32Encoding> ).

Jeśli planujesz użycie kodowania ASCII ( <xref:System.Text.ASCIIEncoding> ), wybierz <xref:System.Text.UTF8Encoding> zamiast tego. Dwa kodowania są identyczne dla zestawu znaków ASCII, ale <xref:System.Text.UTF8Encoding> ma następujące zalety:

- Może reprezentować każdy znak Unicode, który <xref:System.Text.ASCIIEncoding> obsługuje tylko wartości znaków Unicode między u + 0000 i u + 007F.

- Zapewnia wykrywanie błędów i lepsze zabezpieczenia.

- Został dostrojony tak szybko, jak to możliwe i powinien być szybszy niż inne kodowanie. Nawet w przypadku zawartości, która jest całkowicie ASCII, operacje wykonywane przy użyciu programu <xref:System.Text.UTF8Encoding> są szybsze niż operacje wykonywane przy użyciu programu <xref:System.Text.ASCIIEncoding> .

Należy rozważyć użycie <xref:System.Text.ASCIIEncoding> tylko w przypadku starszych aplikacji. Jednak nawet w przypadku starszych aplikacji <xref:System.Text.UTF8Encoding> może być lepszym wyborem z następujących powodów (przy założeniu ustawień domyślnych):

- Jeśli aplikacja ma zawartość, która nie jest ściśle ASCII i koduje ją z <xref:System.Text.ASCIIEncoding> , każdy znak inny niż ASCII jest kodowany jako znak zapytania (?). Jeśli aplikacja następnie dekoduje te dane, informacje zostaną utracone.

- Jeśli aplikacja ma zawartość, która nie jest ściśle ASCII i koduje ją z <xref:System.Text.UTF8Encoding> , wynik wydaje się niezrozumiały, jeśli jest interpretowany jako ASCII. Jeśli jednak aplikacja używa dekodera UTF-8, aby zdekodować te dane, dane są wykonywane pomyślnie.

W aplikacji sieci Web znaki wysyłane do klienta w odpowiedzi na żądanie sieci Web powinny odzwierciedlać kodowanie używane na kliencie. W większości przypadków należy ustawić <xref:System.Web.HttpResponse.ContentEncoding%2A?displayProperty=nameWithType> Właściwość na wartość zwracaną przez <xref:System.Web.HttpRequest.ContentEncoding%2A?displayProperty=nameWithType> Właściwość, aby wyświetlić tekst w kodowaniu, którego oczekuje użytkownik.

<a name="Using"></a>

## <a name="using-an-encoding-object"></a>Używanie obiektu kodowania

Koder konwertuje ciąg znaków (najczęściej są to znaki Unicode) na jego odpowiednik liczbowy (Byte). Można na przykład użyć kodera ASCII do przekonwertowania znaków Unicode na ASCII, aby można było je wyświetlić w konsoli. Aby przeprowadzić konwersję, należy wywołać <xref:System.Text.Encoding.GetBytes%2A?displayProperty=nameWithType> metodę. Jeśli chcesz określić liczbę bajtów potrzebnych do przechowywania zakodowanych znaków przed wykonaniem kodowania, możesz wywołać <xref:System.Text.Encoding.GetByteCount%2A> metodę.

W poniższym przykładzie zastosowano tablicę jednobajtową do kodowania ciągów w dwóch oddzielnych operacjach. Zachowuje indeks wskazujący pozycję początkową w tablicy bajtów dla następnego zestawu bajtów zakodowanych w formacie ASCII. Wywołuje metodę, <xref:System.Text.ASCIIEncoding.GetByteCount%28System.String%29?displayProperty=nameWithType> Aby upewnić się, że tablica bajtów jest wystarczająco duża, aby pomieścić zakodowany ciąg. Następnie wywołuje metodę w <xref:System.Text.ASCIIEncoding.GetBytes%28System.String%2CSystem.Int32%2CSystem.Int32%2CSystem.Byte%5B%5D%2CSystem.Int32%29?displayProperty=nameWithType> celu zakodowania znaków w ciągu.

[!code-csharp[Conceptual.Encoding#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/getbytes1.cs#8)]
[!code-vb[Conceptual.Encoding#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/getbytes1.vb#8)]

Dekoder konwertuje tablicę bajtową, która odzwierciedla określony kodowanie znaków w zestawie znaków, w tablicy znaków lub w ciągu. Aby zdekodować tablicę bajtową do tablicy znaków, należy wywołać <xref:System.Text.Encoding.GetChars%2A?displayProperty=nameWithType> metodę. Aby zdekodować tablicę bajtową do ciągu, należy wywołać <xref:System.Text.Encoding.GetString%2A> metodę. Jeśli chcesz określić liczbę znaków potrzebną do przechowywania zdekodowanych bajtów przed wykonaniem dekodowania, możesz wywołać <xref:System.Text.Encoding.GetCharCount%2A> metodę.

Poniższy przykład koduje trzy ciągi, a następnie dekoduje je w postaci pojedynczej tablicy znaków. Zachowuje indeks wskazujący pozycję początkową w tablicy znaków dla następnego zestawu zdekodowanych znaków. Wywołuje metodę, <xref:System.Text.ASCIIEncoding.GetCharCount%2A> Aby upewnić się, że tablica znaków jest wystarczająco duża, aby pomieścić wszystkie znaki zdekodowane. Następnie wywołuje metodę, <xref:System.Text.ASCIIEncoding.GetChars%28System.Byte%5B%5D%2CSystem.Int32%2CSystem.Int32%2CSystem.Char%5B%5D%2CSystem.Int32%29?displayProperty=nameWithType> Aby zdekodować tablicę bajtów.

[!code-csharp[Conceptual.Encoding#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/getchars1.cs#9)]
[!code-vb[Conceptual.Encoding#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/getchars1.vb#9)]

Metody kodowania i dekodowania klasy pochodnej <xref:System.Text.Encoding> są przeznaczone do pracy nad kompletnym zestawem danych. to oznacza, że wszystkie dane, które mają zostać zakodowane lub zdekodowane, są dostarczane w jednym wywołaniu metody. Jednak w niektórych przypadkach dane są dostępne w strumieniu, a dane, które mają być kodowane lub dekodowane, mogą być dostępne tylko z oddzielnych operacji odczytu. Wymaga to kodowania lub dekodowania operacji, aby zapamiętać każdy zapisany stan w poprzednim wywołaniu. Metody klas pochodnych <xref:System.Text.Encoder> i <xref:System.Text.Decoder> są w stanie obsługiwać operacje kodowania i dekodowania obejmujące wiele wywołań metod.

<xref:System.Text.Encoder>Obiekt dla określonego kodowania jest dostępny we właściwości tego kodowania <xref:System.Text.Encoding.GetEncoder%2A?displayProperty=nameWithType> . <xref:System.Text.Decoder>Obiekt dla określonego kodowania jest dostępny we właściwości tego kodowania <xref:System.Text.Encoding.GetDecoder%2A?displayProperty=nameWithType> . W przypadku operacji dekodowania należy zauważyć, że klasy pochodne z <xref:System.Text.Decoder> zawierają <xref:System.Text.Decoder.GetChars%2A?displayProperty=nameWithType> metodę, ale nie mają metody odpowiadającej <xref:System.Text.Encoding.GetString%2A?displayProperty=nameWithType> .

Poniższy przykład ilustruje różnicę między użyciem <xref:System.Text.Encoding.GetString%2A?displayProperty=nameWithType> <xref:System.Text.Decoder.GetChars%2A?displayProperty=nameWithType> metod i do dekodowania tablicy bajtowej Unicode. Przykład koduje ciąg, który zawiera znaki Unicode do pliku, a następnie używa dwóch metod dekodowania do zdekodowania ich dziesięć bajtów jednocześnie. Ponieważ para dwuskładnikowa występuje w dziesiątych i jedenastych bajtach, jest dekodowane w oddzielnych wywołaniach metod. Ponieważ dane wyjściowe są wyświetlane, <xref:System.Text.Encoding.GetString%2A?displayProperty=nameWithType> Metoda nie jest w stanie poprawnie zdekodować bajtów i zamiast tego zastępuje je literałem U + FFFD (znak zastępczy). Z drugiej strony <xref:System.Text.Decoder.GetChars%2A?displayProperty=nameWithType> Metoda może pomyślnie zdekodować tablicę bajtową, aby uzyskać oryginalny ciąg.

[!code-csharp[Conceptual.Encoding#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/stream1.cs#10)]
[!code-vb[Conceptual.Encoding#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/stream1.vb#10)]

<a name="FallbackStrategy"></a>

## <a name="choosing-a-fallback-strategy"></a>Wybór strategii rezerwowej

Gdy metoda próbuje zakodować lub zdekodować znak, ale nie istnieje żadne mapowanie, musi zaimplementować strategię rezerwową, która określa sposób obsługi mapowania zakończonego niepowodzeniem. Istnieją trzy typy strategii powrotu:

- Dopasowanie najlepszego dopasowania

- Alternatywa wymiany

- Rezerwa wyjątku

> [!IMPORTANT]
> Najczęstsze problemy w operacjach kodowania są wykonywane, gdy znak Unicode nie może zostać zmapowany na konkretne kodowanie strony kodowej. Najczęstsze problemy związane z dekodowaniem są wykonywane, gdy nieprawidłowe sekwencje bajtów nie mogą być przetłumaczone na prawidłowe znaki Unicode. Z tego względu należy wiedzieć, która strategia rezerwowa używa danego obiektu kodowania. Zawsze, gdy jest to możliwe, należy określić strategię rezerwową używaną przez obiekt kodowania podczas tworzenia wystąpienia obiektu.

<a name="BestFit"></a>

### <a name="best-fit-fallback"></a>Dopasowanie najlepszego dopasowania

Gdy znak nie ma dokładnego dopasowania w kodowaniu docelowym, koder może próbować zmapować go do podobnego znaku. (Najlepszym dopasowaniem jest raczej kodowanie, a nie problem z dekodowaniem. Istnieje kilka stron kodowych, które zawierają znaki, których nie można pomyślnie zmapować na Unicode.) Najlepszym dopasowaniem jest wartość domyślna dla kodowania strony kodowej i dwubajtowego zestawu znaków, które są pobierane przez <xref:System.Text.Encoding.GetEncoding%28System.Int32%29?displayProperty=nameWithType> przeciążenia i <xref:System.Text.Encoding.GetEncoding%28System.String%29?displayProperty=nameWithType> .

> [!NOTE]
> Teoretycznie, klasy kodowania Unicode zapewniane w .NET ( <xref:System.Text.UTF8Encoding> , <xref:System.Text.UnicodeEncoding> i <xref:System.Text.UTF32Encoding> ) obsługują każdy znak w każdym zestawie znaków, dzięki czemu mogą one być używane w celu wyeliminowania najbardziej pasujących problemów powrotu.

Najlepiej dopasowane strategie różnią się w zależności od stron kodowych. Na przykład w przypadku niektórych stron kodowych znaki łacińskie o pełnej szerokości są mapowane na bardziej popularne znaki łacińskie połówkowej szerokości. W przypadku innych stron kodowych mapowanie nie jest wykonywane. Nawet w ramach agresywnej strategii najlepiej dopasowanej nie ma żadnych znaków w przypadku niektórych kodowań. Na przykład, ideograph chiński nie ma uzasadnionego mapowania na stronę kodową 1252. W takim przypadku używany jest ciąg zastępczy. Domyślnie ten ciąg jest tylko pojedynczym ZNAKiem zapytania (U + 003F).

> [!NOTE]
> Strategie najlepiej dopasowane nie są udokumentowane szczegółowo. Jednak kilka stron kodowych są udokumentowane w witrynie sieci Web [konsorcjum Unicode](https://www.unicode.org/Public/MAPPINGS/VENDORS/MICSFT/WindowsBestFit/) . Aby uzyskać opis sposobu interpretacji plików mapowania, zapoznaj się z plikiem **README. txt** w tym folderze.

Poniższy przykład używa strony kodowej 1252 (strona kodowa systemu Windows dla języków zachodnich Europy) do zilustrowania najlepszego mapowania i jego wad. <xref:System.Text.Encoding.GetEncoding%28System.Int32%29?displayProperty=nameWithType>Metoda jest używana do pobierania obiektu kodowania dla strony kodowej 1252. Domyślnie używa mapowania najlepszego dopasowania dla znaków Unicode, które nie są obsługiwane. Przykład tworzy wystąpienie ciągu, który zawiera trzy znaki inne niż ASCII — WYRÓŻNIONe Wielka litera S (U + 24C8), indeks GÓRNy 5 (U + 2075) i NIESKOŃCZONość (U + 221E) — rozdzielone spacjami. Jako dane wyjściowe z przykładu pokazują, gdy ciąg jest zakodowany, trzy oryginalne znaki niebędące znakami spacji są zastępowane na podstawie znaku zapytania (U + 003F), cyfry pięć (U + 0035) i cyfry osiem (U + 0038). CYFRa osiem to szczególnie słabe zastąpienie dla nieobsługiwanego znaku NIESKOŃCZONości, a znak zapytania wskazuje, że dla oryginalnego znaku nie jest dostępne żadne mapowanie.

[!code-csharp[Conceptual.Encoding#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/bestfit1.cs#1)]
[!code-vb[Conceptual.Encoding#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/bestfit1.vb#1)]

Najwygodniejsze mapowanie jest domyślnym zachowaniem dla <xref:System.Text.Encoding> obiektu, który koduje dane Unicode na dane strony kodowej, a istnieją starsze aplikacje korzystające z tego zachowania. Jednak większość nowych aplikacji powinna unikać optymalnego zachowania ze względów bezpieczeństwa. Na przykład aplikacje nie powinny umieszczać nazwy domeny za pomocą najlepszego dopasowania kodowania.

> [!NOTE]
> Możesz również zaimplementować niestandardowe mapowanie rezerwy najlepszego dopasowania dla kodowania. Aby uzyskać więcej informacji, zobacz sekcję [implementowanie niestandardowej strategii rezerwowej](character-encoding.md#Custom) .

Jeśli jest to wartość domyślna dla obiektu Encoding, można wybrać inną strategię rezerwową podczas pobierania <xref:System.Text.Encoding> obiektu przez wywołanie metody <xref:System.Text.Encoding.GetEncoding%28System.Int32%2CSystem.Text.EncoderFallback%2CSystem.Text.DecoderFallback%29?displayProperty=nameWithType> lub <xref:System.Text.Encoding.GetEncoding%28System.String%2CSystem.Text.EncoderFallback%2CSystem.Text.DecoderFallback%29?displayProperty=nameWithType> przeciążenia. Poniższa sekcja zawiera przykład zastępujący każdy znak, którego nie można zamapować na stronę kodową 1252 przy użyciu gwiazdki (*).

[!code-csharp[Conceptual.Encoding#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/bestfit1a.cs#3)]
[!code-vb[Conceptual.Encoding#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/bestfit1a.vb#3)]

<a name="Replacement"></a>

### <a name="replacement-fallback"></a>Alternatywa wymiany

Gdy znak nie ma dokładnego dopasowania w schemacie docelowym, ale nie ma odpowiedniego znaku, do którego można zamapować, aplikacja może określić znak zastępczy lub ciąg. Jest to domyślne zachowanie dla dekodera Unicode, który zastępuje dowolną dwubajtową sekwencję, której nie można zdekodować przy użyciu REPLACEMENT_CHARACTER (U + FFFD). Jest to również domyślne zachowanie <xref:System.Text.ASCIIEncoding> klasy, która zastępuje każdy znak, którego nie można kodować ani zdekodować ze znakiem zapytania. Poniższy przykład ilustruje zastąpienie znaków w ciągu Unicode z poprzedniego przykładu. Ponieważ dane wyjściowe są wyświetlane, każdy znak, którego nie można zdekodować do wartości bajtowej ASCII, jest zastępowany przez 0x3F, który jest kodem ASCII dla znaku zapytania.

[!code-csharp[Conceptual.Encoding#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/replacementascii.cs#2)]
[!code-vb[Conceptual.Encoding#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/replacementascii.vb#2)]

Platforma .NET zawiera <xref:System.Text.EncoderReplacementFallback> <xref:System.Text.DecoderReplacementFallback> klasy i, które zastępują ciąg zamienny, jeśli znak nie jest mapowany dokładnie w operacji kodowania lub dekodowania. Domyślnie ten ciąg zamienny jest znakiem zapytania, ale można wywołać przeciążenie konstruktora klasy w celu wybrania innego ciągu. Zazwyczaj ciąg zamienny jest pojedynczym znakiem, chociaż nie jest to wymagane. Poniższy przykład zmienia zachowanie kodera 1252 strony kodowej przez utworzenie wystąpienia <xref:System.Text.EncoderReplacementFallback> obiektu, który używa gwiazdki (*) jako ciągu zastępczego.

[!code-csharp[Conceptual.Encoding#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/bestfit1a.cs#3)]
[!code-vb[Conceptual.Encoding#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/bestfit1a.vb#3)]

> [!NOTE]
> Można również zaimplementować klasę zastępczą dla kodowania. Aby uzyskać więcej informacji, zobacz sekcję [implementowanie niestandardowej strategii rezerwowej](character-encoding.md#Custom) .

Oprócz znaku zapytania (U + 003F) znak ZASTĘPCZy Unicode (U + FFFD) jest często używany jako ciąg zamienny, szczególnie w przypadku dekodowania sekwencji bajtów, których nie można pomyślnie przetłumaczyć na znaki Unicode. Można jednak wybrać dowolny ciąg zamienny, który może zawierać wiele znaków.

<a name="Exception"></a>

### <a name="exception-fallback"></a>Rezerwa wyjątku

Zamiast podawania najlepszego dopasowania lub ciągu zamiennego, koder może zgłosić, <xref:System.Text.EncoderFallbackException> Jeśli nie jest w stanie zakodować zestawu znaków, a dekoder może zgłosić, <xref:System.Text.DecoderFallbackException> Jeśli nie można zdekodować tablicy bajtów. Aby zgłosić wyjątek w operacjach kodowania i dekodowania, należy dostarczyć <xref:System.Text.EncoderExceptionFallback> obiekt i <xref:System.Text.DecoderExceptionFallback> obiekt odpowiednio do <xref:System.Text.Encoding.GetEncoding%28System.String%2CSystem.Text.EncoderFallback%2CSystem.Text.DecoderFallback%29?displayProperty=nameWithType> metody. Poniższy przykład ilustruje rezerwę wyjątku z <xref:System.Text.ASCIIEncoding> klasą.

[!code-csharp[Conceptual.Encoding#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/exceptionascii.cs#4)]
[!code-vb[Conceptual.Encoding#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/exceptionascii.vb#4)]

> [!NOTE]
> Można również zaimplementować niestandardową procedurę obsługi wyjątków dla operacji kodowania. Aby uzyskać więcej informacji, zobacz sekcję [implementowanie niestandardowej strategii rezerwowej](character-encoding.md#Custom) .

<xref:System.Text.EncoderFallbackException>Obiekty i <xref:System.Text.DecoderFallbackException> zapewniają następujące informacje o stanie, który spowodował wyjątek:

- <xref:System.Text.EncoderFallbackException>Obiekt zawiera <xref:System.Text.EncoderFallbackException.IsUnknownSurrogate%2A> metodę, która wskazuje, czy znak lub znaki, których nie można zakodować, reprezentują nieznaną parę surogatu (w tym przypadku metoda zwraca `true` ) lub nieznany pojedynczy znak (w tym przypadku metoda zwraca `false` ). Znaki w parze dwuskładnikowej są dostępne we <xref:System.Text.EncoderFallbackException.CharUnknownHigh%2A?displayProperty=nameWithType> <xref:System.Text.EncoderFallbackException.CharUnknownLow%2A?displayProperty=nameWithType> właściwościach i. Nieznany pojedynczy znak jest dostępny z <xref:System.Text.EncoderFallbackException.CharUnknown%2A?displayProperty=nameWithType> właściwości. <xref:System.Text.EncoderFallbackException.Index%2A?displayProperty=nameWithType>Właściwość wskazuje położenie w ciągu, w którym znaleziono pierwszy znak, który nie może zostać zakodowany.

- <xref:System.Text.DecoderFallbackException>Obiekt zawiera <xref:System.Text.DecoderFallbackException.BytesUnknown%2A> Właściwość, która zwraca tablicę bajtów, których nie można zdekodować. <xref:System.Text.DecoderFallbackException.Index%2A?displayProperty=nameWithType>Właściwość wskazuje pozycję początkową nieznanych bajtów.

Chociaż <xref:System.Text.EncoderFallbackException> obiekty i <xref:System.Text.DecoderFallbackException> zapewniają odpowiednie informacje diagnostyczne o wyjątku, nie zapewniają dostępu do buforu kodowania lub dekodowania. W związku z tym nie zezwalają na zamienianie lub korygowanie nieprawidłowych danych w ramach metody kodowania lub dekodowania.

<a name="Custom"></a>

## <a name="implementing-a-custom-fallback-strategy"></a>Implementowanie niestandardowej strategii rezerwowej

Oprócz najlepszego mapowania, które jest implementowane wewnętrznie przez strony kodowe, platforma .NET zawiera następujące klasy do implementowania strategii rezerwowej:

- Użyj <xref:System.Text.EncoderReplacementFallback> i, <xref:System.Text.EncoderReplacementFallbackBuffer> Aby zamienić znaki w operacjach kodowania.

- Użyj <xref:System.Text.DecoderReplacementFallback> i, <xref:System.Text.DecoderReplacementFallbackBuffer> Aby zamienić znaki podczas dekodowania operacji.

- Użyj <xref:System.Text.EncoderExceptionFallback> i, <xref:System.Text.EncoderExceptionFallbackBuffer> Aby zgłosić, <xref:System.Text.EncoderFallbackException> kiedy nie można zakodować znaku.

- Użyj <xref:System.Text.DecoderExceptionFallback> i, <xref:System.Text.DecoderExceptionFallbackBuffer> Aby zgłosić, <xref:System.Text.DecoderFallbackException> kiedy nie można zdekodować znaku.

Ponadto można zaimplementować niestandardowe rozwiązanie, które używa najlepszego dopasowania powrotu, powrotu zamiennej lub powrotu do wyjątków, wykonując następujące czynności:

1. Utwórz klasę z <xref:System.Text.EncoderFallback> dla operacji kodowania i z <xref:System.Text.DecoderFallback> dla operacji dekodowania.

2. Utwórz klasę z <xref:System.Text.EncoderFallbackBuffer> dla operacji kodowania i z <xref:System.Text.DecoderFallbackBuffer> dla operacji dekodowania.

3. W przypadku powrotu wyjątku, jeśli wstępnie zdefiniowane <xref:System.Text.EncoderFallbackException> i <xref:System.Text.DecoderFallbackException> klasy nie spełniają Twoich potrzeb, należy utworzyć klasę z obiektu wyjątku, takiego jak <xref:System.Exception> lub <xref:System.ArgumentException> .

### <a name="deriving-from-encoderfallback-or-decoderfallback"></a>Wyprowadzanie z EncoderFallback lub DecoderFallback

Aby zaimplementować niestandardowe rozwiązanie alternatywne, należy utworzyć klasę, która dziedziczy z <xref:System.Text.EncoderFallback> dla operacji kodowania i z <xref:System.Text.DecoderFallback> dla operacji dekodowania. Wystąpienia tych klas są przesyłane do <xref:System.Text.Encoding.GetEncoding%28System.String%2CSystem.Text.EncoderFallback%2CSystem.Text.DecoderFallback%29?displayProperty=nameWithType> metody i służą jako pośrednik między klasą kodowania a implementacją rezerwową.

W przypadku tworzenia niestandardowego rozwiązania alternatywnego dla kodera lub dekodera należy zaimplementować następujące elementy członkowskie:

- <xref:System.Text.EncoderFallback.MaxCharCount%2A?displayProperty=nameWithType>Właściwość lub <xref:System.Text.DecoderFallback.MaxCharCount%2A?displayProperty=nameWithType> , która zwraca maksymalną możliwą liczbę znaków, które można zwrócić, aby zamienić pojedynczy znak. W przypadku niestandardowego powrotu wyjątku jego wartość wynosi zero.

- <xref:System.Text.EncoderFallback.CreateFallbackBuffer%2A?displayProperty=nameWithType>Metoda or <xref:System.Text.DecoderFallback.CreateFallbackBuffer%2A?displayProperty=nameWithType> , która zwraca niestandardowy <xref:System.Text.EncoderFallbackBuffer> lub <xref:System.Text.DecoderFallbackBuffer> implementację. Metoda jest wywoływana przez koder, gdy napotka pierwszy znak, który nie może zostać pomyślnie zakodowany, lub przez dekoder w przypadku napotkania pierwszego bajtu, którego nie można pomyślnie zdekodować.

### <a name="deriving-from-encoderfallbackbuffer-or-decoderfallbackbuffer"></a>Wyprowadzanie z EncoderFallbackBuffer lub DecoderFallbackBuffer

Aby zaimplementować niestandardowe rozwiązanie alternatywne, należy również utworzyć klasę, która dziedziczy z <xref:System.Text.EncoderFallbackBuffer> dla operacji kodowania i z <xref:System.Text.DecoderFallbackBuffer> dla operacji dekodowania. Wystąpienia tych klas są zwracane przez <xref:System.Text.EncoderFallback.CreateFallbackBuffer%2A> metodę <xref:System.Text.EncoderFallback> <xref:System.Text.DecoderFallback> klas i. <xref:System.Text.EncoderFallback.CreateFallbackBuffer%2A?displayProperty=nameWithType>Metoda jest wywoływana przez koder, gdy napotka pierwszy znak, który nie jest w stanie kodować, a <xref:System.Text.DecoderFallback.CreateFallbackBuffer%2A?displayProperty=nameWithType> Metoda jest wywoływana przez dekoder, gdy napotka jeden lub więcej bajtów, których nie można zdekodować. <xref:System.Text.EncoderFallbackBuffer>Klasy i <xref:System.Text.DecoderFallbackBuffer> zapewniają implementację rezerwową. Każde wystąpienie reprezentuje bufor, który zawiera znaki rezerwowe, które zastąpią znak, którego nie można zakodować lub nie można zdekodować sekwencji bajtów.

W przypadku tworzenia niestandardowego rozwiązania alternatywnego dla kodera lub dekodera należy zaimplementować następujące elementy członkowskie:

- <xref:System.Text.EncoderFallbackBuffer.Fallback%2A?displayProperty=nameWithType>Metoda or <xref:System.Text.DecoderFallbackBuffer.Fallback%2A?displayProperty=nameWithType> . <xref:System.Text.EncoderFallbackBuffer.Fallback%2A?displayProperty=nameWithType>jest wywoływany przez koder w celu dostarczenia bufora rezerwowego informacjami o znaku, którego nie może zakodować. Ponieważ znak, który ma być zakodowany, może być parą zastępczą, ta metoda jest przeciążona. Jedno Przeciążenie jest przekazanie znaku, który ma zostać zakodowany i jego indeks w ciągu. Drugie Przeciążenie jest przenoszone z górnego i niskiego surogatu wraz z jego indeksem w ciągu. <xref:System.Text.DecoderFallbackBuffer.Fallback%2A?displayProperty=nameWithType>Metoda jest wywoływana przez dekoder w celu dostarczenia bufora rezerwowego informacjami o bajtach, których nie można zdekodować. Ta metoda jest przenoszona tablicą bajtów, której nie można zdekodować, wraz z indeksem pierwszego bajtu. Metoda rezerwowa powinna zwracać, `true` Jeśli bufor rezerwowy może dostarczyć najlepszego lub zastępczego znaku lub znaków; w przeciwnym razie powinien zwrócić `false` . W przypadku powrotu wyjątku Metoda rezerwowa powinna zgłosić wyjątek.

- <xref:System.Text.EncoderFallbackBuffer.GetNextChar%2A?displayProperty=nameWithType>Metoda or <xref:System.Text.DecoderFallbackBuffer.GetNextChar%2A?displayProperty=nameWithType> , która jest wywoływana wielokrotnie przez koder lub dekoder w celu uzyskania następnego znaku z buforu rezerwowego. Gdy wszystkie znaki powrotu zostały zwrócone, metoda powinna zwrócić U + 0000.

- <xref:System.Text.EncoderFallbackBuffer.Remaining%2A?displayProperty=nameWithType>Właściwość lub <xref:System.Text.DecoderFallbackBuffer.Remaining%2A?displayProperty=nameWithType> , która zwraca liczbę znaków pozostałych w buforze rezerwowym.

- <xref:System.Text.EncoderFallbackBuffer.MovePrevious%2A?displayProperty=nameWithType>Metoda or <xref:System.Text.DecoderFallbackBuffer.MovePrevious%2A?displayProperty=nameWithType> , która przenosi bieżącą pozycję w buforze rezerwowym do poprzedniego znaku.

- <xref:System.Text.EncoderFallbackBuffer.Reset%2A?displayProperty=nameWithType>Metoda or <xref:System.Text.DecoderFallbackBuffer.Reset%2A?displayProperty=nameWithType> , która ponownie inicjuje bufor rezerwowy.

Jeśli implementacja rezerwowa jest najlepszym dopasowaną rezerwą lub alternatywą zamienną, klasy pochodne od <xref:System.Text.EncoderFallbackBuffer> i <xref:System.Text.DecoderFallbackBuffer> również utrzymują dwa pola wystąpienia prywatnego: dokładną liczbę znaków w buforze oraz indeks następnego znaku w buforze do zwrócenia.

### <a name="an-encoderfallback-example"></a>Przykład EncoderFallback

W poprzednim przykładzie użyto powrotu zamiennej zastępującej znaki Unicode, które nie odpowiadają znakom ASCII z gwiazdką (*). W poniższym przykładzie zastosowano niestandardową implementację rezerwową najlepiej w celu zapewnienia lepszego mapowania znaków innych niż ASCII.

Poniższy kod definiuje klasę o nazwie `CustomMapper` , która pochodzi od <xref:System.Text.EncoderFallback> do obsługi najlepszego mapowania znaków innych niż ASCII. `CreateFallbackBuffer`Metoda zwraca `CustomMapperFallbackBuffer` obiekt, który dostarcza <xref:System.Text.EncoderFallbackBuffer> implementację. `CustomMapper`Klasa używa <xref:System.Collections.Generic.Dictionary%602> obiektu do przechowywania mapowań nieobsługiwanych znaków Unicode (wartość klucza) i odpowiadających im znaków 8-bitowych (które są przechowywane w dwóch kolejnych bajtach w 64-bitowej liczbie całkowitej). Aby to mapowanie było dostępne dla buforu rezerwowego, `CustomMapper` wystąpienie jest przesyłane jako parametr do `CustomMapperFallbackBuffer` konstruktora klasy. Ponieważ najdłuższym mapowaniem jest ciąg "INF" dla znaku Unicode U + 221E, `MaxCharCount` Właściwość zwraca wartość 3.

[!code-csharp[Conceptual.Encoding#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/custom1.cs#5)]
[!code-vb[Conceptual.Encoding#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/custom1.vb#5)]

Poniższy kod definiuje `CustomMapperFallbackBuffer` klasę, która pochodzi od <xref:System.Text.EncoderFallbackBuffer> . Słownik zawierający najlepsze mapowania i zdefiniowany w `CustomMapper` wystąpieniu jest dostępny z konstruktora klasy. Jego `Fallback` Metoda zwraca `true` Jeśli którykolwiek ze znaków Unicode, które nie mogą kodować KODERa ASCII, jest zdefiniowany w słowniku mapowania; w przeciwnym razie zwraca `false` . Dla każdego powrotu zmienna prywatna `count` wskazuje liczbę znaków, która pozostała do zwrócenia, a zmienna prywatna `index` wskazuje pozycję w buforze ciągów, `charsToReturn` od następnego znaku do zwrócenia.

[!code-csharp[Conceptual.Encoding#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/custom1.cs#6)]
[!code-vb[Conceptual.Encoding#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/custom1.vb#6)]

Poniższy kod powoduje utworzenie wystąpienia `CustomMapper` obiektu i przekazanie jego wystąpienia do <xref:System.Text.Encoding.GetEncoding%28System.String%2CSystem.Text.EncoderFallback%2CSystem.Text.DecoderFallback%29?displayProperty=nameWithType> metody. Dane wyjściowe wskazują, że Najlepsza zgodność implementacja rezerwy pomyślnie obsługuje trzy znaki inne niż ASCII w oryginalnym ciągu.

[!code-csharp[Conceptual.Encoding#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/custom1.cs#7)]
[!code-vb[Conceptual.Encoding#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/custom1.vb#7)]

## <a name="see-also"></a>Zobacz także

- [Wprowadzenie do kodowania znaków w programie .NET](character-encoding-introduction.md)
- <xref:System.Text.Encoder>
- <xref:System.Text.Decoder>
- <xref:System.Text.DecoderFallback>
- <xref:System.Text.Encoding>
- <xref:System.Text.EncoderFallback>
- [Globalizacja i lokalizacja](../globalization-localization/index.md)
