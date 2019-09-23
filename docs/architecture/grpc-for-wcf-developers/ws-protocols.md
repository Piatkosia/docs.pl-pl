---
title: Protokoły WS-* — gRPC dla deweloperów WCF
description: Przegląd protokołów WS-* obsługiwanych przez funkcję WCF i alternatywy dostępne dla gRPC
author: markrendle
ms.date: 09/02/2019
ms.openlocfilehash: cd9af401fc46297fc0c67f5b3e5d6b34177d6a87
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/23/2019
ms.locfileid: "71184030"
---
# <a name="ws--protocols"></a>WS-\* Protocols

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

Jedną z rzeczywistych zalet pracy z programem Windows Communication Foundation (WCF) była obsługa wielu istniejących protokołów _WS-\*_  Standard. W tej sekcji zawarto krótko zależą od tego, jak\* gRPC zarządza tymi samymi protokołami WS-Protocol i jakie opcje są dostępne, gdy nie istnieje alternatywa.

## <a name="metadata-exchange---ws-policy-ws-discovery-and-so-on"></a>Wymiana metadanych — WS-Policy, WS-Discovery itd.

Usługi SOAP udostępniają dokumenty schematu Web Services Description Language (WSDL) z informacjami, takimi jak formaty danych, operacje lub opcje komunikacji. Ten schemat może służyć do generowania kodu klienta.

gRPC działa najlepiej, gdy serwery i klienci są wygenerowane z `.proto` tych samych plików, ale opcjonalne rozszerzenie odbicia serwera zapewnia sposób udostępniania informacji dynamicznych z działającego serwera. Aby uzyskać więcej informacji, zobacz pakiet NuGet [GRPC. odbicie](https://nuget.org/packages/Grpc.Reflection) oraz artykuł dotyczący [odbicia serwera GRPC C# ](https://github.com/grpc/grpc/blob/master/doc/csharp/server_reflection.md) .

Protokół WS-Discovery służy do lokalizowania usług w sieci lokalnej. usługi gRPC są zwykle zlokalizowane przy użyciu systemu DNS lub rejestru usługi, takiego jak Consul lub dozorcy.

## <a name="security--ws-security-ws-federation-xml-encryption-and-so-on"></a>Zabezpieczenia — WS-Security, WS-Federation, szyfrowanie XML i tak dalej

Zabezpieczenia, uwierzytelnianie i autoryzacja zostały omówione bardziej szczegółowo w [rozdziale 6](security.md). Należy jednak zauważyć, że w przeciwieństwie do WCF, gRPC nie obsługuje szyfrowania WS-Security, WS Federacji ani XML. Nawet tak, gRPC zapewnia doskonałe zabezpieczenia; cały ruch sieciowy gRPC jest szyfrowany automatycznie przy użyciu protokołu HTTP/2 za pośrednictwem protokołu TLS, a certyfikaty x509 mogą być używane do wzajemnego uwierzytelniania klienta/serwera.

## <a name="ws-reliablemessaging"></a>WS-ReliableMessaging

gRPC nie zapewnia równoważnej specyfikacji WS-ReliableMessaging. Semantyka ponawiania powinna być obsługiwana w kodzie, prawdopodobnie z biblioteką, taką jak [Polly](https://github.com/App-vNext/Polly). W przypadku uruchamiania w Kubernetes lub podobnych środowiskach aranżacji [usługi](service-mesh.md) mogą również pomóc w zapewnianiu niezawodnej obsługi komunikatów między usługami.

## <a name="ws-transaction-ws-coordination"></a>WS-Transaction, WS-koordynacyjny

Implementacja transakcji rozproszonych w programie WCF używa systemu Windows Distributed Transaction Coordinator lub MSDTC. Współpracuje z menedżerami zasobów, które obsługują takie usługi, jak SQL Server, MSMQ lub systemy plików Windows. Na świecie współczesnych mikrousług, w części ze względu na szerszy zakres używanych technologii, nie jest jeszcze równoważne. Aby zapoznać się z omówieniem transakcji, zobacz [dodatek a](appendix.md).

>[!div class="step-by-step"]
>[Poprzedni](error-handling.md)
>[Następny](migrate-wcf-to-grpc.md)