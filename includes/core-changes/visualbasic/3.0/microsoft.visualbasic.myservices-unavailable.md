---
ms.openlocfilehash: 58e65bae1593f23945a971b896a1db4a929b4587
ms.sourcegitcommit: 79a2d6a07ba4ed08979819666a0ee6927bbf1b01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/28/2019
ms.locfileid: "74567411"
---
### <a name="types-in-microsoftvisualbasicmyservices-namespace-not-available"></a><span data-ttu-id="3d9ee-101">Typy w przestrzeni nazw Microsoft. VisualBasic. WebServices są niedostępne</span><span class="sxs-lookup"><span data-stu-id="3d9ee-101">Types in Microsoft.VisualBasic.MyServices namespace not available</span></span>

<span data-ttu-id="3d9ee-102">Typy w przestrzeni nazw <xref:Microsoft.VisualBasic.MyServices?displayProperty=fullName> są niedostępne.</span><span class="sxs-lookup"><span data-stu-id="3d9ee-102">The types in the <xref:Microsoft.VisualBasic.MyServices?displayProperty=fullName> namespace are not available.</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="3d9ee-103">Wprowadzona wersja</span><span class="sxs-lookup"><span data-stu-id="3d9ee-103">Version introduced</span></span>

<span data-ttu-id="3d9ee-104">.NET Core 3,0 (wersja zapoznawcza 8)</span><span class="sxs-lookup"><span data-stu-id="3d9ee-104">.NET Core 3.0 Preview 8</span></span>

#### <a name="change-description"></a><span data-ttu-id="3d9ee-105">Zmień opis</span><span class="sxs-lookup"><span data-stu-id="3d9ee-105">Change description</span></span>

<span data-ttu-id="3d9ee-106">Typy w przestrzeni nazw <xref:Microsoft.VisualBasic.MyServices?displayProperty=fullName> były dostępne w niektórych wersjach programu .NET Core 3,0 Preview.</span><span class="sxs-lookup"><span data-stu-id="3d9ee-106">The types in the <xref:Microsoft.VisualBasic.MyServices?displayProperty=fullName> namespace were available in some .NET Core 3.0 Preview releases.</span></span> <span data-ttu-id="3d9ee-107">Nie są już dostępne począwszy od programu .NET Core 3,0 w wersji zapoznawczej 9.</span><span class="sxs-lookup"><span data-stu-id="3d9ee-107">They are no longer available starting with .NET Core 3.0 Preview 9.</span></span>

<span data-ttu-id="3d9ee-108">Typy zostały usunięte, aby uniknąć niepotrzebnych zależności zestawów lub istotne zmiany w kolejnych wersjach.</span><span class="sxs-lookup"><span data-stu-id="3d9ee-108">The types were removed to avoid unnecessary assembly dependencies or breaking changes in subsequent releases.</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="3d9ee-109">Zalecane działanie</span><span class="sxs-lookup"><span data-stu-id="3d9ee-109">Recommended action</span></span>

<span data-ttu-id="3d9ee-110">Jeśli kod zależy od użycia typów **Microsoft. VisualBasic. WebServices** i ich członków, istnieją odpowiednie typy i elementy członkowskie w bibliotece klas .NET.</span><span class="sxs-lookup"><span data-stu-id="3d9ee-110">If your code depends on the use of **Microsoft.VisualBasic.MyServices** types and their members, there are corresponding types and members in the .NET class library.</span></span> <span data-ttu-id="3d9ee-111">Poniżej znajduje się mapowanie typów **Microsoft. VisualBasic. WebServices** na ich równoważne typy biblioteki klas .NET:</span><span class="sxs-lookup"><span data-stu-id="3d9ee-111">The following is a mapping of  **Microsoft.VisualBasic.MyServices** types to their equivalent .NET class library types:</span></span>

|<span data-ttu-id="3d9ee-112">Typ Microsoft. VisualBasic. WebServices</span><span class="sxs-lookup"><span data-stu-id="3d9ee-112">Microsoft.VisualBasic.MyServices type</span></span>|<span data-ttu-id="3d9ee-113">Typ biblioteki klas .NET</span><span class="sxs-lookup"><span data-stu-id="3d9ee-113">.NET class library type</span></span>|
|--|--|
|<xref:Microsoft.VisualBasic.MyServices.ClipboardProxy>|<span data-ttu-id="3d9ee-114"><xref:System.Windows.Clipboard?displayProperty=nameWithType> dla aplikacji WPF <xref:System.Windows.Forms.Clipboard?displayProperty=nameWithType> aplikacji Windows Forms</span><span class="sxs-lookup"><span data-stu-id="3d9ee-114"><xref:System.Windows.Clipboard?displayProperty=nameWithType> for WPF applications, <xref:System.Windows.Forms.Clipboard?displayProperty=nameWithType> for Windows Forms applications</span></span>|
|<xref:Microsoft.VisualBasic.MyServices.FileSystemProxy>|<span data-ttu-id="3d9ee-115">Typy w przestrzeni nazw <xref:System.IO></span><span class="sxs-lookup"><span data-stu-id="3d9ee-115">Types in the <xref:System.IO> namespace</span></span>|
|<xref:Microsoft.VisualBasic.MyServices.RegistryProxy>|<span data-ttu-id="3d9ee-116">Typy związane z rejestrem w przestrzeni nazw <xref:Microsoft.Win32></span><span class="sxs-lookup"><span data-stu-id="3d9ee-116">Registry-related types in the <xref:Microsoft.Win32> namespace</span></span>|
|<xref:Microsoft.VisualBasic.MyServices.SpecialDirectoriesProxy>|<xref:System.Environment.GetFolderPath%2A?displayProperty=nameWithType>|

#### <a name="category"></a><span data-ttu-id="3d9ee-117">Kategoria</span><span class="sxs-lookup"><span data-stu-id="3d9ee-117">Category</span></span>

<span data-ttu-id="3d9ee-118">Język Visual Basic</span><span class="sxs-lookup"><span data-stu-id="3d9ee-118">Visual Basic</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="3d9ee-119">Dotyczy interfejsów API</span><span class="sxs-lookup"><span data-stu-id="3d9ee-119">Affected APIs</span></span>

- <xref:Microsoft.VisualBasic.MyServices?displayProperty=fullName>

<!--

### Affected APIs

- `N:Microsoft.VisualBasic.MyServices`

-- >
