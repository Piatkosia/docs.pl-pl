---
title: Procedura konfiguracji jednorazowej dla przykładów Windows Communication Foundation
ms.date: 03/30/2017
ms.assetid: a5848ffd-3eb5-432d-812e-bd948ccb6bca
ms.openlocfilehash: bf25ea4734bad007fa3ac19df0664932d981519c
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90548120"
---
# <a name="one-time-setup-procedure-for-the-windows-communication-foundation-samples"></a>Procedura konfiguracji jednorazowej dla przykładów Windows Communication Foundation

Większość przykładów Windows Communication Foundation (WCF) znajduje się w Internet Information Services (IIS) i uruchamiana ze wspólnego katalogu wirtualnego. Ta procedura konfiguracji jednorazowej tworzy folder na dysku; dodaje również katalog wirtualny do usług IIS o nazwie **servicemodelsamples**.

Katalog wirtualny **servicemodelsamples** służy do kompilowania i uruchamiania wszystkich przykładów korzystających z usługi hostowanej przez usługi IIS. Jest to jedyny katalog wirtualny, który jest wymagany do uruchomienia przykładów. Utworzenie przykładu spowoduje zastąpienie wszystkich wcześniej wdrożonych usług w tym katalogu wirtualnym; tylko ostatnio skompilowany przykład zostanie wdrożony i będzie dostępny w tym katalogu wirtualnym.

> [!NOTE]
> Należy uruchomić wszystkie polecenia w ramach konta administratora lokalnego. W przypadku korzystania z systemu Windows 7, Windows Vista lub Windows Server 2008 R2 należy również uruchomić wiersz polecenia z podwyższonym poziomem uprawnień. Aby to zrobić, kliknij prawym przyciskiem myszy ikonę wiersza polecenia, a następnie kliknij polecenie **Uruchom jako administrator**. Wszystkie polecenia w tym temacie muszą być uruchamiane w wierszu polecenia, który ma odpowiednie ustawienia ścieżki.  Najprostszym sposobem upewnienia się, że jest to przy użyciu wiersza polecenia programu Visual Studio. Aby otworzyć ten monit, kliknij przycisk **Start**, wybierz pozycję **Wszystkie programy**, przewiń w dół do **programu Visual Studio 2010**, wybierz pozycję **Visual Studio Tools**, kliknij prawym przyciskiem myszy pozycję **wiersz polecenia programu Visual Studio (2010)**, a następnie kliknij polecenie **Uruchom jako administrator**. Jeśli masz zainstalowaną jedną z następujących wersji Visual Studio Express, ten wiersz polecenia nie jest dostępny i trzeba będzie dodać "C:\Windows\Microsoft.Net\Framework\v4.0" do ścieżki systemowej.

### <a name="one-time-setup-procedure-for-wcf-samples"></a>Procedura konfiguracji jednorazowej dla przykładów WCF

1. Upewnij się, że ASP.NET został skonfigurowany. Aby uzyskać więcej informacji na temat sposobu konfigurowania usługi ASP.NET, zobacz [instrukcje hostingu internetowych usług informacyjnych](internet-information-service-hosting-instructions.md).

2. Upewnij się, że zainstalowano .NET Framework 4. Wyszukaj w następującym katalogu dla wersji v 4.0 (lub nowszej): **\Windows\Microsoft.NET\Framework**

3. Upewnij się, że masz zainstalowany program Visual Studio 2012 lub nowszy, albo system operacyjny to Windows Server 2008 z dodatkiem SP2 lub nowszym.

4. Uruchom następujące polecenia. Aby uzyskać więcej informacji na temat tego, dlaczego te polecenia muszą być uruchamiane, zobacz [usługa hostowana usług IIS kończy się niepowodzeniem](/previous-versions/dotnet/netframework-3.5/ms752252(v=vs.90)).

    > [!WARNING]
    > Po ponownym zainstalowaniu usług IIS należy ponownie uruchomić następujące polecenia.

    ```console
    "%WINDIR%\Microsoft.Net\Framework\v4.0.30319\aspnet_regiis" –i –enable
    "%WINDIR%\Microsoft.Net\Framework\v4.0.30319\ServiceModelReg.exe" -r
    ```

    > [!WARNING]
    > Uruchomienie polecenia `aspnet_regiis –i –enable` spowoduje, że domyślna pula aplikacji zostanie uruchomiona przy użyciu .NET Framework 4, co może spowodować problemy ze zgodnością dla innych aplikacji na tym samym komputerze.

5. Postępuj zgodnie z [instrukcjami zapory](firewall-instructions.md) dotyczącymi włączania portów używanych przez przykłady.

6. Sprawdź następujący katalog domyślny: \<InstallDrive> :**\ WF_WCF_Samples**. Jeśli wcześniej zainstalowano przykłady, jest to katalog domyślny.

7. Jeśli przykłady nie są zainstalowane, zainstaluj je z [przykładów Windows Communication Foundation (WCF) i Windows Workflow Foundation (WF) dla .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459).

8. Po zainstalowaniu przykładów przejdź do: \<InstallDrive> :**\ WF_WCF_Samples \wcf\setup \\ **

9. Uruchom plik wsadowy **Setupvroot.bat** . Wykonywane są następujące czynności:

    - Katalog wirtualny jest tworzony w usługach IIS o nazwie ServiceModelSamples.

    - Nowe katalogi dysku są tworzone o nazwie%SystemDrive%\Inetpub\wwwroot\ServiceModelSamples i%SystemDrive%\Inetpub\wwwroot\ServiceModelSamples\bin.

    Jeśli wolisz ręcznie skonfigurować te katalogi, zobacz [instrukcje dotyczące instalacji katalogu wirtualnego](virtual-directory-setup-instructions.md). Aby cofnąć wszystkie zmiany wprowadzone w tym kroku, uruchom cleanupvroot.bat po zakończeniu korzystania z przykładów.

    > [!NOTE]
    > Tę procedurę należy wykonać tylko raz na komputerze, chyba że cleanupvroot.bat jest uruchomiona.

10. Musisz przyznać uprawnienia do modyfikowania%SystemDrive%\inetpub\wwwroot na koncie, w ramach którego tworzysz przykłady i użytkownika usługi sieciowej. Podczas kompilowania niektóre przykłady hostowane w sieci Web mogą próbować skopiować skompilowane pliki binarne do wcześniej wymienionej lokalizacji, a jeśli nie ustawisz odpowiednich uprawnień, kompilacja zostanie przerwana. Alternatywnie można pozostawić odpowiednie uprawnienia, a następnie uruchomić wiersz polecenia zestawu SDK lub wiersz polecenia programu Visual Studio (2012) jako administrator lub skompilować przykłady w programie Visual Studio 2012, również uruchomić jako administrator.

    > [!NOTE]
    > Jeśli ten krok nie zostanie ukończony, wszystkie przykłady hostowane przez usługi IIS zakończą się niepowodzeniem podczas kompilowania. Upewnij się, że uprawnienia zostały prawidłowo ustawione, lub Uruchom wiersz polecenia zestawu SDK i wiersz polecenia programu Visual Studio (2012) jako administrator.

11. Utwórz katalog C:\LOGS na komputerze; Niektóre przykłady mogą oczekiwać. Upewnij się, że odpowiednie konto ma przyznany dostęp do zapisu dla tego folderu. W przypadku systemów Windows 7, Windows Vista i Windows Server 2008 R2 to konto jest **usługą sieciową**. W przypadku systemu Windows Server 2008 konto to NT Authority\Network Service. W przypadku systemów Windows XP i Windows Server 2003 konto to ASPNET.

12. Uruchom plik Setupcerttool.bat. Ten plik znajduje się w  \<InstallPath> folderze \ WF_WCF_Samples \wcf\setup\.  Ten skrypt wykona następujące zadania:

    - Utwórz narzędzie FindPrivateKey.

    - Utwórz katalog o nazwie%ProgramFiles%\ServiceModelSampleTools.

    - Skopiuj nowe narzędzie FindPrivateKey do tego katalogu.

    To narzędzie jest wymagane przez przykłady, które używają certyfikatów i są hostowane w usługach IIS.

    > [!NOTE]
    > Ze względów bezpieczeństwa Pamiętaj, aby usunąć definicję katalogu wirtualnego i uprawnienia przyznane w powyższych krokach konfiguracji, uruchamiając plik wsadowy o nazwie Cleanupvroot.bat po zakończeniu z przykładami.

13. Przykłady, które są samodzielne (niehostowane w usługach IIS), wymagają uprawnień do rejestrowania adresów HTTP na komputerze do nasłuchiwania. Uprawnienie do rezerwacji przestrzeni nazw protokołu HTTP pochodzi z konta użytkownika używanego do uruchomienia przykładu. Domyślnie konta administratorów mają uprawnienia do rejestrowania dowolnego adresu HTTP. Kontom innym niż administrator należy nadać uprawnienia do przestrzeni nazw HTTP używanych przez przykłady. Więcej informacji o sposobie konfigurowania rezerwacji przestrzeni nazw znajduje się w temacie [Konfigurowanie protokołów HTTP i https](../feature-details/configuring-http-and-https.md).

14. Niektóre przykłady wymagają usługi kolejkowania komunikatów. Instrukcje instalacji znajdują się w temacie [Instalowanie usługi kolejkowania komunikatów (MSMQ)](installing-message-queuing-msmq.md) .

    > [!NOTE]
    > Upewnij się, że usługa MSMQ została uruchomiona przed uruchomieniem dowolnych przykładów, które wymagają usługi kolejkowania komunikatów.

15. Niektóre przykłady wymagają certyfikatów. Zobacz [instrukcje instalacji certyfikatu serwera Internet Information Services (IIS)](iis-server-certificate-installation-instructions.md).
