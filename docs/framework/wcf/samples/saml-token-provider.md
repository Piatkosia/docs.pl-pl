---
title: Dostawca tokenów SAML
ms.date: 03/30/2017
ms.assetid: eb16e5e2-4c8d-4f61-a479-9c965fcec80c
ms.openlocfilehash: 4e371d518d7ef25152aba83fa00d79893397b07f
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90554426"
---
# <a name="saml-token-provider"></a>Dostawca tokenów SAML
Ten przykład pokazuje, jak zaimplementować niestandardowego dostawcę tokenów SAML klienta. Dostawca tokenu w Windows Communication Foundation (WCF) służy do dostarczania poświadczeń do infrastruktury zabezpieczeń. Dostawca tokenu ogólnie bada cel i wystawia odpowiednie poświadczenia, aby infrastruktura zabezpieczeń mogła zabezpieczyć komunikat. Usługa WCF jest dostarczana z domyślnym dostawcą tokenu Menedżera poświadczeń. Usługa WCF jest również dostarczana z dostawcą tokenu programu CardSpace. Dostawcy tokenów niestandardowych są przydatne w następujących przypadkach:

- Jeśli masz magazyn poświadczeń, którego nie mogą używać dostawcy tokenu.

- Jeśli chcesz zapewnić własny niestandardowy mechanizm przekształcania poświadczeń z punktu, gdy użytkownik poda szczegółowe informacje o tym, kiedy struktura klienta programu WCF używa tych poświadczeń.

- W przypadku kompilowania niestandardowego tokenu.

 Ten przykład pokazuje, jak utworzyć niestandardowego dostawcę tokenów, który umożliwia użycie tokenu SAML uzyskanego spoza struktury klienta WCF.

 Podsumowując, ten przykład ilustruje następujące elementy:

- Jak można skonfigurować klienta przy użyciu niestandardowego dostawcy tokenów.

- Jak można przesłać token SAML do niestandardowych poświadczeń klienta.

- Jak token SAML jest dostarczany do struktury klienta WCF.

- Jak serwer jest uwierzytelniany przez klienta za pomocą certyfikatu X. 509 serwera.

 Usługa udostępnia dwa punkty końcowe do komunikacji z usługą, zdefiniowane przy użyciu App.config pliku konfiguracji. Każdy punkt końcowy składa się z adresu, powiązania i kontraktu. Powiązanie jest skonfigurowane przy użyciu standardu `wsFederationHttpBinding` , który używa zabezpieczeń komunikatów. Jeden z punktów końcowych oczekuje, że klient uwierzytelnia się za pomocą tokenu SAML, który używa symetrycznego klucza testowego, podczas gdy drugi oczekuje, że klient uwierzytelnia się za pomocą tokenu SAML, który używa klucza nieasymetrycznego dowodu. Usługa konfiguruje również certyfikat usługi przy użyciu `serviceCredentials` zachowania. `serviceCredentials`Zachowanie umożliwia skonfigurowanie certyfikatu usługi. Certyfikat usługi jest używany przez klienta do uwierzytelniania usługi i zapewniania ochrony komunikatów. Następująca konfiguracja odwołuje się do certyfikatu "localhost" zainstalowanego podczas konfiguracji przykładowej zgodnie z opisem w instrukcji konfiguracyjnych na końcu tego tematu. `serviceCredentials`Zachowanie umożliwia również Konfigurowanie certyfikatów, które są zaufane do podpisywania tokenów SAML. Następująca konfiguracja odwołuje się do certyfikatu "Alicja" zainstalowanego podczas próby.

```xml
<system.serviceModel>
 <services>
  <service
          name="Microsoft.ServiceModel.Samples.CalculatorService"
          behaviorConfiguration="CalculatorServiceBehavior">
   <host>
    <baseAddresses>
     <!-- configure base address provided by host -->
     <add
  baseAddress="http://localhost:8000/servicemodelsamples/service/" />
    </baseAddresses>
   </host>
   <!-- use base address provided by host -->
   <!-- Endpoint that expect SAML tokens with Symmetric proof keys -->
   <endpoint address="calc/symm"
             binding="wsFederationHttpBinding"
             bindingConfiguration="Binding1"
             contract="Microsoft.ServiceModel.Samples.ICalculator" />
   <!-- Endpoint that expect SAML tokens with Asymmetric proof keys -->
   <endpoint address="calc/asymm"
             binding="wsFederationHttpBinding"
             bindingConfiguration="Binding2"
             contract="Microsoft.ServiceModel.Samples.ICalculator" />
  </service>
 </services>

 <bindings>
  <wsFederationHttpBinding>
   <!-- Binding that expect SAML tokens with Symmetric proof keys -->
   <binding name="Binding1">
    <security mode="Message">
     <message negotiateServiceCredential ="false"
              issuedKeyType="SymmetricKey"
              issuedTokenType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1"  />
    </security>
   </binding>
   <!-- Binding that expect SAML tokens with Asymmetric proof keys -->
   <binding name="Binding2">
    <security mode="Message">
     <message negotiateServiceCredential ="false"
              issuedKeyType="AsymmetricKey"
              issuedTokenType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1"  />
    </security>
   </binding>
  </wsFederationHttpBinding>
 </bindings>

 <behaviors>
  <serviceBehaviors>
   <behavior name="CalculatorServiceBehavior">
    <!--
    The serviceCredentials behavior allows one to define a service certificate.
    A service certificate is used by a client to authenticate the service and provide message protection.
    This configuration references the "localhost" certificate installed during the setup instructions.
    -->
    <serviceCredentials>
     <!-- Set allowUntrustedRsaIssuers to true to allow self-signed, asymmetric key based SAML tokens -->
     <issuedTokenAuthentication allowUntrustedRsaIssuers ="true" >
      <!-- Add Alice to the list of certs trusted to issue SAML tokens -->
      <knownCertificates>
       <add storeLocation="LocalMachine"
            storeName="TrustedPeople"
            x509FindType="FindBySubjectName"
            findValue="Alice"/>
      </knownCertificates>
     </issuedTokenAuthentication>
     <serviceCertificate storeLocation="LocalMachine"
                         storeName="My"
                         x509FindType="FindBySubjectName"
                         findValue="localhost"  />
    </serviceCredentials>
   </behavior>
  </serviceBehaviors>
 </behaviors>

</system.serviceModel>
```

 Poniższe kroki pokazują, jak opracować niestandardowego dostawcę tokenów SAML i zintegrować go z WCF: Framework zabezpieczeń:

1. Napisz niestandardowego dostawcę tokenu SAML.

     Przykład implementuje niestandardowego dostawcę tokenów SAML, który zwraca token zabezpieczający na podstawie potwierdzenia SAML dostarczonego w czasie konstruowania.

     Aby wykonać to zadanie, dostawca niestandardowego tokenu pochodzi od <xref:System.IdentityModel.Selectors.SecurityTokenProvider> klasy i zastępuje <xref:System.IdentityModel.Selectors.SecurityTokenProvider.GetTokenCore%2A> metodę. Ta metoda tworzy i zwraca nowy `SecurityToken` .

    ```csharp
    protected override SecurityToken GetTokenCore(TimeSpan timeout)
    {
     // Create a SamlSecurityToken from the provided assertion
     SamlSecurityToken samlToken = new SamlSecurityToken(assertion);

     // Create a SecurityTokenSerializer that will be used to
     // serialize the SamlSecurityToken
     WSSecurityTokenSerializer ser = new WSSecurityTokenSerializer();
     // Create a memory stream to write the serialized token into
     // Use an initial size of 64Kb
     MemoryStream s = new MemoryStream(UInt16.MaxValue);

     // Create an XmlWriter over the stream
     XmlWriter xw = XmlWriter.Create(s);

     // Write the SamlSecurityToken into the stream
     ser.WriteToken(xw, samlToken);

     // Seek back to the beginning of the stream
     s.Seek(0, SeekOrigin.Begin);

     // Load the serialized token into a DOM
     XmlDocument dom = new XmlDocument();
     dom.Load(s);

     // Create a KeyIdentifierClause for the SamlSecurityToken
     SamlAssertionKeyIdentifierClause samlKeyIdentifierClause = samlToken.CreateKeyIdentifierClause<SamlAssertionKeyIdentifierClause>();

    // Return a GenericXmlToken from the XML for the
    // SamlSecurityToken, the proof token, the valid from and valid
    // until times from the assertion and the key identifier clause
    // created above
    return new GenericXmlSecurityToken(dom.DocumentElement, proofToken, assertion.Conditions.NotBefore, assertion.Conditions.NotOnOrAfter, samlKeyIdentifierClause, samlKeyIdentifierClause, null);
    }
    ```

2. Napisz niestandardowego menedżera tokenów zabezpieczających.

     <xref:System.IdentityModel.Selectors.SecurityTokenManager>Klasa jest używana do tworzenia <xref:System.IdentityModel.Selectors.SecurityTokenProvider> dla określonych <xref:System.IdentityModel.Selectors.SecurityTokenRequirement> , które są przesyłane do niego w `CreateSecurityTokenProvider` metodzie. Menedżer tokenów zabezpieczających jest również używany do tworzenia wystawców tokenów i serializatorów tokenów, ale nie są one objęte tym przykładem. W tym przykładzie niestandardowy Menedżer tokenów zabezpieczających dziedziczy z <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager> klasy i przesłania `CreateSecurityTokenProvider` metodę w celu zwrócenia niestandardowego dostawcy TOKENów SAML, gdy spełnione wymagania dotyczące tokenu wskazują, że żądanie tokenu SAML jest żądane. Jeśli Klasa poświadczeń klienta (zobacz krok 3) nie określiła potwierdzenia, Menedżer tokenów zabezpieczających tworzy odpowiednie wystąpienie.

    ```csharp
    public class SamlSecurityTokenManager : ClientCredentialsSecurityTokenManager
    {
     SamlClientCredentials samlClientCredentials;

     public SamlSecurityTokenManager ( SamlClientCredentials samlClientCredentials)
      : base(samlClientCredentials)
     {
      // Store the creating client credentials
      this.samlClientCredentials = samlClientCredentials;
     }

     public override SecurityTokenProvider CreateSecurityTokenProvider ( SecurityTokenRequirement tokenRequirement )
     {
      // If token requirement matches SAML token return the
      // custom SAML token provider
      if (tokenRequirement.TokenType == SecurityTokenTypes.Saml ||
          tokenRequirement.TokenType == "http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1")
      {
       // Retrieve the SAML assertion and proof token from the
       // client credentials
       SamlAssertion assertion = this.samlClientCredentials.Assertion;
       SecurityToken prooftoken = this.samlClientCredentials.ProofToken;

       // If either the assertion of proof token is null...
       if (assertion == null || prooftoken == null)
       {
        // ...get the SecurityBindingElement and then the
        // specified algorithm suite
        SecurityBindingElement sbe = null;
        SecurityAlgorithmSuite sas = null;

        if ( tokenRequirement.TryGetProperty<SecurityBindingElement> ( "http://schemas.microsoft.com/ws/2006/05/servicemodel/securitytokenrequirement/SecurityBindingElement", out sbe))
        {
         sas = sbe.DefaultAlgorithmSuite;
        }

        // If the token requirement is for a SymmetricKey based token..
        if (tokenRequirement.KeyType == SecurityKeyType.SymmetricKey)
        {
         // Create a symmetric proof token
         prooftoken = SamlUtilities.CreateSymmetricProofToken ( tokenRequirement.KeySize );
         // and a corresponding assertion based on the claims specified in the client credentials
         assertion = SamlUtilities.CreateSymmetricKeyBasedAssertion ( this.samlClientCredentials.Claims, new X509SecurityToken ( samlClientCredentials.ClientCertificate.Certificate ), new X509SecurityToken ( samlClientCredentials.ServiceCertificate.DefaultCertificate ), (BinarySecretSecurityToken)prooftoken, sas);
        }
        // otherwise...
        else
        {
         // Create an asymmetric proof token
         prooftoken = SamlUtilities.CreateAsymmetricProofToken();
         // and a corresponding assertion based on the claims
         // specified in the client credentials
         assertion = SamlUtilities.CreateAsymmetricKeyBasedAssertion ( this.samlClientCredentials.Claims, prooftoken, sas );
        }
       }

       // Create a SamlSecurityTokenProvider based on the assertion and proof token
       return new SamlSecurityTokenProvider(assertion, prooftoken);
      }
      // otherwise use base implementation
      else
      {
       return base.CreateSecurityTokenProvider(tokenRequirement);
      }
    }
    ```

3. Napisz niestandardowe poświadczenie klienta.

     Klasa poświadczeń klienta służy do reprezentowania poświadczeń skonfigurowanych dla serwera proxy klienta i tworzy Menedżera tokenów zabezpieczających, który służy do uzyskiwania wystawców tokenów, dostawców tokenów i serializatorów tokenów.

    ```csharp
    public class SamlClientCredentials : ClientCredentials
    {
     ClaimSet claims;
     SamlAssertion assertion;
     SecurityToken proofToken;

     public SamlClientCredentials() : base()
     {
      // Set SupportInteractive to false to suppress Cardspace UI
      base.SupportInteractive = false;
     }

     protected SamlClientCredentials(SamlClientCredentials other) : base ( other )
     {
      // Just do reference copy given sample nature
      this.assertion = other.assertion;
      this.claims = other.claims;
      this.proofToken = other.proofToken;
     }

     public SamlAssertion Assertion { get { return assertion; } set { assertion = value; } }

     public SecurityToken ProofToken { get { return proofToken; } set { proofToken = value; } }
     public ClaimSet Claims { get { return claims; } set { claims = value; } }

     protected override ClientCredentials CloneCore()
     {
      return new SamlClientCredentials(this);
     }

     public override SecurityTokenManager CreateSecurityTokenManager()
     {
      // return custom security token manager
      return new SamlSecurityTokenManager(this);
     }
    }
    ```

4. Skonfiguruj klienta tak, aby korzystał z niestandardowego poświadczenia klienta.

     Przykład usuwa domyślną klasę poświadczeń klienta i dostarcza nową klasę poświadczeń klienta, aby klient mógł użyć niestandardowego poświadczenia klienta.

    ```csharp
    // Create new credentials class
    SamlClientCredentials samlCC = new SamlClientCredentials();

    // Set the client certificate. This is the cert that will be used to sign the SAML token in the symmetric proof key case
    samlCC.ClientCertificate.SetCertificate(StoreLocation.CurrentUser, StoreName.My, X509FindType.FindBySubjectName, "Alice");

    // Set the service certificate. This is the cert that will be used to encrypt the proof key in the symmetric proof key case
    samlCC.ServiceCertificate.SetDefaultCertificate(StoreLocation.CurrentUser, StoreName.TrustedPeople, X509FindType.FindBySubjectName, "localhost");

    // Create some claims to put in the SAML assertion
    IList<Claim> claims = new List<Claim>();
    claims.Add(Claim.CreateNameClaim(samlCC.ClientCertificate.Certificate.Subject));
    ClaimSet claimset = new DefaultClaimSet(claims);
    samlCC.Claims = claimset;

    // set new credentials
    client.ChannelFactory.Endpoint.Behaviors.Remove(typeof(ClientCredentials));
    client.ChannelFactory.Endpoint.Behaviors.Add(samlCC);
    ```

 W usłudze są wyświetlane oświadczenia skojarzone z obiektem wywołującym. Po uruchomieniu przykładu żądania operacji i odpowiedzi są wyświetlane w oknie konsoli klienta. Naciśnij klawisz ENTER w oknie klienta, aby zamknąć klienta programu.

## <a name="setup-batch-file"></a>Plik wsadowy konfiguracji
 Plik wsadowy Setup.bat dołączony do tego przykładu umożliwia skonfigurowanie serwera z odpowiednim certyfikatem w celu uruchomienia aplikacji samohostowanej wymagającej zabezpieczeń opartych na certyfikatach serwera. Ten plik wsadowy należy zmodyfikować, aby mógł działać na różnych komputerach lub działać w nieobsługiwanym przypadku.

 Poniżej przedstawiono krótkie omówienie różnych sekcji plików wsadowych, dzięki czemu można je zmodyfikować tak, aby były uruchamiane w odpowiedniej konfiguracji.

- Tworzenie certyfikatu serwera:

     Poniższe wiersze z pliku wsadowego Setup.bat utworzyć certyfikat serwera do użycia. `%SERVER_NAME%`Zmienna określa nazwę serwera. Zmień tę zmienną, aby określić własną nazwę serwera. Wartość domyślna w tym pliku wsadowym to localhost.

     Certyfikat jest przechowywany w magazynie (Personal) w lokalizacji magazynu LocalMachine.

    ```console
    echo ************
    echo Server cert setup starting
    echo %SERVER_NAME%
    echo ************
    echo making server cert
    echo ************
    makecert.exe -sr LocalMachine -ss My -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe
    ```

- Instalowanie certyfikatu serwera w zaufanym magazynie certyfikatów klienta:

     Poniższe wiersze w pliku wsadowym Setup.bat kopiują certyfikat serwera do magazynu zaufanych osób klienta. Ten krok jest wymagany, ponieważ certyfikaty wygenerowane przez Makecert.exe nie są niejawnie zaufane przez system klienta. Jeśli masz już certyfikat, który znajduje się w zaufanym certyfikacie głównym klienta — na przykład certyfikat wystawiony przez firmę Microsoft — ten krok zapełniania magazynu certyfikatów klienta z certyfikatem serwera nie jest wymagany.

    ```console
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r LocalMachine -s TrustedPeople
    ```

- Tworzenie certyfikatu wystawcy.

     Poniższe wiersze z pliku wsadowego Setup.bat utworzyć certyfikat wystawcy do użycia. `%USER_NAME%`Zmienna określa nazwę wystawcy. Zmień tę zmienną, aby określić własną nazwę wystawcy. Wartość domyślna w tym pliku wsadowym to Alicja.

     Certyfikat jest przechowywany w magazynie w lokalizacji magazynu CurrentUser.

    ```console
    echo ************
    echo Server cert setup starting
    echo %SERVER_NAME%
    echo ************
    echo making server cert
    echo ************
    makecert.exe -sr CurrentUser -ss My -a sha1 -n CN=%USER_NAME% -sky exchange -pe
    ```

- Instalowanie certyfikatu wystawcy w zaufanym magazynie certyfikatów serwera.

     Poniższe wiersze w pliku wsadowym Setup.bat kopiują certyfikat serwera do magazynu zaufanych osób klienta. Ten krok jest wymagany, ponieważ certyfikaty wygenerowane przez Makecert.exe nie są niejawnie zaufane przez system klienta. Jeśli masz już certyfikat, który znajduje się w zaufanym certyfikacie głównym klienta — na przykład certyfikat wystawiony przez firmę Microsoft — ten krok zapełniania magazynu certyfikatów serwera z certyfikatem wystawcy nie jest wymagany.

    ```console
    certmgr.exe -add -r CurrentUser -s My -c -n %USER_NAME% -r LocalMachine -s TrustedPeople
    ```

#### <a name="to-set-up-and-build-the-sample"></a>Aby skonfigurować i skompilować przykład

1. Upewnij się, że została wykonana [Procedura konfiguracji jednorazowej dla przykładów Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).

2. Aby skompilować rozwiązanie, postępuj zgodnie z instrukcjami w temacie [Tworzenie przykładów Windows Communication Foundation](building-the-samples.md).

> [!NOTE]
> W przypadku użycia Svcutil.exe do ponownego wygenerowania konfiguracji dla tego przykładu należy zmodyfikować nazwę punktu końcowego w konfiguracji klienta, aby odpowiadała kodowi klienta.

#### <a name="to-run-the-sample-on-the-same-computer"></a>Aby uruchomić przykład na tym samym komputerze

1. Uruchom Setup.bat z przykładowego folderu instalacyjnego w wierszu polecenia programu Visual Studio 2012 z uprawnieniami administratora. Spowoduje to zainstalowanie wszystkich certyfikatów wymaganych do uruchomienia przykładu.

    > [!NOTE]
    > Plik wsadowy Setup.bat został zaprojektowany do uruchamiania z wiersza polecenia programu Visual Studio 2012. Zmienna środowiskowa PATH ustawiona w wierszu polecenia programu Visual Studio 2012 wskazuje katalog zawierający pliki wykonywalne wymagane przez skrypt Setup.bat.  
  
2. Uruchom Service.exe z service\bin.  
  
3. Uruchom Client.exe z \client\bin. Aktywność klienta jest wyświetlana w aplikacji konsoli klienta.  
  
4. Jeśli klient i usługa nie mogą się komunikować, zobacz Wskazówki dotyczące [rozwiązywania problemów z przykładami programu WCF](/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90)).  
  
#### <a name="to-run-the-sample-across-computers"></a>Aby uruchomić przykład na wielu komputerach  
  
1. Utwórz katalog na komputerze usługi dla plików binarnych usługi.  
  
2. Skopiuj pliki programu Service Files do katalogu usługi na komputerze usługi. Skopiuj także pliki Setup.bat i Cleanup.bat na komputer usługi.  
  
3. Musisz mieć certyfikat serwera z nazwą podmiotu zawierającą w pełni kwalifikowaną nazwę domeny komputera. Plik Service.exe.config musi zostać zaktualizowany w celu odzwierciedlenia tej nowej nazwy certyfikatu. Można utworzyć certyfikat serwera, modyfikując plik wsadowy Setup.bat. Należy pamiętać, że plik setup.bat należy uruchomić w oknie wiersz polecenia dla deweloperów dla programu Visual Studio otwartego z uprawnieniami administratora. Należy ustawić `%SERVER_NAME%` zmienną na w pełni kwalifikowaną nazwę hosta komputera, który jest używany do hostowania usługi.  
  
4. Skopiuj certyfikat serwera do magazynu CurrentUser-TrustedPeople klienta. Ten krok nie jest konieczny, gdy certyfikat serwera jest wystawiony przez zaufanego wystawcy klienta.  
  
5. W pliku Service.exe.config na komputerze usługi Zmień wartość adresu podstawowego, aby określić w pełni kwalifikowaną nazwę komputera zamiast hosta lokalnego.  
  
6. Na komputerze usługi Uruchom Service.exe z wiersza polecenia.  
  
7. Skopiuj pliki programu klienckiego z folderu \client\bin\, w obszarze folder specyficzny dla języka, do komputera klienckiego.  
  
8. W pliku Client.exe.config na komputerze klienckim Zmień wartość adresu punktu końcowego, aby odpowiadała nowemu adresowi usługi.  
  
9. Na komputerze klienckim uruchom `Client.exe` polecenie w oknie wiersza polecenia.  
  
10. Jeśli klient i usługa nie mogą się komunikować, zobacz Wskazówki dotyczące [rozwiązywania problemów z przykładami programu WCF](/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90)).  
  
#### <a name="to-clean-up-after-the-sample"></a>Aby wyczyścić po przykładzie  
  
1. Uruchom Cleanup.bat w folderze Samples po zakończeniu uruchamiania przykładu.
