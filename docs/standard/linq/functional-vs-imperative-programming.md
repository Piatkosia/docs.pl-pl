---
title: Programowanie funkcjonalne a bezwzględne programowanie — LINQ to XML
description: Poznaj programowanie funkcjonalne i różnice między tradycyjnymi, niezależnymi (proceduralnymi) programowaniem.
ms.date: 07/20/2015
ms.assetid: 5e35c5a0-c949-422a-873b-fca6b2254f57
ms.openlocfilehash: c7d16d61f9865cda7c625f91c2c822be1a327fd6
ms.sourcegitcommit: aa6d8a90a4f5d8fe0f6e967980b8c98433f05a44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2020
ms.locfileid: "90679369"
---
# <a name="functional-programming-vs-imperative-programming-linq-to-xml"></a><span data-ttu-id="aa3a7-103">Programowanie funkcjonalne a programowanie bezwzględne (LINQ to XML)</span><span class="sxs-lookup"><span data-stu-id="aa3a7-103">Functional programming vs. imperative programming (LINQ to XML)</span></span>

<span data-ttu-id="aa3a7-104">W tym artykule porównano i różnią się programowanie funkcjonalne z bardziej tradycyjnym, niewzględnym (proceduralnym) programowaniem.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-104">This article compares and contrasts functional programming with more traditional imperative (procedural) programming.</span></span>

## <a name="functional-programming-vs-imperative-programming"></a><span data-ttu-id="aa3a7-105">Programowanie funkcjonalne a programowanie imperatywne</span><span class="sxs-lookup"><span data-stu-id="aa3a7-105">Functional programming vs. imperative programming</span></span>

<span data-ttu-id="aa3a7-106">Model *programowania funkcjonalnego* został jawnie utworzony w celu obsługi czystego podejścia funkcjonalnego do rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-106">The *functional programming* paradigm was explicitly created to support a pure functional approach to problem solving.</span></span> <span data-ttu-id="aa3a7-107">Programowanie funkcjonalne jest formą *programowania deklaratywnego*.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-107">Functional programming is a form of *declarative programming*.</span></span> <span data-ttu-id="aa3a7-108">W przeciwieństwie do najpopularniejszych języków, w tym języków programowania zorientowanego obiektowo (OOP), takich jak C#, Visual Basic, C++ i Java, zostały zaprojektowane głównie *do obsługi* bezwzględnego (proceduralnego) programowania.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-108">In contrast, most mainstream languages, including object-oriented programming (OOP) languages such as C#, Visual Basic, C++, and Java, were designed to primarily support *imperative* (procedural) programming.</span></span>

<span data-ttu-id="aa3a7-109">W przypadku niezależnego podejścia deweloper zapisuje kod, który określa czynności, które musi wykonać komputer, aby osiągnąć cel.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-109">With an imperative approach, a developer writes code that specifies the steps that the computer must take to accomplish the goal.</span></span> <span data-ttu-id="aa3a7-110">Jest to czasami określane jako programowanie *algorytmów* .</span><span class="sxs-lookup"><span data-stu-id="aa3a7-110">This is sometimes referred to as *algorithmic* programming.</span></span> <span data-ttu-id="aa3a7-111">Z kolei podejście funkcjonalne obejmuje tworzenie problemów jako zestaw funkcji do wykonania.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-111">In contrast, a functional approach involves composing the problem as a set of functions to be executed.</span></span> <span data-ttu-id="aa3a7-112">Należy dokładnie zdefiniować dane wejściowe dla każdej funkcji i co zwraca każda funkcja.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-112">You define carefully the input to each function, and what each function returns.</span></span> <span data-ttu-id="aa3a7-113">W poniższej tabeli opisano niektóre ogólne różnice między tymi dwoma podejściami.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-113">The following table describes some of the general differences between these two approaches.</span></span>

|<span data-ttu-id="aa3a7-114">Charakterystyka</span><span class="sxs-lookup"><span data-stu-id="aa3a7-114">Characteristic</span></span>|<span data-ttu-id="aa3a7-115">Bezwzględne podejście</span><span class="sxs-lookup"><span data-stu-id="aa3a7-115">Imperative approach</span></span>|<span data-ttu-id="aa3a7-116">Podejście funkcjonalne</span><span class="sxs-lookup"><span data-stu-id="aa3a7-116">Functional approach</span></span>|
|--------------------|-------------------------|-------------------------|
|<span data-ttu-id="aa3a7-117">Fokus programisty</span><span class="sxs-lookup"><span data-stu-id="aa3a7-117">Programmer focus</span></span>|<span data-ttu-id="aa3a7-118">Jak wykonywać zadania (algorytmy) i jak śledzić zmiany w stanie.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-118">How to perform tasks (algorithms) and how to track changes in state.</span></span>|<span data-ttu-id="aa3a7-119">Jakie informacje są potrzebne i jakie przekształcenia są wymagane.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-119">What information is desired and what transformations are required.</span></span>|
|<span data-ttu-id="aa3a7-120">Zmiany stanu</span><span class="sxs-lookup"><span data-stu-id="aa3a7-120">State changes</span></span>|<span data-ttu-id="aa3a7-121">Ważne.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-121">Important.</span></span>|<span data-ttu-id="aa3a7-122">Nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-122">Non-existent.</span></span>|
|<span data-ttu-id="aa3a7-123">Kolejność wykonywania</span><span class="sxs-lookup"><span data-stu-id="aa3a7-123">Order of execution</span></span>|<span data-ttu-id="aa3a7-124">Ważne.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-124">Important.</span></span>|<span data-ttu-id="aa3a7-125">Niska ważność.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-125">Low importance.</span></span>|
|<span data-ttu-id="aa3a7-126">Podstawowe sterowanie przepływem</span><span class="sxs-lookup"><span data-stu-id="aa3a7-126">Primary flow control</span></span>|<span data-ttu-id="aa3a7-127">Pętle, warunkowe i wywołania funkcji (Metoda).</span><span class="sxs-lookup"><span data-stu-id="aa3a7-127">Loops, conditionals, and function (method) calls.</span></span>|<span data-ttu-id="aa3a7-128">Wywołania funkcji, w tym rekursja.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-128">Function calls, including recursion.</span></span>|
|<span data-ttu-id="aa3a7-129">Podstawowa jednostka manipulowania</span><span class="sxs-lookup"><span data-stu-id="aa3a7-129">Primary manipulation unit</span></span>|<span data-ttu-id="aa3a7-130">Wystąpienia struktur lub klas.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-130">Instances of structures or classes.</span></span>|<span data-ttu-id="aa3a7-131">Działa jako obiekty pierwszej klasy i kolekcje danych.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-131">Functions as first-class objects and data collections.</span></span>|

<span data-ttu-id="aa3a7-132">Chociaż większość języków została zaprojektowana do obsługi określonego modelu programowania, wiele języków ogólnych jest wystarczająco elastycznych, aby obsługiwało wiele odmian.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-132">Although most languages were designed to support a specific programming paradigm, many general languages are flexible enough to support multiple paradigms.</span></span> <span data-ttu-id="aa3a7-133">Na przykład większość języków zawierających wskaźniki funkcji może służyć do credibly programowania funkcjonalnego.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-133">For example, most languages that contain function pointers can be used to credibly support functional programming.</span></span> <span data-ttu-id="aa3a7-134">Ponadto Języki C# i Visual Basic zawierają jawne rozszerzenia językowe do obsługi programowania funkcjonalnego, w tym wyrażenia lambda i wnioskowania o typie.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-134">Furthermore, C# and Visual Basic include explicit language extensions to support functional programming, including lambda expressions and type inference.</span></span> <span data-ttu-id="aa3a7-135">Technologia LINQ jest formą deklaracyjnego programowania funkcjonalnego.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-135">LINQ technology is a form of declarative, functional programming.</span></span>

## <a name="functional-programming-using-xslt"></a><span data-ttu-id="aa3a7-136">Programowanie funkcjonalne przy użyciu XSLT</span><span class="sxs-lookup"><span data-stu-id="aa3a7-136">Functional programming using XSLT</span></span>

<span data-ttu-id="aa3a7-137">Wielu deweloperów XSLT potrafi poznać czyste podejście funkcjonalne.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-137">Many XSLT developers are familiar with the pure functional approach.</span></span> <span data-ttu-id="aa3a7-138">Najbardziej efektywnym sposobem na Tworzenie arkusza stylów XSLT jest traktowanie każdego szablonu jako odizolowanego, możliwego do redagowania transformacji.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-138">The most effective way to develop an XSLT style sheet is to treat each template as an isolated, composable transformation.</span></span> <span data-ttu-id="aa3a7-139">Kolejność wykonywania jest całkowicie niewyróżniona.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-139">The order of execution is completely de-emphasized.</span></span> <span data-ttu-id="aa3a7-140">XSLT nie zezwala na efekty uboczne (z wyjątkiem tego, że mechanizmy ucieczki do wykonywania kodu proceduralnego mogą wprowadzać efekty uboczne, które powodują, że nie są one czyste).</span><span class="sxs-lookup"><span data-stu-id="aa3a7-140">XSLT doesn't allow side effects (with the exception that escaping mechanisms for executing procedural code can introduce side effects that result in functional impurity).</span></span> <span data-ttu-id="aa3a7-141">Chociaż język XSLT jest skutecznym narzędziem, niektóre jego właściwości nie są optymalne.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-141">However, although XSLT is an effective tool, some of its characteristics aren't optimal.</span></span> <span data-ttu-id="aa3a7-142">Na przykład, konstrukcje programistyczne w języku XML czynią kod stosunkowo pełny i dlatego trudno jest zachować.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-142">For example, expressing programming constructs in XML makes code relatively verbose, and therefore difficult to maintain.</span></span> <span data-ttu-id="aa3a7-143">Ponadto duże zależności dotyczące rekursji dla sterowania przepływem mogą spowodować, że kod trudno odczytać.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-143">Also, the heavy reliance on recursion for flow control can result in code that's hard to read.</span></span> <span data-ttu-id="aa3a7-144">Aby uzyskać więcej informacji na temat XSLT, zobacz [XSLT Transformations](../data/xml/xslt-transformations.md).</span><span class="sxs-lookup"><span data-stu-id="aa3a7-144">For more information about XSLT, see [XSLT Transformations](../data/xml/xslt-transformations.md).</span></span>

<span data-ttu-id="aa3a7-145">Jednak język XSLT udowadniał wartość użycia czystego podejścia funkcjonalnego do przekształcenia XML z jednego kształtu do drugiego.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-145">However, XSLT has proved the value of using a pure functional approach for transforming XML from one shape to another.</span></span> <span data-ttu-id="aa3a7-146">Czyste programowanie funkcjonalne przy użyciu LINQ to XML jest podobne do języka XSLT na wiele sposobów.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-146">Pure functional programming with LINQ to XML is similar in many ways to XSLT.</span></span> <span data-ttu-id="aa3a7-147">Jednak konstrukcje programistyczne wprowadzone przez LINQ to XML, C# i Visual Basic umożliwiają pisanie czystych transformacji funkcjonalnych, które są bardziej czytelne i konserwowane niż XSLT.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-147">However, the programming constructs introduced by LINQ to XML, C#, and Visual Basic allow you to write pure functional transformations that are more readable and maintainable than XSLT.</span></span>

## <a name="advantages-of-pure-functions"></a><span data-ttu-id="aa3a7-148">Zalety czystych funkcji</span><span class="sxs-lookup"><span data-stu-id="aa3a7-148">Advantages of pure functions</span></span>

<span data-ttu-id="aa3a7-149">Podstawową przyczyną wdrożenia przekształceń funkcjonalnych jako czystych funkcji jest możliwość tworzenia czystych funkcji: to jest, samodzielne i bezstanowe.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-149">The primary reason to implement functional transformations as pure functions is that pure functions are composable: that is, self-contained and stateless.</span></span> <span data-ttu-id="aa3a7-150">Te cechy obejmują szereg korzyści, w tym następujące:</span><span class="sxs-lookup"><span data-stu-id="aa3a7-150">These characteristics bring a number of benefits, including the following:</span></span>

- <span data-ttu-id="aa3a7-151">Zwiększ czytelność i łatwość utrzymania.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-151">Increased readability and maintainability.</span></span> <span data-ttu-id="aa3a7-152">Jest to spowodowane tym, że każda funkcja została zaprojektowana w celu wykonania określonego zadania z uwzględnieniem argumentów.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-152">This is because each function is designed to accomplish a specific task given its arguments.</span></span> <span data-ttu-id="aa3a7-153">Funkcja nie polega na żadnym stanie zewnętrznym.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-153">The function doesn't rely on any external state.</span></span>
- <span data-ttu-id="aa3a7-154">Łatwiejsza zmiana na rozwój.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-154">Easier reiterative development.</span></span> <span data-ttu-id="aa3a7-155">Ponieważ kod jest łatwiejszy do refaktoryzacji, zmiany w projekcie są często łatwiejsze do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-155">Because the code is easier to refactor, changes to design are often easier to implement.</span></span> <span data-ttu-id="aa3a7-156">Załóżmy na przykład, że napiszesz skomplikowaną transformację, a następnie dowiesz się, że jakiś kod jest powtórzony kilka razy w transformacji.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-156">For example, suppose you write a complicated transformation, and then realize that some code is repeated several times in the transformation.</span></span> <span data-ttu-id="aa3a7-157">Jeśli refaktoryzacja jest przeprowadzana za pomocą czystej metody, można wywołać czystą metodę w stanie bez obaw o skutki uboczne.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-157">If you refactor through a pure method, you can call your pure method at will without worrying about side effects.</span></span>
- <span data-ttu-id="aa3a7-158">Łatwiejsze testowanie i debugowanie.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-158">Easier testing and debugging.</span></span> <span data-ttu-id="aa3a7-159">Ze względu na to, że czyste funkcje mogą być łatwiejsze do przetestowania w izolacji, można napisać kod testu, który wywołuje czystą funkcję z typowymi wartościami, prawidłowymi przypadkami krawędzi i nieprawidłowymi przypadkami krawędzi.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-159">Because pure functions can more easily be tested in isolation, you can write test code that calls the pure function with typical values, valid edge cases, and invalid edge cases.</span></span>

## <a name="transitioning-for-oop-developers"></a><span data-ttu-id="aa3a7-160">Przechodzenie dla deweloperów OOP</span><span class="sxs-lookup"><span data-stu-id="aa3a7-160">Transitioning for OOP developers</span></span>

<span data-ttu-id="aa3a7-161">W tradycyjnych programowaniu zorientowanym obiektom (OOP) większość deweloperów jest przyzwyczajona do programowania w stylu bezwzględnym/proceduralnym.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-161">In traditional object-oriented programming (OOP), most developers are accustomed to programming in the imperative/procedural style.</span></span> <span data-ttu-id="aa3a7-162">Aby przełączać się do programowania w czystym stylu funkcjonalnym, muszą one wprowadzać przejście w myśli i ich podejście do rozwoju.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-162">To switch to developing in a pure functional style, they have to make a transition in their thinking and their approach to development.</span></span>

<span data-ttu-id="aa3a7-163">Aby rozwiązać problemy, OOP programiści mogą projektować hierarchie klas, skupić się na poprawnym hermetyzacji i myśleć o kategoriach umów.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-163">To solve problems, OOP developers design class hierarchies, focus on proper encapsulation, and think in terms of class contracts.</span></span> <span data-ttu-id="aa3a7-164">Zachowanie i stan typów obiektów to najważniejsze, a funkcje językowe, takie jak klasy, interfejsy, dziedziczenie i polimorfizm, są dostarczane w celu rozwiązania tych problemów.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-164">The behavior and state of object types are paramount, and language features, such as classes, interfaces, inheritance, and polymorphism, are provided to address these concerns.</span></span>

<span data-ttu-id="aa3a7-165">W przeciwieństwie do programowania funkcjonalnego podejścia do problemów obliczeniowych jako ćwiczenia w ocenie czystych, funkcjonalnych transformacji kolekcji danych.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-165">In contrast, functional programming approaches computational problems as an exercise in the evaluation of pure functional transformations of data collections.</span></span> <span data-ttu-id="aa3a7-166">Programowanie funkcjonalne pozwala uniknąć stanu i modyfikowalnych danych, a zamiast tego kładzie nacisk na aplikacje funkcji.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-166">Functional programming avoids state and mutable data, and instead emphasizes the application of functions.</span></span>

<span data-ttu-id="aa3a7-167">Na szczęście język C# i Visual Basic nie wymagają pełnego przestępności do programowania funkcjonalnego, ponieważ obsługują zarówno metody programowania zasadniczego, jak i funkcjonalnego.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-167">Fortunately, C# and Visual Basic don't require the full leap to functional programming, because they support both imperative and functional programming approaches.</span></span> <span data-ttu-id="aa3a7-168">Deweloper może wybrać, które podejście jest najbardziej odpowiednie dla konkretnego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-168">A developer can choose which approach is most appropriate for a particular scenario.</span></span> <span data-ttu-id="aa3a7-169">W rzeczywistości programy często łączą oba podejścia.</span><span class="sxs-lookup"><span data-stu-id="aa3a7-169">In fact, programs often combine both approaches.</span></span>

## <a name="see-also"></a><span data-ttu-id="aa3a7-170">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="aa3a7-170">See also</span></span>

- [<span data-ttu-id="aa3a7-171">Wprowadzenie do czystych przekształceń funkcjonalnych</span><span class="sxs-lookup"><span data-stu-id="aa3a7-171">Introduction to pure functional transformations</span></span>](introduction-pure-functional-transformations.md)
- [<span data-ttu-id="aa3a7-172">Przekształcenia XSLT</span><span class="sxs-lookup"><span data-stu-id="aa3a7-172">XSLT Transformations</span></span>](/../../standard/data/xml/xslt-transformations.md)
- [<span data-ttu-id="aa3a7-173">Refaktoryzacja do czystych funkcji</span><span class="sxs-lookup"><span data-stu-id="aa3a7-173">Refactor into pure functions</span></span>](refactor-pure-functions.md)