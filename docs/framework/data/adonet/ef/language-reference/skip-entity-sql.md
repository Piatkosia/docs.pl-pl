---
title: Pomiń (Entity SQL)
ms.date: 03/30/2017
ms.assetid: e2139412-8ea4-451b-8f10-91af18dfa3ec
ms.openlocfilehash: 68f54dc5118e09d78f98c687e8a44def43b45c7d
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90540995"
---
# <a name="skip-entity-sql"></a>Pomiń (Entity SQL)

Stronicowanie fizyczne można wykonać za pomocą podklauzuli SKIP w klauzuli ORDER BY. Pomiń nie można użyć niezależnie od klauzuli ORDER BY.

## <a name="syntax"></a>Składnia

```sql
[ SKIP n ]
```

## <a name="arguments"></a>Argumenty

`n` \
Liczba elementów do pominięcia.

## <a name="remarks"></a>Uwagi

Jeśli Podklauzula SKIP Expression jest obecna w klauzuli ORDER BY, wyniki zostaną posortowane zgodnie z specyfikacją sortowania, a zestaw wyników będzie zawierał wiersze zaczynające się od następnego wiersza bezpośrednio po wyrażeniu SKIP. Na przykład Pomiń 5 spowoduje pominięcie pierwszych pięciu wierszy i zwrócenie od szóstego wiersza do przodu.

> [!NOTE]
> [!INCLUDE[esql](../../../../../../includes/esql-md.md)]Zapytanie jest nieprawidłowe, jeśli w tym samym wyrażeniu zapytania znajduje się zarówno modyfikator Top, jak i podklauzulę Skip. Zapytanie powinno zostać napisaną przez zmianę wyrażenia TOP na wyrażenie limitu.

> [!NOTE]
> W SQL Server 2000 użycie polecenia Pomiń z KOLEJNOŚCIą według kolumn niebędących kluczami może spowodować zwrócenie niepoprawnych wyników. Jeśli kolumna niebędąca kluczem zawiera zduplikowane dane, może zostać pominięta więcej niż określona liczba wierszy. Wynika to z tego, jak POMIJAnie jest tłumaczone dla SQL Server 2000. Na przykład, w poniższym kodzie może zostać pominięte więcej niż pięć wierszy, jeśli `E.NonKeyColumn` ma zduplikowane wartości:
>
> ```sql
> SELECT [E] FROM Container.EntitySet AS [E] ORDER BY [E].[NonKeyColumn] DESC SKIP 5L
> ```

[!INCLUDE[esql](../../../../../../includes/esql-md.md)]Zapytanie w [instrukcje: Strona z wynikami zapytania](/previous-versions/dotnet/netframework-4.0/bb738702(v=vs.100)) używa operatora order by z opcją Skip, aby określić kolejność sortowania używaną dla obiektów zwracanych w instrukcji SELECT.

## <a name="see-also"></a>Zobacz także

- [ORDER BY](order-by-entity-sql.md)
- [Instrukcje: Strona za poorednictwem wyników zapytania](/previous-versions/dotnet/netframework-4.0/bb738702(v=vs.100))
- [Stronicowanie](paging-entity-sql.md)
- [Do góry](top-entity-sql.md)
