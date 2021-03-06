---
ms.openlocfilehash: daf09748e69e70ad982bcee14461b66579f3bb87
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614861"
---
### <a name="avoiding-endless-recursion-for-iworkflowinstancemanagementtransactedcancel-and-iworkflowinstancemanagementtransactedterminate"></a>Unikanie rekursji nieskończoności dla IWorkflowInstanceManagement. TransactedCancel i IWorkflowInstanceManagement. TransactedTerminate

#### <a name="details"></a>Szczegóły

W pewnych okolicznościach przy użyciu <xref:System.ServiceModel.Activities.IWorkflowInstanceManagement.TransactedCancel%2A?displayProperty=nameWithType> lub <xref:System.ServiceModel.Activities.IWorkflowInstanceManagement.TransactedTerminate%2A?displayProperty=nameWithType> interfejsów API do anulowania lub kończenia wystąpienia usługi worklow wystąpienie przepływu pracy może napotkać przepełnienie stosu z powodu nieskończonej rekursji, gdy `Workflow` środowisko uruchomieniowe próbuje utrzymać wystąpienie usługi w ramach przetwarzania żądania. Ten problem występuje, gdy wystąpienie przepływu pracy jest w stanie, w którym oczekuje na ukończenie innego oczekującego żądania WCF do innej usługi. `TransactedCancel`Operacje i `TransactedTerminate` tworzą elementy robocze, które są umieszczane w kolejce dla wystąpienia usługi przepływu pracy. Te elementy robocze nie są wykonywane w ramach przetwarzania `TransactedCancel/TransactedTerminate` żądania. Ponieważ wystąpienie usługi przepływu pracy jest zajęte, czekając na zakończenie innych oczekujących żądań WCF, element roboczy został utworzony w kolejce. `TransactedCancel/TransactedTerminate`Operacja zostanie ukończona i kontrola zostanie zwrócona z powrotem do klienta. Gdy transakcja skojarzona z `TransactedCancel/TransactedTerminate` operacją próbuje się zatwierdzić, musi zachować stan wystąpienia Service przepływu pracy. Ale ponieważ istnieje oczekujące `WCF` żądanie wystąpienia, środowisko uruchomieniowe przepływu pracy nie może utrwalać wystąpienia usługi przepływu pracy, a pętla rekursji nieskończonej prowadzi do przepełnienia stosu. Ponieważ `TransactedCancel` i `TransactedTerminate` Utwórz tylko element roboczy w pamięci, fakt, że transakcja istnieje, nie ma żadnego efektu. Wycofanie transakcji nie odrzuci elementu pracy. Aby rozwiązać ten problem, w .NET Framework 4.7.2 został wprowadzony, `AppSetting` który można dodać do `web.config/app.config` usługi przepływu pracy, która informuje go o ignorowaniu transakcji dla `TransactedCancel` i `TransactedTerminate` . Pozwala to na zatwierdzenie transakcji bez oczekiwania na utrwalenie wystąpienia przepływu pracy. Element appSetting dla tej funkcji ma nazwę `microsoft:WorkflowServices:IgnoreTransactionsForTransactedCancelAndTransactedTerminate` . Wartość wskazuje, `true` że transakcja powinna być ignorowana, co pozwala uniknąć przepełnienia stosu. Wartość domyślna tego element appSetting to `false` , więc nie ma to żadnego oddziaływać na istniejące wystąpienia usługi przepływu pracy.

#### <a name="suggestion"></a>Sugestia

Jeśli używasz programu AppFabric lub innego <xref:System.ServiceModel.Activities.IWorkflowInstanceManagement> klienta i napotykasz przepełnienie stosu w wystąpieniu przepływu pracy Service podczas próby anulowania lub zakończenia wystąpienia przepływu pracy, możesz dodać następujący element do `<appSettings>` sekcji pliku web.config/app.config dla usługi przepływu pracy:

<pre><code class="lang-xml">&lt;add key=&quot;microsoft:WorkflowServices:IgnoreTransactionsForTransactedCancelAndTransactedTerminate&quot; value=&quot;true&quot;/&gt;&#13;&#10;</code></pre>

Jeśli problem nie wystąpi, nie musisz tego robić.

| Nazwa    | Wartość       |
|:--------|:------------|
| Zakres   | Brzeg        |
| Wersja | 4.7.2       |
| Typ    | Przekierowanie |
