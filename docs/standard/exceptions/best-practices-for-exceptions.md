---
title: Najlepsze rozwiązania dotyczące wyjątków — .NET
description: Poznaj najlepsze rozwiązania dotyczące wyjątków, takich jak korzystanie z try/catch/finally, obsługa typowych warunków bez wyjątków i używanie wstępnie zdefiniowanych typów wyjątków platformy .NET.
ms.date: 12/05/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- exceptions, best practices
ms.assetid: f06da765-235b-427a-bfb6-47cd219af539
ms.openlocfilehash: 90dda00acd32852b032fc383580c5f34022ec9b4
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/05/2020
ms.locfileid: "84447098"
---
# <a name="best-practices-for-exceptions"></a>Najlepsze rozwiązania dotyczące wyjątków

Dobrze zaprojektowana aplikacja obsługuje wyjątki i błędy, aby zapobiegać awariom aplikacji. W tej sekcji opisano najlepsze rozwiązania dotyczące obsługi i tworzenia wyjątków.

## <a name="use-trycatchfinally-blocks-to-recover-from-errors-or-release-resources"></a>Użyj bloków try/catch/finally do odzyskania po błędach lub zwolnienia zasobów

Używaj `try` / `catch` bloków otaczających kod, który może potencjalnie generować wyjątek ***, a*** kod można odzyskać z tego wyjątku. W `catch` blokach zawsze Porządkuj wyjątki od najbardziej pochodnych do najmniej pochodnych. Wszystkie wyjątki pochodzą od <xref:System.Exception> . Bardziej pochodne wyjątki nie są obsługiwane przez klauzulę catch, która poprzedza klauzulę catch dla bazowej klasy wyjątków. Jeśli kod nie może odzyskać z wyjątku, nie należy przechwytywać tego wyjątku. Włącz metody, aby zwiększyć stos wywołań, jeśli jest to możliwe.

Wyczyść zasoby przyłączone do obu `using` instrukcji lub `finally` bloków. Preferuj `using` instrukcje automatycznego czyszczenia zasobów po zgłoszeniu wyjątków. Użyj `finally` bloków, aby wyczyścić zasoby, które nie implementują <xref:System.IDisposable> . Kod w `finally` klauzuli jest prawie zawsze wykonywany nawet wtedy, gdy są zgłaszane wyjątki.

## <a name="handle-common-conditions-without-throwing-exceptions"></a>Obsługa typowych warunków bez zgłaszania wyjątków

W przypadku warunków, które mogą wystąpić, ale mogą wyzwolić wyjątek, należy rozważyć obsługę ich w taki sposób, aby uniknąć tego wyjątku. Na przykład jeśli spróbujesz zamknąć połączenie, które zostało już zamknięte, uzyskasz `InvalidOperationException` . Można uniknąć użycia `if` instrukcji w celu sprawdzenia stanu połączenia przed próbą zamknięcia.

[!code-cpp[Conceptual.Exception.Handling#2](~/samples/snippets/cpp/VS_Snippets_CLR/conceptual.exception.handling/cpp/source.cpp#2)]
[!code-csharp[Conceptual.Exception.Handling#2](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.exception.handling/cs/source.cs#2)]
[!code-vb[Conceptual.Exception.Handling#2](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.exception.handling/vb/source.vb#2)]

Jeśli nie sprawdzasz stanu połączenia przed zamknięciem, możesz wychwycić `InvalidOperationException` wyjątek.

[!code-cpp[Conceptual.Exception.Handling#3](~/samples/snippets/cpp/VS_Snippets_CLR/conceptual.exception.handling/cpp/source.cpp#3)]
[!code-csharp[Conceptual.Exception.Handling#3](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.exception.handling/cs/source.cs#3)]
[!code-vb[Conceptual.Exception.Handling#3](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.exception.handling/vb/source.vb#3)]

Metoda do wyboru zależy od częstotliwości wystąpienia zdarzenia.

- Obsługi wyjątków należy używać, jeśli zdarzenie nie występuje zbyt często, a więc jeśli zdarzenie jest naprawdę wyjątkowe i wskazuje błąd, taki jak nieoczekiwany koniec pliku. Użycie obsługi wyjątków powoduje, że mniej kodu jest wykonywanego w normalnych warunkach.

- Sprawdź, czy w kodzie wystąpią błędy, jeśli zdarzenie jest wykonywane rutynowo i może być uważane za część normalnego wykonania. Po sprawdzeniu typowych warunków błędu jest wykonywany mniej kodu, ponieważ unikasz wyjątków.

## <a name="design-classes-so-that-exceptions-can-be-avoided"></a>Klasy projektowania umożliwiające uniknięcie wyjątków

Klasa może udostępniać metody lub właściwości, które umożliwiają uniknięcie wywołania, które wywoła wyjątek. Na przykład <xref:System.IO.FileStream> Klasa zawiera metody, które ułatwiają określenie, czy osiągnięto koniec pliku. Można ich użyć, aby uniknąć zgłoszonego wyjątku w przypadku odczytu poza końcem pliku. Poniższy przykład pokazuje, jak odczytać na końcu pliku bez wyzwalania wyjątku.

[!code-cpp[Conceptual.Exception.Handling#5](~/samples/snippets/cpp/VS_Snippets_CLR/conceptual.exception.handling/cpp/source.cpp#5)]
[!code-csharp[Conceptual.Exception.Handling#5](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.exception.handling/cs/source.cs#5)]
[!code-vb[Conceptual.Exception.Handling#5](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.exception.handling/vb/source.vb#5)]

Inny sposób, aby uniknąć wyjątków, ma zwrócić wartość null (lub wartość domyślną) dla skrajnie typowych przypadków błędów zamiast zgłaszać wyjątek. Ekstremalnie częste przypadki błędów należy traktować jako normalny przepływ sterowania. Zwracając wartość null (lub domyślną) w takich przypadkach można zminimalizować wpływ na wydajność aplikacji.

W przypadku typów wartości, niezależnie `Nullable<T>` od tego, czy jako wskaźnik błędu mają być brane pod uwagę w przypadku konkretnej aplikacji. Przy użyciu `Nullable<Guid>` , `default` otrzymuje `null` zamiast `Guid.Empty` . Czasami dodanie `Nullable<T>` może sprawiać, że jest to wyraźniejsze, gdy wartość jest obecna lub nieobecna. Czasami dodanie `Nullable<T>` może spowodować utworzenie dodatkowych przypadków do sprawdzenia, że nie jest to konieczne, i służy tylko do tworzenia potencjalnych źródeł błędów.

## <a name="throw-exceptions-instead-of-returning-an-error-code"></a>Zgłoś wyjątki zamiast zwracać kod błędu

Wyjątki zapewniają, że niepowodzenia nie są niezauważalne, ponieważ wywołanie kodu nie sprawdza kodu powrotu.

## <a name="use-the-predefined-net-exception-types"></a>Użyj wstępnie zdefiniowanych typów wyjątków platformy .NET

Wprowadź nową klasę wyjątku tylko wtedy, gdy wstępnie zdefiniowany element nie ma zastosowania. Przykład:

- Zgłoś <xref:System.InvalidOperationException> wyjątek, jeśli zestaw właściwości lub wywołanie metody nie jest odpowiedni dla bieżącego stanu obiektu.

- Zgłoś <xref:System.ArgumentException> wyjątek lub jedną ze wstępnie zdefiniowanych klas, które pochodzą z, <xref:System.ArgumentException> Jeśli są spełnione nieprawidłowe parametry.

## <a name="end-exception-class-names-with-the-word-exception"></a>Koniec nazw klas wyjątków z słowem`Exception`

Gdy niestandardowa jest konieczna, nadaj jej odpowiednią nazwę i utwórz ją z <xref:System.Exception> klasy. Przykład:

[!code-cpp[Conceptual.Exception.Handling#4](~/samples/snippets/cpp/VS_Snippets_CLR/conceptual.exception.handling/cpp/source.cpp#4)]
[!code-csharp[Conceptual.Exception.Handling#4](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.exception.handling/cs/source.cs#4)]
[!code-vb[Conceptual.Exception.Handling#4](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.exception.handling/vb/source.vb#4)]

## <a name="include-three-constructors-in-custom-exception-classes"></a>Dołącz trzy konstruktory do klas wyjątków niestandardowych

Podczas tworzenia własnych klas wyjątków należy używać co najmniej trzech typowych konstruktorów: Konstruktor bez parametrów, Konstruktor, który pobiera komunikat ciągu, oraz Konstruktor, który pobiera komunikat ciągu i wewnętrzny wyjątek.

- <xref:System.Exception.%23ctor>, który używa wartości domyślnych.

- <xref:System.Exception.%23ctor%28System.String%29>, który akceptuje komunikat ciągu.

- <xref:System.Exception.%23ctor%28System.String%2CSystem.Exception%29>, który akceptuje komunikat ciągu i wewnętrzny wyjątek.

Aby zapoznać się z przykładem, zobacz [How to: Create User-Defined Exceptions](how-to-create-user-defined-exceptions.md).

## <a name="ensure-that-exception-data-is-available-when-code-executes-remotely"></a>Upewnij się, że dane wyjątków są dostępne, gdy kod jest wykonywany zdalnie

Podczas tworzenia wyjątków zdefiniowanych przez użytkownika upewnij się, że metadane dla tych wyjątków są dostępne dla kodu, który jest wykonywany zdalnie.

Na przykład w przypadku implementacji platformy .NET obsługujących domeny aplikacji mogą wystąpić wyjątki między domenami aplikacji. Załóżmy, że domena aplikacji A tworzy domenę aplikacji B, która wykonuje kod, który zgłasza wyjątek. W przypadku domeny aplikacji A, aby prawidłowo przechwycić i obsłużyć wyjątek, musi być w stanie znaleźć zestaw zawierający wyjątek zgłoszony przez domenę aplikacji B. Jeśli domena aplikacji B zgłosi wyjątek, który jest zawarty w zestawie w jego bazie aplikacji, ale nie pod bazą aplikacji domeny aplikacji A, domena aplikacji A nie będzie mogła znaleźć wyjątku, a środowisko uruchomieniowe języka wspólnego zgłosi <xref:System.IO.FileNotFoundException> wyjątek. Aby uniknąć tej sytuacji, można na dwa sposoby wdrożyć zestaw zawierający informacje o wyjątku:

- Umieszczając zestaw we wspólnej podstawie aplikacji współużytkowanej przez obie domeny aplikacji.

    \-oraz

- Jeśli domeny nie współużytkują podstawy aplikacji, można podpisać zestaw zawierający informacje o wyjątku, używając silnej nazwy, i wdrożyć ten zestaw w globalnej pamięci podręcznej zestawów.

## <a name="use-grammatically-correct-error-messages"></a>Używaj komunikatów o błędach z prawidłowymi gramatykami

Napisz jasne zdania i Dołącz kończące znaki interpunkcyjne. Każde zdanie w ciągu przypisanym do <xref:System.Exception.Message?displayProperty=nameWithType> Właściwości powinno kończyć się kropką. Na przykład "tabela dziennika ma przepełnienie". być prawidłowym ciągiem komunikatów.

## <a name="include-a-localized-string-message-in-every-exception"></a>Dołącz zlokalizowany komunikat ciągu w każdym wyjątku

Komunikat o błędzie, który użytkownik widzi, pochodzi od <xref:System.Exception.Message?displayProperty=nameWithType> Właściwości zgłoszonego wyjątku, a nie z nazwy klasy wyjątku. Zwykle przypisujesz wartość do <xref:System.Exception.Message?displayProperty=nameWithType> Właściwości przez przekazanie ciągu komunikatu do `message` argumentu [konstruktora wyjątków](xref:System.Exception.%23ctor%2A).

W przypadku zlokalizowanych aplikacji należy podać zlokalizowany ciąg komunikatu dla każdego wyjątku, który aplikacja może zgłosić. Pliki zasobów są używane do udostępniania zlokalizowanych komunikatów o błędach. Aby uzyskać informacje na temat lokalizowania aplikacji i pobierania zlokalizowanych ciągów, zobacz następujące artykuły:

- [Instrukcje: tworzenie wyjątków zdefiniowanych przez użytkownika z zastosowaniem zlokalizowanych komunikatów o wyjątkach](how-to-create-localized-exception-messages.md)
- [Zasoby w aplikacjach klasycznych](../../framework/resources/index.md)
- <xref:System.Resources.ResourceManager?displayProperty=nameWithType>

## <a name="in-custom-exceptions-provide-additional-properties-as-needed"></a>W niestandardowych wyjątkach podaj dodatkowe właściwości zgodnie z wymaganiami

Podaj dodatkowe właściwości wyjątku (oprócz niestandardowego ciągu wiadomości) tylko wtedy, gdy istnieje scenariusz programistyczny, w którym dodatkowe informacje są użyteczne. Na przykład <xref:System.IO.FileNotFoundException> zawiera <xref:System.IO.FileNotFoundException.FileName> Właściwość.

## <a name="place-throw-statements-so-that-the-stack-trace-will-be-helpful"></a>Umieść instrukcje throw, aby ułatwić śledzenie stosu

Ślad stosu rozpoczyna się w instrukcji, w której wyjątek jest zgłaszany i kończąc na `catch` instrukcji, która przechwytuje wyjątek.

## <a name="use-exception-builder-methods"></a>Korzystanie z metod konstruktora wyjątków

Klasy często zgłaszają takie same wyjątki z różnych miejsc w swojej implementacji. Aby uniknąć nadmiernej ilości kodu, należy używać metod pomocników, które tworzą wyjątki i je zwracają. Przykład:

[!code-cpp[Conceptual.Exception.Handling#6](~/samples/snippets/cpp/VS_Snippets_CLR/conceptual.exception.handling/cpp/source.cpp#6)]
[!code-csharp[Conceptual.Exception.Handling#6](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.exception.handling/cs/source.cs#6)]
[!code-vb[Conceptual.Exception.Handling#6](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.exception.handling/vb/source.vb#6)]

W niektórych przypadkach bardziej odpowiednie jest użycie konstruktora wyjątku do skompilowania wyjątku. Przykładem jest globalna Klasa wyjątków, taka jak <xref:System.ArgumentException> .

## <a name="restore-state-when-methods-dont-complete-due-to-exceptions"></a>Przywróć stan, gdy nie ukończono metod z powodu wyjątków

Obiekty wywołujące powinny być w stanie założyć, że nie występują efekty uboczne, gdy wyjątek jest zgłaszany przez metodę. Na przykład jeśli masz kod, który transferuje pieniądze przez wycofanie z jednego konta i zdeponowanie na innym koncie, a podczas wykonywania depozytu zostanie zgłoszony wyjątek, nie chcesz, aby wycofanie zadziałało.

```csharp
public void TransferFunds(Account from, Account to, decimal amount)
{
    from.Withdrawal(amount);
    // If the deposit fails, the withdrawal shouldn't remain in effect.
    to.Deposit(amount);
}
```

```vb
Public Sub TransferFunds(from As Account, [to] As Account, amount As Decimal)
    from.Withdrawal(amount)
    ' If the deposit fails, the withdrawal shouldn't remain in effect.
    [to].Deposit(amount)
End Sub
```

Powyższa metoda nie generuje bezpośrednio żadnych wyjątków, ale musi być pisemnie zapisywana, aby w przypadku niepowodzenia operacji depozytu wycofanie zostało cofnięte.

Jednym ze sposobów obsługi tej sytuacji jest przechwycenie wszelkich wyjątków zgłoszonych przez transakcję przelewu i wycofanie wycofania.

```csharp
private static void TransferFunds(Account from, Account to, decimal amount)
{
    string withdrawalTrxID = from.Withdrawal(amount);
    try
    {
        to.Deposit(amount);
    }
    catch
    {
        from.RollbackTransaction(withdrawalTrxID);
        throw;
    }
}
```

```vb
Private Shared Sub TransferFunds(from As Account, [to] As Account, amount As Decimal)
    Dim withdrawalTrxID As String = from.Withdrawal(amount)
    Try
        [to].Deposit(amount)
    Catch
        from.RollbackTransaction(withdrawalTrxID)
        Throw
    End Try
End Sub
```

Ten przykład ilustruje użycie programu `throw` w celu ponownego wygenerowania oryginalnego wyjątku, co może ułatwić wywoływanie, aby poznać rzeczywistą przyczynę problemu bez konieczności badania <xref:System.Exception.InnerException> właściwości. Alternatywą jest zgłoszenie nowego wyjątku i uwzględnienie pierwotnego wyjątku jako wyjątku wewnętrznego:

```csharp
catch (Exception ex)
{
    from.RollbackTransaction(withdrawalTrxID);
    throw new TransferFundsException("Withdrawal failed.", innerException: ex)
    {
        From = from,
        To = to,
        Amount = amount
    };
}
```

```vb
Catch ex As Exception
    from.RollbackTransaction(withdrawalTrxID)
    Throw New TransferFundsException("Withdrawal failed.", innerException:=ex) With
    {
        .From = from,
        .[To] = [to],
        .Amount = amount
    }
End Try
```

## <a name="see-also"></a>Zobacz także

- [Wyjątki](index.md)
