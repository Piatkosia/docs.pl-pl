---
title: Zabezpieczenia i sytuacja wyścigu
'description:': Describes pitfalls to avoid around security holes exploited by race conditions, including dispose methods, constructors, cached objects, and finalizers.
ms.date: 07/15/2020
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- security [.NET], race conditions
- race conditions
- secure coding, race conditions
- code security, race conditions
ms.assetid: ea3edb80-b2e8-4e85-bfed-311b20cb59b6
ms.openlocfilehash: a667bf69ba72cbe203bd2603c4c6b7a1e58a6d43
ms.sourcegitcommit: b7a8b09828bab4e90f66af8d495ecd7024c45042
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/04/2020
ms.locfileid: "87555113"
---
# <a name="security-and-race-conditions"></a>Zabezpieczenia i sytuacja wyścigu

Innym obszarem zainteresowania jest potencjalna liczba luk w zabezpieczeniach wykorzystywanych przez sytuacje wyścigu. Może się to zdarzyć na kilka sposobów. Tematy podrzędne, które przestrzegają konspektu, niektórych głównych pułapek, które muszą być unikane przez dewelopera.  
  
## <a name="race-conditions-in-the-dispose-method"></a>Warunki wyścigu w metodzie Dispose  

Jeśli metoda **Dispose** klasy (Aby uzyskać więcej informacji, zobacz [zbieranie elementów bezużytecznych](../garbage-collection/index.md)) nie jest zsynchronizowana, istnieje możliwość, że kod czyszczący wewnątrz elementu **Dispose** można uruchomić więcej niż jeden raz, jak pokazano w poniższym przykładzie.  
  
```vb  
Sub Dispose()  
    If Not (myObj Is Nothing) Then  
       Cleanup(myObj)  
       myObj = Nothing  
    End If  
End Sub  
```  
  
```csharp  
void Dispose()
{  
    if (myObj != null)
    {  
        Cleanup(myObj);  
        myObj = null;  
    }  
}  
```  
  
Ponieważ ta implementacja **usuwania** nie jest zsynchronizowana, można ją `Cleanup` wywołać przez pierwszy wątek, a następnie drugi wątek przed `_myObj` ustawieniem **wartość null**. To, czy jest to problem dotyczący zabezpieczeń, zależy od tego, co się dzieje, gdy `Cleanup` kod zostanie uruchomiony. Istotny problem z niezsynchronizowanymi implementacjami **Dispose** obejmuje użycie dojścia do zasobów, takich jak pliki. Niewłaściwe usunięcie może spowodować niewłaściwe użycie, które często prowadzi do luk w zabezpieczeniach.  
  
## <a name="race-conditions-in-constructors"></a>Warunki wyścigu w konstruktorach

W niektórych aplikacjach może być możliwe, aby inne wątki miały dostęp do elementów członkowskich klasy, zanim ich konstruktory klas zostały całkowicie uruchomione. Należy przejrzeć wszystkie konstruktory klas, aby upewnić się, że nie występują problemy z zabezpieczeniami, jeśli taka sytuacja powinna mieć miejsce lub zsynchronizować wątki w razie potrzeby.  
  
## <a name="race-conditions-with-cached-objects"></a>Warunki wyścigu z buforowanymi obiektami  

Kod, który buforuje informacje o zabezpieczeniach lub używa operacji [potwierdzenia](../../framework/misc/using-the-assert-method.md) zabezpieczeń dostępu kodu może być również narażony na sytuacje wyścigu, jeśli inne części klasy nie są odpowiednio zsynchronizowane, jak pokazano w poniższym przykładzie.  
  
```vb  
Sub SomeSecureFunction()  
    If SomeDemandPasses() Then  
        fCallersOk = True  
        DoOtherWork()  
        fCallersOk = False  
    End If  
End Sub  
  
Sub DoOtherWork()  
    If fCallersOK Then  
        DoSomethingTrusted()  
    Else  
        DemandSomething()  
        DoSomethingTrusted()  
    End If  
End Sub  
```  
  
```csharp  
void SomeSecureFunction()
{  
    if (SomeDemandPasses())
    {  
        fCallersOk = true;  
        DoOtherWork();  
        fCallersOk = false;  
    }  
}  
void DoOtherWork()
{  
    if (fCallersOK)
    {  
        DoSomethingTrusted();  
    }  
    else
    {  
        DemandSomething();  
        DoSomethingTrusted();  
    }  
}  
```  
  
Jeśli istnieją inne ścieżki do `DoOtherWork` , które mogą być wywoływane z innego wątku z tym samym obiektem, niezaufany obiekt wywołujący może przekroczyć żądanie.  
  
Jeśli kod buforuje informacje o zabezpieczeniach, należy zapoznać się z informacjami dotyczącymi tej luki w zabezpieczeniach.  
  
## <a name="race-conditions-in-finalizers"></a>Sytuacje wyścigu w finalizatorach  

Sytuacje wyścigu mogą również wystąpić w obiekcie, który odwołuje się do zasobu statycznego lub niezarządzanego, który następnie zwolni w jego finalizatorie. Jeśli wiele obiektów współużytkuje zasób, który jest manipulowany przez finalizator klasy, obiekty muszą zsynchronizować wszystkie dostęp do tego zasobu.  
  
## <a name="see-also"></a>Zobacz też

- [Wytyczne dotyczące bezpiecznego programowania](secure-coding-guidelines.md)
- [Zabezpieczenia ASP.NET Core](/aspnet/core/security/)
