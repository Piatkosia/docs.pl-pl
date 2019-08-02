---
title: Azure Functions — aplikacje bezserwerowe
description: Usługa Azure Functions zapewnia bezserwerowe funkcje wC#wielu językach (, JavaScript, Java) i na platformach, aby zapewnić błyskawiczny kod skalowania sterowanego zdarzeniami.
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 06/26/2018
ms.openlocfilehash: 4febcc01eebf3efce3fc1eb42e19c2ec6c0baa52
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/30/2019
ms.locfileid: "68676806"
---
# <a name="azure-functions"></a><span data-ttu-id="cd958-103">Azure Functions</span><span class="sxs-lookup"><span data-stu-id="cd958-103">Azure Functions</span></span>

<span data-ttu-id="cd958-104">Usługa Azure Functions zapewnia środowisko obliczeniowe bezserwerowe.</span><span class="sxs-lookup"><span data-stu-id="cd958-104">Azure functions provide a serverless compute experience.</span></span> <span data-ttu-id="cd958-105">Funkcja jest wywoływana przez *wyzwalacz* (taki jak dostęp do punktu końcowego http lub Timer) i wykonuje blok kodu lub logiki biznesowej.</span><span class="sxs-lookup"><span data-stu-id="cd958-105">A function is invoked by a *trigger* (such as access to an HTTP endpoint or a timer) and executes a block of code or business logic.</span></span> <span data-ttu-id="cd958-106">Funkcje obsługują także wyspecjalizowane *powiązania* , które łączą się z zasobami, takimi jak magazyn i kolejki.</span><span class="sxs-lookup"><span data-stu-id="cd958-106">Functions also support specialized *bindings* that connect to resources like storage and queues.</span></span>

![Logo usługi Azure Functions](./media/azure-functions-logo.png)

<span data-ttu-id="cd958-108">Istnieją dwie wersje platformy Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="cd958-108">There are two versions of the Azure Functions framework.</span></span> <span data-ttu-id="cd958-109">Starsza wersja obsługuje pełne .NET Framework a nowe środowisko uruchomieniowe obsługuje aplikacje platformy .NET Core dla wielu platform.</span><span class="sxs-lookup"><span data-stu-id="cd958-109">The legacy version supports the full .NET Framework and the new runtime supports cross-platform .NET Core applications.</span></span> <span data-ttu-id="cd958-110">Obsługiwane są dodatkowe C# Języki, takie jak F#JavaScript, i Java.</span><span class="sxs-lookup"><span data-stu-id="cd958-110">Additional languages besides C# such as JavaScript, F#, and Java are supported.</span></span> <span data-ttu-id="cd958-111">Funkcje utworzone w portalu zawierają rozbudowaną składnię skryptów.</span><span class="sxs-lookup"><span data-stu-id="cd958-111">Functions created in the portal provide a rich scripting syntax.</span></span> <span data-ttu-id="cd958-112">Funkcje utworzone jako projekty autonomiczne mogą być wdrażane z pełną obsługą platformy i możliwościami.</span><span class="sxs-lookup"><span data-stu-id="cd958-112">Functions created as standalone projects can be deployed with full platform support and capabilities.</span></span>

<span data-ttu-id="cd958-113">Aby uzyskać więcej informacji, zobacz [dokumentację Azure Functions](https://docs.microsoft.com/azure/azure-functions).</span><span class="sxs-lookup"><span data-stu-id="cd958-113">For more information, see [Azure Functions documentation](https://docs.microsoft.com/azure/azure-functions).</span></span>

## <a name="functions-v1-vs-v2"></a><span data-ttu-id="cd958-114">Funkcje V1 i v2</span><span class="sxs-lookup"><span data-stu-id="cd958-114">Functions v1 vs. v2</span></span>

<span data-ttu-id="cd958-115">Istnieją dwie wersje środowiska uruchomieniowego Azure Functions: 1. x i 2. x.</span><span class="sxs-lookup"><span data-stu-id="cd958-115">There are two versions of the Azure Functions runtime: 1.x and 2.x.</span></span> <span data-ttu-id="cd958-116">Wersja 1. x jest ogólnie dostępna (GA).</span><span class="sxs-lookup"><span data-stu-id="cd958-116">Version 1.x is generally available (GA).</span></span> <span data-ttu-id="cd958-117">Obsługuje ona programowanie na platformie .NET z poziomu portalu lub maszyn z systemem Windows i używa .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="cd958-117">It supports .NET development from the portal or Windows machines and uses the .NET Framework.</span></span> <span data-ttu-id="cd958-118">1. x obsługuje C#, JavaScript i F#, z eksperymentalną obsługą języków Python, php, TypeScript, Batch, bash i PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cd958-118">1.x supports C#, JavaScript, and F#, with experimental support for Python, PHP, TypeScript, Batch, Bash, and PowerShell.</span></span>

<span data-ttu-id="cd958-119">W [wersji 2. x jest również ogólnie dostępna](https://azure.microsoft.com/blog/introducing-azure-functions-2-0/).</span><span class="sxs-lookup"><span data-stu-id="cd958-119">[Version 2.x is also generally available now](https://azure.microsoft.com/blog/introducing-azure-functions-2-0/).</span></span> <span data-ttu-id="cd958-120">Wykorzystuje platformę .NET Core i obsługuje programowanie na wielu platformach na maszynach z systemami Windows, macOS i Linux.</span><span class="sxs-lookup"><span data-stu-id="cd958-120">It leverages .NET Core and supports cross-platform development on Windows, macOS, and Linux machines.</span></span> <span data-ttu-id="cd958-121">2. x dodaje obsługę pierwszej klasy dla języka Java, ale nie obsługuje jeszcze bezpośrednio żadnego z języków eksperymentalnych.</span><span class="sxs-lookup"><span data-stu-id="cd958-121">2.x adds first-class support for Java but doesn't yet directly support any of the experimental languages.</span></span> <span data-ttu-id="cd958-122">Wersja 2. x używa nowego modelu rozszerzalności powiązania, który umożliwia korzystanie z rozszerzeń innych firm na platformie, niezależnej wersji powiązań i bardziej usprawnione środowisko wykonawcze.</span><span class="sxs-lookup"><span data-stu-id="cd958-122">Version 2.x uses a new binding extensibility model that enables third-party extensions to the platform, independent versioning of bindings, and a more streamlined execution environment.</span></span>

> <span data-ttu-id="cd958-123">**Występuje znany problem w 1. x z obsługą [przekierowywania powiązań](https://github.com/Azure/azure-functions-host/issues/992).**</span><span class="sxs-lookup"><span data-stu-id="cd958-123">**There is a known issue in 1.x with [binding redirect support](https://github.com/Azure/azure-functions-host/issues/992).**</span></span> <span data-ttu-id="cd958-124">Problem jest specyficzny dla projektowania platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="cd958-124">The issue is specific to .NET development.</span></span> <span data-ttu-id="cd958-125">Dotyczy to projektów z zależnościami w bibliotekach, które są różnymi wersjami z bibliotek uwzględnionych w środowisku uruchomieniowym.</span><span class="sxs-lookup"><span data-stu-id="cd958-125">Projects with dependencies on libraries that are a different version from the libraries included in the runtime are impacted.</span></span> <span data-ttu-id="cd958-126">Zespół ds. funkcji zatwierdził konkretny postęp dla problemu.</span><span class="sxs-lookup"><span data-stu-id="cd958-126">The functions team has committed to making concrete progress on the problem.</span></span> <span data-ttu-id="cd958-127">Zespół będzie kierował przekierowaniami powiązań w 2. x przed przeprowadzeniem ogólnej dostępności.</span><span class="sxs-lookup"><span data-stu-id="cd958-127">The team will address binding redirects in 2.x before it goes into general availability.</span></span> <span data-ttu-id="cd958-128">Oficjalna instrukcja zespołu z sugerowanymi poprawkami i obejściami jest dostępna tutaj: [Rozpoznawanie zestawu w Azure Functions](https://github.com/Azure/azure-functions-host/wiki/Assembly-Resolution-in-Azure-Functions).</span><span class="sxs-lookup"><span data-stu-id="cd958-128">The official team statement with suggested fixes and workarounds is available here: [Assembly resolution in Azure Functions](https://github.com/Azure/azure-functions-host/wiki/Assembly-Resolution-in-Azure-Functions).</span></span>

<span data-ttu-id="cd958-129">Aby uzyskać więcej informacji, zobacz [porównanie 1. x i 2. x](https://docs.microsoft.com/azure/azure-functions/functions-versions).</span><span class="sxs-lookup"><span data-stu-id="cd958-129">For more information, see [Compare 1.x and 2.x](https://docs.microsoft.com/azure/azure-functions/functions-versions).</span></span>

## <a name="programming-language-support"></a><span data-ttu-id="cd958-130">Obsługa języków programowania</span><span class="sxs-lookup"><span data-stu-id="cd958-130">Programming language support</span></span>

<span data-ttu-id="cd958-131">Następujące języki są obsługiwane w ogólnej dostępności (GA), w wersji zapoznawczej lub eksperymentalnej.</span><span class="sxs-lookup"><span data-stu-id="cd958-131">The following languages are supported either in general availability (GA), preview, or experimental.</span></span>

|<span data-ttu-id="cd958-132">Język</span><span class="sxs-lookup"><span data-stu-id="cd958-132">Language</span></span>      |<span data-ttu-id="cd958-133">1.x</span><span class="sxs-lookup"><span data-stu-id="cd958-133">1.x</span></span>         |<span data-ttu-id="cd958-134">2.x</span><span class="sxs-lookup"><span data-stu-id="cd958-134">2.x</span></span>      |
|--------------|------------|---------|
|<span data-ttu-id="cd958-135">**C#**</span><span class="sxs-lookup"><span data-stu-id="cd958-135">**C#**</span></span>        |<span data-ttu-id="cd958-136">POWSZECHNE</span><span class="sxs-lookup"><span data-stu-id="cd958-136">GA</span></span>          |<span data-ttu-id="cd958-137">Wersja zapoznawcza</span><span class="sxs-lookup"><span data-stu-id="cd958-137">Preview</span></span>  |
|<span data-ttu-id="cd958-138">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="cd958-138">**JavaScript**</span></span>|<span data-ttu-id="cd958-139">POWSZECHNE</span><span class="sxs-lookup"><span data-stu-id="cd958-139">GA</span></span>          |<span data-ttu-id="cd958-140">Wersja zapoznawcza</span><span class="sxs-lookup"><span data-stu-id="cd958-140">Preview</span></span>  |
|<span data-ttu-id="cd958-141">**F#**</span><span class="sxs-lookup"><span data-stu-id="cd958-141">**F#**</span></span>        |<span data-ttu-id="cd958-142">POWSZECHNE</span><span class="sxs-lookup"><span data-stu-id="cd958-142">GA</span></span>          |         |
|<span data-ttu-id="cd958-143">**Java**</span><span class="sxs-lookup"><span data-stu-id="cd958-143">**Java**</span></span>      |            |<span data-ttu-id="cd958-144">Wersja zapoznawcza</span><span class="sxs-lookup"><span data-stu-id="cd958-144">Preview</span></span>  |
|<span data-ttu-id="cd958-145">**Python**</span><span class="sxs-lookup"><span data-stu-id="cd958-145">**Python**</span></span>    |<span data-ttu-id="cd958-146">Eksperymentalne</span><span class="sxs-lookup"><span data-stu-id="cd958-146">Experimental</span></span>|         |
|<span data-ttu-id="cd958-147">**PHP**</span><span class="sxs-lookup"><span data-stu-id="cd958-147">**PHP**</span></span>       |<span data-ttu-id="cd958-148">Eksperymentalne</span><span class="sxs-lookup"><span data-stu-id="cd958-148">Experimental</span></span>|         |
|<span data-ttu-id="cd958-149">**TypeScript**</span><span class="sxs-lookup"><span data-stu-id="cd958-149">**TypeScript**</span></span>|<span data-ttu-id="cd958-150">Eksperymentalne</span><span class="sxs-lookup"><span data-stu-id="cd958-150">Experimental</span></span>|         |
|<span data-ttu-id="cd958-151">**Sekwencja**</span><span class="sxs-lookup"><span data-stu-id="cd958-151">**Batch**</span></span>     |<span data-ttu-id="cd958-152">Eksperymentalne</span><span class="sxs-lookup"><span data-stu-id="cd958-152">Experimental</span></span>|         |
|<span data-ttu-id="cd958-153">**Bash**</span><span class="sxs-lookup"><span data-stu-id="cd958-153">**Bash**</span></span>      |<span data-ttu-id="cd958-154">Eksperymentalne</span><span class="sxs-lookup"><span data-stu-id="cd958-154">Experimental</span></span>|         |
|<span data-ttu-id="cd958-155">**Program PowerShell**</span><span class="sxs-lookup"><span data-stu-id="cd958-155">**PowerShell**</span></span>|<span data-ttu-id="cd958-156">Eksperymentalne</span><span class="sxs-lookup"><span data-stu-id="cd958-156">Experimental</span></span>|         |

<span data-ttu-id="cd958-157">Aby uzyskać więcej informacji, zobacz [obsługiwane języki](https://docs.microsoft.com/azure/azure-functions/supported-languages).</span><span class="sxs-lookup"><span data-stu-id="cd958-157">For more information, see [Supported languages](https://docs.microsoft.com/azure/azure-functions/supported-languages).</span></span>

## <a name="app-service-plans"></a><span data-ttu-id="cd958-158">Plany usługi App Service</span><span class="sxs-lookup"><span data-stu-id="cd958-158">App service plans</span></span>

<span data-ttu-id="cd958-159">Funkcje są obsługiwane przez *plan usługi App Service*.</span><span class="sxs-lookup"><span data-stu-id="cd958-159">Functions are backed by an *app service plan*.</span></span> <span data-ttu-id="cd958-160">Plan definiuje zasoby używane przez aplikację Functions.</span><span class="sxs-lookup"><span data-stu-id="cd958-160">The plan defines the resources used by the functions app.</span></span> <span data-ttu-id="cd958-161">Można przypisać plany do regionu, określić rozmiar i liczbę maszyn wirtualnych, które będą używane, i wybrać warstwę cenową.</span><span class="sxs-lookup"><span data-stu-id="cd958-161">You can assign plans to a region, determine the size and number of virtual machines that will be used, and pick a pricing tier.</span></span> <span data-ttu-id="cd958-162">W przypadku prawdziwej metody bezserwerowej aplikacje funkcji mogą korzystać z planu **zużycia** .</span><span class="sxs-lookup"><span data-stu-id="cd958-162">For a true serverless approach, function apps may use the **consumption** plan.</span></span> <span data-ttu-id="cd958-163">Plan zużycia spowoduje automatyczne skalowanie zaplecza na podstawie obciążenia.</span><span class="sxs-lookup"><span data-stu-id="cd958-163">The consumption plan will scale the back end automatically based on load.</span></span>

<span data-ttu-id="cd958-164">Aby uzyskać więcej informacji, zobacz [plany usługi App Service](https://docs.microsoft.com/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview).</span><span class="sxs-lookup"><span data-stu-id="cd958-164">For more information, see [App service plans](https://docs.microsoft.com/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview).</span></span>

## <a name="create-your-first-function"></a><span data-ttu-id="cd958-165">Tworzenie pierwszej funkcji</span><span class="sxs-lookup"><span data-stu-id="cd958-165">Create your first function</span></span>

<span data-ttu-id="cd958-166">Istnieją trzy typowe sposoby tworzenia aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="cd958-166">There are three common ways you can create function apps.</span></span>

* <span data-ttu-id="cd958-167">Funkcje skryptów w portalu.</span><span class="sxs-lookup"><span data-stu-id="cd958-167">Script functions in the portal.</span></span>
* <span data-ttu-id="cd958-168">Tworzenie niezbędnych zasobów przy użyciu interfejsu wiersza polecenia platformy Azure (CLI).</span><span class="sxs-lookup"><span data-stu-id="cd958-168">Create the necessary resources using the Azure Command Line Interface (CLI).</span></span>
* <span data-ttu-id="cd958-169">Twórz funkcje lokalnie przy użyciu ulubionego środowiska IDE i publikuj je na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="cd958-169">Build functions locally using your favorite IDE and publish them to Azure.</span></span>

<span data-ttu-id="cd958-170">Aby uzyskać więcej informacji na temat tworzenia funkcji skryptowej w portalu, zobacz [Tworzenie pierwszej funkcji w Azure Portal](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function).</span><span class="sxs-lookup"><span data-stu-id="cd958-170">For more information on creating a scripted function in the portal, see [Create your first function in the Azure portal](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function).</span></span>

<span data-ttu-id="cd958-171">Aby skompilować z poziomu interfejsu wiersza polecenia platformy Azure, zobacz [Tworzenie pierwszej funkcji przy użyciu interfejsu wiersza polecenia platformy Azure](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="cd958-171">To build from the Azure CLI, see [Create your first function using the Azure CLI](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function-azure-cli).</span></span>

<span data-ttu-id="cd958-172">Aby utworzyć funkcję z programu Visual Studio, zobacz [Tworzenie pierwszej funkcji przy użyciu programu Visual Studio](https://docs.microsoft.com/azure/azure-functions/functions-create-your-first-function-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="cd958-172">To create a function from Visual Studio, see [Create your first function using Visual Studio](https://docs.microsoft.com/azure/azure-functions/functions-create-your-first-function-visual-studio).</span></span>

## <a name="understand-triggers-and-bindings"></a><span data-ttu-id="cd958-173">Omówienie wyzwalaczy i powiązań</span><span class="sxs-lookup"><span data-stu-id="cd958-173">Understand triggers and bindings</span></span>

<span data-ttu-id="cd958-174">Funkcje są wywoływane przez *wyzwalacz* i mogą mieć dokładnie jeden.</span><span class="sxs-lookup"><span data-stu-id="cd958-174">Functions are invoked by a *trigger* and can have exactly one.</span></span> <span data-ttu-id="cd958-175">Oprócz wywoływania funkcji, niektóre wyzwalacze również pełnią rolę powiązań.</span><span class="sxs-lookup"><span data-stu-id="cd958-175">In addition to invoking the function, certain triggers also serve as bindings.</span></span> <span data-ttu-id="cd958-176">Oprócz wyzwalacza można również zdefiniować wiele powiązań.</span><span class="sxs-lookup"><span data-stu-id="cd958-176">You may also define multiple bindings in addition to the trigger.</span></span> <span data-ttu-id="cd958-177">*Powiązania* zapewniają deklaratywny sposób łączenia danych z kodem.</span><span class="sxs-lookup"><span data-stu-id="cd958-177">*Bindings* provide a declarative way to connect data to your code.</span></span> <span data-ttu-id="cd958-178">Mogą być przekazywane (dane wejściowe) lub odbierać dane (dane wyjściowe).</span><span class="sxs-lookup"><span data-stu-id="cd958-178">They can be passed in (input) or receive data (output).</span></span> <span data-ttu-id="cd958-179">Wyzwalacze i powiązania ułatwiają korzystanie z funkcji.</span><span class="sxs-lookup"><span data-stu-id="cd958-179">Triggers and bindings make functions easy to work with.</span></span> <span data-ttu-id="cd958-180">Powiązania usuwają koszty ręcznego tworzenia połączeń bazy danych lub systemu plików.</span><span class="sxs-lookup"><span data-stu-id="cd958-180">Bindings remove the overhead of manually creating database or file system connections.</span></span> <span data-ttu-id="cd958-181">Wszystkie informacje dotyczące powiązań są zawarte w specjalnym pliku *Functions. JSON* dla skryptów lub zadeklarowane z atrybutami w kodzie.</span><span class="sxs-lookup"><span data-stu-id="cd958-181">All of the information needed for the bindings is contained in a special *functions.json* file for scripts or declared with attributes in code.</span></span>

<span data-ttu-id="cd958-182">Niektóre typowe wyzwalacze obejmują:</span><span class="sxs-lookup"><span data-stu-id="cd958-182">Some common triggers include:</span></span>

* <span data-ttu-id="cd958-183">Blob Storage: wywołaj funkcję, gdy plik lub folder zostanie przekazany lub zmieniony w magazynie.</span><span class="sxs-lookup"><span data-stu-id="cd958-183">Blob Storage: invoke your function when a file or folder is uploaded or changed in storage.</span></span>
* <span data-ttu-id="cd958-184">HTTP: wywoływanie funkcji, takiej jak interfejs API REST.</span><span class="sxs-lookup"><span data-stu-id="cd958-184">HTTP: invoke your function like a REST API.</span></span>
* <span data-ttu-id="cd958-185">Kolejka: wywoływanie funkcji, gdy istnieją elementy w kolejce.</span><span class="sxs-lookup"><span data-stu-id="cd958-185">Queue: invoke your function when items exist in a queue.</span></span>
* <span data-ttu-id="cd958-186">Czasomierz: wywołaj funkcję na zwykłych erze.</span><span class="sxs-lookup"><span data-stu-id="cd958-186">Timer: invoke your function on a regular cadence.</span></span>

<span data-ttu-id="cd958-187">Przykłady powiązań obejmują:</span><span class="sxs-lookup"><span data-stu-id="cd958-187">Examples of bindings include:</span></span>

* <span data-ttu-id="cd958-188">CosmosDB: łatwo Nawiązuj połączenie z bazą danych w celu załadowania lub zapisania plików.</span><span class="sxs-lookup"><span data-stu-id="cd958-188">CosmosDB: easily connect to the database to load or save files.</span></span>
* <span data-ttu-id="cd958-189">Table Storage: Pracuj z magazynem kluczy/wartości z aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="cd958-189">Table Storage: work with key/value storage from your function app.</span></span>
* <span data-ttu-id="cd958-190">Queue Storage: łatwo Pobieraj elementy z kolejki lub umieszczaj nowe elementy w kolejce.</span><span class="sxs-lookup"><span data-stu-id="cd958-190">Queue Storage: easily retrieve items from a queue, or place new items on the queue.</span></span>

<span data-ttu-id="cd958-191">Poniższy przykładowy plik *Functions. JSON* definiuje wyzwalacz i powiązanie:</span><span class="sxs-lookup"><span data-stu-id="cd958-191">The following example *functions.json* file defines a trigger and a binding:</span></span>

```json
{
  "bindings": [
    {
      "name": "myBlob",
      "type": "blobTrigger",
      "direction": "in",
      "path": "images/{name}",
      "connection": "AzureWebJobsStorage"
    },
    {
      "name": "$return",
      "type": "queue",
      "direction": "out",
      "queueName": "images",
      "connection": "AzureWebJobsStorage"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="cd958-192">W tym przykładzie funkcja jest wyzwalana przez zmianę w magazynie obiektów BLOB w `images` kontenerze.</span><span class="sxs-lookup"><span data-stu-id="cd958-192">In this example, the function is triggered by a change to blob storage in the `images` container.</span></span> <span data-ttu-id="cd958-193">Informacje dotyczące pliku są przesyłane, więc wyzwalacz działa również jako powiązanie.</span><span class="sxs-lookup"><span data-stu-id="cd958-193">The information for the file is passed in, so the trigger also acts as a binding.</span></span> <span data-ttu-id="cd958-194">Istnieje inne powiązanie, aby umieścić informacje w kolejce o `images`nazwie.</span><span class="sxs-lookup"><span data-stu-id="cd958-194">Another binding exists to put information onto a queue named `images`.</span></span>

<span data-ttu-id="cd958-195">Oto C# skrypt dla funkcji:</span><span class="sxs-lookup"><span data-stu-id="cd958-195">Here is the C# script for the function:</span></span>

```csharp
public static string Run(Stream myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
    return name;
}
```

<span data-ttu-id="cd958-196">Przykładem jest prosta funkcja, która przyjmuje nazwę pliku, który został zmodyfikowany lub przekazany do usługi BLOB Storage, i umieszcza go w kolejce do późniejszego przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="cd958-196">The example is a simple function that takes the name of the file that was modified or uploaded to blob storage, and places it on a queue for later processing.</span></span>

<span data-ttu-id="cd958-197">Aby zapoznać się z pełną listą wyzwalaczy i powiązań, zobacz temat [Azure Functions wyzwalacze i koncepcje powiązań](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings).</span><span class="sxs-lookup"><span data-stu-id="cd958-197">For a full list of triggers and bindings, see [Azure Functions triggers and bindings concepts](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings).</span></span>

## <a name="proxies"></a><span data-ttu-id="cd958-198">Serwery proxy</span><span class="sxs-lookup"><span data-stu-id="cd958-198">Proxies</span></span>

<span data-ttu-id="cd958-199">Serwery proxy zapewniają funkcję przekierowywania dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cd958-199">Proxies provide redirect functionality for your application.</span></span> <span data-ttu-id="cd958-200">Serwery proxy uwidaczniają punkt końcowy i mapują ten punkt końcowy na inny zasób.</span><span class="sxs-lookup"><span data-stu-id="cd958-200">Proxies expose an endpoint and map that endpoint to another resource.</span></span> <span data-ttu-id="cd958-201">Dzięki serwerom proxy można:</span><span class="sxs-lookup"><span data-stu-id="cd958-201">With proxies, you can:</span></span>

* <span data-ttu-id="cd958-202">Przekieruj żądanie przychodzące do innego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="cd958-202">Reroute an incoming request to another endpoint.</span></span>
* <span data-ttu-id="cd958-203">Zmodyfikuj żądanie przychodzące przed jego przekazaniem.</span><span class="sxs-lookup"><span data-stu-id="cd958-203">Modify the incoming request before it's passed along.</span></span>
* <span data-ttu-id="cd958-204">Zmodyfikuj lub Podaj odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="cd958-204">Modify or provide a response.</span></span>

<span data-ttu-id="cd958-205">Serwery proxy są używane w scenariuszach takich jak:</span><span class="sxs-lookup"><span data-stu-id="cd958-205">Proxies are used for scenarios such as:</span></span>

* <span data-ttu-id="cd958-206">Uproszczenie, skrócenie lub zmiana adresu URL.</span><span class="sxs-lookup"><span data-stu-id="cd958-206">Simplifying, shortening, or changing the URL.</span></span>
* <span data-ttu-id="cd958-207">Zapewnianie spójnego prefiksu interfejsu API dla wielu usług zaplecza.</span><span class="sxs-lookup"><span data-stu-id="cd958-207">Providing a consistent API prefix to multiple back-end services.</span></span>
* <span data-ttu-id="cd958-208">Imitacja odpowiedzi na opracowywany punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="cd958-208">Mocking a response to an endpoint being developed.</span></span>
* <span data-ttu-id="cd958-209">Dostarczanie statycznej odpowiedzi do dobrze znanego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="cd958-209">Providing a static response to a well-known endpoint.</span></span>
* <span data-ttu-id="cd958-210">Utrzymywanie spójności punktu końcowego interfejsu API podczas przenoszenia lub migrowania zaplecza.</span><span class="sxs-lookup"><span data-stu-id="cd958-210">Keeping an API endpoint consistent while the back end is moved or migrated.</span></span>

<span data-ttu-id="cd958-211">Serwery proxy są przechowywane jako definicje JSON.</span><span class="sxs-lookup"><span data-stu-id="cd958-211">Proxies are stored as JSON definitions.</span></span> <span data-ttu-id="cd958-212">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="cd958-212">Here is an example:</span></span>

```json
{
  "$schema": "http://json.schemastore.org/proxies",
  "proxies": {
    "Domain Redirect": {
      "matchCondition": {
        "route": "/{shortUrl}"
      },
      "backendUri": "http://%WEBSITE_HOSTNAME%/api/UrlRedirect/{shortUrl}"
    },
    "Root": {
      "matchCondition": {
        "route": "/"
      },
      "responseOverrides": {
        "response.statusCode": "301",
        "response.statusReason": "Moved Permanently",
        "response.headers.location": "https://docs.microsoft.com/"
      }
    }
  }
}
```

<span data-ttu-id="cd958-213">`Domain Redirect` Serwer proxy przyjmuje skróconą trasę i mapuje go do zasobu o większej funkcji.</span><span class="sxs-lookup"><span data-stu-id="cd958-213">The `Domain Redirect` proxy takes a shortened route and maps it to the longer function resource.</span></span> <span data-ttu-id="cd958-214">Transformacja wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="cd958-214">The transformation looks like:</span></span>

`https://--shorturl--/123` -> `https://--longurl--.azurewebsites.net/api/UrlRedirect/123`

<span data-ttu-id="cd958-215">Serwer proxy wykonuje wszystkie czynności wysyłane do głównego adresu URL`https://--shorturl--/`() i przekierowuje go do witryny dokumentacji. `Root`</span><span class="sxs-lookup"><span data-stu-id="cd958-215">The `Root` proxy takes anything sent to the root URL (`https://--shorturl--/`) and redirects it to the documentation site.</span></span>

<span data-ttu-id="cd958-216">Przykład korzystania z serwerów proxy przedstawiono na platformie Azure wideo [: Przenieś swoją aplikację do chmury, korzystając z bezserwerowego Azure Functions](https://channel9.msdn.com/events/Connect/2017/E102).</span><span class="sxs-lookup"><span data-stu-id="cd958-216">An example of using proxies is shown in the video [Azure: Bring your app to the cloud with serverless Azure Functions](https://channel9.msdn.com/events/Connect/2017/E102).</span></span> <span data-ttu-id="cd958-217">W czasie rzeczywistym aplikacja ASP.NET Core uruchomiona na lokalnym SQL Server jest migrowana do chmury platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cd958-217">In real time, an ASP.NET Core application running on local SQL Server is migrated to the Azure Cloud.</span></span> <span data-ttu-id="cd958-218">Serwery proxy służą do refaktoryzacji tradycyjnego projektu interfejsu API sieci Web do korzystania z funkcji.</span><span class="sxs-lookup"><span data-stu-id="cd958-218">Proxies are used to help refactor a traditional Web API project to use functions.</span></span>

<span data-ttu-id="cd958-219">Aby uzyskać więcej informacji na temat serwerów proxy, zobacz [Work with serwery proxy usługi Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-proxies).</span><span class="sxs-lookup"><span data-stu-id="cd958-219">For more information about Proxies, see [Work with Azure Functions Proxies](https://docs.microsoft.com/azure/azure-functions/functions-proxies).</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="cd958-220">[Poprzedni](azure-serverless-platform.md)Następny
>[](application-insights.md)</span><span class="sxs-lookup"><span data-stu-id="cd958-220">[Previous](azure-serverless-platform.md)
[Next](application-insights.md)</span></span>