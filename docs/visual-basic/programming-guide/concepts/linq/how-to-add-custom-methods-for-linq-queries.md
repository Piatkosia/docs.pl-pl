---
title: 'Instrukcje: dodawanie metod niestandardowych dla zapytań LINQ'
ms.date: 08/28/2020
ms.assetid: 099b2e2a-83cd-45c6-aa4d-01b398b5faaf
ms.openlocfilehash: 7d38a45263135fa10dc53dc0d09b8129838e78e6
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/30/2020
ms.locfileid: "89117782"
---
# <a name="how-to-add-custom-methods-for-linq-queries-visual-basic"></a>Instrukcje: dodawanie metod niestandardowych dla zapytań LINQ (Visual Basic)

Rozszerzasz zestaw metod używanych przez zapytania LINQ przez dodawanie metod rozszerzających do <xref:System.Collections.Generic.IEnumerable%601> interfejsu. Na przykład oprócz standardowej średniej lub maksymalnej operacji można utworzyć niestandardową metodę agregującą w celu obliczenia pojedynczej wartości z sekwencji wartości. Należy również utworzyć metodę, która działa jako filtr niestandardowy lub określona transformacja danych dla sekwencji wartości i zwraca nową sekwencję. Przykładami takich metod są <xref:System.Linq.Enumerable.Distinct%2A> , <xref:System.Linq.Enumerable.Skip%2A> , i <xref:System.Linq.Enumerable.Reverse%2A> .

Rozszerzając <xref:System.Collections.Generic.IEnumerable%601> interfejs, można zastosować niestandardowe metody do dowolnej wyliczalnej kolekcji. Aby uzyskać więcej informacji, zobacz [metody rozszerzenia](../../language-features/procedures/extension-methods.md).

## <a name="adding-an-aggregate-method"></a>Dodawanie metody agregującej

Metoda agregująca oblicza pojedynczą wartość z zestawu wartości. LINQ zawiera kilka metod agregujących, w tym <xref:System.Linq.Enumerable.Average%2A> , <xref:System.Linq.Enumerable.Min%2A> i <xref:System.Linq.Enumerable.Max%2A> . Można utworzyć własną metodę agregującą, dodając metodę rozszerzenia do <xref:System.Collections.Generic.IEnumerable%601> interfejsu.

Poniższy przykład kodu pokazuje, jak utworzyć metodę rozszerzenia wywołana, `Median` Aby obliczyć medianę dla sekwencji liczb typu `double` .

:::code language="vb" source="./snippets/LinqExtension.vb" :::

Ta metoda rozszerzenia jest wywoływana dla każdej wyliczalnej kolekcji w taki sam sposób, w jaki wywołujemy inne metody agregacji z <xref:System.Collections.Generic.IEnumerable%601> interfejsu.

> [!NOTE]
> W Visual Basic można użyć wywołania metody lub standardowej składni zapytania dla `Aggregate` `Group By` klauzuli OR. Aby uzyskać więcej informacji, zobacz [klauzula agregująca](../../../language-reference/queries/aggregate-clause.md) i [klauzula GROUP by](../../../language-reference/queries/group-by-clause.md).

Poniższy przykład kodu pokazuje, jak używać `Median` metody dla tablicy typu `double` .

:::code language="vb" source="./snippets/Program.vb" ID="MedianUsage":::

### <a name="overloading-an-aggregate-method-to-accept-various-types"></a>Przeciążanie metody agregującej w celu zaakceptowania różnych typów

Można przeciążyć metodę agregacji, aby akceptować sekwencje różnych typów. Standardowe podejście polega na utworzeniu przeciążenia dla każdego typu. Innym rozwiązaniem jest utworzenie przeciążenia, które będzie miało typ ogólny i przekonwertować go na określony typ za pomocą delegata. Można również połączyć oba podejścia.

#### <a name="to-create-an-overload-for-each-type"></a>Aby utworzyć Przeciążenie dla każdego typu

Można utworzyć określone Przeciążenie dla każdego typu, który ma być obsługiwany. Poniższy przykład kodu przedstawia Przeciążenie `Median` metody dla `integer` typu.

:::code language="vb" source="./snippets/OtherExtensions.vb" ID="IntOverload":::

Teraz można wywoływać `Median` przeciążenia dla obu `integer` typów i `double` typy, jak pokazano w poniższym kodzie:

:::code language="vb" source="./snippets/Program.vb" ID="OverloadUsage":::

#### <a name="to-create-a-generic-overload"></a>Aby utworzyć Przeciążenie ogólne

Można również utworzyć Przeciążenie, które akceptuje sekwencję obiektów ogólnych. To przeciążenie przyjmuje delegat jako parametr i używa go do konwersji sekwencji obiektów typu ogólnego do określonego typu.

Poniższy kod przedstawia Przeciążenie `Median` metody, która przyjmuje <xref:System.Func%602> Delegat jako parametr. Ten delegat pobiera obiekt typu ogólnego `T` i zwraca obiekt typu `double` .

:::code language="vb" source="./snippets/OtherExtensions.vb" ID="GenericOverload":::

Teraz można wywołać `Median` metodę dla sekwencji obiektów dowolnego typu. Jeśli typ nie ma własnego przeciążenia metody, należy przekazać parametr delegata. W Visual Basic można użyć wyrażenia lambda do tego celu. Ponadto, jeśli używasz `Aggregate` `Group By` klauzuli or zamiast wywołania metody, można przekazać dowolną wartość lub wyrażenie, które znajduje się w zakresie tej klauzuli.

Poniższy przykładowy kod pokazuje, jak wywołać `Median` metodę dla tablicy liczb całkowitych i tablicy ciągów. Dla ciągów, mediany dla długości ciągów w tablicy jest obliczany. W przykładzie pokazano, jak przekazać <xref:System.Func%602> parametr delegata do `Median` metody dla każdego przypadku.

:::code language="vb" source="./snippets/Program.vb" ID="GenericUsage":::

## <a name="adding-a-method-that-returns-a-collection"></a>Dodawanie metody zwracającej kolekcję

Interfejs można rozszerzyć <xref:System.Collections.Generic.IEnumerable%601> za pomocą niestandardowej metody zapytania, która zwraca sekwencję wartości. W tym przypadku metoda musi zwracać kolekcję typu <xref:System.Collections.Generic.IEnumerable%601> . Takie metody mogą służyć do zastosowania filtrów lub transformacji danych do sekwencji wartości.

Poniższy przykład pokazuje, jak utworzyć metodę rozszerzenia o nazwie `AlternateElements` , która zwraca każdy inny element w kolekcji, rozpoczynając od pierwszego elementu.

:::code language="vb" source="./snippets/OtherExtensions.vb" ID="SequenceElement":::

Można wywołać tę metodę rozszerzenia dla każdej wyliczalnej kolekcji tak samo jak w przypadku wywołania innych metod z <xref:System.Collections.Generic.IEnumerable%601> interfejsu, jak pokazano w poniższym kodzie:

:::code language="vb" source="./snippets/Program.vb" ID="SequenceUsage":::

## <a name="see-also"></a>Zobacz też

- <xref:System.Collections.Generic.IEnumerable%601>
- [Metody rozszerzania](../../language-features/procedures/extension-methods.md)
