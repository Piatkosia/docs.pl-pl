---
title: Instalowanie usługi kolejkowania komunikatów (MSMQ)
description: Dowiedz się, jak zainstalować usługę kolejkowania komunikatów 4,0 i kolejkowanie komunikatów 3,0 do użycia z przykładami WFC w ramach procedury jednorazowej konfiguracji.
ms.date: 03/30/2017
ms.assetid: 7ddcd497-3e04-427e-bc04-3610ad98b01e
ms.openlocfilehash: 0d0cb87b40b1cb11eb7692c2fa1e890ec815b13d
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/23/2020
ms.locfileid: "85244468"
---
# <a name="installing-message-queuing-msmq"></a>Instalowanie usługi kolejkowania komunikatów (MSMQ)
W poniższych procedurach pokazano, jak zainstalować usługę kolejkowania komunikatów 4,0 i kolejkowanie komunikatów 3,0.  
  
> [!NOTE]
> Usługa kolejkowania komunikatów 4,0 nie jest dostępna w systemach Windows XP i Windows Server 2003.  
  
#### <a name="to-install-message-queuing-40-on-windows-server-2008-or-windows-server-2008-r2"></a>Aby zainstalować usługę kolejkowania komunikatów 4,0 w systemie Windows Server 2008 lub Windows Server 2008 R2  
  
1. W Menedżer serwera kliknij pozycję **funkcje**.  
  
2. W okienku po prawej stronie w obszarze **Podsumowanie funkcji**kliknij pozycję **Dodaj funkcje**.  
  
3. W oknie wyników rozwiń węzeł **kolejkowanie komunikatów**.  
  
4. Rozwiń węzeł **usługi kolejkowania komunikatów**.  
  
5. Kliknij pozycję **Integracja usług katalogowych** (w przypadku komputerów przyłączonych do domeny), a następnie kliknij pozycję **Obsługa protokołu HTTP**.  
  
6. Kliknij przycisk **dalej**, a następnie kliknij przycisk **Instaluj**.  
  
#### <a name="to-install-message-queuing-40-on-windows-7-or-windows-vista"></a>Aby zainstalować usługę kolejkowania komunikatów 4,0 w systemie Windows 7 lub Windows Vista  
  
1. Otwórz **Panel sterowania**.  
  
2. Kliknij pozycję **programy** , a następnie w obszarze **programy i funkcje**kliknij pozycję **Włącz lub wyłącz funkcje systemu Windows**.  
  
3. Rozwiń węzeł serwer usługi Microsoft Message Queue (MSMQ), rozwiń węzeł serwer usługi kolejkowania komunikatów (MSMQ) firmy Microsoft, a następnie zaznacz pola wyboru dla następujących funkcji usługi kolejkowania komunikatów, które mają zostać zainstalowane:  
  
    - Integracja z usługą MSMQ Active Directory Domain Services (dla komputerów przyłączonych do domeny).  
  
    - Obsługa protokołu HTTP w usłudze MSMQ.  
  
4. Kliknij przycisk **OK**.  
  
5. Jeśli zostanie wyświetlony monit o ponowne uruchomienie komputera, kliknij przycisk **OK** , aby zakończyć instalację.  
  
#### <a name="to-install-message-queuing-30-on-windows-xp-and-windows-server-2003"></a>Aby zainstalować usługę kolejkowania komunikatów 3,0 w systemach Windows XP i Windows Server 2003  
  
1. Otwórz **Panel sterowania**.  
  
2. Kliknij przycisk **Dodaj Usuń programy** , a następnie kliknij przycisk **Dodaj składniki systemu Windows**.  
  
3. Wybierz pozycję Kolejkowanie komunikatów i kliknij pozycję **szczegóły**.  
  
    > [!NOTE]
    > W przypadku korzystania z systemu Windows Server 2003 wybierz opcję serwer aplikacji, aby uzyskać dostęp do usługi kolejkowania komunikatów.  
  
4. Upewnij się, że opcja obsługa protokołu HTTP usługi MSMQ została wybrana na stronie szczegółów.  
  
5. Kliknij przycisk **OK** , aby zamknąć stronę szczegóły, a następnie kliknij przycisk **dalej**. Ukończ instalację.  
  
6. Jeśli zostanie wyświetlony monit o ponowne uruchomienie komputera, kliknij przycisk **OK** , aby zakończyć instalację.  
  
## <a name="see-also"></a>Zobacz też

- [Instrukcje dotyczące konfiguracji](set-up-instructions.md)
