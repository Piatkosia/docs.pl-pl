---
title: Wprowadzenie do zdarzeń
description: Zapoznaj się z informacjami o zdarzeniach w programie .NET Core i naszych celach projektowania języka dla zdarzeń w tym omówieniu.
ms.date: 06/20/2016
ms.assetid: 9b8d2a00-1584-4a5b-8994-5003d54d8e0c
ms.openlocfilehash: 4da44c151244e8b5de34f550040c271131d9598c
ms.sourcegitcommit: e7acba36517134238065e4d50bb4a1cfe47ebd06
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2020
ms.locfileid: "89465237"
---
# <a name="introduction-to-events"></a>Wprowadzenie do zdarzeń

[Poprzednie](delegates-patterns.md)

Zdarzenia są takie jak Delegaty, mechanizm *późnego wiązania* . W rzeczywistości zdarzenia są tworzone w oparciu o obsługę języka dla delegatów.

Zdarzenia są sposobem na wyemitowanie obiektu (do wszystkich zainteresowanych składników w systemie), które wystąpiły. Każdy inny składnik może subskrybować zdarzenie i otrzymywać powiadomienia o zdarzeniu.

Prawdopodobnie wykorzystano zdarzenia w niektórych programowaniu. Wiele systemów graficznych ma model zdarzeń służący do zgłaszania interakcji z użytkownikiem. Te zdarzenia spowodują przemieszczenie myszy, naciśnięcie przycisków i podobne interakcje. Jest to jeden z najczęstszych, ale nie jedyny scenariusz, w którym są używane zdarzenia.

Można zdefiniować zdarzenia, które powinny być zgłaszane dla klas. Ważnym zagadnieniem podczas pracy ze zdarzeniami jest fakt, że nie istnieje żaden obiekt zarejestrowany dla danego zdarzenia. Należy napisać kod, aby nie zgłaszał zdarzeń, gdy nie skonfigurowano żadnych odbiorników.

Subskrybowanie zdarzenia również tworzy sprzężenie między dwoma obiektami (źródłem zdarzenia i ujścia zdarzeń). Musisz się upewnić, że obiekt ujścia zdarzeń anuluje subskrypcję źródła zdarzeń, gdy nie będą już zainteresowani zdarzeniami.

## <a name="design-goals-for-event-support"></a>Cele projektu dotyczące obsługi zdarzeń

Projektowanie języka dla zdarzeń przeznaczonych dla następujących celów:

- Włącz bardzo minimalne sprzęganie między źródłem zdarzenia a obiektem sink zdarzenia. Te dwa składniki mogą nie być zapisywane w tej samej organizacji i mogą nawet być aktualizowane w odniesieniu do całkowicie różnych harmonogramów.

- Subskrybowanie zdarzeń powinno być bardzo proste i anulowanie subskrypcji tego samego zdarzenia.

- Źródła zdarzeń powinny obsługiwać wielu subskrybentów zdarzeń. Dział IT powinien również obsługiwać niedołączone Subskrybenci zdarzeń.

Można zobaczyć, że cele dla zdarzeń są bardzo podobne do celów delegatów.
Dlatego obsługa języka zdarzeń jest oparta na obsłudze języka delegatów.

## <a name="language-support-for-events"></a>Obsługa języka dla zdarzeń

Składnia do definiowania zdarzeń oraz subskrybowanie lub anulowanie subskrypcji zdarzeń jest rozszerzeniem składni dla delegatów.

Aby zdefiniować zdarzenie, użyj `event` słowa kluczowego:

```csharp
public event EventHandler<FileListArgs> Progress;
```

Typ zdarzenia ( `EventHandler<FileListArgs>` w tym przykładzie) musi być typem delegata. Podczas deklarowania zdarzenia należy przestrzegać kilku Konwencji. Zwykle typ delegata zdarzenia ma zwracaną wartość void.
Deklaracje zdarzeń powinny być czasownikiem lub wyrażeniem orzeczenia.
Użyj minionych natężeń, gdy zdarzenie zgłosi coś, co się stało. Użyj obecnego zlecenia dwuprzyciskowego (na przykład `Closing` ), aby zgłosić coś, co się dzieje. Często użycie obecnego dwustopniowego oznacza, że Klasa obsługuje pewne zachowanie w zakresie dostosowywania. Jednym z najczęstszych scenariuszy jest obsługa anulowania. Na przykład `Closing` zdarzenie może zawierać argument, który wskazuje, czy operacja zamknięcia powinna być kontynuowana, czy nie.  Inne scenariusze mogą umożliwić wywoływanie obiektów wywołujących w celu zmodyfikowania zachowania przez zaktualizowanie Właściwości argumentów zdarzeń. Możesz zgłosić zdarzenie, aby wskazać proponowaną następną akcję do wykonania przez algorytm. Program obsługi zdarzeń może wykonać inną akcję przez modyfikację właściwości argumentu zdarzenia.

Aby zgłosić zdarzenie, należy wywołać programy obsługi zdarzeń przy użyciu składni delegata wywołania:

```csharp
Progress?.Invoke(this, new FileListArgs(file));
```

Zgodnie z opisem w sekcji [delegatów](delegates-patterns.md),?.
ułatwia to zapewnienie, że nie próbujesz podnieść zdarzenia, gdy nie ma subskrybentów tego zdarzenia.

Subskrybujesz zdarzenie przy użyciu `+=` operatora:

```csharp
EventHandler<FileListArgs> onProgress = (sender, eventArgs) =>
    Console.WriteLine(eventArgs.FoundFile);

fileLister.Progress += onProgress;
```

Metoda obsługi zazwyczaj ma prefiks "on", po którym następuje nazwa zdarzenia, jak pokazano powyżej.

Anulowanie subskrypcji przy użyciu `-=` operatora:

```csharp
fileLister.Progress -= onProgress;
```

Ważne jest, aby zadeklarować zmienną lokalną dla wyrażenia, które reprezentuje procedurę obsługi zdarzeń. Dzięki temu anulowanie subskrypcji spowoduje usunięcie programu obsługi.
Jeśli zamiast tego użyto treści wyrażenia lambda, podjęto próbę usunięcia programu obsługi, który nigdy nie został dołączony, co nic nie robi.

W następnym artykule dowiesz się więcej na temat typowych wzorców zdarzeń i różnej zmienności w tym przykładzie.

[Dalej](event-pattern.md)
