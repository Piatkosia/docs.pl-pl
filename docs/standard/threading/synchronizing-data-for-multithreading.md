---
title: Synchronizowanie danych na potrzeby wielowątkowości
description: Dowiedz się, jak synchronizować dane dla wielowątkowości w programie .NET. Wybierz strategie, takie jak regiony kodu zsynchronizowanego, synchronizacja ręczna lub synchronizowane konteksty.
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- synchronization, threads
- threading [.NET], synchronizing threads
- managed threading
ms.assetid: b980eb4c-71d5-4860-864a-6dfe3692430a
ms.openlocfilehash: 63ee85f3d8bab865ce34566ec381d23676b27991
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/02/2020
ms.locfileid: "93188591"
---
# <a name="synchronizing-data-for-multithreading"></a>Synchronizowanie danych na potrzeby wielowątkowości

Gdy wiele wątków może wykonywać wywołania do właściwości i metod pojedynczego obiektu, ma krytyczne znaczenie, aby te wywołania były synchronizowane. W przeciwnym razie jeden wątek może przerwać działanie innego wątku, a obiekt może pozostać w nieprawidłowym stanie. Klasa, której członkowie są chronieni przed takimi zakłóceniami, jest nazywana wątkowo bezpiecznym.  
  
Platforma .NET udostępnia kilka strategii do synchronizowania dostępu do wystąpienia i statycznych elementów członkowskich:  
  
- Zsynchronizowane regiony kodu. Możesz użyć <xref:System.Threading.Monitor> obsługi klasy lub kompilatora dla tej klasy, aby synchronizować tylko blok kodu, który go potrzebuje, zwiększając wydajność.  
  
- Ręczna synchronizacja. Możesz użyć obiektów synchronizacji dostarczonych przez bibliotekę klas .NET. Zobacz [Omówienie elementów pierwotnych synchronizacji](overview-of-synchronization-primitives.md), które obejmują dyskusję <xref:System.Threading.Monitor> klasy.  
  
- Synchronizowane konteksty. Tylko dla aplikacji .NET Framework i Xamarin, można użyć, <xref:System.Runtime.Remoting.Contexts.SynchronizationAttribute> Aby włączyć prostą, automatyczną synchronizację <xref:System.ContextBoundObject> obiektów.  
  
- Klasy kolekcji w <xref:System.Collections.Concurrent?displayProperty=nameWithType> przestrzeni nazw. Te klasy zapewniają wbudowaną synchronizację operacji dodawania i usuwania. Aby uzyskać więcej informacji, zobacz [kolekcje bezpieczne dla wątków](../collections/thread-safe/index.md).  
  
 Środowisko uruchomieniowe języka wspólnego udostępnia model wątku, w którym klasy mieszczą się w różnych kategoriach, które można synchronizować na różne sposoby, w zależności od wymagań. W poniższej tabeli przedstawiono obsługę synchronizacji dla pól i metod z daną kategorią synchronizacji.  
  
|Kategoria|Pola globalne|Pola statyczne|Metody statyczne|Pola wystąpienia|Metody Instance|Określone bloki kodu|  
|--------------|-------------------|-------------------|--------------------|---------------------|----------------------|--------------------------|  
|Brak synchronizacji|Nie|Nie|Nie|Nie|Nie|Nie|  
|Zsynchronizowany kontekst|Nie|Nie|Nie|Tak|Tak|Nie|  
|Zsynchronizowane regiony kodu|Nie|Nie|Tylko wtedy, gdy oznaczono|Nie|Tylko wtedy, gdy oznaczono|Tylko wtedy, gdy oznaczono|  
|Synchronizacja ręczna|Ręcznie|Ręcznie|Ręcznie|Ręcznie|Ręcznie|Ręcznie|  
  
## <a name="no-synchronization"></a>Brak synchronizacji  
 Jest to wartość domyślna dla obiektów. Dowolny wątek może uzyskać dostęp do dowolnej metody lub pola w dowolnym momencie. Tylko jeden wątek jednocześnie powinien uzyskać dostęp do tych obiektów.  
  
## <a name="manual-synchronization"></a>Synchronizacja ręczna  
 Biblioteka klas .NET udostępnia wiele klas do synchronizowania wątków. Zobacz [Omówienie elementów pierwotnych synchronizacji](overview-of-synchronization-primitives.md).  
  
## <a name="synchronized-code-regions"></a>Zsynchronizowane regiony kodu  
 Można użyć <xref:System.Threading.Monitor> klasy lub słowa kluczowego kompilatora do synchronizowania bloków kodu, metod wystąpień i metod statycznych. Nie ma obsługi zsynchronizowanych pól statycznych.  
  
 Zarówno Visual Basic, jak i C# obsługują oznaczenie bloków kodu za pomocą słowa kluczowego określonego języka, `lock` instrukcji w języku C# lub `SyncLock` instrukcji w Visual Basic. Gdy kod jest wykonywany przez wątek, podejmowana jest próba uzyskania blokady. Jeśli blokada została już uzyskana przez inny wątek, bloki wątku do momentu udostępnienia blokady staną się dostępne. Gdy wątek opuszcza zsynchronizowany blok kodu, blokada zostaje wydana, niezależnie od tego, jak wątek opuszcza blok.  
  
> [!NOTE]
> `lock`Instrukcje i `SyncLock` są implementowane za pomocą <xref:System.Threading.Monitor.Enter%2A?displayProperty=nameWithType> i <xref:System.Threading.Monitor.Exit%2A?displayProperty=nameWithType> , dlatego inne metody <xref:System.Threading.Monitor> można używać w połączeniu z nimi w zsynchronizowanym regionie.  
  
 Możesz również dekorować metodę z <xref:System.Runtime.CompilerServices.MethodImplAttribute> wartością <xref:System.Runtime.CompilerServices.MethodImplOptions.Synchronized?displayProperty=nameWithType> , która ma taki sam skutek jak użycie <xref:System.Threading.Monitor> lub jeden z słów kluczowych kompilatora, aby zablokować całą treść metody.  
  
 <xref:System.Threading.Thread.Interrupt%2A?displayProperty=nameWithType> może służyć do przerwania wątku poza operacje blokowania, takie jak oczekiwanie na dostęp do synchronizowanego regionu kodu. **Wątek. Interrupt** jest również używany do przerwania wątków, takich jak <xref:System.Threading.Thread.Sleep%2A?displayProperty=nameWithType> .  
  
> [!IMPORTANT]
> Nie blokuj typu — to znaczy, `typeof(MyType)` w języku C#, `GetType(MyType)` w Visual Basic lub `MyType::typeid` w języku C++ — w celu ochrony `static` metod ( `Shared` metod w Visual Basic). Zamiast tego użyj prywatnego obiektu statycznego. Podobnie nie należy używać `this` języka C# ( `Me` w Visual Basic) do blokowania metod wystąpienia. Zamiast tego użyj obiektu prywatnego. Klasę lub wystąpienie można zablokować za pomocą kodu innego niż własny, potencjalnie powodującego zakleszczenie lub problemy z wydajnością.  
  
### <a name="compiler-support"></a>Obsługa kompilatora  
 Zarówno Visual Basic, jak i C# obsługują słowo kluczowe języka, które używa <xref:System.Threading.Monitor.Enter%2A?displayProperty=nameWithType> i <xref:System.Threading.Monitor.Exit%2A?displayProperty=nameWithType> do blokowania obiektu. Visual Basic obsługuje instrukcję [SyncLock](../../visual-basic/language-reference/statements/synclock-statement.md) ; Język C# obsługuje instrukcję [Lock](../../csharp/language-reference/keywords/lock-statement.md) .  
  
 W obu przypadkach, jeśli wyjątek jest zgłaszany w bloku kodu, blokada uzyskana przez **blokadę** lub **SyncLock** jest automatycznie wydawana. Kompilatory C# i Visual Basic emitują blok **try** / **finally** z **monitorem. Wprowadź** na początku try, a **monitor. Exit** w bloku **finally** . Jeśli w bloku **blokady** lub **SyncLock** zostanie zgłoszony wyjątek, program obsługi **finally** zostanie uruchomiony w celu umożliwienia wykonania wszelkich operacji oczyszczania.  
  
## <a name="synchronized-context"></a>Zsynchronizowany kontekst  

Tylko w aplikacjach .NET Framework i Xamarin, można użyć <xref:System.Runtime.Remoting.Contexts.SynchronizationAttribute> na dowolnym, <xref:System.ContextBoundObject> Aby zsynchronizować wszystkie metody wystąpień i pola. Wszystkie obiekty w tej samej domenie kontekstu mają tę samą blokadę. Wiele wątków może uzyskać dostęp do metod i pól, ale tylko jeden wątek jest dozwolony w dowolnym momencie.  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.Runtime.Remoting.Contexts.SynchronizationAttribute>
- [Wątki i wątkowość](threads-and-threading.md)
- [Przegląd elementów podstawowych synchronizacji](overview-of-synchronization-primitives.md)
- [SyncLock — Instrukcja](../../visual-basic/language-reference/statements/synclock-statement.md)
- [lock, instrukcja](../../csharp/language-reference/keywords/lock-statement.md)
