---
title: Zabezpieczenia transportu z uwierzytelnianiem systemu Windows
description: Zapoznaj się z tym scenariuszem, który pokazuje klient lub usługę WCF zabezpieczone przez zabezpieczenia systemu Windows. W tym przykładzie usługa intranetowa wyświetla informacje o zasobach ludzkich.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 96dd26e2-46e7-4de0-9a29-4fcb05bf187b
ms.openlocfilehash: 9b81f2f2fb6352af254146951ed35ad4fdca8caa
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90545210"
---
# <a name="transport-security-with-windows-authentication"></a>Zabezpieczenia transportu z uwierzytelnianiem systemu Windows
W poniższym scenariuszu przedstawiono klienta i usługę Windows Communication Foundation (WCF) zabezpieczony przez zabezpieczenia systemu Windows. Aby uzyskać więcej informacji na temat programowania, zobacz [How to: Zabezpieczanie usługi przy użyciu poświadczeń systemu Windows](../how-to-secure-a-service-with-windows-credentials.md).  
  
 Intranetowa usługa sieci Web Wyświetla informacje o zasobach ludzkich. Klient jest aplikacją formularzy systemu Windows. Aplikacja jest wdrażana w domenie z kontrolerem Kerberos zabezpieczania domeny.  
  
 ![Zabezpieczenia transportu z uwierzytelnianiem systemu Windows](./media/transport-security-with-windows-authentication/secured-windows-authentication.gif)  
  
|Charakterystyka|Opis|  
|--------------------|-----------------|  
|Tryb zabezpieczeń|Transport|  
|Współdziałanie|Tylko WCF|  
|Uwierzytelnianie (serwer)<br /><br /> Uwierzytelnianie (klient)|Tak (przy użyciu zintegrowanego uwierzytelniania systemu Windows)<br /><br /> Tak (przy użyciu zintegrowanego uwierzytelniania systemu Windows)|  
|Integralność|Yes|  
|Poufność|Yes|  
|Transport|Waga. PROTOKOŁ|  
|Wiązanie|<xref:System.ServiceModel.NetTcpBinding>|  
  
## <a name="service"></a>Usługa  
 Poniższy kod i konfiguracja są przeznaczone do niezależnego uruchamiania. Wykonaj jedną z następujących czynności:  
  
- Tworzenie usługi autonomicznej przy użyciu kodu bez konfiguracji.  
  
- Utwórz usługę przy użyciu podanej konfiguracji, ale nie Definiuj żadnych punktów końcowych.  
  
### <a name="code"></a>Kod  
 Poniższy kod przedstawia sposób tworzenia punktu końcowego usługi, który korzysta z zabezpieczeń systemu Windows.  
  
 [!code-csharp[C_SecurityScenarios#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#3)]
 [!code-vb[C_SecurityScenarios#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#3)]  
  
### <a name="configuration"></a>Konfiguracja  
 Aby skonfigurować punkt końcowy usługi, można użyć następującej konfiguracji zamiast kodu:  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
    <behaviors />  
    <services>  
      <service behaviorConfiguration="" name="ServiceModel.Calculator">  
        <endpoint address="net.tcp://localhost:8008/Calculator"
                  binding="netTcpBinding"  
          bindingConfiguration="WindowsClientOverTcp"
                  name="WindowsClientOverTcp"  
                  contract="ServiceModel.ICalculator" />  
      </service>  
    </services>  
    <bindings>  
      <netTcpBinding>  
        <binding name="WindowsClientOverTcp">  
          <security mode="Transport">  
            <transport clientCredentialType="Windows" />  
          </security>  
        </binding>  
      </netTcpBinding>  
    </bindings>  
    <client />  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="client"></a>Klient  
 Poniższy kod i konfiguracja są przeznaczone do niezależnego uruchamiania. Wykonaj jedną z następujących czynności:  
  
- Utwórz klienta autonomicznego przy użyciu kodu (i kodu klienta).  
  
- Utwórz klienta, który nie definiuje żadnych adresów punktów końcowych. Zamiast tego należy użyć konstruktora klienta, który przyjmuje nazwę konfiguracji jako argument. Na przykład:  
  
     [!code-csharp[C_SecurityScenarios#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#0)]
     [!code-vb[C_SecurityScenarios#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#0)]  
  
### <a name="code"></a>Kod  
 Poniższy kod tworzy klienta. Powiązanie jest skonfigurowane do korzystania z zabezpieczeń trybu transportu przy użyciu transportu TCP z typem poświadczeń klienta ustawionym na Windows.  
  
 [!code-csharp[C_SecurityScenarios#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#4)]
 [!code-vb[C_SecurityScenarios#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#4)]  
  
### <a name="configuration"></a>Konfiguracja  
 W celu utworzenia klienta można użyć poniższej konfiguracji zamiast kodu.  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
    <bindings>  
      <netTcpBinding>  
        <binding name="NetTcpBinding_ICalculator" >  
          <security mode="Transport">  
            <transport clientCredentialType="Windows" />  
          </security>  
        </binding>  
      </netTcpBinding>  
    </bindings>  
    <client>  
      <endpoint address="net.tcp://localhost:8008/Calculator"
                binding="netTcpBinding"
                bindingConfiguration="NetTcpBinding_ICalculator"
                contract="ICalculator"  
                name="NetTcpBinding_ICalculator">  
      </endpoint>  
    </client>  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="see-also"></a>Zobacz także

- [Przegląd zabezpieczeń](security-overview.md)
- [Instrukcje: Zabezpieczanie usługi za pomocą poświadczeń systemu Windows](../how-to-secure-a-service-with-windows-credentials.md)
- [Model zabezpieczeń dla sieci szkieletowej aplikacji systemu Windows Server](/previous-versions/appfabric/ee677202(v=azure.10))
