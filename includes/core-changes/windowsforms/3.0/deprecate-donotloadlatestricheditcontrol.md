---
ms.openlocfilehash: 265fc5bea97bf85bcb9cc8111f915e14297d9957
ms.sourcegitcommit: 79a2d6a07ba4ed08979819666a0ee6927bbf1b01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/28/2019
ms.locfileid: "74643985"
---
### <a name="switchsystemwindowsformsdonotloadlatestricheditcontrol-compatibility-switch-not-supported"></a><span data-ttu-id="60c27-101">Przełącznik. System. Windows. Forms. DoNotLoadLatestRichEditControl nie jest obsługiwany.</span><span class="sxs-lookup"><span data-stu-id="60c27-101">Switch.System.Windows.Forms.DoNotLoadLatestRichEditControl compatibility switch not supported</span></span>

<span data-ttu-id="60c27-102">Przełącznik zgodności `Switch.System.Windows.Forms.UseLegacyImages`, który został wprowadzony w .NET Framework 4.7.1, nie jest obsługiwany w Windows Forms na platformie .NET Core 3,0.</span><span class="sxs-lookup"><span data-stu-id="60c27-102">The `Switch.System.Windows.Forms.UseLegacyImages` compatibility switch, which was introduced in .NET Framework 4.7.1, is not supported in Windows Forms on .NET Core 3.0.</span></span>

#### <a name="change-description"></a><span data-ttu-id="60c27-103">Zmień opis</span><span class="sxs-lookup"><span data-stu-id="60c27-103">Change description</span></span>

<span data-ttu-id="60c27-104">W .NET Framework 4.6.2 i poprzednich wersjach kontrolka <xref:System.Windows.Forms.RichTextBox> może utworzyć wystąpienie dla systemu Win32 RichEdit Control v 3.0 i dla aplikacji, które są przeznaczone dla .NET Framework 4.7.1, formant <xref:System.Windows.Forms.RichTextBox> będzie tworzyć wystąpienie RichEdit v 4.1 (w *msftedit. dll*).</span><span class="sxs-lookup"><span data-stu-id="60c27-104">In the .NET Framework 4.6.2 and previous versions, the <xref:System.Windows.Forms.RichTextBox> control would instantiate the Win32 RichEdit control v3.0, and for applications that target .NET Framework 4.7.1, the  <xref:System.Windows.Forms.RichTextBox> control would instantiate RichEdit v4.1 (in *msftedit.dll*).</span></span> <span data-ttu-id="60c27-105">Wprowadzono przełącznik zgodności `Switch.System.Windows.Forms.DoNotLoadLatestRichEditControl`, aby umożliwić aplikacjom, które są przeznaczone .NET Framework 4.7.1 i nowsze wersje, aby zrezygnować z nowej kontrolki RichEdit v 4.1 i zamiast tego użyć starego formantu RichEdit v3.</span><span class="sxs-lookup"><span data-stu-id="60c27-105">The `Switch.System.Windows.Forms.DoNotLoadLatestRichEditControl` compatibility switch was introduced to allow applications that target .NET Framework 4.7.1 and later versions to opt-out of the new RichEdit v4.1 control and use the old RichEdit v3 control instead.</span></span>

<span data-ttu-id="60c27-106">W programie .NET Core przełącznik `Switch.System.Windows.Forms.DoNotLoadLatestRichEditControl` nie jest obsługiwany.</span><span class="sxs-lookup"><span data-stu-id="60c27-106">In .NET Core, the `Switch.System.Windows.Forms.DoNotLoadLatestRichEditControl` switch is not supported.</span></span> <span data-ttu-id="60c27-107">Obsługiwane są tylko nowe wersje kontrolki <xref:System.Windows.Forms.RichTextBox>.</span><span class="sxs-lookup"><span data-stu-id="60c27-107">Only new versions of the  <xref:System.Windows.Forms.RichTextBox> control are supported.</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="60c27-108">Wprowadzona wersja</span><span class="sxs-lookup"><span data-stu-id="60c27-108">Version introduced</span></span>

<span data-ttu-id="60c27-109">3,0 wersja zapoznawcza 9</span><span class="sxs-lookup"><span data-stu-id="60c27-109">3.0 Preview 9</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="60c27-110">Zalecane działanie</span><span class="sxs-lookup"><span data-stu-id="60c27-110">Recommended action</span></span>

<span data-ttu-id="60c27-111">Usuń przełącznik.</span><span class="sxs-lookup"><span data-stu-id="60c27-111">Remove the switch.</span></span> <span data-ttu-id="60c27-112">Przełącznik nie jest obsługiwany i żadna alternatywna funkcja nie jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="60c27-112">The switch is not supported, and no alternative functionality is available.</span></span>

#### <a name="category"></a><span data-ttu-id="60c27-113">Kategoria</span><span class="sxs-lookup"><span data-stu-id="60c27-113">Category</span></span>

<span data-ttu-id="60c27-114">Windows Forms</span><span class="sxs-lookup"><span data-stu-id="60c27-114">Windows Forms</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="60c27-115">Dotyczy interfejsów API</span><span class="sxs-lookup"><span data-stu-id="60c27-115">Affected APIs</span></span>

- <xref:System.Windows.Forms.RichTextBox?displayProperty=nameWithType>

<!-- 

### Affected APIs

-  `T:System.Windows.Forms.RichTextBox` 

-->