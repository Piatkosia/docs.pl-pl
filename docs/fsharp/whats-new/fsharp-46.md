---
title: Co nowego w F# 4,6 — F# Przewodnik
description: Zapoznaj się z omówieniem nowych funkcji dostępnych w F# 4,6.
ms.date: 11/27/2019
ms.openlocfilehash: 81d3e988d044cb16f8ec079118fd0ede2dabc587
ms.sourcegitcommit: 79a2d6a07ba4ed08979819666a0ee6927bbf1b01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/28/2019
ms.locfileid: "74644083"
---
# <a name="whats-new-in-f-46"></a><span data-ttu-id="71ee1-103">Co nowego w F# 4,6</span><span class="sxs-lookup"><span data-stu-id="71ee1-103">What's new in F# 4.6</span></span>

<span data-ttu-id="71ee1-104">F#4,6 dodaje wiele ulepszeń do F# języka.</span><span class="sxs-lookup"><span data-stu-id="71ee1-104">F# 4.6 adds multiple improvements to the F# language.</span></span>

## <a name="get-started"></a><span data-ttu-id="71ee1-105">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="71ee1-105">Get started</span></span>

<span data-ttu-id="71ee1-106">F#4,6 jest dostępny we wszystkich dystrybucjach .NET Core i narzędziach programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="71ee1-106">F# 4.6 is available in all .NET Core distributions and Visual Studio tooling.</span></span> <span data-ttu-id="71ee1-107">[Zacznij korzystać z F# ](../get-started/index.md) programu, aby dowiedzieć się więcej.</span><span class="sxs-lookup"><span data-stu-id="71ee1-107">[Get started with F#](../get-started/index.md) to learn more.</span></span>

## <a name="anonymous-records"></a><span data-ttu-id="71ee1-108">Rekordy anonimowe</span><span class="sxs-lookup"><span data-stu-id="71ee1-108">Anonymous records</span></span>

<span data-ttu-id="71ee1-109">[Rekordy anonimowe](../language-reference/anonymous-records.md) są nowym rodzajem F# typu wprowadzonym F# w 4,6.</span><span class="sxs-lookup"><span data-stu-id="71ee1-109">[Anonymous records](../language-reference/anonymous-records.md) are a new kind of F# type introduced in F# 4.6.</span></span> <span data-ttu-id="71ee1-110">Są to proste zagregowane wartości nazwanych, które nie muszą być zadeklarowane przed użyciem.</span><span class="sxs-lookup"><span data-stu-id="71ee1-110">They are simple aggregates of named values that don't need to be declared before use.</span></span> <span data-ttu-id="71ee1-111">Można zadeklarować je jako struktury lub typy referencyjne.</span><span class="sxs-lookup"><span data-stu-id="71ee1-111">You can declare them as either structs or reference types.</span></span> <span data-ttu-id="71ee1-112">Domyślnie są to typy odwołań.</span><span class="sxs-lookup"><span data-stu-id="71ee1-112">They're reference types by default.</span></span>

```fsharp
open System

let getCircleStats radius =
    let d = radius * 2.0
    let a = Math.PI * (radius ** 2.0)
    let c = 2.0 * Math.PI * radius

    {| Diameter = d; Area = a; Circumference = c |}

let r = 2.0
let stats = getCircleStats r
printfn "Circle with radius: %f has diameter %f, area %f, and circumference %f"
    r stats.Diameter stats.Area stats.Circumference
```

<span data-ttu-id="71ee1-113">Mogą być również zadeklarowane jako struktury dla, gdy chcesz grupować typy wartości i działają w scenariuszach z uwzględnieniem wydajności:</span><span class="sxs-lookup"><span data-stu-id="71ee1-113">They can also be declared as structs for when you want to group value types and are operating in performance-sensitive scenarios:</span></span>

```fsharp
open System

let getCircleStats radius =
    let d = radius * 2.0
    let a = Math.PI * (radius ** 2.0)
    let c = 2.0 * Math.PI * radius

    struct {| Diameter = d; Area = a; Circumference = c |}

let r = 2.0
let stats = getCircleStats r
printfn "Circle with radius: %f has diameter %f, area %f, and circumference %f"
    r stats.Diameter stats.Area stats.Circumference
```

<span data-ttu-id="71ee1-114">Są one bardzo wydajne i mogą być używane w wielu scenariuszach.</span><span class="sxs-lookup"><span data-stu-id="71ee1-114">They're quite powerful and can be used in numerous scenarios.</span></span> <span data-ttu-id="71ee1-115">Dowiedz się więcej z [anonimowymi rekordami](../language-reference/anonymous-records.md).</span><span class="sxs-lookup"><span data-stu-id="71ee1-115">Learn more at [Anonymous records](../language-reference/anonymous-records.md).</span></span>

## <a name="valueoption-functions"></a><span data-ttu-id="71ee1-116">Funkcje ValueOption</span><span class="sxs-lookup"><span data-stu-id="71ee1-116">ValueOption functions</span></span>

<span data-ttu-id="71ee1-117">Typ ValueOption dodany w F# 4,5 ma teraz "parzystość funkcji powiązanej z modułem" z typem opcji.</span><span class="sxs-lookup"><span data-stu-id="71ee1-117">The ValueOption type added in F# 4.5 now has "module-bound function parity" with the Option type.</span></span> <span data-ttu-id="71ee1-118">Poniżej przedstawiono niektóre z najczęściej używanych przykładów:</span><span class="sxs-lookup"><span data-stu-id="71ee1-118">Some of the more commonly-used examples are as follows:</span></span>

```fsharp
// Multiply a value option by 2 if it has  value
let xOpt = ValueSome 99
let result = xOpt |> ValueOption.map (fun v -> v * 2)

// Reverse a string if it exists
let strOpt = ValueSome "Mirror image"
let reverse (str: string) =
    match str with
    | null
    | "" -> None
    | s ->
        str.ToCharArray()
        |> Array.rev
        |> string
        |> Some

let reversedString = strOpt |> Option.bind reverse
```

<span data-ttu-id="71ee1-119">Pozwala to na użycie ValueOption, podobnie jak opcja w scenariuszach, gdzie typ wartości zwiększa wydajność.</span><span class="sxs-lookup"><span data-stu-id="71ee1-119">This allows for ValueOption to be used just like Option in scenarios where having a value type improves performance.</span></span>