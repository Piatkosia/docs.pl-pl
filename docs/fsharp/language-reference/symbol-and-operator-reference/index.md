---
title: Odwołanie do symbolu i operatora
description: 'Poznaj symbole i operatory, które są używane w języku programowania języka F #.'
ms.date: 08/15/2020
fl_keywords:
- '|>_FS'
ms.openlocfilehash: 5943352f0a1710ba7a666a79b7871b7269c75a6b
ms.sourcegitcommit: ae2e8a61a93c5cf3f0035c59e6b064fa2f812d14
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/02/2020
ms.locfileid: "89359093"
---
# <a name="symbol-and-operator-reference"></a>Odwołanie do symbolu i operatora

Ten artykuł zawiera tabelę symboli i operatorów, które są używane w języku F #.

## <a name="table-of-symbols-and-operators"></a>Tabela symboli i operatorów

W poniższej tabeli opisano symbole używane w języku F # i przedstawiono krótki opis niektórych użycia symbolu i linki, aby uzyskać więcej informacji. Symbole są uporządkowane według kolejności zestawu znaków ASCII.

|Symbol lub operator|Linki|Opis|
|------------------|-----|-----------|
|`!`|[Komórki odwołań](../reference-cells.md)<br /><br />[Wyrażenia obliczeń](../computation-expressions.md)|<ul><li>Odwołuje się do komórki odwołania.<br /></li><li>Po słowie kluczowym, wskazuje zmodyfikowaną wersję zachowania słowa kluczowego jako kontrolowanego przez przepływ pracy.<br /></li></ul>|
|`!=`||<ul><li>Nieużywane w języku F #. Służy `<>` do wykonywania operacji nierówności.<br /></li></ul>|
|`"`|[Literały](../literals.md)<br /><br />[Ciągi](../strings.md)|<ul><li>Ogranicza ciąg tekstowy.<br /></li></ul>|
|`"""`|[Ciągi](../strings.md)|Ogranicza Verbatim ciąg tekstowy. Różni się od `@"..."` w tym, że można wskazać znak cudzysłowu przy użyciu pojedynczego cudzysłowu w ciągu.|
|`#`|[Dyrektywy kompilatora](../compiler-directives.md)<br /><br />[Typy elastyczne](../flexible-types.md)|<ul><li>Prefiks preprocesora lub dyrektywy kompilatora, takich jak `#light` .<br /></li><li>Gdy jest używany z typem, wskazuje *elastyczny typ*, który odwołuje się do typu lub dowolnego jednego z jego typów pochodnych.<br /></li></ul>|
|`$`||<ul><li>Używane wewnętrznie dla niektórych nazw zmiennych i funkcji generowanych przez kompilator.<br /></li></ul>|
|`%`|[Operatory arytmetyczne](arithmetic-operators.md)<br /><br />[Cytaty kodu](../code-quotations.md)|<ul><li>Oblicza resztę całkowitą.<br /></li><li>Służy do łączenia wyrażeń w cudzysłowy w kodzie wpisanych.<br /></li></ul>|
|`%%`|[Cytaty kodu](../code-quotations.md)|<ul><li>Służy do łączenia wyrażeń z niewpisanymi cytatami kodu.<br /></li></ul>|
|`%?`|[Operatory dopuszczające wartość null](nullable-operators.md)|<ul><li>Oblicza resztę całkowitą, gdy po prawej stronie jest typem dopuszczającym wartość null.<br /></li></ul>|
|`&`|[Wyrażenia dopasowania](../match-expressions.md)|<ul><li>Oblicza adres modyfikowalnej wartości do użycia podczas współdziałania z innymi językami.<br /></li><li>Używany w wzorcach i.<br /></li></ul>|
|`&&`|[Operatory logiczne](boolean-operators.md)|<ul><li>Oblicza wartość logiczną i operację.<br /></li></ul>|
|`&&&`|[Operatory bitowe](bitwise-operators.md)|<ul><li>Oblicza wartość bitową i operację.<br /></li></ul>|
|`'`|[Literały](../literals.md)<br /><br />[Automatyczna generalizacja](../generics/automatic-generalization.md)|<ul><li>Ogranicza literał jednoznakowy.<br /></li><li>Wskazuje parametr typu ogólnego.<br /></li></ul>|
|<code>&#96;&#96;...&#96;&#96;</code>||<ul><li>Ogranicza identyfikator, który w przeciwnym razie nie będzie prawidłowym identyfikatorem, na przykład słowa kluczowego języka.<br /></li></ul>|
|`( )`|[Typ jednostki](../unit-type.md)|<ul><li>Reprezentuje pojedynczą wartość typu jednostki.<br /></li></ul>|
|`(...)`|[Krotki](../tuples.md)<br /><br />[Przeciążanie operatora](../operator-overloading.md)|<ul><li>Wskazuje kolejność, w której obliczane są wyrażenia.<br /></li><li>Ogranicza spójność krotki.<br /></li><li>Używane w definicjach operatora.<br /></li></ul>|
|`(*...*)`||<ul><li>Ogranicza komentarz, który może obejmować wiele wierszy.<br /></li></ul>|
|<code>(&#124;...&#124;)</code>|[Wzorce aktywne](../active-patterns.md)|<ul><li>Ogranicza Aktywny wzorzec. Nazywane również *klipami bananów*.<br /></li></ul>|
|`*`|[Operatory arytmetyczne](arithmetic-operators.md)<br /><br />[Krotki](../tuples.md)<br /><br />[Jednostki miary](../units-of-measure.md)|<ul><li>Gdy jest używany jako operator binarny, mnoży lewe i prawe strony.<br /></li><li>W typach, wskazuje parowanie w spójnej kolekcji.<br /></li><li>Używane w jednostkach typu miary.<br /></li></ul>|
|`*?`|[Operatory dopuszczające wartość null](nullable-operators.md)|<ul><li>Mnoży lewe i prawe strony, gdy po prawej stronie jest typem dopuszczającym wartość null.<br /></li></ul>|
|`**`|[Operatory arytmetyczne](arithmetic-operators.md)|<ul><li>Oblicza operacje potęgowania ( `x ** y` oznacza `x` potęgę `y` ).<br /></li></ul>|
|`+`|[Operatory arytmetyczne](arithmetic-operators.md)|<ul><li>Gdy jest używany jako operator binarny, dodaje lewe i prawe strony.<br /></li><li>Gdy jest używany jako operator jednoargumentowy, wskazuje liczbę dodatnią. (Formalnie zwraca tę samą wartość z niezmienionym znakiem).<br /></li></ul>|
|`+?`|[Operatory dopuszczające wartość null](nullable-operators.md)|<ul><li>Dodaje lewe i prawe strony, gdy po prawej stronie jest typem dopuszczającym wartość null.<br /></li></ul>|
|`,`|[Krotki](../tuples.md)|<ul><li>Oddziela elementy krotki lub parametrów typu.<br /></li></ul>|
|`-`|[Operatory arytmetyczne](arithmetic-operators.md)|<ul><li>Gdy jest używany jako operator binarny, odejmuje prawą stronę od lewej strony.<br /></li><li>Gdy jest używany jako operator jednoargumentowy, wykonuje operację negacji.<br /></li></ul>|
|`-?`|[Operatory dopuszczające wartość null](nullable-operators.md)|<ul><li>Odejmuje prawą stronę od lewej strony, gdy po prawej stronie jest typem dopuszczającym wartość null.<br /></li></ul>|
|`->`|[Funkcje](../functions/index.md)<br /><br />[Wyrażenia dopasowania](../match-expressions.md)|<ul><li>W typach funkcji, ogranicza argumenty i zwraca wartości.<br /></li><li>Zwraca wyrażenie (w wyrażeniach sekwencji); odpowiednik `yield` słowa kluczowego.<br /></li><li>Używane w wyrażeniach dopasowania<br /></li></ul>|
|`.`|[Elementy członkowskie](../members/index.md)<br /><br />[Typy pierwotne](../basic-types.md)|<ul><li>Uzyskuje dostęp do elementu członkowskiego i oddziela poszczególne nazwy w pełni kwalifikowana nazwa.<br /></li><li>Określa punkt dziesiętny w liczbie zmiennoprzecinkowej.<br /></li></ul>|
|`..`|[Pętle: `for...in` wyrażenie](../loops-for-in-expression.md)|<ul><li>Określa zakres.<br /></li></ul>|
|`.. ..`|[Pętle: `for...in` wyrażenie](../loops-for-in-expression.md)|<ul><li>Określa zakres wraz z przyrostem.<br /></li></ul>|
|`.[...]`|[Tablice](../arrays.md)|<ul><li>Uzyskuje dostęp do elementu tablicy.<br /></li></ul>|
|`/`|[Operatory arytmetyczne](arithmetic-operators.md)<br /><br />[Jednostki miary](../units-of-measure.md)|<ul><li>Dzieli lewą stronę (licznik) po prawej stronie (mianownik).<br /></li><li>Używane w jednostkach typu miary.<br /></li></ul>|
|`/?`|[Operatory dopuszczające wartość null](nullable-operators.md)|<ul><li>Dzieli lewą stronę po prawej stronie, gdy po prawej stronie jest typem dopuszczającym wartość null.<br /></li></ul>|
|`//`||<ul><li>Wskazuje początek jednowierszowego komentarza.<br /></li></ul>|
|`///`|[Dokumentacja XML](../xml-documentation.md)|<ul><li>Wskazuje komentarz XML.<br /></li></ul>|
|`:`|[Funkcje](../functions/index.md)|<ul><li>W adnotacji typu oddziela parametr lub nazwę elementu członkowskiego od jego typu.<br /></li></ul>|
|`::`|[Listy](../lists.md)<br /><br />[Wyrażenia dopasowania](../match-expressions.md)|<ul><li>Tworzy listę. Element po lewej stronie jest dołączany do listy po prawej stronie.<br /></li><li>Używane w dopasowywaniu wzorców do oddzielenia części listy.<br /></li></ul>|
|`:=`|[Komórki odwołań](../reference-cells.md)|<ul><li>Przypisuje wartość do komórki odwołania.<br /></li></ul>|
|`:>`|[Rzutowanie i konwersje](../casting-and-conversions.md)|<ul><li>Konwertuje typ na typ, który jest wyższy w hierarchii.<br /></li></ul>|
|`:?`|[Wyrażenia dopasowania](../match-expressions.md)|<ul><li>Zwraca `true` czy wartość pasuje do określonego typu (w tym, czy jest to podtyp); w przeciwnym razie zwraca wartość `false` (operator testu typu).<br /></li></ul>|
|`:?>`|[Rzutowanie i konwersje](../casting-and-conversions.md)|<ul><li>Konwertuje typ na typ, który jest niższy w hierarchii.<br /></li></ul>|
|`;`|[Pełna składnia](../verbose-syntax.md)<br /><br />[Listy](../lists.md)<br /><br />[Rekordy](../records.md)|<ul><li>Oddziela wyrażenia (używane głównie w składni verbose).<br /></li><li>Oddziela elementy listy.<br /></li><li>Oddziela pola rekordu.<br /></li></ul>|
|`<`|[Operatory arytmetyczne](arithmetic-operators.md)|<ul><li>Oblicza mniejszą ilość operacji.<br /></li></ul>|
|`<?`|[Operatory dopuszczające wartość null](nullable-operators.md)|Oblicza wartość mniejszą niż operacja, gdy po prawej stronie jest typem dopuszczającym wartość null.|
|`<<`|[Funkcje](../functions/index.md)|<ul><li>Redaguje dwie funkcje w odwrotnej kolejności; druga jest wykonywana pierwszy (operator kompozycji wstecznej).<br /></li></ul>|
|`<<<`|[Operatory bitowe](bitwise-operators.md)|<ul><li>Przenosi bity w ilości po lewej stronie w lewo o liczbę bitów określoną po prawej stronie.<br /></li></ul>|
|`<-`|[Wartości](../values/index.md)|<ul><li>Przypisuje wartość do zmiennej.<br /></li></ul>|
|`<...>`|[Automatyczna generalizacja](../generics/automatic-generalization.md)|<ul><li>Ogranicza parametry typu.<br /></li></ul>|
|`<>`|[Operatory arytmetyczne](arithmetic-operators.md)|<ul><li>Zwraca wartość `true` , jeśli lewa strona nie jest równa prawej stronie; w przeciwnym razie zwraca wartość false.<br /></li></ul>|
|`<>?`|[Operatory dopuszczające wartość null](nullable-operators.md)|<ul><li>Oblicza nierówną operację, gdy po prawej stronie jest typem dopuszczającym wartość null.<br /></li></ul>|
|`<=`|[Operatory arytmetyczne](arithmetic-operators.md)|<ul><li>Zwraca `true` czy po lewej stronie jest mniejsza lub równa prawej stronie; w przeciwnym razie zwraca `false` .<br /></li></ul>|
|`<=?`|[Operatory dopuszczające wartość null](nullable-operators.md)|<ul><li>Oblicza wartość "mniejszej lub równej", gdy po prawej stronie jest typem DOPUSZCZANYM do wartości null.<br /></li></ul>|
|<code>&#124;></code>|[Funkcje](../functions/index.md)|<ul><li>Przekazuje wynik lewej strony do funkcji po prawej stronie (operator potoku dalej).<br /></li></ul>|
|<code>&#124;&#124;></code>|[&#40; &#124;&#124;&#62; &#41;&#60; t 1, t 2, "U&#62; funkcja](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-operators.html#(%20%7C%7C%3E%20))|<ul><li>Przekazuje krotkę dwóch argumentów po lewej stronie do funkcji po prawej stronie.<br /></li></ul>|
|<code>&#124;&#124;&#124;></code>|[&#40; &#124;&#124;&#124;&#62; &#41;&#60; 1,1, t 2, t 3, "U&#62; funkcja](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-operators.html#(%20%7C%7C%7C%3E%20))|<ul><li>Przekazuje krotkę trzech argumentów po lewej stronie do funkcji po prawej stronie.<br /></li></ul>|
|<code>&lt;&#124;</code>|[Funkcje](../functions/index.md)|<ul><li>Przekazuje wynik wyrażenia po prawej stronie do funkcji po lewej stronie (operator potoku wstecznego).<br /></li></ul>|
|<code>&lt;&#124;&#124;</code>|[&#40; &#60;&#124;&#124; &#41;&#60; t 1, t 2, "U&#62; funkcja](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-operators.html#(%20%3C%7C%7C%20))|<ul><li>Przekazuje krotkę dwóch argumentów po prawej stronie do funkcji po lewej stronie.<br /></li></ul>|
|<code>&lt;&#124;&#124;&#124;</code>|[&#40; &#60;&#124;&#124;&#124; &#41;&#60; 1,1, t 2, t 3, "U&#62; funkcja](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-operators.html#(%20%3C%7C%7C%7C%20))|<ul><li>Przekazuje krotkę trzech argumentów po prawej stronie do funkcji po lewej stronie.<br /></li></ul>|
|`<@...@>`|[Cytaty kodu](../code-quotations.md)|<ul><li>Ogranicza wpisaną ofertę kodu.<br /></li></ul>|
|`<@@...@@>`|[Cytaty kodu](../code-quotations.md)|<ul><li>Ogranicza nietypu cytat kodu.<br /></li></ul>|
|`=`|[Operatory arytmetyczne](arithmetic-operators.md)|<ul><li>Zwraca wartość `true` , jeśli lewa strona jest równa prawej stronie; w przeciwnym razie zwraca `false` .<br /></li></ul>|
|`=?`|[Operatory dopuszczające wartość null](nullable-operators.md)|<ul><li>Oblicza operację "EQUAL", gdy po prawej stronie jest typem dopuszczającym wartość null.<br /></li></ul>|
|`==`||<ul><li>Nieużywane w języku F #. Używane `=` dla operacji równości.<br /></li></ul>|
|`>`|[Operatory arytmetyczne](arithmetic-operators.md)|<ul><li>Zwraca `true` czy po lewej stronie jest większa od prawej strony; w przeciwnym razie zwraca `false` .<br /></li></ul>|
|`>?`|[Operatory dopuszczające wartość null](nullable-operators.md)|<ul><li>Oblicza operację "większe niż", gdy po prawej stronie jest typem dopuszczającym wartość null.<br /></li></ul>|
|`>>`|[Funkcje](../functions/index.md)|<ul><li>Redaguje dwie funkcje (operator kompozycji dalej).<br /></li></ul>|
|`>>>`|[Operatory bitowe](bitwise-operators.md)|<ul><li>Przenosi bity w ilości po lewej stronie w prawo o liczbę miejsc określoną po prawej stronie.<br /></li></ul>|
|`>=`|[Operatory arytmetyczne](arithmetic-operators.md)|<ul><li>Zwraca `true` czy po lewej stronie jest większa lub równa prawej stronie; w przeciwnym razie zwraca `false` .<br /></li></ul>|
|`>=?`|[Operatory dopuszczające wartość null](nullable-operators.md)|<ul><li>Oblicza operacje "większe niż lub równe", gdy po prawej stronie jest typem dopuszczającym wartość null.<br /></li></ul>|
|`?`|[Parametry i argumenty](../parameters-and-arguments.md)|<ul><li>Określa opcjonalny argument.<br /></li><li>Używany jako operator dla wywołań metody dynamicznej i właściwości. Musisz wprowadzić własną implementację.<br /></li></ul>|
|`? ... <- ...`||<ul><li>Używany jako operator do ustawiania właściwości dynamicznych. Musisz wprowadzić własną implementację.<br /></li></ul>|
|`?>=`, `?>`, `?<=`, `?<`, `?=`, `?<>`, `?+`, `?-`, `?*`, `?/`|[Operatory dopuszczające wartość null](nullable-operators.md)|<ul><li>Równoważne z odpowiednimi operatorami bez prefiks, gdzie typ dopuszczający wartość null znajduje się po lewej stronie.<br /></li></ul>|
|`>=?`, `>?`, `<=?`, `<?`, `=?`, `<>?`, `+?`, `-?`, `*?`, `/?`|[Operatory dopuszczające wartość null](nullable-operators.md)|<ul><li>Równoważne z odpowiednimi operatorami bez sufiks, gdzie typ dopuszczający wartość null znajduje się po prawej stronie.<br /></li></ul>|
|`?>=?`, `?>?`, `?<=?`, `?<?`, `?=?`, `?<>?`, `?+?`, `?-?`, `?*?`, `?/?`|[Operatory dopuszczające wartość null](nullable-operators.md)|<ul><li>Równoważne z odpowiednimi operatorami bez otaczających znaków zapytania, gdy obie strony mają Typy dopuszczające wartość null.<br /></li></ul>|
|`@`|[Listy](../lists.md)<br /><br />[Ciągi](../strings.md)|<ul><li>Łączy dwie listy.<br /></li><li>Po umieszczeniu przed literałem ciągu wskazuje, że ciąg ma być interpretowany jako Verbatim, bez interpretacji znaków ucieczki.<br /></li></ul>|
|`[...]`|[Listy](../lists.md)|<ul><li>Ogranicza elementy listy.<br /></li></ul>|
|<code>[&#124;...&#124;]</code>|[Tablice](../arrays.md)|<ul><li>Ogranicza elementy tablicy.<br /></li></ul>|
|`[<...>]`|[Atrybuty](../attributes.md)|<ul><li>Ogranicza atrybut.<br /></li></ul>|
|`\`|[Ciągi](../strings.md)|<ul><li>Wyprowadza następny znak; używane w literałach znakowych i ciągów.<br /></li></ul>|
|`^`|[Statycznie rozwiązywane parametry typu](../generics/statically-resolved-type-parameters.md)<br /><br />[Ciągi](../strings.md)|<ul><li>Określa parametry typu, które muszą zostać rozwiązane w czasie kompilacji, a nie w czasie wykonywania.<br /></li><li>Łączy ciągi.<br /></li></ul>|
|`^^^`|[Operatory bitowe](bitwise-operators.md)|<ul><li>Oblicza bitową lub wyłączną operację.<br /></li></ul>|
|`_`|[Wyrażenia dopasowania](../match-expressions.md)<br /><br />[Typy ogólne](../generics/index.md)|<ul><li>Wskazuje wzorzec wieloznaczny.<br /></li><li>Określa anonimowy parametr ogólny.<br /></li></ul>|
|<code>&#96;</code>|[Automatyczna generalizacja](../generics/automatic-generalization.md)|<ul><li>Używane wewnętrznie do wskazania parametru typu ogólnego.<br /></li></ul>|
|`{...}`|[Sekwencje](../sequences.md)<br /><br />[Rekordy](../records.md)|<ul><li>Ogranicza wyrażenia sekwencji i wyrażenia obliczeń.<br /></li><li>Używane w definicjach rekordów.<br /></li></ul>|
|<code>&#124;</code>|[Wyrażenia dopasowania](../match-expressions.md)|<ul><li>Ogranicza poszczególne przypadki dopasowania, indywidualne przypadki Unii rozłącznych i wartości wyliczane.<br /></li></ul>|
|<code>&#124;&#124;</code>|[Operatory logiczne](boolean-operators.md)|<ul><li>Oblicza wartość logiczną lub operację.<br /></li></ul>|
|<code>&#124;&#124;&#124;</code>|[Operatory bitowe](bitwise-operators.md)|<ul><li>Oblicza wartość bitową lub operację.<br /></li></ul>|
|`~~`|[Przeciążanie operatora](../operator-overloading.md)|<ul><li>Używane do deklarowania przeciążenia dla jednoargumentowego operatora negacji.<br /></li></ul>|
|`~~~`|[Operatory bitowe](bitwise-operators.md)|<ul><li>Oblicza wartość bitową bez operacji.<br /></li></ul>|
|`~-`|[Przeciążanie operatora](../operator-overloading.md)|<ul><li>Używane do deklarowania przeciążenia dla jednoargumentowego operatora minus.<br /></li></ul>|
|`~+`|[Przeciążanie operatora](../operator-overloading.md)|<ul><li>Używane do deklarowania przeciążenia dla jednoargumentowego operatora Plus.<br /></li></ul>|

## <a name="operator-precedence"></a>Kolejność wykonywania działań

W poniższej tabeli przedstawiono kolejność pierwszeństwa operatorów i innych słów kluczowych wyrażeń w języku F #, w kolejności od najniższego pierwszeństwa do najwyższego pierwszeństwa. Na liście znajduje się również łączność, jeśli ma zastosowanie.

|Operator|Łączność|
|--------|-------------|
|`as`|Prawe|
|`when`|Prawe|
|<code>&#124;</code> wodzie|Lewe|
|`;`|Prawe|
|`let`|Niekojarzenie|
|`function`, `fun`, `match`, `try`|Niekojarzenie|
|`if`|Niekojarzenie|
|`not`|Prawe|
|`->`|Prawe|
|`:=`|Prawe|
|`,`|Niekojarzenie|
|`or`, <code>&#124;&#124;</code>|Lewe|
|`&`, `&&`|Lewe|
|`:>`, `:?>`|Prawe|
|`<`*op*, `>` *op*, `=` , <code>&#124;</code> *op*, `&` *op*,`&`<br /><br />(w tym,, `<<<` `>>>` <code>&#124;&#124;&#124;</code> , `&&&` )|Lewe|
|`^`*op*<br /><br />(w tym `^^^` )|Prawe|
|`::`|Prawe|
|`:?`|Bez skojarzenia|
|`-`*op*, `+` *op*|Dotyczy wrostkowe używanych przez te symbole|
|`*`*op*, `/` *op*, `%` *op*|Lewe|
|`**`*op*|Prawe|
|`f x` (aplikacja funkcji)|Lewe|
|<code>&#124;</code> (dopasowanie wzorca)|Prawe|
|Operatory prefiksu ( `+` *op*, `-` *op*, `%` ,,,, `%%` `&` `&&` `!` *op*, `~` *op*)|Lewe|
|`.`|Lewe|
|`f(x)`|Lewe|
|`f<`*Typ*`>`|Lewe|

Język F # obsługuje Przeciążenie operatora niestandardowego. Oznacza to, że można zdefiniować własne operatory. W poprzedniej tabeli, *op* może być dowolną prawidłową (prawdopodobnie pustą) sekwencją znaków operatora, wbudowanym lub zdefiniowanym przez użytkownika. W związku z tym można użyć tej tabeli, aby określić sekwencję znaków, która ma być używana dla operatora niestandardowego do osiągnięcia żądanego poziomu pierwszeństwa. Znaki wiodące `.` są ignorowane, gdy kompilator określi pierwszeństwo.

## <a name="see-also"></a>Zobacz też

- [Dokumentacja języka F #](../index.md)
- [Przeciążanie operatora](../operator-overloading.md)
