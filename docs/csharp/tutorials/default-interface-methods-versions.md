---
title: 'Bezpieczne aktualizowanie interfejsów przy użyciu domyślnych metod interfejsu w języku C #'
description: W tym zaawansowanym samouczku przedstawiono sposób bezpiecznego dodawania nowych funkcji do istniejących definicji interfejsów bez przerywania wszystkich klas i struktur, które implementują ten interfejs.
ms.date: 05/06/2019
ms.technlogy: csharp-advanced-concepts
ms.custom: mvc
ms.openlocfilehash: 1e73f9001414631975248f1a1658833d2785169b
ms.sourcegitcommit: 1eae045421d9ea2bfc82aaccfa5b1ff1b8c9e0e4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/16/2020
ms.locfileid: "84803211"
---
# <a name="tutorial-update-interfaces-with-default-interface-methods-in-c-80"></a>Samouczek: aktualizowanie interfejsów przy użyciu domyślnych metod interfejsu w języku C# 8,0

Począwszy od języka C# 8,0 na platformie .NET Core 3,0, można zdefiniować implementację podczas deklarowania elementu członkowskiego interfejsu. Najbardziej typowym scenariuszem jest bezpieczne dodanie elementów członkowskich do interfejsu już wydanego i używanego przez klientów niezliczone.

Z tego samouczka dowiesz się, jak wykonywać następujące czynności:

> [!div class="checklist"]
>
> * Bezpiecznie rozszerzając interfejsy przez dodanie metod z implementacjami.
> * Utwórz sparametryzowane implementacje, aby zapewnić większą elastyczność.
> * Włącz realizatorów, aby zapewnić bardziej konkretną implementację w postaci przesłonięcia.

## <a name="prerequisites"></a>Wymagania wstępne

Musisz skonfigurować maszynę do uruchamiania programu .NET Core, w tym kompilatora C# 8,0. Kompilator języka C# 8,0 jest dostępny, począwszy od [programu Visual Studio 2019 w wersji 16,3](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) lub [zestawu .NET Core 3,0 SDK](https://dotnet.microsoft.com/download).

## <a name="scenario-overview"></a>Omówienie scenariusza

Ten samouczek rozpoczyna się od wersji 1 biblioteki relacji klienta. Możesz uzyskać aplikację Starter w naszym [repozytorium przykładów w witrynie GitHub](https://github.com/dotnet/samples/tree/master/csharp/tutorials/default-interface-members-versions/starter/customer-relationship). Firma, która utworzyła tę bibliotekę, zaplanowali klientom istniejące aplikacje do przyjęcia ich biblioteki. Zapewniają one minimalne definicje interfejsów dla użytkowników ich bibliotek do wdrożenia. Oto definicja interfejsu klienta:

[!code-csharp[InitialCustomerInterface](~/samples/snippets/csharp/tutorials/default-interface-members-versions/starter/customer-relationship/ICustomer.cs?name=SnippetICustomerVersion1)]

Zdefiniowano drugi interfejs, który reprezentuje zamówienie:

[!code-csharp[InitialOrderInterface](~/samples/snippets/csharp/tutorials/default-interface-members-versions/starter/customer-relationship/IOrder.cs?name=SnippetIorderVersion1)]

Z tych interfejsów zespół może stworzyć bibliotekę dla swoich użytkowników, aby mogli tworzyć lepsze środowisko dla swoich klientów. Ich celem było stworzenie szczegółowej relacji z istniejącymi klientami i poprawa ich relacji z nowymi klientami.

Teraz czas na uaktualnienie biblioteki do kolejnej wersji. Jedną z żądanych funkcji jest włączenie rabatu lojalnościowego dla klientów, którzy mają wiele zamówień. Ten nowy rabat dla lojalności zostanie zastosowany za każdym razem, gdy klient przyniesie zamówienie. Określony rabat jest właściwością każdego indywidualnego klienta. Każda implementacja programu `ICustomer` może ustawiać różne reguły rabatu lojalnościowego.

Najbardziej naturalnym sposobem dodawania tej funkcji jest udoskonalenie `ICustomer` interfejsu za pomocą metody w celu zastosowania dowolnego rabatu lojalnościowego. Ta sugestia projektowa została spowodowana przez doświadczonych deweloperów: "interfejsy są niemodyfikowalne po ich udostępnieniu! To jest istotna zmiana! " W języku C# 8,0 dodano *domyślne implementacje interfejsu* do uaktualniania interfejsów. Autorzy biblioteki mogą dodawać nowych członków do interfejsu i udostępniać domyślną implementację dla tych elementów członkowskich.

Domyślne implementacje interfejsu umożliwiają deweloperom uaktualnienie interfejsu, jednocześnie umożliwiając wszystkim wykonawcom przesłonięcie tej implementacji. Użytkownicy biblioteki mogą zaakceptować implementację domyślną jako nieistotną zmianę. Jeśli ich reguły biznesowe są inne, mogą przesłonić.

## <a name="upgrade-with-default-interface-methods"></a>Uaktualnianie przy użyciu domyślnych metod interfejsu

Zespół wyraził zgodę na najprawdopodobniej domyślną implementację: Rabat dla klientów.

Uaktualnienie powinno zapewnić funkcjonalność, aby ustawić dwie właściwości: liczbę zamówień wymaganych do uzyskania rabatu oraz procent rabatu. Dzięki temu jest idealnym scenariuszem dla domyślnych metod interfejsu. Możesz dodać metodę do `ICustomer` interfejsu i podać najbardziej prawdopodobną implementację. Wszystkie istniejące i nowe implementacje mogą korzystać z implementacji domyślnej lub udostępniać własne.

Najpierw Dodaj nową metodę do interfejsu, w tym treść metody:

[!code-csharp[InitialOrderInterface](~/samples/snippets/csharp/tutorials/default-interface-members-versions/finished/customer-relationship/ICustomer.cs?name=SnippetLoyaltyDiscountVersionOne)]

Autor biblioteki zapisał pierwszy test w celu sprawdzenia implementacji:

[!code-csharp[TestDefaultImplementation](~/samples/snippets/csharp/tutorials/default-interface-members-versions/finished/customer-relationship/Program.cs?name=SnippetTestDefaultImplementation)]

Zwróć uwagę na następujące części testu:

[!code-csharp[TestDefaultImplementation](~/samples/snippets/csharp/tutorials/default-interface-members-versions/finished/customer-relationship/Program.cs?name=SnippetHighlightCast)]

Rzutowanie z `SampleCustomer` do na `ICustomer` jest niezbędne. `SampleCustomer`Klasa nie musi podawać implementacji dla elementu `ComputeLoyaltyDiscount` , który jest dostarczany przez `ICustomer` interfejs. Jednak `SampleCustomer` Klasa nie dziedziczy członków z jego interfejsów. Ta reguła nie została zmieniona. Aby wywołać jakąkolwiek metodę zadeklarowaną i zaimplementowaną w interfejsie, zmienna musi być typem interfejsu, `ICustomer` w tym przykładzie.

## <a name="provide-parameterization"></a>Podaj parametryzacja

To dobry początek. Jednak domyślna implementacja jest zbyt restrykcyjna. Wielu użytkowników tego systemu może wybrać różne progi dla liczby zakupów, innej długości członkostwa lub innego rabatu procentowego. Aby zapewnić większym klientom możliwość uaktualnienia, możesz określić te parametry. Dodajmy metodę statyczną, która ustawia te trzy parametry kontrolujące implementację domyślną:

[!code-csharp[VersionTwoImplementation](~/samples/snippets/csharp/tutorials/default-interface-members-versions/finished/customer-relationship/ICustomer.cs?name=SnippetLoyaltyDiscountVersionTwo)]

W tym małym fragmencie kodu pokazano wiele nowych funkcji językowych. Interfejsy mogą teraz zawierać statyczne elementy członkowskie, w tym pola i metody. Włączono również różne Modyfikatory dostępu. Dodatkowe pola są prywatne, Nowa metoda jest publiczna. Każdy modyfikator jest dozwolony w składowych interfejsu.

Aplikacje korzystające z ogólnej formuły do obliczania rabatu lojalnościowego, ale innych parametrów nie muszą podawać implementacji niestandardowej. można ustawić argumenty za pomocą metody statycznej. Na przykład poniższy kod ustawia "zwiększenie klienta", który nadaje klientowi więcej niż jeden miesiąc:

[!code-csharp[SetLoyaltyThresholds](~/samples/snippets/csharp/tutorials/default-interface-members-versions/finished/customer-relationship/Program.cs?name=SnippetSetLoyaltyThresholds)]

## <a name="extend-the-default-implementation"></a>Zwiększ implementację domyślną

Kod, który został dodany do tej pory, udostępnia wygodną implementację dla tych scenariuszy, w których użytkownicy chcą, podobnie jak w przypadku implementacji domyślnej, lub w celu zapewnienia niepowiązanego zestawu reguł. Aby uzyskać ostateczną funkcję, należy ponownie oznaczyć kod jako bit, aby włączyć scenariusze, w których użytkownicy mogą chcieć skompilować zgodnie z domyślną implementacją.

Rozważ uruchomienie, które chce przyciągnąć nowych klientów. Oferują rabat w wysokości 50% od pierwszego zamówienia klienta. W przeciwnym razie istniejący klienci otrzymują rabat w warstwie Standardowa. Autor biblioteki musi przenieść domyślną implementację do `protected static` metody, tak aby każda klasa implementująca ten interfejs może ponownie wykorzystać kod w ich implementacji. Domyślna implementacja elementu członkowskiego interfejsu wywołuje tę metodę udostępnioną również:

[!code-csharp[VersionTwoImplementation](~/samples/snippets/csharp/tutorials/default-interface-members-versions/finished/customer-relationship/ICustomer.cs?name=SnippetFinalVersion)]

W implementacji klasy implementującej ten interfejs przesłonięcie może wywołać statyczną metodę pomocnika i zwiększyć tę logikę w celu zapewnienia rabatu "nowy klient":

[!code-csharp[VersionTwoImplementation](~/samples/snippets/csharp/tutorials/default-interface-members-versions/finished/customer-relationship/SampleCustomer.cs?name=SnippetOverrideAndExtend)]

Cały gotowy kod można zobaczyć w naszym [repozytorium przykładów w witrynie GitHub](https://github.com/dotnet/samples/tree/master/csharp/tutorials/default-interface-members-versions/finished/customer-relationship). Możesz uzyskać aplikację Starter w naszym [repozytorium przykładów w witrynie GitHub](https://github.com/dotnet/samples/tree/master/csharp/tutorials/default-interface-members-versions/starter/customer-relationship).

Te nowe funkcje oznaczają, że interfejsy można aktualizować bezpiecznie, gdy istnieje domyślna implementacja dla tych nowych członków. Starannie Projektuj interfejsy, aby przedstawić koncepcje pojedynczych funkcjonalnych, które mogą być implementowane przez wiele klas. Dzięki temu można łatwiej uaktualnić te definicje interfejsów, gdy zostaną odnalezione nowe wymagania dla tego samego pomysłu funkcjonalnego.
