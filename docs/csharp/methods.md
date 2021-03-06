---
title: Metody — Przewodnik C#
description: Przegląd metod, parametrów metody i wartości zwracanych metody
ms.technology: csharp-fundamentals
ms.date: 05/21/2018
ms.assetid: 577a8527-1081-4b36-9b9e-0685b6553c6e
ms.openlocfilehash: d5ca96ab3a07b85fa525dd06c975f8e3221c82e8
ms.sourcegitcommit: 67ebdb695fd017d79d9f1f7f35d145042d5a37f7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/20/2020
ms.locfileid: "92223667"
---
# <a name="methods-in-c"></a>Metody w (C#)

Metoda jest blokiem kodu, który zawiera serie instrukcji. Program powoduje wykonanie instrukcji przez wywołanie metody i określenie wszelkich wymaganych argumentów metody. W języku C# Każda wykonana instrukcja jest wykonywana w kontekście metody. `Main`Metoda jest punktem wejścia dla każdej aplikacji w języku C# i jest wywoływana przez środowisko uruchomieniowe języka wspólnego (CLR), gdy program jest uruchomiony.

> [!NOTE]
> W tym temacie omówiono nazwane metody. Aby uzyskać informacje na temat funkcji anonimowych, zobacz [funkcje anonimowe](programming-guide/statements-expressions-operators/anonymous-functions.md).

<a name="signatures"></a>

## <a name="method-signatures"></a>Sygnatury metod

Metody są zadeklarowane w `class` lub `struct` przez określenie:

- Opcjonalny poziom dostępu, taki jak `public` lub `private` . Wartość domyślna to `private`.
- Opcjonalne modyfikatory, takie jak `abstract` lub `sealed` .
- Wartość zwracana lub, `void` Jeśli metoda nie ma wartości none.
- Nazwa metody.
- Dowolne parametry metody. Parametry metody są ujęte w nawiasy i są rozdzielone przecinkami. Puste nawiasy wskazują, że metoda nie wymaga żadnych parametrów.

Te części wspólnie tworzą sygnaturę metody.

> [!IMPORTANT]
> Zwracany typ metody nie jest częścią podpisu metody do celów przeciążania metody. Jednakże jest częścią podpisu metody podczas określania zgodności między delegatem a metodą, do której wskazuje.

W poniższym przykładzie zdefiniowano klasę o nazwie `Motorcycle` , która zawiera pięć metod:

[!code-csharp[csSnippets.Methods#40](../../samples/snippets/csharp/concepts/methods/methods40.cs#40)]

Należy zauważyć, że `Motorcycle` Klasa zawiera przeciążoną metodę, `Drive` . Dwie metody mają taką samą nazwę, ale muszą być zróżnicowane według ich typów parametrów.

<a name="invocation"></a>

## <a name="method-invocation"></a>Wywołanie metody

Metody mogą być *wystąpieniami* lub *statycznymi*. Wywoływanie metody wystąpienia wymaga utworzenia wystąpienia obiektu i wywołania metody dla tego obiektu; Metoda wystąpienia działa na tym wystąpieniu i jego danych. Należy wywołać metodę statyczną, odwołując się do nazwy typu, do którego należy Metoda; metody statyczne nie działają na danych wystąpienia. Próba wywołania metody statycznej za pomocą wystąpienia obiektu generuje błąd kompilatora.

Wywołanie metody jest podobne do uzyskiwania dostępu do pola. Po nazwie obiektu (jeśli wywoływana jest metoda wystąpienia) lub nazwa typu (jeśli wywołujesz `static` metodę), Dodaj kropkę, nazwę metody i nawiasów. Argumenty są wyświetlane w nawiasach i są oddzielone przecinkami.

Definicja metody Określa nazwy i typy wymaganych parametrów. Gdy wywołujący wywołuje metodę, dostarcza konkretnych wartości, nazywanych argumentami, dla każdego parametru. Argumenty muszą być zgodne z typem parametru, ale nazwa argumentu, jeśli jest używana w wywoływanym kodzie, nie musi być taka sama jak parametr o nazwie zdefiniowanej w metodzie. W poniższym przykładzie `Square` Metoda zawiera pojedynczy parametr typu `int` o nazwie *i*. Pierwsze wywołanie metody przekazuje `Square` metodę zmienną typu `int` o nazwie *NUM*; sekundową, stałą liczbową i trzecim wyrażeniem.

[!code-csharp[csSnippets.Methods#74](../../samples/snippets/csharp/concepts/methods/params74.cs#74)]

Najbardziej typowa forma wywołania metody użyła argumentów pozycyjnych; dostarcza argumenty w takiej samej kolejności jak parametry metody. W związku z tym metody `Motorcycle` klasy mogą być wywoływane jak w poniższym przykładzie. Wywołanie `Drive` metody, na przykład, zawiera dwa argumenty, które odpowiadają dwóm parametrom w składni metody. Pierwszy jest wartością `miles` parametru, drugą wartością `speed` parametru.

[!code-csharp[csSnippets.Methods#41](../../samples/snippets/csharp/concepts/methods/methods40.cs#41)]

Można również użyć *nazwanych argumentów* zamiast argumentów pozycyjnych podczas wywoływania metody. Przy użyciu nazwanych argumentów należy określić nazwę parametru, po którym następuje dwukropek (":") i argument. Argumenty metody mogą pojawiać się w dowolnej kolejności, o ile wszystkie wymagane argumenty są obecne. W poniższym przykładzie zastosowano nazwane argumenty do wywołania `TestMotorcycle.Drive` metody. W tym przykładzie nazwane argumenty są przekazane w odwrotnej kolejności z listy parametrów metody.

[!code-csharp[csSnippets.Methods#45](../../samples/snippets/csharp/concepts/methods/named1.cs#45)]

Metodę można wywołać przy użyciu obu argumentów pozycyjnych i nazwanych argumentów. Jednak argumenty pozycyjne mogą następować po nazwanych argumentach tylko wtedy, gdy nazwane argumenty znajdują się w poprawnych pozycjach. Poniższy przykład wywołuje `TestMotorcycle.Drive` metodę z poprzedniego przykładu przy użyciu jednego argumentu pozycyjnego i jednego argumentu nazwanego.

[!code-csharp[csSnippets.Methods#46](../../samples/snippets/csharp/concepts/methods/named2.cs#46)]

<a name="inherited"></a>

## <a name="inherited-and-overridden-methods"></a>Dziedziczone i zastąpione metody

Oprócz elementów członkowskich, które są jawnie zdefiniowane w typie, typ dziedziczy składowe zdefiniowane w jego klasach bazowych. Ponieważ wszystkie typy w systemie typu zarządzanego dziedziczą bezpośrednio lub pośrednio z <xref:System.Object> klasy, wszystkie typy dziedziczą elementy członkowskie, takie jak <xref:System.Object.Equals(System.Object)> , <xref:System.Object.GetType> , i <xref:System.Object.ToString> . Poniższy przykład definiuje `Person` klasę, tworzy wystąpienie dwóch `Person` obiektów i wywołuje `Person.Equals` metodę, aby określić, czy dwa obiekty są równe. `Equals`Metoda nie jest jednak zdefiniowana w `Person` klasie; jest dziedziczona z <xref:System.Object> .

[!code-csharp[csSnippets.Methods#104](../../samples/snippets/csharp/concepts/methods/inherited1.cs#104)]

Typy mogą przesłaniać dziedziczone elementy członkowskie przy użyciu `override` słowa kluczowego i dostarczając implementację przesłoniętej metody. Sygnatura metody musi być taka sama jak w przypadku przesłoniętej metody. Poniższy przykład jest podobny do poprzedniego, z tą różnicą, że zastępuje <xref:System.Object.Equals(System.Object)> metodę. (Również zastępuje <xref:System.Object.GetHashCode> metodę, ponieważ dwie metody są przeznaczone do zapewnienia spójnych wyników).

[!code-csharp[csSnippets.Methods#105](../../samples/snippets/csharp/concepts/methods/overridden1.cs#105)]

<a name="passing"></a>

## <a name="passing-parameters"></a>Przekazywanie parametrów

Typy w C# to *typy wartości* lub *typy referencyjne*. Listę wbudowanych typów wartości można znaleźć w temacie [Types](./tour-of-csharp/types.md). Domyślnie zarówno typy wartości, jak i typy odwołań są przesyłane do metody przez wartość.

<a name="byval"></a>

### <a name="passing-parameters-by-value"></a>Przekazywanie parametrów według wartości

Gdy typ wartości jest przenoszona do metody przez wartość, kopia obiektu zamiast samego obiektu jest przenoszona do metody. W związku z tym zmiany w obiekcie wywołanej metody nie mają wpływu na oryginalny obiekt, gdy sterowanie powraca do obiektu wywołującego.

Poniższy przykład przekazuje typ wartości do metody przez wartość, a wywołana metoda próbuje zmienić wartość typu wartości. Definiuje zmienną typu `int` , która jest typem wartości, inicjuje jej wartość na 20 i przekazuje ją do metody o nazwie, `ModifyValue` która zmienia wartość zmiennej na 30. Gdy metoda zwraca, jednak wartość zmiennej pozostaje niezmieniona.

[!code-csharp[csSnippets.Methods#10](../../samples/snippets/csharp/concepts/methods/byvalue10.cs#10)]

Gdy obiekt typu referencyjnego jest przekazanie do metody przez wartość, odwołanie do obiektu jest przesyłane przez wartość. Oznacza to, że metoda nie odbiera samego obiektu, ale argument, który wskazuje lokalizację obiektu. Jeśli zmienisz element członkowski obiektu za pomocą tego odwołania, zmiana zostanie odzwierciedlona w obiekcie, gdy sterowanie powróci do metody wywołującej. Jednak zastąpienie obiektu przesłanego do metody nie ma wpływu na oryginalny obiekt, gdy sterowanie powraca do obiektu wywołującego.

W poniższym przykładzie zdefiniowano klasę (będącą typem referencyjnym) o nazwie `SampleRefType` . Tworzy wystąpienie `SampleRefType` obiektu, przypisuje 44 do jego `value` pola i przekazuje obiekt do `ModifyObject` metody. Ten przykład zasadniczo działa tak samo jak w poprzednim przykładzie — przekazuje argument przez wartość do metody. Ale ponieważ jest używany typ referencyjny, wynik jest różny. Modyfikacja wprowadzona w `ModifyObject` `obj.value` polu również zmienia `value` pola argumentu, `rt` w `Main` metodzie na 33, jako dane wyjściowe z przykładu.

[!code-csharp[csSnippets.Methods#42](../../samples/snippets/csharp/concepts/methods/byvalue42.cs#42)]

<a name="byref"></a>

### <a name="passing-parameters-by-reference"></a>Przekazywanie parametrów według odwołania

Parametr można przekazać przez odwołanie, gdy chcesz zmienić wartość argumentu w metodzie i chcieć odzwierciedlić tę zmianę, gdy sterowanie powraca do metody wywołującej. Aby przekazać parametr przez odwołanie, należy użyć [`ref`](language-reference/keywords/ref.md) [`out`](language-reference/keywords/out-parameter-modifier.md) słowa kluczowego or. Możesz również przekazać wartość przez odwołanie, aby uniknąć kopiowania, ale nadal uniemożliwiać modyfikacje przy użyciu [`in`](language-reference/keywords/in-parameter-modifier.md) słowa kluczowego.

Poniższy przykład jest identyczny z poprzednim, z wyjątkiem tego, że wartość jest przenoszona przez odwołanie do `ModifyValue` metody. Gdy wartość parametru jest modyfikowana w `ModifyValue` metodzie, zmiana wartości jest odzwierciedlona, gdy sterowanie powraca do obiektu wywołującego.

[!code-csharp[csSnippets.Methods#106](../../samples/snippets/csharp/concepts/methods/byref106.cs#106)]

Typowy wzorzec wykorzystywany przez parametry ref obejmuje zamianę wartości zmiennych. Dwie zmienne są przekazywane do metody przez odwołanie, a metoda zamienia ich zawartość. Poniższy przykład zamienia wartości całkowite.

[!code-csharp[csSnippets.Methods#106](../../samples/snippets/csharp/concepts/methods/swap107.cs#107)]

Przekazywanie parametru typu odwołania umożliwia zmianę wartości samego odwołania, a nie wartości poszczególnych elementów lub pól.

<a name="paramarray"></a>

### <a name="parameter-arrays"></a>Tablice parametrów

Czasami wymaganie podania dokładnej liczby argumentów do metody jest restrykcyjne. Za pomocą `params` słowa kluczowego, aby wskazać, że parametr jest tablicą parametrów, można wywołać metodę o zmiennej liczbie argumentów. Parametr oznaczony `params` słowem kluczowym musi być typem tablicowym i musi być ostatnim parametrem na liście parametrów metody.

Obiekt wywołujący może następnie wywołać metodę na jeden z czterech sposobów:

- Przekazując tablicę odpowiedniego typu, która zawiera żądaną liczbę elementów.
- Przekazując do metody rozdzieloną przecinkami listę pojedynczych argumentów odpowiedniego typu.
- Przez przekazanie `null` .
- Nie dostarczając argumentu do tablicy parametrów.

W poniższym przykładzie zdefiniowano metodę o nazwie `GetVowels` , która zwraca wszystkie samogłosy z tablicy parametrów. `Main`Metoda ilustruje wszystkie cztery sposoby wywoływania metody. Obiekty wywołujące nie muszą podawać żadnych argumentów dla parametrów, które zawierają `params` modyfikator. W takim przypadku parametr jest pustą tablicą.

[!code-csharp[csSnippets.Methods#75](~/samples/snippets/csharp/concepts/methods/params75.cs#75)]

<a name="optional"></a>

## <a name="optional-parameters-and-arguments"></a>Opcjonalne parametry i argumenty

Definicja metody może określać, że parametry są wymagane lub są opcjonalne. Domyślnie parametry są wymagane. Parametry opcjonalne są określane przez dołączenie wartości domyślnej parametru w definicji metody. Gdy metoda jest wywoływana, jeśli nie podano żadnego argumentu dla parametru opcjonalnego, zamiast tego zostanie użyta wartość domyślna.

Wartość domyślna parametru musi być przypisana przy użyciu jednego z następujących rodzajów wyrażeń:

- Stała, taka jak ciąg literału lub liczba.
- Wyrażenie formularza `new ValType()` , gdzie `ValType` jest typem wartości. Należy zauważyć, że spowoduje to wywołanie niejawnego konstruktora bez parametrów typu wartości, który nie jest rzeczywistym elementem członkowskim typu.
- Wyrażenie formularza `default(ValType)` , gdzie `ValType` jest typem wartości.

Jeśli metoda obejmuje parametry wymagane i opcjonalne, parametry opcjonalne są definiowane na końcu listy parametrów po wszystkich wymaganych parametrach.

W poniższym przykładzie zdefiniowano metodę, `ExampleMethod` która ma jeden wymagany i dwa parametry opcjonalne.

[!code-csharp[csSnippets.Methods#21](../../samples/snippets/csharp/concepts/methods/optional1.cs#21)]

Jeśli metoda z wieloma opcjonalnymi argumentami jest wywoływana przy użyciu argumentów pozycyjnych, obiekt wywołujący musi podać argument dla wszystkich parametrów opcjonalnych z pierwszego do ostatniego, dla którego podano argument. W przypadku  `ExampleMethod` metody, na przykład jeśli obiekt wywołujący dostarcza argument dla `description` parametru, musi również podać jeden dla `optionalInt` parametru. `opt.ExampleMethod(2, 2, "Addition of 2 and 2");` jest prawidłowym wywołaniem metody; `opt.ExampleMethod(2, , "Addition of 2 and 0");` generuje błąd kompilatora "Brak argumentu".

Jeśli metoda jest wywoływana przy użyciu nazwanych argumentów lub kombinacji argumentów pozycyjnych i nazwanych, obiekt wywołujący może pominąć wszystkie argumenty, które po ostatnim argumencie pozycyjnym w wywołaniu metody.

Poniższy przykład wywołuje `ExampleMethod` metodę trzykrotnie.  Pierwsze dwa wywołania metod używają argumentów pozycyjnych. Pierwsze pomija oba argumenty opcjonalne, podczas gdy drugi pomija ostatni argument. Trzecie wywołanie metody dostarcza argument pozycyjny dla wymaganego parametru, ale używa argumentu nazwanego do podania wartości do `description` parametru podczas pomijania `optionalInt` argumentu.

[!code-csharp[csSnippets.Methods#22](../../samples/snippets/csharp/concepts/methods/optional1.cs#22)]

Użycie parametrów opcjonalnych wpływa na *rozdzielczość przeciążenia*lub sposób, w jaki kompilator języka C# określa, które określone Przeciążenie powinno być wywoływane przez wywołanie metody w następujący sposób:

- Metoda, indeksator lub Konstruktor jest kandydatem do wykonania, jeśli każdy z jego parametrów jest opcjonalny lub odpowiada według nazwy lub według pozycji, do pojedynczego argumentu w instrukcji wywołującej i ten argument można przekonwertować na typ parametru.
- W przypadku znalezienia więcej niż jednego kandydata reguły rozpoznawania przeciążenia dla preferowanych konwersji są stosowane do argumentów, które są jawnie określone. Pominięte argumenty dla parametrów opcjonalnych są ignorowane.
- Jeśli dwie kandydaci są uważane za równie dobre, preferencja przechodzi do kandydata, który nie ma parametrów opcjonalnych, dla których argumenty zostały pominięte w wywołaniu. Jest to konsekwencja ogólne preferencje rozpoznawania przeciążenia dla kandydatów, które mają mniej parametrów.

<a name="return"></a>

## <a name="return-values"></a>Wartości zwracane

Metody mogą zwracać wartość do obiektu wywołującego. Jeśli typ zwracany (typ wymieniony przed nazwą metody) nie jest `void` , Metoda może zwrócić wartość za pomocą `return` słowa kluczowego. Instrukcja ze `return` słowem kluczowym, po której następuje zmienna, stała lub wyrażenie zgodne z typem zwracanym zwróci tę wartość do obiektu wywołującego metodę. Metody z typem zwracanym innym niż void są wymagane do `return` zwrócenia wartości za pomocą słowa kluczowego. `return`Słowo kluczowe również przerywa wykonywanie metody.

Jeśli zwracanym typem jest `void` , `return` instrukcja bez wartości jest nadal przydatna do zatrzymania wykonywania metody. Bez `return` słowa kluczowego, Metoda zostanie zatrzymana po osiągnięciu końca bloku kodu.

Na przykład te dwie metody używają `return` słowa kluczowego do zwracania liczb całkowitych:

[!code-csharp[csSnippets.Methods#44](../../samples/snippets/csharp/concepts/methods/return44.cs#44)]

Aby użyć wartości zwracanej z metody, Metoda wywołująca może użyć wywołania metody, wszędzie tam, gdzie wartość tego samego typu byłaby wystarczająca. Możesz również przypisać wartość zwracaną do zmiennej. Na przykład następujące dwa przykłady kodu mają ten sam cel:

[!code-csharp[csSnippets.Methods#45](../../samples/snippets/csharp/concepts/methods/return44.cs#45)]

[!code-csharp[csSnippets.Methods#46](../../samples/snippets/csharp/concepts/methods/return44.cs#46)]

Użycie zmiennej lokalnej, w tym przypadku, `result` do przechowywania wartości jest opcjonalne. Może to pomóc w czytelności kodu lub może być konieczne, jeśli konieczne będzie przechowywanie pierwotnej wartości argumentu dla całego zakresu metody.

Czasami chcesz, aby Metoda zwracała więcej niż jedną wartość. Począwszy od języka C# 7,0, można to łatwo zrobić, używając *typów krotek* i *literałów krotek*. Typ krotki definiuje typy danych elementów krotki. Literały krotki zapewniają rzeczywiste wartości zwracanej krotki. W poniższym przykładzie `(string, string, string, int)` definiuje typ krotki, który jest zwracany przez `GetPersonalInfo` metodę. Wyrażenie `(per.FirstName, per.MiddleName, per.LastName, per.Age)` jest literałem krotki; Metoda zwraca pierwszą, środkową i nazwisko, wraz z wiekiem `PersonInfo` obiektu.

```csharp
public (string, string, string, int) GetPersonalInfo(string id)
{
    PersonInfo per = PersonInfo.RetrieveInfoById(id);
    return (per.FirstName, per.MiddleName, per.LastName, per.Age);
}
```

Obiekt wywołujący może następnie użyć zwróconej krotki z kodem podobnym do poniższego:

```csharp
var person = GetPersonalInfo("111111111")
Console.WriteLine($"{person.Item1} {person.Item3}: age = {person.Item4}");
```

Nazwy można także przypisać do elementów krotki w definicji typu krotki. W poniższym przykładzie pokazano alternatywną wersję `GetPersonalInfo` metody używającej nazwanych elementów:

```csharp
public (string FName, string MName, string LName, int Age) GetPersonalInfo(string id)
{
    PersonInfo per = PersonInfo.RetrieveInfoById(id);
    return (per.FirstName, per.MiddleName, per.LastName, per.Age);
}
```

Poprzednie wywołanie `GetPersonInfo` metody można następnie zmodyfikować w następujący sposób:

```csharp
var person = GetPersonalInfo("111111111");
Console.WriteLine($"{person.FName} {person.LName}: age = {person.Age}");
```

Jeśli metoda przekazuje tablicę jako argument i modyfikuje wartość poszczególnych elementów, nie jest to konieczne, aby Metoda zwracała tablicę, chociaż można to zrobić dla dobrego stylu lub przepływu funkcjonalnych wartości.  Wynika to z faktu, że C# przekazuje wszystkie typy odwołań według wartości, a wartość odwołania tablicy jest wskaźnikiem do tablicy. W poniższym przykładzie zmiany zawartości `values` tablicy, które są wykonywane w `DoubleValues` metodzie, są zauważalne przez dowolny kod, który zawiera odwołanie do tablicy.

[!code-csharp[csSnippets.Methods#101](../../samples/snippets/csharp/concepts/methods/returnarray1.cs#101)]

<a name="extension"></a>

## <a name="extension-methods"></a>Metody rozszerzeń

Zwykle istnieją dwa sposoby dodawania metody do istniejącego typu:

- Zmodyfikuj kod źródłowy dla tego typu. Nie można tego zrobić, jeśli nie jesteś własnym kodem źródłowym typu. Jest to istotna zmiana, jeśli dodasz także wszystkie pola danych prywatnych do obsługi metody.
- Zdefiniuj nową metodę w klasie pochodnej. Nie można dodać metody w ten sposób przy użyciu dziedziczenia dla innych typów, takich jak struktury i wyliczenia. Nie można ich również użyć do dodania metody do klasy zapieczętowanej.

Metody rozszerzające umożliwiają "dodanie" metody do istniejącego typu bez modyfikowania samego typu lub implementowania nowej metody w dziedziczonym typie. Metoda rozszerzająca również nie musi znajdować się w tym samym zestawie, co rozszerza typ. Wywoływana jest metoda rozszerzająca, tak jakby była to zdefiniowana składowa typu.

Aby uzyskać więcej informacji, zobacz [metody rozszerzenia](programming-guide/classes-and-structs/extension-methods.md).

<a name="async"></a>

## <a name="async-methods"></a>Metody asynchroniczne

Za pomocą funkcji asynchronicznej można wywołać metody asynchroniczne bez używania jawnych wywołań zwrotnych lub ręcznie podzielić kod na wiele metod lub wyrażenia lambda.

Jeśli oznaczesz metodę za pomocą modyfikatora [asynchronicznego](language-reference/keywords/async.md) , możesz użyć operatora [await](language-reference/operators/await.md) w metodzie. Gdy kontrolka osiągnie `await` wyrażenie w metodzie asynchronicznej, sterowanie powraca do obiektu wywołującego, jeśli oczekiwane zadanie nie zostało ukończone, a postęp w metodzie ze `await` słowem kluczowym jest zawieszony do momentu zakończenia zadania oczekiwania. Po zakończeniu zadania wykonywanie może zostać wznowione w metodzie.

> [!NOTE]
> Metoda asynchroniczna wraca do obiektu wywołującego, gdy napotka on pierwszy oczekujący obiekt, który nie został jeszcze ukończony lub otrzymuje koniec metody asynchronicznej, zależnie od tego, co się dzieje.

Metoda asynchroniczna może mieć zwracany typ <xref:System.Threading.Tasks.Task%601> , <xref:System.Threading.Tasks.Task> , lub `void` . `void`Typ zwracany jest używany głównie do definiowania programów obsługi zdarzeń, gdy `void` wymagany jest typ zwracany. Metoda async zwracająca wartość `void` nie może być oczekiwana, a obiekt wywołujący metodę void nie może przechwytywać wyjątków, które metoda zgłasza. Począwszy od języka C# 7,0, Metoda asynchroniczna może mieć [dowolny typ zwracany podobne do zadania](./whats-new/csharp-7.md#generalized-async-return-types).

W poniższym przykładzie `DelayAsync` jest metoda async, która zawiera instrukcję return, która zwraca liczbę całkowitą. Ponieważ jest to Metoda asynchroniczna, jej Deklaracja metody musi być typem zwracanym `Task<int>` . Ponieważ typem zwracanym jest `Task<int>` , obliczanie `await` wyrażenia w `DoSomethingAsync` tworzy liczbę całkowitą, jak pokazano w poniższej `int result = await delayTask` instrukcji.

:::code language="csharp" source="programming-guide/classes-and-structs/snippets/classes-and-structs/methods/Program.cs":::

Metoda async nie może deklarować parametrów [in](language-reference/keywords/in-parameter-modifier.md), [ref](language-reference/keywords/ref.md)ani [out](language-reference/keywords/out-parameter-modifier.md) , ale może wywoływać metody, które mają takie parametry.

 Aby uzyskać więcej informacji na temat metod asynchronicznych, zobacz [programowanie asynchroniczne z asynchroniczne i oczekujące](async.md) i [asynchroniczne typy zwracane](programming-guide/concepts/async/async-return-types.md).

<a name="expr"></a>

## <a name="expression-bodied-members"></a>Składowe z wyrażeniem w treści

Często istnieją definicje metod, które po prostu zwracają bezpośrednio z wynikiem wyrażenia lub które mają pojedynczą instrukcję jako treść metody.  Istnieje skrót do definiowania takich metod przy użyciu `=>` :

```csharp
public Point Move(int dx, int dy) => new Point(x + dx, y + dy);
public void Print() => Console.WriteLine(First + " " + Last);
// Works with operators, properties, and indexers too.
public static Complex operator +(Complex a, Complex b) => a.Add(b);
public string Name => First + " " + Last;
public Customer this[long id] => store.LookupCustomer(id);
```

Jeśli metoda zwraca `void` lub jest metodą asynchroniczną, treść metody musi być wyrażeniem instrukcji (analogicznie jak w przypadku wyrażeń lambda).  W przypadku właściwości i indeksatorów muszą one być tylko do odczytu i nie można używać `get` słowa kluczowego metody dostępu.

<a name="iterators"></a>

## <a name="iterators"></a>Iteratory

Iterator wykonuje niestandardową iterację w kolekcji, na przykład listę lub tablicę. Iterator używa instrukcji [yield return](language-reference/keywords/yield.md) , aby zwrócić każdy element po jednym naraz. Po `yield return` osiągnięciu instrukcji zostanie zapamiętana bieżąca lokalizacja, aby obiekt wywołujący mógł zażądać następnego elementu w sekwencji.

Zwracany typ iteratora może mieć wartość <xref:System.Collections.IEnumerable> , <xref:System.Collections.Generic.IEnumerable%601> , <xref:System.Collections.IEnumerator> , lub <xref:System.Collections.Generic.IEnumerator%601> .

Aby uzyskać więcej informacji, zobacz [Iteratory](programming-guide/concepts/iterators.md).

## <a name="see-also"></a>Zobacz też

- [Modyfikatory dostępu](language-reference/keywords/access-modifiers.md)
- [Klasy statyczne i statyczni członkowie klas](programming-guide/classes-and-structs/static-classes-and-static-class-members.md)
- [Dziedziczenie](programming-guide/classes-and-structs/inheritance.md)
- [Klasy abstrakcyjne i zapieczętowane oraz członkowie klas](programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md)
- [params](language-reference/keywords/params.md)
- [określoną](language-reference/keywords/out-parameter-modifier.md)
- [ref](language-reference/keywords/ref.md)
- [podczas](language-reference/keywords/in-parameter-modifier.md)
- [Przekazywanie parametrów](programming-guide/classes-and-structs/passing-parameters.md)
