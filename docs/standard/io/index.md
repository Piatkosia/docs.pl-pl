---
title: We/wy plików i strumienia — .NET
description: Poznaj podstawy operacji we/wy plików i strumienia, które są transferem danych do lub z nośnika magazynu w programie .NET.
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- IO namespace
- files, I/O
- System.IO namespace
- I/O [.NET]
- streams, I/O
- data streams, I/O
ms.assetid: 4f4a33a9-66b7-4cd7-a285-4ad3e4276cd2
ms.openlocfilehash: aced59995c8d0f478d0565c8fb8faa4f40c32968
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/02/2020
ms.locfileid: "93189202"
---
# <a name="file-and-stream-io"></a>We/Wy plików i strumieni

Termin „We/Wy (wejście/wyjście) plików i strumieni” dotyczy transferu danych do lub z nośnika magazynowania. W programie .NET `System.IO` przestrzenie nazw zawierają typy umożliwiające odczyt i zapis, zarówno synchronicznie, jak i asynchronicznie, w strumieniach danych i plikach. Te przestrzenie nazw zawierają również typy, które wykonują kompresję i dekompresję plików, oraz typy, które umożliwiają komunikację za pośrednictwem potoków i portów szeregowych.

Plik to uporządkowana i nazwana kolekcja bajtów, która ma stały magazyn. Podczas pracy z plikami użytkownik pracuje ze ścieżkami katalogów, magazynem dysku oraz nazwami plików i katalogów. Natomiast strumień to sekwencja bajtów służąca do odczytu i zapisu w magazynie zapasowym, który może być jednym z kilku nośników magazynu (na przykład dysk lub pamięć). Tak jak istnieje kilka magazynów zapasowych innych niż dyski, tak samo istnieje kilka rodzajów strumieni innych niż strumienie plików, takie jak strumienie sieci, pamięci i potoku.

## <a name="files-and-directories"></a>Pliki i katalogi

Możesz użyć typów w <xref:System.IO?displayProperty=nameWithType> przestrzeni nazw do współpracy z plikami i katalogami. Na przykład można pobierać i ustawiać właściwości plików i katalogów oraz pobierać kolekcje plików i katalogów na podstawie kryteriów wyszukiwania.

W przypadku konwencji nazewnictwa ścieżek i sposobów wyrażania ścieżki plików dla systemów Windows, w tym z składnią urządzenia DOS obsługiwaną w programie .NET Core 1,1 i nowszych .NET Framework i nowszych, zobacz [formaty ścieżki plików w systemach Windows](file-path-formats.md).

Poniżej przedstawiono kilka powszechnie używanych klas związanych z plikami i katalogami:

- <xref:System.IO.File> — zawiera metody statyczne służące do tworzenia, kopiowania, usuwania, przemieszczania i otwierania plików oraz ułatwiają tworzenie <xref:System.IO.FileStream> obiektów.

- <xref:System.IO.FileInfo> — zawiera metody wystąpień służące do tworzenia, kopiowania, usuwania, przemieszczania i otwierania plików oraz pomaga utworzyć <xref:System.IO.FileStream> obiekt.

- <xref:System.IO.Directory> — zawiera metody statyczne służące do tworzenia, przechodzenia i wyliczania katalogów i podkatalogów.

- <xref:System.IO.DirectoryInfo> — zawiera metody wystąpień służące do tworzenia, przechodzenia i wyliczania katalogów i podkatalogów.

- <xref:System.IO.Path> — dostarcza metody i właściwości do przetwarzania ciągów katalogów w sposób Międzyplatformowy.

Podczas wywoływania metod systemu plików należy zawsze zapewnić niezawodną obsługę wyjątków. Aby uzyskać więcej informacji, zobacz [Obsługa błędów we/wy](handling-io-errors.md).

Oprócz korzystania z tych klas Visual Basic użytkownicy mogą używać metod i właściwości dostarczonych przez <xref:Microsoft.VisualBasic.FileIO.FileSystem?displayProperty=nameWithType> klasę dla operacji we/wy pliku.

Zobacz [jak: kopiowanie katalogów](how-to-copy-directories.md), [instrukcje: Tworzenie listy](/previous-versions/dotnet/netframework-4.0/5cf8zcfh(v=vs.100))katalogów i [instrukcje: Wyliczanie katalogów i plików](how-to-enumerate-directories-and-files.md).

## <a name="streams"></a>Strumienie

Abstrakcyjna klasa bazowa <xref:System.IO.Stream> obsługuje odczytywanie i zapisywanie bajtów. Wszystkie klasy, które reprezentują strumienie dziedziczące z <xref:System.IO.Stream> klasy. <xref:System.IO.Stream>Klasa i jej klasy pochodne zapewniają wspólny widok źródeł danych i repozytoriów oraz izoluje programistę od konkretnych szczegółów dotyczących systemu operacyjnego i urządzeń bazowych.

Strumienie obejmują trzy podstawowe operacje:

- Odczyt — transfer danych ze strumienia do struktury danych, takiej jak tablica bajtów.

- Zapis — transfer danych ze strumienia do źródła danych.

- Wyszukiwanie — badanie i modyfikowanie bieżącej pozycji w strumieniu.

W zależności od podstawowego źródła danych lub repozytorium, strumień może obsługiwać tylko niektóre z tych możliwości. Na przykład Klasa nie <xref:System.IO.Pipes.PipeStream> obsługuje wyszukiwania. <xref:System.IO.Stream.CanRead%2A>Właściwości, <xref:System.IO.Stream.CanWrite%2A> , i <xref:System.IO.Stream.CanSeek%2A> strumienia określają operacje obsługiwane przez strumień.

Poniżej przedstawiono niektóre powszechnie używane klasy strumieni:

- <xref:System.IO.FileStream> — do odczytu i zapisu w pliku.

- <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream> — do odczytu i zapisu w pliku w magazynie izolowanym.

- <xref:System.IO.MemoryStream> — do odczytu i zapisu do pamięci jako magazynu zapasowego.

- <xref:System.IO.BufferedStream> — w celu zwiększenia wydajności operacji odczytu i zapisu.

- <xref:System.Net.Sockets.NetworkStream> — do odczytu i zapisu w gniazdach sieciowych.

- <xref:System.IO.Pipes.PipeStream> — do odczytu i zapisu w przypadku potoków anonimowych i nazwanych.

- <xref:System.Security.Cryptography.CryptoStream> — służy do łączenia strumieni danych z transformacjami kryptograficznymi.

Aby zapoznać się z przykładem asynchronicznej pracy z strumieniami, zobacz [asynchroniczne operacje we/wy pliku](asynchronous-file-i-o.md).

## <a name="readers-and-writers"></a>Czytelnicy i autorzy

<xref:System.IO?displayProperty=nameWithType>Przestrzeń nazw udostępnia również typy do odczytywania zakodowanych znaków ze strumieni i zapisywania ich w strumieniach. Zazwyczaj strumienie są projektowane do obsługi bajtowych danych wejściowych i wyjściowych. Typy czytników i składników zapisywania obsługują konwersję zakodowanych znaków do i z postaci bajtowej, więc strumień może ukończyć operację. Każda Klasa czytnika i składnika zapisywania jest skojarzona ze strumieniem, który można pobrać za pomocą `BaseStream` właściwości klasy.

Poniżej przedstawiono niektóre powszechnie używane klasy czytników i składników zapisywania:

- <xref:System.IO.BinaryReader> i <xref:System.IO.BinaryWriter> — do odczytywania i pisania typów danych pierwotnych jako wartości binarnych.

- <xref:System.IO.StreamReader> i <xref:System.IO.StreamWriter> — do odczytywania i pisania znaków przy użyciu wartości kodowania do konwersji znaków na i z bajtów.

- <xref:System.IO.StringReader> i <xref:System.IO.StringWriter> — do odczytu i zapisu znaków do i z ciągów.

- <xref:System.IO.TextReader> i <xref:System.IO.TextWriter> — służy jako abstrakcyjne klasy bazowe dla innych czytelników i autorów, które odczytują i zapisują znaki i ciągi, ale nie dane binarne.

Zobacz [jak: odczytywanie tekstu z pliku](how-to-read-text-from-a-file.md), [jak: pisać tekst do pliku](how-to-write-text-to-a-file.md), [instrukcje: odczytywanie znaków z ciągu](how-to-read-characters-from-a-string.md)i [instrukcje: Wpisywanie znaków w ciągu](how-to-write-characters-to-a-string.md).

## <a name="asynchronous-io-operations"></a>Asynchroniczne operacje we/wy

Odczyt lub zapis dużej ilości danych może wymagać użycia wielu zasobów. Te zadania należy wykonywać asynchronicznie, jeśli aplikacja ma ciągle reagować na działania użytkownika. Podczas synchronicznych operacji We/Wy wątek interfejsu użytkownika jest blokowany, aż do zakończenia wykonywania zasobochłonnej operacji.  Podczas tworzenia aplikacji do sklepu Windows 8. x używaj asynchronicznych operacji we/wy, aby zapobiec tworzeniu wrażenie, że aplikacja przestała działać.

Asynchroniczne elementy członkowskie zawierają `Async` nazwy, takie jak <xref:System.IO.Stream.CopyToAsync%2A> ,, <xref:System.IO.Stream.FlushAsync%2A>  <xref:System.IO.Stream.ReadAsync%2A> , i <xref:System.IO.Stream.WriteAsync%2A> metody. Te metody są używane z `async` `await` słowami kluczowymi i.

Aby uzyskać więcej informacji, zobacz [asynchroniczne operacje we/wy na plikach](asynchronous-file-i-o.md).

## <a name="compression"></a>Kompresja

Termin „kompresja” dotyczy procesu zmniejszania rozmiaru pliku, który ma być przechowywany. Dekompresja to proces wyodrębniania zawartości skompresowanego pliku, dzięki czemu będzie on miał format umożliwiający używanie go. <xref:System.IO.Compression?displayProperty=nameWithType>Przestrzeń nazw zawiera typy służące do kompresowania i dekompresowania plików i strumieni.

Następujące klasy są często używane podczas kompresowania i dekompresowania plików i strumieni:

- <xref:System.IO.Compression.ZipArchive> — służy do tworzenia i pobierania wpisów w archiwum zip.

- <xref:System.IO.Compression.ZipArchiveEntry> — dla reprezentowania skompresowanego pliku.

- <xref:System.IO.Compression.ZipFile> — na potrzeby tworzenia, wyodrębniania i otwierania skompresowanego pakietu.

- <xref:System.IO.Compression.ZipFileExtensions> — służy do tworzenia i wyodrębniania wpisów w skompresowanym pakiecie.

- <xref:System.IO.Compression.DeflateStream> — na potrzeby kompresowania i dekompresowania strumieni przy użyciu algorytmu Wklęśnięcie.

- <xref:System.IO.Compression.GZipStream> — na potrzeby kompresowania i dekompresowania strumieni w formacie gzip.

Zobacz [jak: kompresowanie i wyodrębnianie plików](how-to-compress-and-extract-files.md).

## <a name="isolated-storage"></a>Wydzielona pamięć masowa

Wydzielona pamięć masowa to mechanizm magazynu, który dostarcza izolację i bezpieczeństwo przez definiowanie ustandaryzowanych metod kojarzenia kodu z zapisanymi danymi. Ta pamięć masowa oferuje wirtualny system plików, który jest izolowany dla konkretnego użytkownika, zestawu i (opcjonalnie) domeny. Wydzielona pamięć masowa jest szczególnie użyteczna, gdy aplikacja nie ma uprawnień dostępu do plików użytkownika. Można zapisać ustawienia lub pliki aplikacji w sposób, który jest kontrolowany przez zasady zabezpieczeń komputera.

Izolowany magazyn nie jest dostępny dla aplikacji ze sklepu Windows 8. x. Zamiast tego należy używać klas danych aplikacji w <xref:Windows.Storage?displayProperty=nameWithType> przestrzeni nazw. Aby uzyskać więcej informacji, zobacz [dane aplikacji](/previous-versions/windows/apps/hh464917(v=win.10)).

Podczas implementowania wydzielonej pamięci masowej często używane są następujące klasy:

- <xref:System.IO.IsolatedStorage.IsolatedStorage> — udostępnia klasę bazową dla zaizolowanych implementacji magazynu.

- <xref:System.IO.IsolatedStorage.IsolatedStorageFile> — zapewnia izolowany obszar przechowywania zawierający pliki i katalogi.

- <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream> — udostępnia plik w magazynie izolowanym.

Zobacz [izolowany magazyn](isolated-storage.md).

## <a name="io-operations-in-windows-store-apps"></a>Operacje we/wy w aplikacjach ze sklepu Windows

Aplikacje ze sklepu .NET dla systemu Windows 8. x zawierają wiele typów do odczytu i zapisu do strumieni; Jednak ten zestaw nie obejmuje wszystkich typów we/wy platformy .NET.

Kilka ważnych różnic podczas korzystania z operacji we/wy w aplikacjach ze sklepu Windows 8. x:

- Typy przeznaczone wyłącznie dla operacji na plikach, takich <xref:System.IO.File> jak <xref:System.IO.FileInfo> , <xref:System.IO.Directory> i <xref:System.IO.DirectoryInfo> , nie są zawarte w aplikacji ze sklepu .NET dla systemu Windows 8. x. Zamiast tego należy użyć typów w <xref:Windows.Storage?displayProperty=nameWithType> przestrzeni nazw środowisko wykonawcze systemu Windows, takich jak <xref:Windows.Storage.StorageFile> i <xref:Windows.Storage.StorageFolder> .

- Magazyn izolowany nie jest dostępny. Zamiast tego należy użyć [danych aplikacji](/previous-versions/windows/apps/hh464917(v=win.10)).

- Użyj metod asynchronicznych, takich jak <xref:System.IO.Stream.ReadAsync%2A> i <xref:System.IO.Stream.WriteAsync%2A> , aby zapobiec blokowaniu wątku interfejsu użytkownika.

- Typy kompresji oparte na ścieżce <xref:System.IO.Compression.ZipFile> i <xref:System.IO.Compression.ZipFileExtensions> nie są dostępne. Zamiast tego należy użyć typów w <xref:Windows.Storage.Compression?displayProperty=nameWithType> przestrzeni nazw.

W razie potrzeby można wykonywać konwersje między strumieniami programu .NET Framework i strumieniami środowiska wykonawczego systemu Windows. Aby uzyskać więcej informacji, zobacz [jak: konwertowanie między strumieniami .NET Framework a strumieniami środowisko wykonawcze systemu Windows](how-to-convert-between-dotnet-streams-and-winrt-streams.md) lub <xref:System.IO.WindowsRuntimeStreamExtensions> .

Aby uzyskać więcej informacji na temat operacji we/wy w aplikacji ze sklepu Windows 8. x, zobacz [Szybki Start: odczytywanie i zapisywanie plików](/previous-versions/windows/apps/hh758325(v=win.10)).

## <a name="io-and-security"></a>We/wy i zabezpieczenia

W przypadku używania klas w <xref:System.IO?displayProperty=nameWithType> przestrzeni nazw należy spełnić wymagania dotyczące zabezpieczeń systemu operacyjnego, takie jak listy kontroli dostępu (ACL), aby kontrolować dostęp do plików i katalogów. To wymaganie jest uzupełnieniem jakichkolwiek <xref:System.Security.Permissions.FileIOPermission> wymagań. Listami ACL można zarządzać programowo. Aby uzyskać więcej informacji, zobacz [jak: Dodawanie lub usuwanie wpisów listy Access Control](how-to-add-or-remove-access-control-list-entries.md).

Domyślne zasady zabezpieczeń uniemożliwiają aplikacjom internetowym i intranetowym uzyskiwanie dostępu do plików na komputerze użytkownika. W związku z tym nie należy używać klas we/wy, które wymagają ścieżki do pliku fizycznego podczas pisania kodu, który zostanie pobrany za pośrednictwem Internetu lub intranetu. Zamiast tego należy używać [izolowanego magazynu](isolated-storage.md) dla aplikacji platformy .NET.

Sprawdzanie zabezpieczeń jest wykonywane tylko wtedy, gdy jest konstruowany strumień. W związku z tym nie należy otwierać strumienia, a następnie przekazywać go do kodu lub domeny aplikacji o niższym poziomie zaufania.

## <a name="related-topics"></a>Powiązane tematy

- [Typowe zadania we/wy](common-i-o-tasks.md)\
Lista zadań We/Wy skojarzonych z plikami, katalogami, i strumieniami oraz łącza do odpowiedniej zawartości i przykładów dla każdego zadania.

- [Asynchroniczne operacje we/wy pliku](asynchronous-file-i-o.md)\
Opis korzyści związanych z wydajnością oraz podstawowych asynchronicznych operacji We/Wy.

- [Magazyn izolowany](isolated-storage.md)\
Opis mechanizmu pamięci masowej danych, który dostarcza izolację i bezpieczeństwo przez definiowanie ustandaryzowanych opcji kojarzenia kodu z zapisanymi danymi.

- [Rurach](pipe-operations.md)\
Opisuje operacje anonimowe i nazwane potoki w programie .NET.

- [Pliki mapowane w pamięci](memory-mapped-files.md)\
Opis plików zamapowanych w pamięci, które zawierają zawartość plików znajdujących się na dysku w pamięci wirtualnej. Zamapowanych w pamięci plików można używać, aby edytować bardzo duże pliki i tworzyć współużytkowaną pamięć służącą do komunikacji między procesami.
