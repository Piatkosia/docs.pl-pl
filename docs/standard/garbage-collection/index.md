---
title: Zbieranie elementów bezużytecznych platformy .NET
description: Informacje o odzyskiwaniu elementów bezużytecznych w programie .NET. Moduł zbierający elementy bezużyteczne platformy .NET zarządza alokacją i ilością pamięci dla aplikacji.
ms.date: 04/21/2020
ms.technology: dotnet-standard
helpviewer_keywords:
- memory, garbage collection
- garbage collection, automatic memory management
- GC [.NET]
- memory, allocating
- common language runtime, garbage collection
- garbage collector
- cleanup operations
- garbage collection
- memory, releasing
- common language runtime, automatic memory management
- automatic memory management
- runtime, automatic memory management
- runtime, garbage collection
- garbage collection, about
ms.assetid: 22b6cb97-0c80-4eeb-a2cf-5ed7655e37f9
ms.openlocfilehash: 39b5bf62935054bd4b9be2d228cc42202aa89144
ms.sourcegitcommit: b1442669f1982d3a1cb18ea35b5acfb0fc7d93e4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2020
ms.locfileid: "93063192"
---
# <a name="garbage-collection"></a>Wyrzucanie elementów bezużytecznych

. Moduł wyrzucania elementów bezużytecznych sieci zarządza alokacją i ilością pamięci dla aplikacji. Zawsze podczas tworzenia nowego obiektu środowisko uruchomieniowe języka wspólnego przydziela pamięć dla obiektu z zarządzanego stosu. Tak długo, jak przestrzeń adresowa jest dostępna w zarządzanym stosie, środowisko wykonawcze w dalszym ciągu przydziela miejsce dla nowych obiektów. Jednak pamięć nie jest nieskończona. Ostatecznie moduł zbierający elementy bezużyteczne musi wykonać kolekcję w celu zwolnienia pamięci. Aparat optymalizacji w module odśmiecania pamięci ustala najlepszy moment na wykonanie procesu wyrzucania w oparciu o dokonywane przydziały. Gdy moduł zbierający elementy bezużyteczne wykonuje kolekcję, sprawdza czy istnieją obiekty na zarządzanym stosie, które nie są już używane przez aplikację, i wykonuje niezbędne operacje do odzyskania ich pamięci.  
  
## <a name="in-this-section"></a>W tej sekcji
  
|Tytuł|Opis|  
|-----------|-----------------|  
|[Podstawowe informacje dotyczące wyrzucania elementów bezużytecznych](fundamentals.md)|Opisuje jak działa wyrzucanie elementów bezużytecznych, jak obiekty są przydzielane na zarządzanym stosie oraz inne podstawowe pojęcia.|  
|[Stacja robocza i odzyskiwanie pamięci serwera](workstation-server-gc.md)|Opisuje różnice między odzyskiwaniem pamięci stacji roboczej dla aplikacji klienckich i odzyskiwania pamięci serwera dla aplikacji serwera.|
|[Odzyskiwanie pamięci w tle](background-gc.md)|Opisuje wyrzucanie elementów bezużytecznych w tle, czyli zbieranie obiektów generacji 0 i 1, gdy kolekcja generacji 2 jest w toku.|
|[Sterta obiektów wielkich](large-object-heap.md)|Opisuje stertę dużego obiektu (LOH) i sposób, w jaki duże obiekty są zbierane jako elementy bezużyteczne.|
|[Odzyskiwanie pamięci i wydajność](performance.md)|Opisuje testy wydajności, które można użyć do diagnozowania problemów z wydajnością wyrzucania elementów bezużytecznych.|  
|[Wywołane kolekcje](induced.md)|Opisuje, jak sprawić, aby nastąpiło wyrzucanie elementów bezużytecznych.|  
|[Tryby opóźnienia](latency.md)|Opisuje tryby, które określają ingerencję operacji wyrzucania elementów bezużytecznych.|  
|[Optymalizacja udostępnionej usługi hostingu internetowego](optimization-for-shared-web-hosting.md)|Opisuje, jak zoptymalizować wyrzucanie elementów bezużytecznych na serwerach współużytkowanych przez kilka małych witryn sieci Web.|  
|[Powiadomienia dotyczące odzyskiwania pamięci](notifications.md)|Opisuje, jak określić kiedy zbliża się pełne wyrzucanie elementów bezużytecznych i kiedy zostało ono ukończone.|  
|[Monitorowanie zasobów domen aplikacji](app-domain-resource-monitoring.md)|Opisuje, jak monitorować wykorzystanie procesora i pamięci przez domenę aplikacji.|  
|[Słabe odwołania](weak-references.md)|Opisuje funkcje, które pozwalają modułowi zbierającemu elementy bezużyteczne na zbieranie obiektu, wciąż zezwalając aplikacjom na dostęp do tego obiektu.|  
  
## <a name="reference"></a>Odwołanie

- <xref:System.GC?displayProperty=nameWithType>  
- <xref:System.GCCollectionMode?displayProperty=nameWithType>  
- <xref:System.GCNotificationStatus?displayProperty=nameWithType>  
- <xref:System.Runtime.GCLatencyMode?displayProperty=nameWithType>  
- <xref:System.Runtime.GCSettings?displayProperty=nameWithType>  
- <xref:System.Runtime.GCSettings.LargeObjectHeapCompactionMode%2A?displayProperty=nameWithType>  
- <xref:System.Object.Finalize%2A?displayProperty=nameWithType>  
- <xref:System.IDisposable?displayProperty=nameWithType>  
  
## <a name="see-also"></a>Zobacz też

- [Oczyszczanie zasobów niezarządzanych](unmanaged.md)
