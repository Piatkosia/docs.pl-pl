---
title: <clientCredentials>
ms.date: 03/30/2017
ms.assetid: 1e6eef0d-a34e-4d74-b0f7-f65d2181858d
ms.openlocfilehash: 6094006df24ee824c419a783ab29d7604757577c
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91201463"
---
# \<clientCredentials>

Określa poświadczenia używane do uwierzytelniania klienta w usłudze.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<endpointBehaviors>**](endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<clientCredentials>**  
  
## <a name="syntax"></a>Składnia  
  
```xml  
<clientCredentials type="String"
                   supportInteractive="Boolean" >
  <clientCertificate>
  </clientCertificate>
  <digest>
  </digest>
  <isuedToken>
  </isuedToken>
  <peer>
  </peer>
  <serviceCertificate>
  </serviceCertificate>
  <windowsAuthentication>
  </windowsAuthentication>
</clientCredentials>
```  
  
## <a name="attributes-and-elements"></a>Atrybuty i elementy  

 W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|  
|---------------|-----------------|  
|`supportInteractive`|Wartość logiczna określająca, czy użytkownik interaktywny może uczestniczyć w wyborze poświadczenia klienta w czasie wykonywania. Wartość domyślna to `true`.|  
|`type`|Ciąg określający typ tego elementu konfiguracji.|  
  
### <a name="child-elements"></a>Elementy podrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|[\<clientCertificate>](clientcertificate-of-clientcredentials-element.md)|Określa certyfikat używany do uwierzytelniania klienta w usłudze. Ten element jest typu <xref:System.ServiceModel.Configuration.X509InitiatorCertificateClientElement> .|  
|[\<httpDigest>](httpdigest-element.md)|Określa skrót używany do uwierzytelniania klienta w usłudze. Ten element jest typu <xref:System.ServiceModel.Configuration.HttpDigestClientElement> .|  
|[\<issuedToken>](issuedtoken.md)|Określa niestandardowy typ tokenu używany do uwierzytelniania klienta w usłudze bezpiecznego tokenu (STS). Ten element jest typu <xref:System.ServiceModel.Configuration.IssuedTokenClientElement> .|  
|[\<peer>](peer-of-clientcredentials-element.md)|Określa bieżące poświadczenie elementu równorzędnego. Ten element jest typu <xref:System.ServiceModel.Configuration.PeerCredentialElement> .|  
|[\<serviceCertificate>](servicecertificate-of-clientcredentials-element.md)|Określa certyfikat używany do uwierzytelniania usługi na kliencie i udostępnia strukturę do ustawiania opcji certyfikatu. Ten certyfikat musi być dostarczony z usługi do klienta jako poza pasmem. Ten element jest typu <xref:System.ServiceModel.Configuration.X509RecipientCertificateClientElement> .|  
|[\<windows>](windows-of-clientcredentials-element.md)|Określa poświadczenie systemu Windows. Wartość domyślna to poświadczenie bieżącego wątku. Ten element jest typu <xref:System.ServiceModel.Configuration.WindowsClientElement> .|  
  
### <a name="parent-elements"></a>Elementy nadrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|[\<behavior>](behavior-of-endpointbehaviors.md)|Określa zachowanie punktu końcowego.|  
  
## <a name="remarks"></a>Uwagi  

 Poświadczenia klienta służą do uwierzytelniania klienta programu w przypadku, gdy wymagane jest uwierzytelnianie wzajemne. Ta sekcja konfiguracji może również służyć do określania certyfikatów usługi dla scenariuszy, w których klient musi zabezpieczyć komunikaty do usługi za pomocą certyfikatu usługi.  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.ServiceModel.Configuration.ClientCredentialsElement>
- <xref:System.ServiceModel.Description.ClientCredentials>
- [Zachowania zabezpieczeń](../../../wcf/feature-details/security-behaviors-in-wcf.md)
- [Zabezpieczanie klientów [WCF]](../../../wcf/securing-clients.md)
