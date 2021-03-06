---
title: lock — Instrukcja (odwołanie w C#)
description: Używanie instrukcji blokowania języka C# do synchronizowania dostępu do wątku z udostępnionym zasobem
ms.date: 04/02/2020
f1_keywords:
- lock_CSharpKeyword
- lock
helpviewer_keywords:
- lock keyword [C#]
ms.assetid: 656da1a4-707e-4ef6-9c6e-6d13b646af42
ms.openlocfilehash: 6e9a6975977588ba7692c925d7940cd2ec26671f
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2020
ms.locfileid: "84406693"
---
# <a name="lock-statement-c-reference"></a>lock — Instrukcja (odwołanie w C#)

`lock`Instrukcja uzyskuje blokadę wykluczania wzajemnego dla danego obiektu, wykonuje blok instrukcji, a następnie zwalnia blokadę. Gdy blokada jest utrzymywana, wątek, który przechowuje blokadę, może ponownie uzyskać i zwolnić blokadę. Każdy inny wątek jest blokowany przed uzyskaniem blokady i czeka na zwolnienie blokady.

`lock`Instrukcja ma postać

```csharp
lock (x)
{
    // Your code...
}
```

gdzie `x` jest wyrażeniem [typu odwołania](reference-types.md). Jest to dokładnie równoważne

```csharp
object __lockObj = x;
bool __lockWasTaken = false;
try
{
    System.Threading.Monitor.Enter(__lockObj, ref __lockWasTaken);
    // Your code...
}
finally
{
    if (__lockWasTaken) System.Threading.Monitor.Exit(__lockObj);
}
```

Ponieważ kod używa [try... blok finally](try-finally.md) jest uwalniany nawet wtedy, gdy wyjątek jest zgłaszany w treści `lock` instrukcji.

Nie można użyć [operatora await](../operators/await.md) w treści `lock` instrukcji.

## <a name="guidelines"></a>Wytyczne

Podczas synchronizowania dostępu do wątku z udostępnionym zasobem należy zablokować wystąpienie obiektu dedykowanego (na przykład `private readonly object balanceLock = new object();` ) lub inne wystąpienie, które prawdopodobnie nie będzie używane jako obiekt blokady przez niepowiązane części kodu. Należy unikać używania tego samego wystąpienia obiektu blokady dla różnych udostępnionych zasobów, ponieważ może to spowodować zakleszczenie lub zablokowanie rywalizacji. W szczególności należy unikać używania następujących funkcji jako obiektów blokowania:

- `this`, ponieważ mogą one być używane przez wywołujących jako blokadę.
- <xref:System.Type>wystąpienia, ponieważ mogą być uzyskane przez operatora lub odbicie [typeof](../operators/type-testing-and-cast.md#typeof-operator) .
- wystąpienia ciągów, w tym literały ciągów, ponieważ mogą być [internice](/dotnet/api/system.string.intern#remarks).

Przytrzymaj blokadę przez krótki czas, jak to możliwe, aby zmniejszyć rywalizację o blokady.

## <a name="example"></a>Przykład

W poniższym przykładzie zdefiniowano `Account` klasę, która synchronizuje dostęp do jego `balance` pola prywatnego przez zablokowanie na dedykowanym `balanceLock` wystąpieniu. Użycie tego samego wystąpienia do blokowania gwarantuje, że `balance` nie można jednocześnie aktualizować pola przez dwa wątki próbujące wywołać `Debit` `Credit` metody lub.

[!code-csharp[lock-statement-example](snippets/LockStatementExample.cs)]

## <a name="c-language-specification"></a>specyfikacja języka C#

Aby uzyskać więcej informacji, zobacz sekcję [blokowanie instrukcji](~/_csharplang/spec/statements.md#the-lock-statement) w [specyfikacji języka C#](~/_csharplang/spec/introduction.md).

## <a name="see-also"></a>Zobacz też

- [Dokumentacja języka C#](../index.md)
- [Słowa kluczowe języka C#](index.md)
- <xref:System.Threading.Monitor?displayProperty=nameWithType>
- <xref:System.Threading.SpinLock?displayProperty=nameWithType>
- <xref:System.Threading.Interlocked?displayProperty=nameWithType>
- [Przegląd elementów podstawowych synchronizacji](../../../standard/threading/overview-of-synchronization-primitives.md)
