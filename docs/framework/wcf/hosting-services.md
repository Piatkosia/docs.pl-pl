---
title: Usługi hostingowe
description: Dowiedz się więcej na temat opcji hostingu usługi WCF. Usługa musi być hostowana w środowisku uruchomieniowym, które tworzy go i kontroluje jego kontekst i okres istnienia.
ms.date: 03/30/2017
helpviewer_keywords:
- hosting services [WCF]
ms.assetid: 192be927-6be2-4fda-98f0-e513c4881acc
ms.openlocfilehash: 86ce392bb76b22e2b6a65fa1d005ed8e9589af15
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/23/2020
ms.locfileid: "85246389"
---
# <a name="hosting-services"></a>Usługi hostingu

Aby stał się aktywny, usługa musi być hostowana w środowisku uruchomieniowym, które tworzy go i kontroluje jego kontekst i okres istnienia. Usługi Windows Communication Foundation (WCF) są przeznaczone do uruchamiania w dowolnym procesie systemu Windows, który obsługuje kod zarządzany.

Funkcja WCF oferuje ujednolicony model programowania do tworzenia aplikacji zorientowanych na usługę. Ten model programowania pozostaje spójny i jest niezależny od środowiska wykonawczego, w którym usługa jest wdrażana. W rzeczywistości oznacza to, że kod dla usług wygląda znacznie tak samo niezależnie od opcji hostingu.

Te opcje hostingu obejmują uruchamianie w ramach aplikacji konsolowej w środowiskach serwerowych, takich jak usługa systemu Windows działająca w procesie roboczym zarządzanym przez Internet Information Services (IIS) lub przez usługę aktywacji procesów systemu Windows (WAS). Deweloperzy wybierają środowisko hostingu spełniające wymagania dotyczące wdrażania usługi. Te wymagania mogą pochodzić od platformy, w której wdrażana jest aplikacja, transport, w którym musi wysyłać i odbierać komunikaty, lub w przypadku tego typu odtwarzania procesów i innych procesów zarządzania procesami wymaganymi w celu zapewnienia odpowiedniej dostępności lub innych wymagań związanych z zarządzaniem lub niezawodnością. W następnej sekcji znajdują się informacje i wskazówki dotyczące opcji hostingu.

## <a name="hosting-options"></a>Opcje hostingu

### <a name="self-host-in-a-managed-application"></a>Samodzielne hostowanie w aplikacji zarządzanej
 Usługi WCF mogą być hostowane w dowolnej zarządzanej aplikacji. Jest to najbardziej elastyczna opcja, ponieważ wymaga najmniejszej ilości infrastruktury do wdrożenia. Kod usługi można osadzić w kodzie aplikacji zarządzanej, a następnie utworzyć i otworzyć wystąpienie, <xref:System.ServiceModel.ServiceHost> Aby udostępnić usługę. Aby uzyskać więcej informacji, zobacz [jak: Hostowanie usługi WCF w zarządzanej aplikacji](how-to-host-a-wcf-service-in-a-managed-application.md).

 Ta opcja włącza dwa typowe scenariusze: usługi WCF działające w aplikacjach konsolowych i rozbudowane aplikacje klienckie, takie jak te oparte na Windows Presentation Foundation (WPF) lub Windows Forms (WinForms). Hosting usługi WCF w aplikacji konsolowej jest zwykle przydatny w fazie tworzenia aplikacji. Dzięki temu można łatwo debugować, łatwo uzyskać informacje o śledzeniu z usługi, aby dowiedzieć się, co się dzieje w aplikacji, i łatwo poruszać się, kopiując je do nowych lokalizacji. Ta opcja hostingu ułatwia również rozbudowane aplikacje klienckie, takie jak aplikacje WPF i WinForms, do komunikowania się ze światem zewnętrznym. Na przykład klient współpracy równorzędnej, który korzysta z platformy WPF dla interfejsu użytkownika, a także obsługuje usługę WCF, która umożliwia innym klientom łączenie się z działem IT i udostępnianie informacji.

### <a name="managed-windows-services"></a>Zarządzane usługi systemu Windows

Ta opcja hostingu polega na zarejestrowaniu domeny aplikacji (AppDomain), która hostuje usługę WCF jako usługę zarządzaną systemu Windows (wcześniej znaną jako usługa NT), aby okres istnienia usługi był kontrolowany przez menedżera kontroli usług (SCM) dla usług systemu Windows. Podobnie jak w przypadku opcji samoobsługowego, ten typ środowiska hostingu wymaga, aby część kodu hostingu była zapisywana jako część aplikacji. Usługa jest zaimplementowana jako usługa systemu Windows i jako usługa WCF, powodująca dziedziczenie z <xref:System.ServiceProcess.ServiceBase> klasy, a także z interfejsu kontraktu usługi WCF. <xref:System.ServiceModel.ServiceHost>Zostanie utworzony i otwarty w ramach zastąpionej <xref:System.ServiceProcess.ServiceBase.OnStart%28System.String%5B%5D%29> metody i zamknięty w ramach przesłoniętej <xref:System.ServiceProcess.ServiceBase.OnStop> metody. Należy również zaimplementować klasę Instalatora, która dziedziczy z programu, <xref:System.Configuration.Install.Installer> Aby umożliwić programowi zainstalowanie programu jako usługi systemu Windows za pomocą narzędzia Installutil.exe. Aby uzyskać więcej informacji, zobacz [jak: Hostowanie usługi WCF w usłudze zarządzanej systemu Windows](./feature-details/how-to-host-a-wcf-service-in-a-managed-windows-service.md). Scenariusz włączony przez opcję hostingu zarządzanej usługi systemu Windows polega na długotrwałej usłudze WCF hostowanej poza usługami IIS w bezpiecznym środowisku, które nie jest aktywowane przy użyciu komunikatów. Okres istnienia usługi jest kontrolowany przez system operacyjny. Ta opcja hostingu jest dostępna we wszystkich wersjach systemu Windows.

### <a name="internet-information-services-iis"></a>Internet Information Services (IIS)

Opcja hostingu usług IIS jest zintegrowana z usługą ASP.NET i używa funkcji oferowanych przez te technologie, takich jak odtwarzanie procesów, zamykanie bezczynności, monitorowanie kondycji procesu i Aktywacja oparta na komunikatach. W systemach operacyjnych Windows XP i Windows Server 2003 jest to preferowane rozwiązanie do hostowania aplikacji usługi sieci Web, które muszą być wysoce dostępne i wysoce skalowalne. Program IIS oferuje również zintegrowane możliwości zarządzania, których klienci oczekują od produktu serwerowego klasy korporacyjnej. Ta opcja hostingu wymaga poprawnego skonfigurowania usług IIS, ale nie wymaga, aby żaden kod hostingu był zapisywana jako część aplikacji. Aby uzyskać więcej informacji o sposobie konfigurowania hostingu usług IIS dla usługi WCF, zobacz [How to: hosting a WCF Service in IIS](./feature-details/how-to-host-a-wcf-service-in-iis.md).

 Usługi hostowane przez usługi IIS mogą korzystać tylko z transportu HTTP. W przypadku wdrożenia w usługach IIS 5,1 wprowadzono pewne ograniczenia w systemie Windows XP. W przypadku aktywacji opartej na komunikatach dla usługi WCF przez usługi IIS 5,1 w systemie Windows XP jest blokowana jakakolwiek inna usługa WCF hostowana na tym samym komputerze z użyciem portu 80 do komunikacji. Usługi WCF mogą działać w tym samym elemencie AppDomain/Pool aplikacji/procesie roboczym, co w przypadku innych aplikacji hostowanych przez usługi IIS 6,0 w systemie Windows Server 2003. Jednak ponieważ programy WCF i IIS 6,0 używają stosu HTTP w trybie jądra (HTTP.sys), usługi IIS 6,0 mogą współużytkować port 80 z innymi własnymi usługami WCF działającymi na tym samym komputerze, w przeciwieństwie do usług IIS 5,1.

### <a name="windows-process-activation-service-was"></a>Usługa aktywacji procesów systemu Windows (WAS)

Usługa aktywacji procesów systemu Windows (WAS) to nowy mechanizm aktywacji procesów dla systemu Windows Server 2008, który jest również dostępny w systemie Windows Vista. Zachowuje on znany model procesów usług IIS 6,0 (pule aplikacji i aktywacja procesów opartych na komunikatach) oraz funkcje hostingu (takie jak szybka ochrona przed awariami, monitorowanie kondycji i odtwarzanie), ale usuwa zależność od protokołu HTTP z architektury aktywacji. Program IIS 7,0 korzysta z aktywacji opartej na komunikatach za pośrednictwem protokołu HTTP. Dodatkowe składniki programu WCF również pozwalają zapewnić aktywację opartą na komunikatach przez inne protokoły obsługiwane przez WCF, takie jak TCP, MSMQ i nazwane potoki. Umożliwia to aplikacjom korzystającym z protokołów komunikacyjnych korzystanie z funkcji usług IIS, takich jak odtwarzanie procesów, ochrona przed seriami błędów i wspólny system konfiguracji, który był dostępny tylko dla aplikacji opartych na protokole HTTP.

 Ta opcja hostingu wymaga poprawnego skonfigurowania, ale nie wymaga pisania kodu hostingu jako części aplikacji. Aby uzyskać więcej informacji na temat sposobu konfigurowania usług, zobacz [jak: Hostowanie usługi WCF w usłudze was](./feature-details/how-to-host-a-wcf-service-in-was.md).

## <a name="choose-a-hosting-environment"></a>Wybierz środowisko hostingu
 Poniższa tabela zawiera podsumowanie najważniejszych zalet i scenariuszy związanych z poszczególnymi opcjami hostingu.

|Środowisko hostingu|Typowe scenariusze|Najważniejsze zalety i ograniczenia|
|-------------------------|----------------------|----------------------------------|
|Aplikacja zarządzana ("samodzielny")|-Aplikacje konsolowe używane podczas opracowywania.<br />— Bogate aplikacje klienckie WinForm i WPF, które uzyskują dostęp do usług.|Ruchom.<br />— Łatwa do wdrożenia.<br />— Nie rozwiązanie dla przedsiębiorstw dla usług.|
|Usługi systemu Windows (wcześniej znane jako usługi NT)|-Długotrwała usługa WCF hostowana poza usługami IIS.|— Okres istnienia procesu usługi kontrolowany przez system operacyjny, a nie aktywowany przy użyciu komunikatów.<br />— Obsługiwane przez wszystkie wersje systemu Windows.<br />— Bezpieczne środowisko.|
|IIS 5,1, IIS 6,0|— Uruchamianie usługi WCF obok zawartości ASP.NET w Internecie przy użyciu protokołu HTTP.|-Proces odtwarzania.<br />-Bezczynne zamknięcie.<br />-Proces monitorowania kondycji.<br />— Aktywacja oparta na komunikatach.<br />-Tylko HTTP.|
|Usługa aktywacji procesów systemu Windows (WAS)|— Uruchamianie usługi WCF bez instalowania usług IIS w Internecie przy użyciu różnych protokołów transportowych.|— Usługi IIS nie są wymagane.<br />-Proces odtwarzania.<br />-Bezczynne zamknięcie.<br />-Proces monitorowania kondycji.<br />— Aktywacja oparta na komunikatach.<br />-Działa z protokołami HTTP, TCP, nazwanymi potokami i usługą MSMQ.|
|IIS 7.0|— Uruchamianie usługi WCF z zawartością ASP.NET.<br />— Uruchamianie usługi WCF w Internecie przy użyciu różnych protokołów transportowych.|-Korzyści.<br />— Zintegrowane z ASP.NET i zawartością usług IIS.|

 Wybór środowiska hostingu zależy od wersji systemu Windows, w którym została wdrożona, transporty wymaganej do wysyłania komunikatów oraz typu procesu i domeny aplikacji, których wymaga. Poniższa tabela zawiera podsumowanie danych związanych z tymi wymaganiami.

|Środowisko hostingu|Dostępność platformy|Obsługiwane transporty|Proces i odtwarzanie elementu AppDomain|
|-------------------------|---------------------------|--------------------------|-------------------------------------|
|Zarządzane aplikacje ("samodzielne")|Windows XP, Windows Server 2003, Windows Vista,<br /><br /> Windows Server 2008|PROTOKOŁY<br /><br /> NET. TCP,<br /><br /> NET. pipe,<br /><br /> NET. MSMQ|Nie|
|Usługi systemu Windows (wcześniej znane jako usługi NT)|Windows XP, Windows Server 2003, Windows Vista,<br /><br /> Windows Server 2008|PROTOKOŁY<br /><br /> NET. TCP,<br /><br /> NET. pipe,<br /><br /> NET. MSMQ|Nie|
|USŁUGI IIS 5,1|Windows XP|HTTP|Tak|
|IIS 6,0|Windows Server 2003|HTTP|Tak|
|Usługa aktywacji procesów systemu Windows (WAS)|Windows Vista, Windows Server 2008|PROTOKOŁY<br /><br /> NET. TCP,<br /><br /> NET. pipe,<br /><br /> NET. MSMQ|Tak|

 Należy pamiętać, że uruchomienie usługi lub dowolnego rozszerzenia z niezaufanego hosta narusza zabezpieczenia. Ponadto podczas otwierania <xref:System.ServiceModel.ServiceHost> pod personifikacją aplikacja musi upewnić się, że użytkownik nie jest wylogowany, na przykład przez buforowanie <xref:System.Security.Principal.WindowsIdentity> użytkownika.

## <a name="see-also"></a>Zobacz też

- [Podstawowy cykl życia programowania](basic-programming-lifecycle.md)
- [Implementowanie kontraktów usług](implementing-service-contracts.md)
- [Instrukcje: hostowanie usługi WCF w programie IIS](./feature-details/how-to-host-a-wcf-service-in-iis.md)
- [Instrukcje: hostowanie usługi WCF w usłudze WAS](./feature-details/how-to-host-a-wcf-service-in-was.md)
- [Instrukcje: hostowanie usługi WCF w usłudze zarządzanej systemu Windows](./feature-details/how-to-host-a-wcf-service-in-a-managed-windows-service.md)
- [Instrukcje: hostowanie usługi WCF w zarządzanej aplikacji](how-to-host-a-wcf-service-in-a-managed-application.md)
