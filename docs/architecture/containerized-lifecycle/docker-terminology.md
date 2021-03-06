---
title: Terminologia platformy Docker
description: Poznaj podstawową terminologię używaną codziennie podczas pracy z platformą Docker.
ms.date: 08/06/2020
ms.openlocfilehash: b47639a2995c3a0a30ea7111c16bbea21f1048ba
ms.sourcegitcommit: ef50c99928183a0bba75e07b9f22895cd4c480f8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/07/2020
ms.locfileid: "87915198"
---
# <a name="docker-terminology"></a>Terminologia platformy Docker

W tej sekcji przedstawiono terminy i definicje, z którymi należy zapoznać się przed zagłębieniem się w platformę Docker. Aby uzyskać więcej definicji, zobacz obszerny [słownik](https://docs.docker.com/glossary/) udostępniany przez platformę Docker.

**Obraz kontenera**: pakiet ze wszystkimi zależnościami i informacjami wymaganymi do utworzenia kontenera. Obraz zawiera wszystkie zależności (takie jak struktury) oraz konfigurację wdrażania i wykonywania, które mają być używane przez środowisko uruchomieniowe kontenera. Zazwyczaj obraz pochodzi z wielu obrazów podstawowych, które są warstwowo ułożone na siebie, aby utworzyć system plików kontenera. Obraz jest niezmienny, gdy zostanie utworzony.

**Pliku dockerfile**: plik tekstowy zawierający instrukcje dotyczące tworzenia obrazu platformy Docker. Podobnie jak skrypt wsadowy, pierwszy wiersz określa podstawowy obraz, a następnie postępuje zgodnie z instrukcjami, aby zainstalować wymagane programy, skopiować pliki i tak dalej, aż do momentu uzyskania potrzebnego środowiska roboczego.

**Kompilacja**: Akcja tworzenia obrazu kontenera na podstawie informacji i kontekstu dostarczonych przez jego pliku dockerfile oraz dodatkowych plików w folderze, w którym utworzono obraz. Możesz tworzyć obrazy za pomocą następującego polecenia platformy Docker:

```bash
docker build
```

**Container**: wystąpienie obrazu platformy Docker. Kontener reprezentuje wykonywanie pojedynczej aplikacji, procesu lub usługi. Składa się z zawartości obrazu platformy Docker, środowiska wykonawczego i standardowego zestawu instrukcji. W przypadku skalowania usługi należy utworzyć wiele wystąpień kontenera z tego samego obrazu. Lub zadanie usługi Batch może utworzyć wiele kontenerów z tego samego obrazu, przekazując różne parametry do każdego wystąpienia.

**Woluminy**: udostępniają zapisywalny system plików, który może być używany przez kontener. Ponieważ obrazy są dostępne tylko do odczytu, ale większość programów musi zapisywać w systemie plików, woluminy dodają warstwę zapisywalną na podstawie obrazu kontenera, dzięki czemu programy mają dostęp do systemu plików zapisywalnych. Program nie wie, że uzyskuje dostęp do warstwowego systemu plików, jest to tylko system plików w zwykły sposób. Woluminy na żywo w systemie hosta i zarządzane przez platformę Docker.

**Tag**: znacznik lub etykieta, które można zastosować do obrazów w taki sposób, aby można było zidentyfikować różne obrazy lub wersje tego samego obrazu (w zależności od numeru wersji lub środowiska docelowego).

**Kompilacja wieloetapowa**: jest funkcją, ponieważ platforma docker 17,05 lub nowsza, która pomaga zmniejszyć rozmiar obrazów końcowych. Na przykład do kompilowania i publikowania można użyć dużego obrazu podstawowego zawierającego zestaw SDK, a następnie można użyć małego obrazu podstawowego tylko dla środowiska uruchomieniowego, który będzie obsługiwał aplikację.

**Repozytorium (repozytorium)**: Kolekcja powiązanych obrazów platformy Docker oznaczona tagami z tagiem wskazującym wersję obrazu. Niektóre repozytoria zawierają wiele wariantów określonego obrazu, takich jak obraz zawierający zestawy SDK (grubszy), obraz zawierający tylko środowiska uruchomieniowe (jaśniejszy) itp. Te warianty mogą być oznaczone tagami. Pojedyncze repozytorium może zawierać warianty platformy, takie jak obraz systemu Linux i obraz Windows.

**Rejestr**: usługa, która zapewnia dostęp do repozytoriów. Domyślnym rejestrem większości obrazów publicznych jest [centrum platformy Docker](https://hub.docker.com/) (należące do platformy Docker jako organizacja). Rejestr zawiera zwykle repozytoria z wielu zespołów. Firmy często mają prywatne rejestry do przechowywania utworzonych przez siebie obrazów i zarządzania nimi. Azure Container Registry jest kolejnym przykładem.

**Obraz**z obsługą wielu rozwiązań: w przypadku wielu architektur jest to funkcja, która upraszcza wybór odpowiedniego obrazu, zgodnie z platformą, na której działa platforma Docker. Na przykład gdy pliku dockerfile żąda obrazu podstawowego **z MCR.Microsoft.com/dotnet/Core/SDK:3.1** z rejestru, faktycznie otrzymuje **3,1-SDK-nanoserver-1909**, **3,1-SDK-nanoserver-1809** lub **3,1-SDK-Buster-Slim**, w zależności od systemu operacyjnego i wersji, w której działa program Docker.

**Centrum platformy Docker**: Rejestr publiczny służący do przekazywania obrazów i pracy z nimi. Centrum platformy Docker zapewnia hosting obrazów platformy Docker, rejestry publiczne lub prywatne, wyzwalacze kompilacji i elementy webhook oraz integrację z usługą GitHub i Bitbucket.

**Azure Container Registry**: zasób publiczny służący do pracy z obrazami platformy Docker i jej składnikami na platformie Azure. Dzięki temu rejestr znajduje się blisko wdrożeń na platformie Azure i zapewnia kontrolę nad dostępem, dzięki czemu można korzystać z Azure Active Directory grup i uprawnień.

**Zaufany rejestr platformy Docker (DTR)**: usługa rejestru platformy Docker (z platformy Docker), którą można zainstalować lokalnie, tak aby była w centrum danych i sieci organizacji. Jest to wygodne w przypadku obrazów prywatnych, które powinny być zarządzane w przedsiębiorstwie. Zaufany rejestr platformy Docker jest dołączony jako część produktu centrum danych platformy Docker. Aby uzyskać więcej informacji, zobacz artykuł [Docker Trusted Registry (DTR)](https://www.docker.com/sites/default/files/Docker%20Trusted%20Registry.pdf).

**Docker Community Edition (CE)**: narzędzia deweloperskie dla systemu Windows i macOS do tworzenia, uruchamiania i testowania kontenerów lokalnie. Docker CE for Windows zapewnia środowiska deweloperskie dla kontenerów systemu Linux i Windows. Host platformy Docker systemu Linux w systemie Windows jest oparty na maszynie wirtualnej [funkcji Hyper-V](https://www.microsoft.com/cloud-platform/server-virtualization) . Host dla kontenerów systemu Windows jest bezpośrednio oparty na systemie Windows. Program Docker CE dla komputerów Mac jest oparty na strukturze funkcji hypervisor firmy Apple i [funkcji hypervisor xhyve](https://github.com/mist64/xhyve), która udostępnia maszynę wirtualną hosta platformy Docker systemu Linux na Mac OS X. Docker CE for Windows i dla komputerów Mac zastępuje Przybornik platformy Docker, który został oparty na bazie danych Oracle VirtualBox.

**Docker Enterprise Edition (EE)**: skalowanie w poziomie korporacyjnym narzędzi platformy Docker dla systemów Linux i Windows.

**Redaguj**: Narzędzie wiersza polecenia i format pliku YAML z metadanymi do definiowania i uruchamiania aplikacji wielokontenerowych. Należy zdefiniować pojedynczą aplikację na podstawie wielu obrazów z co najmniej jednym plikami. yml, która może zastąpić wartości w zależności od środowiska. Po utworzeniu definicji można wdrożyć całą aplikację obejmującą wiele kontenerów za pomocą jednego polecenia (Docker-Zredaguj), które tworzy kontener na obraz na hoście platformy Docker.

**Klaster**: Kolekcja hostów platformy Docker uwidoczniona tak, jakby była jednym wirtualnym hostem platformy Docker, dzięki czemu aplikacja może być skalowana do wielu wystąpień usług rozmieszczonych na wielu hostach w klastrze. Klastry platformy Docker można tworzyć za pomocą Kubernetes, Azure Service Fabric, Docker Swarm i mesosphere DC/OS.

**Orchestrator**: Narzędzie upraszczające Zarządzanie klastrami i hostami platformy Docker. Koordynatorzy umożliwiają zarządzanie obrazami, kontenerami i hostami za pomocą interfejsu wiersza polecenia (CLI) lub graficznego interfejsu użytkownika. Można zarządzać sieciami kontenera, konfiguracjami, równoważeniem obciążenia, odnajdywaniem usług, wysoką dostępnością, konfiguracją hosta platformy Docker i innymi. Koordynator jest odpowiedzialny za uruchamianie, dystrybuowanie, skalowanie i korygowanie obciążeń w kolekcji węzłów. Zazwyczaj produkty Orchestrator są tymi samymi produktami, które zapewniają infrastrukturę klastra, taką jak Kubernetes i Azure Service Fabric, między innymi ofertami na rynku.

>[!div class="step-by-step"]
>[Poprzedni](what-is-docker.md) 
> [Dalej](docker-containers-images-and-registries.md)
