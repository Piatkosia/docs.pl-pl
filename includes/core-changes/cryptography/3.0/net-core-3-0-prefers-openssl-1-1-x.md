---
ms.openlocfilehash: 877f9d99b660c4af843e4d8d525219c1df6c99a9
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/20/2020
ms.locfileid: "83720956"
---
### <a name="net-core-30-prefers-openssl-11x-to-openssl-10x"></a>.NET Core 3,0 preferuje OpenSSL 1.1. x do OpenSSL 1.0. x

.NET Core dla systemu Linux, który działa między wieloma dystrybucjami systemu Linux, może obsługiwać zarówno OpenSSL 1.0. x, jak i OpenSSL 1.1. x.  Programy .NET Core 2,1 i .NET Core 2,2 szukają najpierw 1.0. x, a następnie wracają do wersji 1.1. x; program .NET Core 3,0 szuka najpierw 1.1. x. Ta zmiana została wprowadzona w celu dodania obsługi nowych standardów kryptograficznych.

Ta zmiana może mieć wpływ na biblioteki lub aplikacje, które wykonują współdziałanie platformy z typami międzyoperacyjności specyficznymi dla OpenSSL w programie .NET Core.

#### <a name="change-description"></a>Zmień opis

W programie .NET Core 2,2 i starszych wersjach środowisko uruchomieniowe preferuje ładowanie OpenSSL 1.0. x over 1.1. x. Oznacza to, że <xref:System.IntPtr> <xref:System.Runtime.InteropServices.SafeHandle> typy i dla współdziałania z OpenSSL są używane z libcrypto. so. 1.0.0/libcrypto. so. 1.0/libcrypto. so. 10 przez preferencję.

Począwszy od platformy .NET Core 3,0, środowisko uruchomieniowe preferuje ładowanie OpenSSL 1.1. x over OpenSSL 1.0. x, <xref:System.IntPtr> więc <xref:System.Runtime.InteropServices.SafeHandle> typy współdziałania z OpenSSL są używane z libcrypto. so. 1.1/libcrypto. tak. 11/libcrypto. tak. 1.1.0/libcrypto. tak. 1.1.1 według preferencji. W związku z tym biblioteki i aplikacje, które współdziałają z usługą OpenSSL, mogą mieć niezgodne wskaźniki z wartościami dostępnymi dla platformy .NET Core podczas uaktualniania z platformy .NET Core 2,1 lub .NET Core 2,2.

#### <a name="version-introduced"></a>Wprowadzona wersja

3.0

#### <a name="recommended-action"></a>Zalecana akcja

Biblioteki i aplikacje, które wykonują bezpośrednie operacje z OpenSSL należy zachować ostrożność, aby upewnić się, że korzystają z tej samej wersji programu OpenSSL, co środowisko uruchomieniowe programu .NET Core.

Wszystkie biblioteki lub aplikacje, które używają <xref:System.IntPtr> lub <xref:System.Runtime.InteropServices.SafeHandle> wartości z typów kryptograficznych platformy .NET Core bezpośrednio z OpenSSL, powinny porównać wersję biblioteki, której używają z nową <xref:System.Security.Cryptography.SafeEvpPKeyHandle.OpenSslVersion?displayProperty=nameWithType> właściwością, aby upewnić się, że wskaźniki są zgodne.

#### <a name="category"></a>Kategoria

Kryptografia

#### <a name="affected-apis"></a>Dotyczy interfejsów API

- <xref:System.Security.Cryptography.SafeEvpPKeyHandle.%23ctor%2A>
- <xref:System.Security.Cryptography.RSAOpenSsl.%23ctor(System.IntPtr)>
- <xref:System.Security.Cryptography.RSAOpenSsl.%23ctor(System.Security.Cryptography.SafeEvpPKeyHandle)>
- <xref:System.Security.Cryptography.RSAOpenSsl.DuplicateKeyHandle?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.DSAOpenSsl.%23ctor(System.IntPtr)>
- <xref:System.Security.Cryptography.DSAOpenSsl.%23ctor(System.Security.Cryptography.SafeEvpPKeyHandle)>
- <xref:System.Security.Cryptography.DSAOpenSsl.DuplicateKeyHandle?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.ECDsaOpenSsl.%23ctor(System.IntPtr)>
- <xref:System.Security.Cryptography.ECDsaOpenSsl.%23ctor(System.Security.Cryptography.SafeEvpPKeyHandle)>
- <xref:System.Security.Cryptography.ECDsaOpenSsl.DuplicateKeyHandle?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.ECDiffieHellmanOpenSsl.%23ctor(System.IntPtr)>
- <xref:System.Security.Cryptography.ECDiffieHellmanOpenSsl.%23ctor(System.Security.Cryptography.SafeEvpPKeyHandle)>
- <xref:System.Security.Cryptography.ECDiffieHellmanOpenSsl.DuplicateKeyHandle?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.X509Certificates.X509Certificate.Handle?displayProperty=nameWithType>

<!--

#### Affected APIs

- `Overload:System.Security.Cryptography.SafeEvpPKeyHandle.#ctor`
- `M:System.Security.Cryptography.RSAOpenSsl.#ctor(System.IntPtr)`
- `M:System.Security.Cryptography.RSAOpenSsl.#ctor(System.Security.Cryptography.SafeEvpPKeyHandle)`
- `M:System.Security.Cryptography.RSAOpenSsl.DuplicateKeyHandle`
- `M:System.Security.Cryptography.DSAOpenSsl.#ctor(System.IntPtr)`
- `M:System.Security.Cryptography.DSAOpenSsl.#ctor(System.Security.Cryptography.SafeEvpPKeyHandle)`
- `M:System.Security.Cryptography.DSAOpenSsl.DuplicateKeyHandle`
- `M:System.Security.Cryptography.ECDsaOpenSsl.#ctor(System.IntPtr)`
- `M:System.Security.Cryptography.ECDsaOpenSsl.#ctor(System.Security.CryptographySafeEvpPKeyHandle)`
- `M:System.Security.Cryptography.ECDsaOpenSsl.DuplicateKeyHandle`
- `M:System.Security.Cryptography.ECDiffieHellmanOpenSsl.#ctor(System.IntPtr)`
- `M:System.Security.Cryptography.ECDiffieHellmanOpenSsl.#ctor(System.Security.Cryptography.SafeEvpPKeyHandle)`
- `M:System.Security.Cryptography.ECDiffieHellmanOpenSsl.DuplicateKeyHandle`
- `P:System.Security.Cryptography.X509Certificates.X509Certificate.Handle`

-->
