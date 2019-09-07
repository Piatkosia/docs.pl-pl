---
title: Przepływ pracy tworzenia oprogramowania dla aplikacji platformy Docker
description: Zapoznaj się ze szczegółami przepływu pracy dotyczącymi tworzenia aplikacji opartych na platformie Docker. Rozpocznij krok po kroku i przejdź do szczegółów, aby zoptymalizować wieloetapowe dockerfile i zakończyć pracę z uproszczonym przepływem pracy dostępnym w przypadku korzystania z programu Visual Studio.
ms.date: 01/07/2019
ms.openlocfilehash: 34d2a90cb5208736b1b414e25ac3e627929f45a0
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/30/2019
ms.locfileid: "70296176"
---
# <a name="development-workflow-for-docker-apps"></a>Przepływ pracy tworzenia oprogramowania dla aplikacji platformy Docker

Cykl życia aplikacji jest uruchamiany na komputerze, jako deweloper, w którym można nakodować aplikację przy użyciu preferowanego języka i testować go lokalnie. Za pomocą tego przepływu pracy niezależnie od tego, jaki język, struktura i platforma wybierzesz, zawsze opracowujesz i testujesz kontenery Docker, ale wykonujesz je lokalnie.

Każdy kontener (wystąpienie obrazu platformy Docker) zawiera następujące składniki:

- Wybór systemu operacyjnego, na przykład, dystrybucja systemu Linux, Windows nano Server lub Windows Server Core.

- Pliki dodawane podczas opracowywania, na przykład kod źródłowy i pliki binarne aplikacji.

- Informacje o konfiguracji, takie jak ustawienia środowiska i zależności.

## <a name="workflow-for-developing-docker-container-based-applications"></a>Przepływ pracy dla opracowywania aplikacji opartych na kontenerach platformy Docker

W tej sekcji opisano przepływ pracy programowania w *pętli wewnętrznej* dla aplikacji opartych na kontenerach platformy Docker. Przepływ pracy z pętlą wewnętrzną oznacza, że nie rozważa on szerszego przepływu pracy DevOps, który może obejmować wdrożenie w środowisku produkcyjnym, a jedynie koncentruje się na rozwoju pracy na komputerze dewelopera. Początkowe kroki konfigurowania środowiska nie są uwzględniane, ponieważ te kroki są wykonywane tylko raz.

Aplikacja składa się z własnych usług i dodatkowych bibliotek (zależności). Poniżej przedstawiono podstawowe kroki, które zwykle są wykonywane podczas kompilowania aplikacji platformy Docker, jak pokazano na rysunku 5-1.

![Proces opracowywania aplikacji platformy Docker: 1. Zakoduj aplikację, 2-Write pliku dockerfile/s, 3 — Tworzenie obrazów zdefiniowanych w pliku dockerfile/s, 4 — (opcjonalnie) redagowanie usług w pliku Docker-Compose. yml, 5-lub aplikacji platformy Docker, 6 — Testowanie aplikacji lub mikrousług, 7 — wypychanie do repozytorium i powtarzanie. ](./media/image1.png)

**Rysunek 5-1.** Przepływ pracy krok po kroku dla opracowywania aplikacji w kontenerze platformy Docker

W tej sekcji opisano szczegółowy proces, a każdy z najważniejszych kroków jest wyjaśniony przez skoncentrowanie się na środowisku programu Visual Studio.

W przypadku korzystania z podejścia edytora/interfejsu wiersza polecenia (na przykład Visual Studio Code i interfejsu wiersza polecenia platformy Docker w systemie macOS lub Windows) należy wiedzieć każdy krok, ogólnie bardziej szczegółowo niż w przypadku korzystania z programu Visual Studio. Aby uzyskać więcej informacji na temat pracy w środowisku interfejsu wiersza polecenia, zapoznaj się z [cyklem życia aplikacji platformy Docker w książce elektronicznej przy użyciu platform i narzędzi firmy Microsoft](https://aka.ms/dockerlifecycleebook/).

W przypadku korzystania z programu Visual Studio 2017 wiele z tych kroków jest obsługiwanych przez Ciebie, co znacznie zwiększa wydajność pracy. Jest to szczególnie prawdziwe w przypadku korzystania z programu Visual Studio 2017 i określania aplikacji obsługujących wiele kontenerów. Na przykład po kliknięciu tylko jednego kliknięcia myszą program Visual Studio dodaje plik pliku dockerfile i Docker-Compose. yml do projektów z konfiguracją dla aplikacji. Po uruchomieniu aplikacji w programie Visual Studio kompiluje ona obraz platformy Docker i uruchamia aplikację wielokontenerową bezpośrednio w Docker; Umożliwia to nawet debugowanie kilku kontenerów jednocześnie. Te funkcje spowodują zwiększenie szybkości tworzenia oprogramowania.

Jednak po prostu, ponieważ program Visual Studio wykonuje te czynności automatycznie nie oznacza to, że nie musisz wiedzieć, co się dzieje w objściu z platformą Docker. W związku z tym poniższe wskazówki zawierają szczegółowe informacje o każdym kroku.

![1 — kod aplikacji](./media/image2.png)

## <a name="step-1-start-coding-and-create-your-initial-application-or-service-baseline"></a>Krok 1. Rozpocznij kodowanie i Utwórz początkową aplikację lub linię bazową usługi

Tworzenie aplikacji platformy Docker jest podobne do sposobu tworzenia aplikacji bez platformy Docker. Różnica polega na tym, że podczas tworzenia aplikacji dla platformy Docker wdrażane i testowane są aplikacje lub usługi działające w kontenerach platformy Docker w środowisku lokalnym (Konfiguracja maszyny wirtualnej z systemem Linux przez platformę Docker lub bezpośrednio w systemie Windows, jeśli są używane kontenery systemu Windows).

### <a name="set-up-your-local-environment-with-visual-studio"></a>Konfigurowanie środowiska lokalnego przy użyciu programu Visual Studio

Aby rozpocząć, upewnij się, że masz zainstalowaną [platformę Docker Community Edition (CE)](https://docs.docker.com/docker-for-windows/) dla systemu Windows, zgodnie z opisem w poniższych instrukcjach:

[Wprowadzenie do Docker CE for Windows](https://docs.docker.com/docker-for-windows/)

Ponadto konieczne jest zainstalowanie programu Visual Studio 2017 w wersji 15,7 lub nowszej z zainstalowanym **międzyplatformowym obciążeniem programistycznym platformy .NET Core** , jak pokazano na rysunku 5-2.

![Wybór obciążenia dla wielu platform w programie .NET Core podczas instalacji programu Visual Studio.](./media/image3.png)

**Rysunek 5-2**. Wybieranie obciążenia **programowania dla wielu platform .NET Core** podczas instalacji programu Visual Studio 2017

Możesz rozpocząć kodowanie aplikacji w zwykłym środowisku .NET (zwykle w programie .NET Core, jeśli planujesz korzystanie z kontenerów) nawet przed włączeniem platformy Docker w aplikacji oraz wdrożenie i przetestowanie na platformie Docker. Zaleca się jednak rozpoczęcie pracy z platformą Docker najszybciej, jak to możliwe, ponieważ będzie to realne środowisko i ewentualne problemy mogą zostać odnalezione najszybciej, jak to możliwe. Jest to zalecane, ponieważ program Visual Studio ułatwia współpracę z platformą Docker, która niemal jest przejrzysta — najlepszym przykładem w przypadku debugowania aplikacji wielokontenerowych z programu Visual Studio.

### <a name="additional-resources"></a>Dodatkowe zasoby

- **Wprowadzenie do Docker CE for Windows** \
  <https://docs.docker.com/docker-for-windows/>

- **Visual Studio 2017** \
  [https://visualstudio.microsoft.com/downloads/](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2017)

![2 — wieloetapowe dockerfile zapisu](./media/image4.png)

## <a name="step-2-create-a-dockerfile-related-to-an-existing-net-base-image"></a>Krok 2. Tworzenie pliku dockerfile związanych z istniejącym obrazem podstawowym platformy .NET

Dla każdego niestandardowego obrazu, który chcesz skompilować, potrzebujesz pliku dockerfile. wymagany jest również pliku dockerfile dla każdego kontenera do wdrożenia, niezależnie od tego, czy wdrażasz automatycznie z programu Visual Studio, czy ręcznie przy użyciu interfejsu wiersza polecenia platformy Docker (narzędzia Docker Run i Docker-redagowanie). Jeśli aplikacja zawiera pojedynczą usługę niestandardową, potrzebna jest jedna pliku dockerfile. Jeśli aplikacja zawiera wiele usług (podobnie jak w przypadku architektury mikrousług), potrzebna jest jedna pliku dockerfile dla każdej usługi.

Pliku dockerfile jest umieszczany w folderze głównym aplikacji lub usługi. Zawiera polecenia, które informują platformę Docker, jak skonfigurować i uruchomić aplikację lub usługę w kontenerze. Możesz ręcznie utworzyć pliku dockerfile w kodzie i dodać go do projektu wraz z zależnościami programu .NET.

Za pomocą programu Visual Studio i jego narzędzi dla platformy Docker to zadanie wymaga tylko kilku kliknięć myszą. Podczas tworzenia nowego projektu w programie Visual Studio 2017 istnieje opcja o nazwie **Włącz kontener (Docker)** , jak pokazano na rysunku 5-3.

![Pole wyboru Włącz obsługę platformy Docker podczas tworzenia nowego projektu ASP.NET Core w programie Visual Studio 2017](./media/image5.png)

**Rysunek 5-3**. Włączanie obsługi platformy Docker podczas tworzenia nowego projektu ASP.NET Core w programie Visual Studio 2017

Możesz również włączyć obsługę platformy Docker w istniejącym projekcie aplikacji sieci Web ASP.NET Core, klikając prawym przyciskiem myszy projekt w **Eksplorator rozwiązań** i wybierając polecenie **Dodaj** > **obsługę platformy Docker**, jak pokazano na rysunku 5-4.

![Opcja menu Dodaj obsługę platformy Docker w programie Visual Studio](./media/image6.png)

**Rysunek 5-4**. Włączanie obsługi platformy Docker w istniejącym projekcie programu Visual Studio 2017

Ta akcja dodaje *pliku dockerfile* do projektu z wymaganą konfiguracją i jest dostępna tylko w projektach ASP.NET Core.

W podobny sposób program Visual Studio może również dodać plik Docker-Compose. yml dla całego rozwiązania przy użyciu opcji **dodaj > kontener Orchestrator support**. W kroku 4 podaliśmy tę opcję bardziej szczegółowo.

### <a name="using-an-existing-official-net-docker-image"></a>Korzystanie z istniejącego oficjalnego obrazu platformy Docker .NET

Zwykle można utworzyć niestandardowy obraz dla kontenera na podstawie obrazu podstawowego, który uzyskuje się z oficjalnego repozytorium, takiego jak rejestr usługi [Docker Hub](https://hub.docker.com/) . To dokładnie, co się dzieje w przypadku włączenia obsługi platformy Docker w programie Visual Studio. Pliku dockerfile będzie używać istniejącego `aspnetcore` obrazu.

Wcześniej objaśniono, które obrazy platformy Docker i repozytoria, których można użyć, w zależności od wybranego środowiska i systemu operacyjnego. Na przykład jeśli chcesz używać ASP.NET Core (Linux lub Windows), obraz do użycia to `mcr.microsoft.com/dotnet/core/aspnet:2.2`. W związku z tym wystarczy określić podstawowy obraz platformy Docker, który będzie używany w danym kontenerze. Możesz to zrobić, dodając `FROM mcr.microsoft.com/dotnet/core/aspnet:2.2` do pliku dockerfile. Ta wartość zostanie automatycznie wykonana przez program Visual Studio, ale jeśli zaktualizowano wersję, należy ją zaktualizować.

Korzystanie z oficjalnego repozytorium programu .NET Image z usługi Docker Hub z numerem wersji zapewnia, że te same funkcje językowe są dostępne na wszystkich komputerach (w tym na temat programowania, testowania i produkcji).

W poniższym przykładzie przedstawiono przykładową pliku dockerfile dla kontenera ASP.NET Core.

```Dockerfile
FROM mcr.microsoft.com/dotnet/core/aspnet:2.2
ARG source
WORKDIR /app
EXPOSE 80
COPY ${source:-obj/Docker/publish} .
ENTRYPOINT ["dotnet", " MySingleContainerWebApp.dll "]
```

W tym przypadku obraz jest oparty na wersji 2,2 ASP.NET Core oficjalnego obrazu platformy Docker (wiele rozwiązań dla systemów Linux i Windows). To ustawienie `FROM mcr.microsoft.com/dotnet/core/aspnet:2.2`. (Aby uzyskać więcej informacji na temat tego obrazu podstawowego, zobacz stronę [obrazu platformy Docker programu .NET Core](https://hub.docker.com/_/microsoft-dotnet-core/) ). W pliku dockerfile należy również nakazać platformie Docker nasłuchiwanie na porcie TCP, który będzie używany w środowisku uruchomieniowym (w tym przypadku port 80, zgodnie z konfiguracją ustawienia UWIDACZNIAnia).

Możesz określić dodatkowe ustawienia konfiguracji w pliku dockerfile, w zależności od używanego języka i platformy. Na przykład wiersz `["dotnet", "MySingleContainerWebApp.dll"]` punktu wejścia informuje platformę Docker, aby uruchomić aplikację platformy .NET Core. Jeśli używasz zestawu SDK i interfejs wiersza polecenia platformy .NET Core (interfejs dotnet CLI) do kompilowania i uruchamiania aplikacji .NET, to ustawienie będzie inne. Dolna linia polega na tym, że linia ENTRYPOINT i inne ustawienia będą się różnić w zależności od języka i platformy wybranej dla aplikacji.

### <a name="additional-resources"></a>Dodatkowe zasoby

- **Kompilowanie obrazów platformy Docker dla aplikacji platformy .NET Core** \
  [https://docs.microsoft.com/dotnet/core/docker/building-net-docker-images](../../../core/docker/building-net-docker-images.md)

- **Utwórz własny obraz**. W oficjalnej dokumentacji platformy Docker. \
  <https://docs.docker.com/engine/tutorials/dockerimages/>

- **Aktualne z użyciem obrazów kontenerów platformy .NET** \
  <https://devblogs.microsoft.com/dotnet/staying-up-to-date-with-net-container-images/>

- **Korzystanie z programu .NET i platformy Docker razem z aktualizacją DockerCon 2018** \
  <https://devblogs.microsoft.com/dotnet/using-net-and-docker-together-dockercon-2018-update/>

### <a name="using-multi-arch-image-repositories"></a>Używanie repozytoriów obrazów wieloskładnikowych

Pojedyncze repozytorium może zawierać warianty platformy, takie jak obraz systemu Linux i obraz Windows. Ta funkcja umożliwia dostawcom, takim jak firma Microsoft (twórcy obrazów podstawowych), tworzenie jednego repozytorium w celu pokrycia wielu platform (z systemem Linux i Windows). Na przykład repozytorium [dotnet/Core](https://hub.docker.com/_/microsoft-dotnet-core/) dostępne w rejestrze usługi Docker Hub zapewnia obsługę systemu Linux i Windows nano Server przy użyciu tej samej nazwy repozytorium.

Jeśli określisz tag, nadajesz platformie, która jest jawna, jak w następujących przypadkach:

- `microsoft/dotnet:2.2-aspnetcore-runtime-stretch-slim` \
  Elementy docelowe: środowisko uruchomieniowe programu .NET Core 2,2 — tylko w systemie Linux

- `microsoft/dotnet:2.2-aspnetcore-runtime-nanoserver-1809` \
  Targets: środowisko uruchomieniowe programu .NET Core 2,2 — tylko w systemie Windows nano Server

Ale w przypadku określenia tej samej nazwy obrazu, nawet w tym samym tagu, obrazy z obsługą wielodostępności (na `aspnetcore` przykład obraz) będą używały wersji systemu Linux lub Windows w zależności od wdrażanego systemu operacyjnego hosta platformy Docker, jak pokazano w następującym przykładzie:

- `microsoft/dotnet:2.2-aspnetcore-runtime` \
  Wiele arch: środowisko uruchomieniowe programu .NET Core 2,2 — tylko w systemie Linux lub Windows nano Server w zależności od systemu operacyjnego hosta platformy Docker

W ten sposób podczas ściągania obrazu z hosta z systemem Windows zostanie ściągnięty wariant systemu Windows, a pociągnięcie tego samego obrazu z hosta z systemem Linux spowoduje pobranie wariantu z systemem Linux.

### <a name="multi-stage-builds-in-dockerfile"></a>Kompilacje wieloetapowe w pliku dockerfile

Pliku dockerfile jest podobny do skryptu wsadowego. Podobnie jak w przypadku konfigurowania maszyny z poziomu wiersza polecenia.

Rozpoczyna się od obrazu podstawowego, który konfiguruje kontekst początkowy, podobnie jak startowy system plików, który znajduje się na szczycie systemu operacyjnego hosta. Nie jest to system operacyjny, ale możesz określić, czy tak jak w przypadku systemu operacyjnego w kontenerze.

Wykonanie każdego wiersza polecenia powoduje utworzenie nowej warstwy w systemie plików ze zmianami z poprzedniego, tak aby w przypadku łączenia wygenerowała system plików w systemie.

Ze względu na to, że każda nowa warstwa "zatrzyma się" na poprzednim, a rozmiar obrazu pojawia się w każdym poleceniu, obrazy mogą być bardzo duże, jeśli trzeba je uwzględnić, na przykład zestaw SDK, który jest wymagany do kompilowania i publikowania aplikacji.

Jest to miejsce, w którym kompilacje wieloetapowe są uzyskiwane na powierzchni (od platformy Docker 17,05 lub nowszej), aby wykonać ich magiczną.

Głównym pomysłem jest to, że można oddzielić proces wykonywania pliku dockerfile w etapach, gdzie etap jest obrazem początkowym, po którym następuje co najmniej jedno polecenie, a ostatni etap Określa końcowy rozmiar obrazu.

W krótkim przypadku kompilacje wieloetapowe umożliwiają podział tworzenia w różnych fazach, a następnie złożenie obrazu końcowego, pobierając tylko odpowiednie katalogi z etapów pośrednich. Ogólna strategia korzystania z tej funkcji to:

1. Użyj podstawowego obrazu zestawu SDK (niezależnie od tego, jak jest to duże), ze wszystkimi elementami potrzebnymi do kompilowania i publikowania aplikacji w folderze, a następnie

2. Użyj obrazu podstawowego, małego, samego środowiska uruchomieniowego i skopiuj folder publikacji z poprzedniego etapu, aby utworzyć mały obraz końcowy.

Prawdopodobnie najlepszym sposobem na zrozumienie wieloetapowego jest przechodzenie przez pliku dockerfile szczegóły, wiersz po wierszu, więc zaczynamy od początkowego pliku dockerfile utworzonego przez program Visual Studio podczas dodawania obsługi platformy Docker do projektu i przejdziesz do pewnych optymalizacji później.

Początkowy pliku dockerfile może wyglądać następująco:

```Dockerfile
 1  FROM mcr.microsoft.com/dotnet/core/aspnet:2.2 AS base
 2  WORKDIR /app
 3  EXPOSE 80
 4
 5  FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build
 6  WORKDIR /src
 7  COPY src/Services/Catalog/Catalog.API/Catalog.API.csproj …
 8  COPY src/BuildingBlocks/HealthChecks/src/Microsoft.AspNetCore.HealthChecks …
 9  COPY src/BuildingBlocks/HealthChecks/src/Microsoft.Extensions.HealthChecks …
10  COPY src/BuildingBlocks/EventBus/IntegrationEventLogEF/ …
11  COPY src/BuildingBlocks/EventBus/EventBus/EventBus.csproj …
12  COPY src/BuildingBlocks/EventBus/EventBusRabbitMQ/EventBusRabbitMQ.csproj …
13  COPY src/BuildingBlocks/EventBus/EventBusServiceBus/EventBusServiceBus.csproj …
14  COPY src/BuildingBlocks/WebHostCustomization/WebHost.Customization …
15  COPY src/BuildingBlocks/HealthChecks/src/Microsoft.Extensions …
16  COPY src/BuildingBlocks/HealthChecks/src/Microsoft.Extensions …
17  RUN dotnet restore src/Services/Catalog/Catalog.API/Catalog.API.csproj
18  COPY . .
19  WORKDIR /src/src/Services/Catalog/Catalog.API
20  RUN dotnet build Catalog.API.csproj -c Release -o /app
21
22  FROM build AS publish
23  RUN dotnet publish Catalog.API.csproj -c Release -o /app
24
25  FROM base AS final
26  WORKDIR /app
27  COPY --from=publish /app .
28  ENTRYPOINT ["dotnet", "Catalog.API.dll"]
```

Są to szczegóły, wiersz po wierszu:

<!-- markdownlint-disable MD029-->
1. Rozpocznij etap z obrazem podstawowym "mały" tylko środowisko uruchomieniowe, wywołaj jego **bazę** jako odwołanie.
2. Utwórz katalog **/App** w obrazie.
3. Uwidocznij port **80**.
<!-- skip -->
5. Rozpocznij nowy etap przy użyciu obrazu "Large" do kompilowania/publikowania, wywołaj **kompilację do kompilacji** w celu uzyskania odwołania.
6. Utwórz katalog **/src** w obrazie.
7. Do wiersza 16, skopiuj przywoływane pliki projects **. csproj** , aby umożliwić późniejsze przywracanie pakietów.
<!-- skip -->
17. Przywróć pakiety dla projektu **Catalog. API** i projektów, do których istnieją odwołania.
18. Skopiuj **wszystkie drzewa katalogów dla rozwiązania** (z wyjątkiem plików/katalogów znajdujących się w pliku **. dockerignore** ) z katalogu **/src** w obrazie.
19. Zmień bieżący folder na **katalog. interfejs API** .
20. Kompiluj projekt (i inne zależności projektu) i dane wyjściowe do katalogu **/App** w obrazie.
<!-- skip -->
22. Rozpocznij nowy etap Kontynuuj od kompilacji, wywołaj go **,** Aby uzyskać odwołanie.
23. Publikuj projekt (i zależności) i dane wyjściowe do katalogu **/App** w obrazie.
<!-- skip -->
25. Rozpocznij nowy etap, kontynuując od **podstaw** i Wywołaj **ostateczną**
26. Zmień bieżący katalog na **/App**
27. Skopiuj katalog **/App** z **publikacji** Stage do bieżącego katalogu
28. Zdefiniuj polecenie do uruchomienia po rozpoczęciu kontenera.
<!-- markdownlint-enable MD029-->

Teraz zapoznaj się z pewnymi optymalizacjami, aby zwiększyć wydajność całego procesu, która w przypadku eShopOnContainers, oznacza około 22 minut lub dłużej, aby skompilować kompletne rozwiązanie w kontenerach systemu Linux.

Będziesz korzystać z funkcji pamięci podręcznej warstwy platformy Docker, która jest dość prosta: Jeśli obraz podstawowy i polecenia są takie same jak niektóre wcześniej wykonane, można po prostu użyć warstwy, bez konieczności wykonywania poleceń, co spowoduje zapisanie pewnego czasu.

W związku z tym skupmy się na etapie **kompilacji** , wiersze 5-6 są w większości takie same, ale linie 7-17 są różne dla każdej usługi z eShopOnContainers, więc muszą być wykonywane co jeden raz, jednak Jeśli zmieniono wiersze 7-16 na:

```Dockerfile
COPY . .
```

Następnie będzie ona taka sama dla każdej usługi, dlatego skopiuje całe rozwiązanie i utworzy większą warstwę, ale:

1) Proces kopiowania będzie wykonywany tylko po raz pierwszy (oraz podczas ponownego kompilowania, gdy plik zostanie zmieniony) i użyje pamięci podręcznej dla wszystkich innych usług i

2) Ponieważ większy obraz występuje w pośrednim etapie, nie ma wpływu na końcowy rozmiar obrazu.

Kolejna znacząca Optymalizacja obejmuje `restore` polecenie wykonane w wierszu 17, które jest również inne dla każdej usługi eShopOnContainers. Jeśli zmienisz ten wiersz na tylko:

```Dockerfile
RUN dotnet restore
```

Spowoduje to przywrócenie pakietów dla całego rozwiązania, ale następnie ponownie, będzie miało miejsce tylko raz, a nie 15 razy z bieżącą strategią.

Jednak program `dotnet restore` jest uruchamiany tylko wtedy, gdy w folderze istnieje pojedynczy plik projektu lub rozwiązania, więc osiągnięcie tego jest nieco bardziej skomplikowane i sposób jego rozwiązania, bez konieczności zbyt wielu szczegółów:

1. Dodaj następujące wiersze do **. dockerignore**:

   - `*.sln`, aby zignorować wszystkie pliki rozwiązań w głównym drzewie folderów

   - `!eShopOnContainers-ServicesAndWebApps.sln`, aby uwzględnić tylko ten plik rozwiązania.

2. Uwzględnij `dotnet restore`argument do, dlatego również ignoruje projekt platformy Docker-Zredaguj i przywraca tylko pakiety dla rozwiązania eShopOnContainers-ServicesAndWebApps. `/ignoreprojectextensions:.dcproj`

W przypadku optymalizacji końcowej następuje po prostu, że wiersz 20 jest nadmiarowy, ponieważ wiersz 23 również kompiluje aplikację i znajduje się w stanie, bezpośrednio po wierszu 20, dlatego inne czasochłonne polecenie.

Otrzymany plik jest następnie:

```Dockerfile
 1  FROM mcr.microsoft.com/dotnet/core/aspnet:2.2 AS base
 2  WORKDIR /app
 3  EXPOSE 80
 4
 5  FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS publish
 6  WORKDIR /src
 7  COPY . .
 8  RUN dotnet restore /ignoreprojectextensions:.dcproj
 9  WORKDIR /src/src/Services/Catalog/Catalog.API
10  RUN dotnet publish Catalog.API.csproj -c Release -0 /app
11
12  FROM base AS final
13  WORKDIR /app
14  COPY --from=publish /app
15  ENTRYPOINT ["dotnet", "Catalog.API.dll"]
```

### <a name="creating-your-base-image-from-scratch"></a>Tworzenie obrazu podstawowego od podstaw

Możesz utworzyć własny obraz podstawowy platformy Docker od podstaw. Ten scenariusz nie jest zalecany dla osoby, która rozpoczyna się od platformy Docker, ale jeśli chcesz ustawić określone bity obrazu podstawowego, możesz to zrobić.

### <a name="additional-resources"></a>Dodatkowe zasoby

- **Obrazy .NET Core z obsługą wielodostępności**. \
  <https://github.com/dotnet/announcements/issues/14>

- **Utwórz obraz podstawowy**. Oficjalna dokumentacja platformy Docker. \
  <https://docs.docker.com/develop/develop-images/baseimages/>

![3 — Tworzenie obrazów zdefiniowanych w wieloetapowe dockerfile](./media/image7.png)

## <a name="step-3-create-your-custom-docker-images-and-embed-your-application-or-service-in-them"></a>Krok 3. Tworzenie niestandardowych obrazów platformy Docker i osadzanie w nich aplikacji lub usługi

Dla każdej usługi w aplikacji należy utworzyć powiązany obraz. Jeśli aplikacja składa się z pojedynczej usługi lub aplikacji sieci Web, wystarczy tylko jeden obraz.

Należy pamiętać, że obrazy platformy Docker są kompilowane automatycznie w programie Visual Studio. Poniższe kroki są wymagane tylko w przypadku przepływu pracy edytora/interfejsu wiersza polecenia i wyjaśniono, aby wyjaśnić, co się dzieje poniżej.

Programista musi opracowywać i testować lokalnie do momentu wypchnięcia ukończonej funkcji lub zmiany systemu kontroli źródła (na przykład do usługi GitHub). Oznacza to, że należy utworzyć obrazy platformy Docker i wdrożyć kontenery na lokalnym hoście platformy Docker (maszynie wirtualnej z systemem Windows lub Linux) i uruchamiać, testować i debugować względem tych lokalnych kontenerów.

Aby utworzyć niestandardowy obraz w środowisku lokalnym przy użyciu interfejsu wiersza polecenia platformy Docker i pliku dockerfile, można użyć narzędzia Docker Build, jak pokazano na rysunku 5-5.

![Ekran postępu tworzenia obrazu platformy Docker](./media/image8.png)

**Rysunek 5-5**. Tworzenie niestandardowego obrazu platformy Docker

Opcjonalnie, zamiast bezpośrednio uruchamiać kompilację platformy Docker z folderu projektu, można najpierw wygenerować folder do wdrożenia z wymaganymi bibliotekami i plikami binarnymi platformy .NET `dotnet publish`, uruchamiając `docker build` polecenie, a następnie użyć polecenia.

Spowoduje to utworzenie obrazu platformy Docker o nazwie `cesardl/netcore-webapi-microservice-docker:first`. W tym przypadku: pierwszy jest tagiem reprezentującym określoną wersję. Możesz powtórzyć ten krok dla każdego niestandardowego obrazu, który trzeba utworzyć dla złożonej aplikacji platformy Docker.

Gdy aplikacja składa się z wielu kontenerów (czyli aplikacji z wieloma kontenerami), można również użyć `docker-compose up --build` polecenia, aby skompilować wszystkie powiązane obrazy za pomocą jednego polecenia, korzystając z metadanych uwidocznionych w pokrewnych plikach Docker-Compose. yml .

Istniejące obrazy można znaleźć w lokalnym repozytorium za pomocą polecenia Docker images, jak pokazano na rysunku 5-6.

![Widok ekranu obrazów z listy obrazów platformy Docker](./media/image9.png)

**Rysunek 5-6.** Wyświetlanie istniejących obrazów przy użyciu polecenia Docker images

### <a name="creating-docker-images-with-visual-studio"></a>Tworzenie obrazów platformy Docker za pomocą programu Visual Studio

Gdy używasz programu Visual Studio do tworzenia projektu z obsługą platformy Docker, nie utworzysz jawnie obrazu. Zamiast tego obraz jest tworzony po naciśnięciu klawisza **F5** (lub **klawisza CTRL-F5**), aby uruchomić aplikację lub usługę dockerized. Ten krok jest automatycznie w programie Visual Studio i nie jest wyświetlany, ale ważne jest, aby wiedzieć, co się dzieje poniżej.

![4 — (opcjonalnie) redagowanie usług w pliku Docker-Compose. yml](./media/image10.png)

## <a name="step-4-define-your-services-in-docker-composeyml-when-building-a-multi-container-docker-application"></a>Krok 4. Zdefiniuj usługi w Docker-Compose. yml podczas kompilowania aplikacji platformy Docker z obsługą kontenera

Plik [Docker-Compose. yml](https://docs.docker.com/compose/compose-file/) umożliwia zdefiniowanie zestawu powiązanych usług, które mają zostać wdrożone jako aplikacja złożona z poleceniami wdrażania. Konfiguruje także relacje zależności i konfigurację uruchomieniową.

Aby użyć pliku Docker-Compose. yml, należy utworzyć plik w głównym lub głównym folderze rozwiązania o zawartości podobnej do następującej w następującym przykładzie:

```yml
version: '3.4'

services:

  webmvc:
    image: eshop/web
    environment:
      - CatalogUrl=http://catalog.api
      - OrderingUrl=http://ordering.api
    ports:
      - "80:80"
    depends_on:
      - catalog.api
      - ordering.api

  catalog.api:
    image: eshop/catalog.api
    environment:
      - ConnectionString=Server=sql.data;Port=1433;Database=CatalogDB;…
    ports:
      - "81:80"
    depends_on:
      - sql.data

  ordering.api:
    image: eshop/ordering.api
    environment:
      - ConnectionString=Server=sql.data;Database=OrderingDb;…
    ports:
      - "82:80"
    extra_hosts:
      - "CESARDLBOOKVHD:10.0.75.1"
    depends_on:
      - sql.data

  sql.data:
    image: mssql-server-linux:latest
    environment:
      - SA_PASSWORD=Pass@word
      - ACCEPT_EULA=Y
    ports:
      - "5433:1433"
```

Ten plik Docker-Compose. yml jest uproszczoną i scaloną wersją. Zawiera statyczne dane konfiguracji dla każdego kontenera (takie jak nazwa obrazu niestandardowego), które jest zawsze wymagane i informacje o konfiguracji, które mogą być zależne od środowiska wdrażania, takie jak parametry połączenia. W kolejnych sekcjach dowiesz się, jak podzielić konfigurację Docker-Compose. yml na wiele plików programu Docker i zastąpić wartości w zależności od typu środowiska i wykonywania (debugowanie lub wydanie).

Przykład pliku Docker-Compose. yml definiuje cztery usługi `webmvc` : usługa (aplikacja sieci Web), dwa mikrousługi (`ordering.api` i `basket.api` `sql.data`) oraz jeden kontener źródła danych, na podstawie SQL Server dla systemu Linux działającego jako wbudowane. Każda usługa zostanie wdrożona jako kontener, dlatego dla każdego z nich wymagany jest obraz platformy Docker.

Plik Docker-Compose. yml określa nie tylko te kontenery, które są używane, ale w jaki sposób są indywidualnie skonfigurowane. Na przykład `webmvc` definicja kontenera w pliku. yml:

- Używa wstępnie skompilowanego `eshop/web:latest` obrazu. Można jednak skonfigurować obraz, który ma zostać skompilowany w ramach wykonywania operacji Docker — tworzenie z dodatkową konfiguracją w oparciu o kompilację: sekcja w pliku Docker-redagowanie.

- Inicjuje dwie zmienne środowiskowe (CatalogUrl i OrderingUrl).

- Przekazuje uwidoczniony port 80 w kontenerze do zewnętrznego portu 80 na komputerze-hoście.

- Łączy aplikację sieci Web z katalogiem i usługą porządkowania przy użyciu ustawienia depends_on. Powoduje to, że usługa czeka na uruchomienie tych usług.

Będziemy ponownie odwiedzać plik Docker-Compose. yml w dalszej części, gdy będziemy omawiać sposób implementacji mikrousług i aplikacji wielokontenerowych.

### <a name="working-with-docker-composeyml-in-visual-studio-2017"></a>Praca z Docker-Compose. yml w programie Visual Studio 2017

Oprócz dodania pliku dockerfile do projektu, jak wspomniano wcześniej, program Visual Studio 2017 (z 15,8 on) może dodać obsługę programu Orchestrator dla Docker Compose do rozwiązania.

Po dodaniu obsługi programu Orchestrator Container, jak pokazano na rysunku 5-7 po raz pierwszy, program Visual Studio tworzy pliku dockerfile dla projektu i tworzy nowy projekt (sekcja usługi) w rozwiązaniu z kilkoma plikami globalnymi `docker-compose*.yml` , a następnie dodaje projekt do tych plików. Następnie możesz otworzyć pliki Docker-Compose. yml i zaktualizować je za pomocą dodatkowych funkcji.

Musisz powtórzyć ten formularz dla każdego projektu, który ma zostać uwzględniony w pliku Docker-Compose. yml.

W czasie tego pisania program Visual Studio obsługuje Docker Compose i Service Fabric koordynatorów.

![Opcja menu kontekstowego umożliwiająca dodanie obsługi programu Orchestrator do projektu ASP.NET Core](./media/image21.png)

**Rysunek 5-7**. Dodawanie obsługi platformy Docker w programie Visual Studio 2017 przez kliknięcie prawym przyciskiem myszy ASP.NET Core projektu

Po dodaniu obsługi programu Orchestrator do rozwiązania w programie Visual Studio zobaczysz również nowy węzeł (w `docker-compose.dcproj` pliku projektu) w Eksplorator rozwiązań zawierającym dodane pliki Docker-Compose. yml, jak pokazano na rysunku 5-8.

![Docker — Tworzenie węzła w Eksplorator rozwiązań](./media/image11.png)

**Rysunek 5-8**. Węzeł drzewa **platformy Docker — tworzenie** w programie Visual Studio 2017 Eksplorator rozwiązań

Za pomocą `docker-compose up` polecenia można wdrożyć wielokontenerową aplikację z pojedynczym plikiem Docker-Compose. yml. Jednak program Visual Studio dodaje grupę tych grup, aby można było przesłonić wartości w zależności od środowiska (programowania lub produkcji) oraz typu wykonywania (wersja lub debugowanie). Ta funkcja zostanie omówiona w dalszych sekcjach.

![5 — Uruchamianie kontenerów lub aplikacji złożonej](./media/image12.png)

## <a name="step-5-build-and-run-your-docker-application"></a>Krok 5. Kompilowanie i uruchamianie aplikacji platformy Docker

Jeśli aplikacja ma tylko jeden kontener, można uruchomić ją, wdrażając ją na hoście platformy Docker (maszynie wirtualnej lub serwerze fizycznym). Jeśli jednak aplikacja zawiera wiele usług, można wdrożyć ją jako aplikację składającą się z pojedynczego interfejsu wiersza polecenia (Docker-Zredaguj) lub z programem Visual Studio, który będzie używać tego polecenia w obszarze okładki. Przyjrzyjmy się różnym opcjom.

### <a name="option-a-running-a-single-container-application"></a>Opcja A: Uruchamianie aplikacji z jednym kontenerem

#### <a name="using-docker-cli"></a>Korzystanie z interfejsu wiersza polecenia platformy Docker

Kontener platformy Docker można uruchomić za pomocą `docker run` polecenia, jak pokazano na rysunku 5-9:

```console
  docker run -t -d -p 80:5000 cesardl/netcore-webapi-microservice-docker:first
```

Powyższe polecenie spowoduje utworzenie nowego wystąpienia kontenera z określonego obrazu przy każdym uruchomieniu. Można użyć `--name` parametru, aby nadać nazwę kontenerowi, a następnie użyć `docker start {name}` (lub użyć identyfikatora kontenera lub nazwy automatycznej) do uruchomienia istniejącego wystąpienia kontenera.

![Widok ekranu podczas uruchamiania kontenera Docker przy użyciu polecenia Docker Run](./media/image13.png)

**Rysunek 5-9**. Uruchamianie kontenera Docker przy użyciu polecenia Docker Run

W takim przypadku polecenie powiąże wewnętrzny port 5000 kontenera z portem 80 komputera hosta. Oznacza to, że host nasłuchuje na porcie 80 i przesyła dalej do portu 5000 w kontenerze.

Wyświetlany skrót jest identyfikatorem kontenera i jest również przypisywany losowo czytelną nazwę, `--name` Jeśli opcja nie jest używana.

#### <a name="using-visual-studio"></a>Korzystanie z programu Visual Studio

Jeśli nie dodano obsługi usługi Orchestrator kontenera, możesz również uruchomić aplikację z jednym kontenerem w programie Visual Studio, naciskając **klawisze CTRL-F5** i można także użyć klawisza **F5** do debugowania aplikacji w kontenerze. Kontener jest uruchamiany lokalnie przy użyciu uruchomienia platformy Docker.

### <a name="option-b-running-a-multi-container-application"></a>Opcja B: Uruchamianie aplikacji z obsługą kontenera

W większości scenariuszy przedsiębiorstwa aplikacja platformy Docker będzie składać się z wielu usług, co oznacza, że należy uruchomić aplikację obejmującą wiele kontenerów, jak pokazano na rysunku 5-10.

![Maszyna wirtualna z kilkoma kontenerami platformy Docker](./media/image14.png)

**Rysunek 5-10**. Maszyna wirtualna z wdrożonymi kontenerami platformy Docker

#### <a name="using-docker-cli"></a>Korzystanie z interfejsu wiersza polecenia platformy Docker

Aby uruchomić aplikację z obsługą kontenera przy użyciu interfejsu wiersza polecenia platformy Docker, `docker-compose up` należy wykonać polecenie. To polecenie używa pliku **Docker-Compose. yml** , który posiadasz na poziomie rozwiązania do wdrożenia aplikacji wielokontenerowej. Rysunek 5-11 przedstawia wyniki podczas uruchamiania polecenia z głównego katalogu rozwiązania, który zawiera plik Docker-Compose. yml.

![Widok ekranu podczas uruchamiania polecenia Docker-Zredaguj w górę](./media/image15.png)

**Rysunek 5-11**. Przykładowe wyniki podczas uruchamiania polecenia Docker-Zredaguj w górę

Po uruchomieniu polecenia "Docker-Zredaguj" aplikacja i powiązane z nim kontenery zostaną wdrożone na hoście platformy Docker, jak przedstawiono na rysunku 5-10.

#### <a name="using-visual-studio"></a>Korzystanie z programu Visual Studio

Uruchamianie aplikacji wielokontenerowej przy użyciu programu Visual Studio 2017 nie może być prostsze. Wystarczy nacisnąć **kombinację klawiszy CTRL-F5** , aby uruchomić lub **F5** w celu debugowania, jak zwykle, konfigurując projekt **Docker-Zredaguj** jako projekt startowy.  Program Visual Studio obsługuje wszystkie potrzebne ustawienia, dzięki czemu można tworzyć punkty przerwania w zwykły sposób i debugować, co kończy się niezależnymi procesami uruchomionymi na "serwerach zdalnych", podobnie jak w przypadku tego.

Jak wspomniano wcześniej, za każdym razem, gdy dodasz obsługę rozwiązania Docker do projektu w ramach rozwiązania, ten projekt jest konfigurowany w pliku globalnym (na poziomie rozwiązania) Docker-Compose. yml, który umożliwia jednoczesne uruchamianie lub debugowanie całego rozwiązania. Program Visual Studio uruchomi jeden kontener dla każdego projektu, który ma włączoną obsługę rozwiązania Docker, i wykona wszystkie czynności wewnętrzne (dotnet publish, kompilacja platformy Docker itp.).

Jeśli chcesz skorzystać ze wszystkich drudgery, zapoznaj się z plikiem:

`{root solution folder}\obj\Docker\docker-compose.vs.debug.g.yml`

Ważnym punktem jest to, jak pokazano na rysunku 5-12 w programie Visual Studio 2017 istnieje dodatkowe polecenie **platformy Docker** dla akcji klawisza F5. Ta opcja umożliwia uruchamianie lub debugowanie aplikacji wielokontenerowych przez uruchomienie wszystkich kontenerów, które są zdefiniowane w plikach Docker-Compose. yml na poziomie rozwiązania. Możliwość debugowania rozwiązań obejmujących wiele kontenerów oznacza, że można ustawić kilka punktów przerwania, każdy punkt przerwania w innym projekcie (kontener), a podczas debugowania z programu Visual Studio zatrzymano punkty przerwania zdefiniowane w różnych projektach i uruchomione na różne kontenery.

![Pasek narzędzi debugowania programu Visual Studio z uruchomionym programem Docker — redagowanie projektu](./media/image16.png)

**Rysunek 5-12**. Uruchamianie aplikacji z obsługą kontenera w programie Visual Studio 2017

### <a name="additional-resources"></a>Dodatkowe zasoby

- **Wdrażanie kontenera ASP.NET na zdalnym hoście platformy Docker** \
  <https://docs.microsoft.com/azure/vs-azure-tools-docker-hosting-web-apps-in-docker>

### <a name="a-note-about-testing-and-deploying-with-orchestrators"></a>Uwaga dotycząca testowania i wdrażania w programie Orchestrator

Polecenia platformy Docker — tworzenie i Docker (lub uruchamianie i debugowanie kontenerów w programie Visual Studio) są odpowiednie do testowania kontenerów w środowisku deweloperskim. Nie należy jednak używać tej metody w przypadku wdrożeń produkcyjnych, w których należy kierować się koordynatorami, takimi jak [Kubernetes](https://kubernetes.io/) lub [Service Fabric](https://azure.microsoft.com/services/service-fabric/). Jeśli używasz programu Kubernetes, musisz użyć [zasobników](https://kubernetes.io/docs/concepts/workloads/pods/pod/) , aby organizować kontenery i [usługi](https://kubernetes.io/docs/concepts/services-networking/service/) w sieci. [Wdrożenia](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) są również używane do organizowania pod względem tworzenia i modyfikowania.

![6 — Testowanie aplikacji lub mikrousług](./media/image17.png)

## <a name="step-6-test-your-docker-application-using-your-local-docker-host"></a>Krok 6. Testowanie aplikacji platformy Docker przy użyciu lokalnego hosta platformy Docker

Ten krok będzie się różnić w zależności od tego, co aplikacja działa. W prostej aplikacji sieci Web platformy .NET Core wdrożonej jako pojedynczy kontener lub usługa można uzyskać dostęp do usługi, otwierając przeglądarkę na hoście platformy Docker i przechodząc do tej lokacji, jak pokazano na rysunku 5-13. (Jeśli konfiguracja w pliku dockerfile mapuje kontener na port na hoście, który jest inny niż 80, Uwzględnij port hosta w adresie URL).

![Widok przeglądarki odpowiedzi punktu końcowego interfejsu API](./media/image18.png)

**Rysunek 5-13**. Przykład testowania aplikacji platformy Docker lokalnie przy użyciu hosta lokalnego

Jeśli localhost nie wskazuje adresu IP hosta platformy Docker (domyślnie w przypadku korzystania z platformy Docker CE powinien), aby przejść do usługi, użyj adresu IP karty sieciowej maszyny.

Należy zauważyć, że ten adres URL w przeglądarce używa portu 80 dla określonego przykładowego kontenera. Jednak wewnętrznie żądania są przekierowywane do portu 5000, ponieważ było ono wdrożone przy użyciu polecenia Docker Run, zgodnie z opisem w poprzednim kroku.

Możesz również testować aplikację przy użyciu zwinięcia z terminalu, jak pokazano na rysunku 5-14. W przypadku instalacji platformy Docker w systemie Windows domyślny adres IP hosta platformy Docker jest zawsze 10.0.75.1 oprócz rzeczywistego adresu IP maszyny.

![Widok ekranu odpowiedzi punktu końcowego interfejsu API z zwinięciem](./media/image19.png)

**Rysunek 5-14**. Przykład testowania aplikacji platformy Docker lokalnie przy użyciu narzędzia zwinięcie

### <a name="testing-and-debugging-containers-with-visual-studio-2017"></a>Testowanie i debugowanie kontenerów za pomocą programu Visual Studio 2017

Podczas uruchamiania i debugowania kontenerów za pomocą programu Visual Studio 2017 można debugować aplikację .NET w taki sam sposób, jak w przypadku uruchamiania bez kontenerów.

### <a name="testing-and-debugging-without-visual-studio"></a>Testowanie i debugowanie bez programu Visual Studio

Jeśli tworzysz program przy użyciu podejścia edytora/interfejsu wiersza polecenia, debugowanie kontenerów jest trudniejsze i chcesz debugować, generując dane śledzenia.

### <a name="additional-resources"></a>Dodatkowe zasoby

- **Debugowanie aplikacji w lokalnym kontenerze platformy Docker** \
  [https://docs.microsoft.com/visualstudio/containers/edit-and-refresh](/visualstudio/containers/edit-and-refresh)

- **Steve Lasker. Kompiluj, Debuguj i wdrażaj ASP.NET Core aplikacje przy użyciu platformy Docker.** Plików. \
  <https://channel9.msdn.com/Events/Visual-Studio/Visual-Studio-2017-Launch/T115>

## <a name="simplified-workflow-when-developing-containers-with-visual-studio"></a>Uproszczony przepływ pracy podczas tworzenia kontenerów za pomocą programu Visual Studio

Efektywnie, przepływ pracy w przypadku korzystania z programu Visual Studio jest znacznie prostszy niż w przypadku korzystania z metody edytora/interfejsu wiersza polecenia. Większość kroków wymaganych przez platformę Docker związanych z plikami pliku dockerfile i Docker-Compose. yml jest ukryta lub uproszczona przez program Visual Studio, jak pokazano na rysunku 5-15.

![Uproszczony przepływ pracy tworzenia kontenerów za pomocą programu Visual Studio: 1. Zakoduj aplikację, 2 — Dodaj obsługę platformy Docker do projektów (tylko raz), 3-uruchamiaj kontener lub aplikację Docker-Zredaguj, 4 — Przetestuj aplikację lub mikrousługi, 5 — wypychanie do repozytorium i powtarzanie.](./media/image20.png)

**Rysunek 5-15**. Uproszczony przepływ pracy podczas programowania przy użyciu programu Visual Studio

Ponadto należy wykonać krok 2 (dodanie obsługi platformy Docker do projektów) tylko raz. W związku z tym przepływ pracy jest podobny do zwykłych zadań programistycznych podczas korzystania z platformy .NET do innych celów programistycznych. Musisz wiedzieć, co się dzieje w obszarze okładki (proces kompilowania obrazu, jakie obrazy podstawowe są używane, wdrożenia kontenerów itp.), a czasami trzeba również edytować plik pliku dockerfile lub Docker-Compose. yml w celu dostosowania zachowań. Jednak większość pracy jest znacznie uproszczona przy użyciu programu Visual Studio, dzięki czemu znacznie zwiększa produktywność.

### <a name="additional-resources"></a>Dodatkowe zasoby

- **Steve Lasker. Programowanie platformy .NET Docker za pomocą programu Visual Studio 2017** \
  <https://channel9.msdn.com/Events/Visual-Studio/Visual-Studio-2017-Launch/T111>

## <a name="using-powershell-commands-in-a-dockerfile-to-set-up-windows-containers"></a>Konfigurowanie kontenerów systemu Windows za pomocą poleceń programu PowerShell w pliku dockerfile

[Kontenery systemu Windows](https://docs.microsoft.com/virtualization/windowscontainers/about/index) umożliwiają konwertowanie istniejących aplikacji systemu Windows do obrazów platformy Docker i wdrażanie ich przy użyciu tych samych narzędzi, co w pozostałej części ekosystemu platformy Docker. Aby korzystać z kontenerów systemu Windows, należy uruchomić polecenia programu PowerShell w pliku dockerfile, jak pokazano w następującym przykładzie:

```Dockerfile
FROM microsoft/windowsservercore
LABEL Description="IIS" Vendor="Microsoft" Version="10"
RUN powershell -Command Add-WindowsFeature Web-Server
CMD [ "ping", "localhost", "-t" ]
```

W takim przypadku używany jest podstawowy obraz systemu Windows Server Core (ustawienie od) i Instalowanie usług IIS za pomocą polecenia programu PowerShell (ustawienie URUCHOMIENIOWe). W podobny sposób można również użyć poleceń programu PowerShell, aby skonfigurować dodatkowe składniki, takie jak ASP.NET 4. x, .NET 4,6 lub dowolne inne oprogramowanie systemu Windows. Na przykład następujące polecenie w pliku dockerfile konfiguruje ASP.NET 4,5:

```Dockerfile
RUN powershell add-windowsfeature web-asp-net45
```

### <a name="additional-resources"></a>Dodatkowe zasoby

- **aspnet-docker/Dockerfile.** Przykładowe polecenia programu PowerShell do uruchomienia z wieloetapowe dockerfile w celu uwzględnienia funkcji systemu Windows. \
  <https://github.com/Microsoft/aspnet-docker/blob/master/4.7.1-windowsservercore-ltsc2016/runtime/Dockerfile>

>[!div class="step-by-step"]
>[Poprzedni](index.md)Następny
>[](../multi-container-microservice-net-applications/index.md)