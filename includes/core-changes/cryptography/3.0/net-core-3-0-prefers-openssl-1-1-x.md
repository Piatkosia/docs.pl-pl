---
ms.openlocfilehash: b49b2f88b130bb952b77964d5bf38374dc606385
ms.sourcegitcommit: 79a2d6a07ba4ed08979819666a0ee6927bbf1b01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/28/2019
ms.locfileid: "74567982"
---
### <a name="net-core-30-prefers-openssl-11x-to-openssl-10x"></a><span data-ttu-id="02d1c-101">.NET Core 3,0 preferuje OpenSSL 1.1. x do OpenSSL 1.0. x</span><span class="sxs-lookup"><span data-stu-id="02d1c-101">.NET Core 3.0 prefers OpenSSL 1.1.x to OpenSSL 1.0.x</span></span>

<span data-ttu-id="02d1c-102">.NET Core dla systemu Linux, który działa między wieloma dystrybucjami systemu Linux, może obsługiwać zarówno OpenSSL 1.0. x, jak i OpenSSL 1.1. x.</span><span class="sxs-lookup"><span data-stu-id="02d1c-102">.NET Core for Linux, which works across multiple Linux distributions, can support both OpenSSL 1.0.x and OpenSSL 1.1.x.</span></span>  <span data-ttu-id="02d1c-103">Programy .NET Core 2,1 i .NET Core 2,2 szukają najpierw 1.0. x, a następnie wracają do wersji 1.1. x; program .NET Core 3,0 szuka najpierw 1.1. x.</span><span class="sxs-lookup"><span data-stu-id="02d1c-103">.NET Core 2.1 and .NET Core 2.2 look for 1.0.x first, then fall back to 1.1.x; .NET Core 3.0 looks for 1.1.x first.</span></span> <span data-ttu-id="02d1c-104">Ta zmiana została wprowadzona w celu dodania obsługi nowych standardów kryptograficznych.</span><span class="sxs-lookup"><span data-stu-id="02d1c-104">This change was made to add support for new cryptographic standards.</span></span>

<span data-ttu-id="02d1c-105">Ta zmiana może mieć wpływ na biblioteki lub aplikacje, które wykonują współdziałanie platformy z typami międzyoperacyjności specyficznymi dla OpenSSL w programie .NET Core.</span><span class="sxs-lookup"><span data-stu-id="02d1c-105">This change may impact libraries or applications that do platform interop with the OpenSSL-specific interop types in .NET Core.</span></span>

#### <a name="change-description"></a><span data-ttu-id="02d1c-106">Zmień opis</span><span class="sxs-lookup"><span data-stu-id="02d1c-106">Change description</span></span>

<span data-ttu-id="02d1c-107">W programie .NET Core 2,2 i starszych wersjach środowisko uruchomieniowe preferuje ładowanie OpenSSL 1.0. x over 1.1. x.</span><span class="sxs-lookup"><span data-stu-id="02d1c-107">In .NET Core 2.2 and earlier versions, the runtime prefers loading OpenSSL 1.0.x over 1.1.x.</span></span> <span data-ttu-id="02d1c-108">Oznacza to, że typy <xref:System.IntPtr> i <xref:System.Runtime.InteropServices.SafeHandle> dla elementu Interop z OpenSSL są używane z libcrypto. so. 1.0.0/libcrypto. so. 1.0/libcrypto. so. 10 według preferencji.</span><span class="sxs-lookup"><span data-stu-id="02d1c-108">This means that the <xref:System.IntPtr> and <xref:System.Runtime.InteropServices.SafeHandle> types for interop with OpenSSL are used with libcrypto.so.1.0.0 / libcrypto.so.1.0 / libcrypto.so.10 by preference.</span></span>

<span data-ttu-id="02d1c-109">Począwszy od platformy .NET Core 3,0, środowisko uruchomieniowe preferuje ładowanie OpenSSL 1.1. x over OpenSSL 1.0. x, dlatego typy <xref:System.IntPtr> i <xref:System.Runtime.InteropServices.SafeHandle> dla elementu Interop with OpenSSL są używane z libcrypto. so. 1.1/libcrypto. tak. 11/libcrypto. tak. 1.1.0/libcrypto. tak. 1.1.1 według preferencji.</span><span class="sxs-lookup"><span data-stu-id="02d1c-109">Starting with .NET Core 3.0, the runtime prefers loading OpenSSL 1.1.x over OpenSSL 1.0.x, so the <xref:System.IntPtr> and <xref:System.Runtime.InteropServices.SafeHandle> types for interop with OpenSSL are used with libcrypto.so.1.1 / libcrypto.so.11 / libcrypto.so.1.1.0 / libcrypto.so.1.1.1 by preference.</span></span> <span data-ttu-id="02d1c-110">W związku z tym biblioteki i aplikacje, które współdziałają z usługą OpenSSL, mogą mieć niezgodne wskaźniki z wartościami dostępnymi dla platformy .NET Core podczas uaktualniania z platformy .NET Core 2,1 lub .NET Core 2,2.</span><span class="sxs-lookup"><span data-stu-id="02d1c-110">As a result, libraries and applications that interoperate with OpenSSL directly may have incompatible pointers with the .NET Core-exposed values when upgrading from .NET Core 2.1 or .NET Core 2.2.</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="02d1c-111">Wprowadzona wersja</span><span class="sxs-lookup"><span data-stu-id="02d1c-111">Version introduced</span></span>

<span data-ttu-id="02d1c-112">3.0</span><span class="sxs-lookup"><span data-stu-id="02d1c-112">3.0</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="02d1c-113">Zalecane działanie</span><span class="sxs-lookup"><span data-stu-id="02d1c-113">Recommended action</span></span>

<span data-ttu-id="02d1c-114">Biblioteki i aplikacje, które wykonują bezpośrednie operacje z OpenSSL należy zachować ostrożność, aby upewnić się, że korzystają z tej samej wersji programu OpenSSL, co środowisko uruchomieniowe programu .NET Core.</span><span class="sxs-lookup"><span data-stu-id="02d1c-114">Libraries and applications that do direct operations with OpenSSL need to be careful to ensure they are using the same version of OpenSSL as the .NET Core runtime.</span></span>

<span data-ttu-id="02d1c-115">Wszystkie biblioteki lub aplikacje, które używają wartości <xref:System.IntPtr> lub <xref:System.Runtime.InteropServices.SafeHandle> z typów kryptograficznych platformy .NET Core bezpośrednio z OpenSSL, powinny porównać wersję biblioteki, której używają z nową właściwością <xref:System.Security.Cryptography.SafeEvpPKeyHandle.OpenSslVersion?displayProperty=nameWithType>, aby upewnić się, że wskaźniki są zgodne.</span><span class="sxs-lookup"><span data-stu-id="02d1c-115">All libraries or applications that use <xref:System.IntPtr> or <xref:System.Runtime.InteropServices.SafeHandle> values from the .NET Core cryptographic types directly with OpenSSL should compare the version of the library they use with the new <xref:System.Security.Cryptography.SafeEvpPKeyHandle.OpenSslVersion?displayProperty=nameWithType> property to ensure the pointers are compatible.</span></span>

#### <a name="category"></a><span data-ttu-id="02d1c-116">Kategoria</span><span class="sxs-lookup"><span data-stu-id="02d1c-116">Category</span></span>

<span data-ttu-id="02d1c-117">Kryptografia</span><span class="sxs-lookup"><span data-stu-id="02d1c-117">Cryptography</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="02d1c-118">Dotyczy interfejsów API</span><span class="sxs-lookup"><span data-stu-id="02d1c-118">Affected APIs</span></span>

- <xref:System.Security.Cryptography.SafeEvpPKeyHandle.%23ctor%2A?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.RSAOpenSsl.%23ctor(System.IntPtr)?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.RSAOpenSsl.%23ctor(System.Security.Cryptography.SafeEvpPKeyHandle)?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.RSAOpenSsl.DuplicateKeyHandle?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.DSAOpenSsl.%23ctor(System.IntPtr)?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.DSAOpenSsl.%23ctor(System.Security.Cryptography.SafeEvpPKeyHandle)?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.DSAOpenSsl.DuplicateKeyHandle?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.ECDsaOpenSsl.%23ctor(System.IntPtr)?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.ECDsaOpenSsl.%23ctor(System.Security.Cryptography.SafeEvpPKeyHandle)?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.ECDsaOpenSsl.DuplicateKeyHandle?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.ECDiffieHellmanOpenSsl.%23ctor(System.IntPtr)?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.ECDiffieHellmanOpenSsl.%23ctor(System.Security.Cryptography.SafeEvpPKeyHandle)?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.ECDiffieHellmanOpenSsl.DuplicateKeyHandle?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.X509Certificates.X509Certificate.Handle?displayProperty=nameWithType>

<!--

### Affected APIs

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