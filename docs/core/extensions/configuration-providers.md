---
title: Dostawcy konfiguracji w programie .NET
description: Dowiedz się, w jaki sposób interfejs API dostawcy konfiguracji jest używany do konfigurowania aplikacji platformy .NET.
author: IEvangelist
ms.author: dapine
ms.date: 09/16/2020
ms.openlocfilehash: d5333e8e52feb7d28e2149a988dc7ce53a926a50
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "90874750"
---
# <a name="configuration-providers-in-net"></a><span data-ttu-id="bf385-103">Dostawcy konfiguracji w programie .NET</span><span class="sxs-lookup"><span data-stu-id="bf385-103">Configuration providers in .NET</span></span>

<span data-ttu-id="bf385-104">Konfiguracja w programie .NET jest możliwa z dostawcami konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="bf385-104">Configuration in .NET is possible with configuration providers.</span></span> <span data-ttu-id="bf385-105">Istnieje kilka typów dostawców korzystających z różnych źródeł konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="bf385-105">There are several types of providers that rely on various configuration sources.</span></span> <span data-ttu-id="bf385-106">Ten artykuł zawiera szczegółowe informacje o różnych dostawcach konfiguracji i odpowiednich źródłach.</span><span class="sxs-lookup"><span data-stu-id="bf385-106">This article details all of the different configuration providers and their corresponding sources.</span></span>

- [<span data-ttu-id="bf385-107">Dostawca konfiguracji plików</span><span class="sxs-lookup"><span data-stu-id="bf385-107">File configuration provider</span></span>](#file-configuration-provider)
- [<span data-ttu-id="bf385-108">Dostawca konfiguracji zmiennej środowiskowej</span><span class="sxs-lookup"><span data-stu-id="bf385-108">Environment variable configuration provider</span></span>](#environment-variable-configuration-provider)
- [<span data-ttu-id="bf385-109">Dostawca konfiguracji wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="bf385-109">Command-line configuration provider</span></span>](#command-line-configuration-provider)
- [<span data-ttu-id="bf385-110">Dostawca konfiguracji klucza dla plików</span><span class="sxs-lookup"><span data-stu-id="bf385-110">Key-per-file configuration provider</span></span>](#key-per-file-configuration-provider)
- [<span data-ttu-id="bf385-111">Dostawca konfiguracji pamięci</span><span class="sxs-lookup"><span data-stu-id="bf385-111">Memory configuration provider</span></span>](#memory-configuration-provider)

## <a name="file-configuration-provider"></a><span data-ttu-id="bf385-112">Dostawca konfiguracji plików</span><span class="sxs-lookup"><span data-stu-id="bf385-112">File configuration provider</span></span>

<span data-ttu-id="bf385-113"><xref:Microsoft.Extensions.Configuration.FileConfigurationProvider> jest klasą bazową do ładowania konfiguracji z systemu plików.</span><span class="sxs-lookup"><span data-stu-id="bf385-113"><xref:Microsoft.Extensions.Configuration.FileConfigurationProvider> is the base class for loading configuration from the file system.</span></span> <span data-ttu-id="bf385-114">Następujący dostawcy konfiguracji pochodzą z `FileConfigurationProvider` :</span><span class="sxs-lookup"><span data-stu-id="bf385-114">The following configuration providers derive from `FileConfigurationProvider`:</span></span>

- [<span data-ttu-id="bf385-115">Dostawca konfiguracji JSON</span><span class="sxs-lookup"><span data-stu-id="bf385-115">JSON configuration provider</span></span>](#json-configuration-provider)
- [<span data-ttu-id="bf385-116">Dostawca konfiguracji XML</span><span class="sxs-lookup"><span data-stu-id="bf385-116">XML configuration provider</span></span>](#xml-configuration-provider)
- [<span data-ttu-id="bf385-117">Dostawca konfiguracji pliku INI</span><span class="sxs-lookup"><span data-stu-id="bf385-117">INI configuration provider</span></span>](#ini-configuration-provider)

### <a name="json-configuration-provider"></a><span data-ttu-id="bf385-118">Dostawca konfiguracji JSON</span><span class="sxs-lookup"><span data-stu-id="bf385-118">JSON configuration provider</span></span>

<span data-ttu-id="bf385-119"><xref:Microsoft.Extensions.Configuration.Json.JsonConfigurationProvider>Klasa ładuje konfigurację z pliku JSON.</span><span class="sxs-lookup"><span data-stu-id="bf385-119">The <xref:Microsoft.Extensions.Configuration.Json.JsonConfigurationProvider> class loads configuration from a JSON file.</span></span> <span data-ttu-id="bf385-120">Zainstaluj [`Microsoft.Extensions.Configuration.Json`](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.Json) pakiet NuGet.</span><span class="sxs-lookup"><span data-stu-id="bf385-120">Install the [`Microsoft.Extensions.Configuration.Json`](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.Json) NuGet package.</span></span>

<span data-ttu-id="bf385-121">Przeciążenia mogą określać:</span><span class="sxs-lookup"><span data-stu-id="bf385-121">Overloads can specify:</span></span>

- <span data-ttu-id="bf385-122">Czy plik jest opcjonalny</span><span class="sxs-lookup"><span data-stu-id="bf385-122">Whether the file is optional</span></span>
- <span data-ttu-id="bf385-123">Czy konfiguracja zostanie ponownie załadowana w przypadku zmiany pliku</span><span class="sxs-lookup"><span data-stu-id="bf385-123">Whether the configuration is reloaded if the file changes</span></span>

<span data-ttu-id="bf385-124">Spójrzmy na poniższy kod:</span><span class="sxs-lookup"><span data-stu-id="bf385-124">Consider the following code:</span></span>

:::code language="csharp" source="snippets/configuration/console-json/Program.cs" range="1-33,37-38" highlight="17-23":::

<span data-ttu-id="bf385-125">Powyższy kod ma następujące działanie:</span><span class="sxs-lookup"><span data-stu-id="bf385-125">The preceding code:</span></span>

- <span data-ttu-id="bf385-126">Czyści wszystkich istniejących dostawców konfiguracji, którzy zostali dodani domyślnie w <xref:Microsoft.Extensions.Hosting.Host.CreateDefaultBuilder(System.String[])> metodzie.</span><span class="sxs-lookup"><span data-stu-id="bf385-126">Clears all existing configuration providers that were added by default in the <xref:Microsoft.Extensions.Hosting.Host.CreateDefaultBuilder(System.String[])> method.</span></span>
- <span data-ttu-id="bf385-127">Konfiguruje dostawcę konfiguracji JSON w celu załadowania *appsettings.jsw* i  *AppSettings* `Environment` . pliki *JSON* z następującymi opcjami:</span><span class="sxs-lookup"><span data-stu-id="bf385-127">Configures the JSON configuration provider to load the *appsettings.json* and  *appsettings*.`Environment`.*json* files with the following options:</span></span>
  - <span data-ttu-id="bf385-128">`optional: true`: Plik jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="bf385-128">`optional: true`: The file is optional.</span></span>
  - <span data-ttu-id="bf385-129">`reloadOnChange: true` : Plik zostanie ponownie załadowany podczas zapisywania zmian.</span><span class="sxs-lookup"><span data-stu-id="bf385-129">`reloadOnChange: true` : The file is reloaded when changes are saved.</span></span>

<span data-ttu-id="bf385-130">Ustawienia JSON są zastępowane przez ustawienia w obszarze [dostawca konfiguracji zmiennych środowiskowych](#environment-variable-configuration-provider) i [dostawca konfiguracji wiersza polecenia](#command-line-configuration-provider).</span><span class="sxs-lookup"><span data-stu-id="bf385-130">The JSON settings are overridden by settings in the [Environment variables configuration provider](#environment-variable-configuration-provider) and the [Command-line configuration provider](#command-line-configuration-provider).</span></span>

<span data-ttu-id="bf385-131">Przykład *appsettings.jsw* pliku z różnymi ustawieniami konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="bf385-131">An example *appsettings.json* file with various configuration settings follows:</span></span>

:::code language="json" source="snippets/configuration/console-json/appsettings.json":::

<span data-ttu-id="bf385-132">Z tego <xref:Microsoft.Extensions.Configuration.IConfigurationBuilder> wystąpienia po dodaniu dostawców konfiguracji można wywołać, <xref:Microsoft.Extensions.Configuration.IConfigurationBuilder.Build?displayProperty=nameWithType> Aby uzyskać <xref:Microsoft.Extensions.Configuration.IConfigurationRoot> obiekt.</span><span class="sxs-lookup"><span data-stu-id="bf385-132">From the <xref:Microsoft.Extensions.Configuration.IConfigurationBuilder> instance, after configuration providers have been added you can call <xref:Microsoft.Extensions.Configuration.IConfigurationBuilder.Build?displayProperty=nameWithType> to get the <xref:Microsoft.Extensions.Configuration.IConfigurationRoot> object.</span></span> <span data-ttu-id="bf385-133">Katalog główny konfiguracji reprezentuje element główny hierarchii konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="bf385-133">The configuration root represents the root of a configuration hierarchy.</span></span> <span data-ttu-id="bf385-134">Sekcje z konfiguracji można powiązać z wystąpieniami obiektów .NET i w późniejszym czasie <xref:Microsoft.Extensions.Options.IOptions%601> za pośrednictwem iniekcji zależności.</span><span class="sxs-lookup"><span data-stu-id="bf385-134">Sections from the configuration can be bound to instances of .NET objects, and later provided as <xref:Microsoft.Extensions.Options.IOptions%601> through dependency injection.</span></span>

<span data-ttu-id="bf385-135">Należy wziąć pod uwagę `TransientFaultHandlingOptions` Typ rekordu zdefiniowany w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="bf385-135">Consider the `TransientFaultHandlingOptions` record type defined as follows:</span></span>

:::code language="csharp" source="snippets/configuration/console-json/TransientFaultHandlingOptions.cs":::

<span data-ttu-id="bf385-136">Aby uzyskać informacje na temat typów rekordów, zobacz [typy rekordów w języku C# 9](../../csharp/whats-new/csharp-9.md#record-types).</span><span class="sxs-lookup"><span data-stu-id="bf385-136">For information on record types, see [Record types in C# 9](../../csharp/whats-new/csharp-9.md#record-types).</span></span>

<span data-ttu-id="bf385-137">Poniższy kod kompiluje katalog główny konfiguracji, tworzy powiązanie sekcji z `TransientFaultHandlingOptions` typem rekordu i drukuje powiązane wartości do okna konsoli:</span><span class="sxs-lookup"><span data-stu-id="bf385-137">The following code builds the configuration root, binds a section to the `TransientFaultHandlingOptions` record type, and prints the bound values to the console window:</span></span>

:::code language="csharp" source="snippets/configuration/console-json/Program.cs" range="25-32":::

<span data-ttu-id="bf385-138">Aplikacja zapisze następujące przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="bf385-138">The application would write the following sample output:</span></span>

:::code language="csharp" source="snippets/configuration/console-json/Program.cs" range="34-36":::

### <a name="xml-configuration-provider"></a><span data-ttu-id="bf385-139">Dostawca konfiguracji XML</span><span class="sxs-lookup"><span data-stu-id="bf385-139">XML configuration provider</span></span>

<span data-ttu-id="bf385-140"><xref:Microsoft.Extensions.Configuration.Xml.XmlConfigurationProvider>Klasa ładuje konfigurację z pliku XML w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="bf385-140">The <xref:Microsoft.Extensions.Configuration.Xml.XmlConfigurationProvider> class loads configuration from an XML file at runtime.</span></span> <span data-ttu-id="bf385-141">Zainstaluj [`Microsoft.Extensions.Configuration.Xml`](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.Xml) pakiet NuGet.</span><span class="sxs-lookup"><span data-stu-id="bf385-141">Install the [`Microsoft.Extensions.Configuration.Xml`](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.Xml) NuGet package.</span></span>

<span data-ttu-id="bf385-142">Poniższy kod ilustruje konfigurację plików XML przy użyciu dostawcy konfiguracji XML.</span><span class="sxs-lookup"><span data-stu-id="bf385-142">The following code demonstrates configuration of XML files using the XML configuration provider.</span></span>

:::code language="csharp" source="snippets/configuration/console-xml/Program.cs" range="1-28,46,52-53" highlight="17-28":::

<span data-ttu-id="bf385-143">Powyższy kod ma następujące działanie:</span><span class="sxs-lookup"><span data-stu-id="bf385-143">The preceding code:</span></span>

- <span data-ttu-id="bf385-144">Czyści wszystkich istniejących dostawców konfiguracji, którzy zostali dodani domyślnie w <xref:Microsoft.Extensions.Hosting.Host.CreateDefaultBuilder(System.String[])> metodzie.</span><span class="sxs-lookup"><span data-stu-id="bf385-144">Clears all existing configuration providers that were added by default in the <xref:Microsoft.Extensions.Hosting.Host.CreateDefaultBuilder(System.String[])> method.</span></span>
- <span data-ttu-id="bf385-145">Konfiguruje dostawcę konfiguracji XML do ładowania *appsettings.xml* i *repeating-example.xml* plików z następującymi opcjami:</span><span class="sxs-lookup"><span data-stu-id="bf385-145">Configures the XML configuration provider to load the *appsettings.xml* and *repeating-example.xml* files with the following options:</span></span>
  - <span data-ttu-id="bf385-146">`optional: true`: Plik jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="bf385-146">`optional: true`: The file is optional.</span></span>
  - <span data-ttu-id="bf385-147">`reloadOnChange: true` : Plik zostanie ponownie załadowany podczas zapisywania zmian.</span><span class="sxs-lookup"><span data-stu-id="bf385-147">`reloadOnChange: true` : The file is reloaded when changes are saved.</span></span>
- <span data-ttu-id="bf385-148">Konfiguruje dostawcę konfiguracji zmiennych środowiskowych.</span><span class="sxs-lookup"><span data-stu-id="bf385-148">Configures the environment variables configuration provider.</span></span>
- <span data-ttu-id="bf385-149">Konfiguruje dostawcę konfiguracji wiersza polecenia, jeśli podano `args` argumenty.</span><span class="sxs-lookup"><span data-stu-id="bf385-149">Configures the command-line configuration provider if the given `args` contains arguments.</span></span>

<span data-ttu-id="bf385-150">Ustawienia XML są zastępowane przez ustawienia w obszarze [dostawca konfiguracji zmiennych środowiskowych](#environment-variable-configuration-provider) i [dostawca konfiguracji wiersza polecenia](#command-line-configuration-provider).</span><span class="sxs-lookup"><span data-stu-id="bf385-150">The XML settings are overridden by settings in the [Environment variables configuration provider](#environment-variable-configuration-provider) and the [Command-line configuration provider](#command-line-configuration-provider).</span></span>

<span data-ttu-id="bf385-151">Przykładowy plik *appsettings.xml* z różnymi ustawieniami konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="bf385-151">An example *appsettings.xml* file with various configuration settings follows:</span></span>

:::code language="xml" source="snippets/configuration/console-xml/appsettings.xml":::

<span data-ttu-id="bf385-152">Powtarzające się elementy, które używają tej samej nazwy elementu, działają, jeśli `name` atrybut jest używany do odróżnienia elementów:</span><span class="sxs-lookup"><span data-stu-id="bf385-152">Repeating elements that use the same element name work if the `name` attribute is used to distinguish the elements:</span></span>

:::code language="xml" source="snippets/configuration/console-xml/repeating-example.xml":::

<span data-ttu-id="bf385-153">Poniższy kod odczytuje poprzedni plik konfiguracji i wyświetla klucze i wartości:</span><span class="sxs-lookup"><span data-stu-id="bf385-153">The following code reads the previous configuration file and displays the keys and values:</span></span>

:::code language="csharp" source="snippets/configuration/console-xml/Program.cs" range="30-45":::

<span data-ttu-id="bf385-154">Aplikacja zapisze następujące przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="bf385-154">The application would write the following sample output:</span></span>

:::code language="csharp" source="snippets/configuration/console-xml/Program.cs" range="47-51":::

<span data-ttu-id="bf385-155">Atrybuty mogą służyć do dostarczania wartości:</span><span class="sxs-lookup"><span data-stu-id="bf385-155">Attributes can be used to supply values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <key attribute="value" />
  <section>
    <key attribute="value" />
  </section>
</configuration>
```

<span data-ttu-id="bf385-156">Poprzedni plik konfiguracji ładuje następujące klucze z `value` :</span><span class="sxs-lookup"><span data-stu-id="bf385-156">The previous configuration file loads the following keys with `value`:</span></span>

- `key:attribute`
- `section:key:attribute`

### <a name="ini-configuration-provider"></a><span data-ttu-id="bf385-157">Dostawca konfiguracji pliku INI</span><span class="sxs-lookup"><span data-stu-id="bf385-157">INI configuration provider</span></span>

<span data-ttu-id="bf385-158"><xref:Microsoft.Extensions.Configuration.Ini.IniConfigurationProvider>Klasa ładuje konfigurację z pliku ini w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="bf385-158">The <xref:Microsoft.Extensions.Configuration.Ini.IniConfigurationProvider> class loads configuration from an INI file at runtime.</span></span> <span data-ttu-id="bf385-159">Zainstaluj [`Microsoft.Extensions.Configuration.Ini`](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.Ini)  pakiet NuGet.</span><span class="sxs-lookup"><span data-stu-id="bf385-159">Install the [`Microsoft.Extensions.Configuration.Ini`](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.Ini)  NuGet package.</span></span>

<span data-ttu-id="bf385-160">Poniższy kod czyści wszystkich dostawców konfiguracji i dodaje `IniConfigurationProvider` dwa pliki ini jako Źródło:</span><span class="sxs-lookup"><span data-stu-id="bf385-160">The following code clears all the configuration providers and adds the `IniConfigurationProvider` with two INI files as the source:</span></span>

:::code language="csharp" source="snippets/configuration/console-ini/Program.cs" range="1-31,38-39" highlight="18-24":::

<span data-ttu-id="bf385-161">Przykładowy plik *appsettings.ini* z różnymi ustawieniami konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="bf385-161">An example *appsettings.ini* file with various configuration settings follows:</span></span>

:::code language="ini" source="snippets/configuration/console-ini/appsettings.ini":::

<span data-ttu-id="bf385-162">Poniższy kod wyświetla poprzednie ustawienia konfiguracji, pisząc je w oknie konsoli:</span><span class="sxs-lookup"><span data-stu-id="bf385-162">The following code displays the preceding configuration settings by writing them to the console window:</span></span>

:::code language="csharp" source="snippets/configuration/console-ini/Program.cs" range="26-30":::

<span data-ttu-id="bf385-163">Aplikacja zapisze następujące przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="bf385-163">The application would write the following sample output:</span></span>

:::code language="csharp" source="snippets/configuration/console-ini/Program.cs" range="32-37":::

## <a name="environment-variable-configuration-provider"></a><span data-ttu-id="bf385-164">Dostawca konfiguracji zmiennej środowiskowej</span><span class="sxs-lookup"><span data-stu-id="bf385-164">Environment variable configuration provider</span></span>

<span data-ttu-id="bf385-165">Przy użyciu konfiguracji domyślnej, <xref:Microsoft.Extensions.Configuration.EnvironmentVariables.EnvironmentVariablesConfigurationProvider> Ładowanie konfiguracji ze zmiennej środowiskowej par klucz-wartość po czytaniu *appsettings.jsw*, *appSettings.* `Environment` *. JSON*i Menedżer wpisów tajnych.</span><span class="sxs-lookup"><span data-stu-id="bf385-165">Using the default configuration, the <xref:Microsoft.Extensions.Configuration.EnvironmentVariables.EnvironmentVariablesConfigurationProvider> loads configuration from environment variable key-value pairs after reading *appsettings.json*, *appsettings.*`Environment`*.json*, and Secret manager.</span></span> <span data-ttu-id="bf385-166">W związku z tym kluczowe wartości są odczytywane z wartości zastąpienia środowiska odczytywane z *appsettings.jsw*, *appSettings.* `Environment` *. JSON*i Menedżer wpisów tajnych.</span><span class="sxs-lookup"><span data-stu-id="bf385-166">Therefore, key values read from the environment override values read from *appsettings.json*, *appsettings.*`Environment`*.json*, and Secret manager.</span></span>

<span data-ttu-id="bf385-167">`:`Separator nie działa ze zmiennymi kluczy hierarchicznych na wszystkich platformach.</span><span class="sxs-lookup"><span data-stu-id="bf385-167">The `:` separator doesn't work with environment variable hierarchical keys on all platforms.</span></span> <span data-ttu-id="bf385-168">Podwójne podkreślenie ( `__` ) jest automatycznie zastępowane przez `:` i jest obsługiwane przez wszystkie platformy.</span><span class="sxs-lookup"><span data-stu-id="bf385-168">The double underscore (`__`) is automatically replaced by a `:` and is supported by all platforms.</span></span> <span data-ttu-id="bf385-169">Na przykład `:` separator nie jest obsługiwany przez [bash](https://linuxhint.com/bash-environment-variables), ale `__` jest.</span><span class="sxs-lookup"><span data-stu-id="bf385-169">For example, the `:` separator is not supported by [Bash](https://linuxhint.com/bash-environment-variables), but `__` is.</span></span>

<span data-ttu-id="bf385-170">Następujące `set` polecenia:</span><span class="sxs-lookup"><span data-stu-id="bf385-170">The following `set` commands:</span></span>

- <span data-ttu-id="bf385-171">Ustaw klucze środowiska i wartości z poprzedniego przykładu w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="bf385-171">Set the environment keys and values of the preceding example on Windows.</span></span>
- <span data-ttu-id="bf385-172">Przetestuj ustawienia, zmieniając ich wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="bf385-172">Test the settings by changing them from their default values.</span></span> <span data-ttu-id="bf385-173">`dotnet run`Polecenie musi być uruchamiane w katalogu projektu.</span><span class="sxs-lookup"><span data-stu-id="bf385-173">The `dotnet run` command must be run in the project directory.</span></span>

```dotnetcli
set SecretKey="Secret key from environment"
set TransientFaultHandlingOptions__Enabled="true"
set TransientFaultHandlingOptions__AutoRetryDelay="00:00:13"

dotnet run
```

<span data-ttu-id="bf385-174">Poprzednie ustawienia środowiska:</span><span class="sxs-lookup"><span data-stu-id="bf385-174">The preceding environment settings:</span></span>

- <span data-ttu-id="bf385-175">Są ustawiane tylko w ramach procesów uruchomionych z poziomu okna polecenia, które zostały ustawione w.</span><span class="sxs-lookup"><span data-stu-id="bf385-175">Are only set in processes launched from the command window they were set in.</span></span>
- <span data-ttu-id="bf385-176">Nie będą odczytywane przez aplikacje sieci Web uruchomione przy użyciu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bf385-176">Won't be read by web apps launched with Visual Studio.</span></span>

<span data-ttu-id="bf385-177">Następujące polecenia [setx](/windows-server/administration/windows-commands/setx) mogą służyć do ustawiania kluczy środowiskowych i wartości w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="bf385-177">The following [setx](/windows-server/administration/windows-commands/setx) commands can be used to set the environment keys and values on Windows.</span></span> <span data-ttu-id="bf385-178">W przeciwieństwie do `set` , `setx` Ustawienia są utrwalane.</span><span class="sxs-lookup"><span data-stu-id="bf385-178">Unlike `set`, `setx` settings are persisted.</span></span> <span data-ttu-id="bf385-179">`/M` ustawia zmienną w środowisku systemowym.</span><span class="sxs-lookup"><span data-stu-id="bf385-179">`/M` sets the variable in the system environment.</span></span> <span data-ttu-id="bf385-180">Jeśli `/M` przełącznik nie jest używany, zmienna środowiskowa użytkownika jest ustawiona.</span><span class="sxs-lookup"><span data-stu-id="bf385-180">If the `/M` switch isn't used, a user environment variable is set.</span></span>

```dotnetcli
setx SecretKey "Secret key from setx environment" /M
setx TransientFaultHandlingOptions__Enabled "true" /M
setx TransientFaultHandlingOptions__AutoRetryDelay "00:00:05" /M

dotnet run
```

<span data-ttu-id="bf385-181">Aby sprawdzić, czy poprzednie polecenia zastępują *appsettings.js* i *appSettings.* `Environment` *. JSON*:</span><span class="sxs-lookup"><span data-stu-id="bf385-181">To test that the preceding commands override *appsettings.json* and *appsettings.*`Environment`*.json*:</span></span>

- <span data-ttu-id="bf385-182">Za pomocą programu Visual Studio: Zamknij i uruchom ponownie program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bf385-182">With Visual Studio: Exit and restart Visual Studio.</span></span>
- <span data-ttu-id="bf385-183">Za pomocą interfejsu wiersza polecenia: Uruchom nowe okno poleceń i wprowadź `dotnet run` .</span><span class="sxs-lookup"><span data-stu-id="bf385-183">With the CLI: Start a new command window and enter `dotnet run`.</span></span>

<span data-ttu-id="bf385-184">Połącz <xref:Microsoft.Extensions.Configuration.EnvironmentVariablesExtensions.AddEnvironmentVariables%2A> z ciągiem, aby określić prefiks dla zmiennych środowiskowych:</span><span class="sxs-lookup"><span data-stu-id="bf385-184">Call <xref:Microsoft.Extensions.Configuration.EnvironmentVariablesExtensions.AddEnvironmentVariables%2A> with a string to specify a prefix for environment variables:</span></span>

:::code language="csharp" source="snippets/configuration/console-env/Program.cs" highlight="15-16":::

<span data-ttu-id="bf385-185">Powyższy kod ma następujące działanie:</span><span class="sxs-lookup"><span data-stu-id="bf385-185">In the preceding code:</span></span>

- <span data-ttu-id="bf385-186">`config.AddEnvironmentVariables(prefix: "CustomPrefix_")` zostanie dodany po domyślnych dostawcach konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="bf385-186">`config.AddEnvironmentVariables(prefix: "CustomPrefix_")` is added after the default configuration providers.</span></span> <span data-ttu-id="bf385-187">Przykład określania kolejności dostawców konfiguracji można znaleźć w temacie [dostawca konfiguracji XML](#xml-configuration-provider).</span><span class="sxs-lookup"><span data-stu-id="bf385-187">For an example of ordering the configuration providers, see [XML configuration provider](#xml-configuration-provider).</span></span>
- <span data-ttu-id="bf385-188">Zmienne środowiskowe ustawione z `CustomPrefix_` prefiksem przesłaniają domyślnych dostawców konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="bf385-188">Environment variables set with the `CustomPrefix_` prefix override the default configuration providers.</span></span> <span data-ttu-id="bf385-189">Obejmuje to zmienne środowiskowe bez prefiksu.</span><span class="sxs-lookup"><span data-stu-id="bf385-189">This includes environment variables without the prefix.</span></span>

<span data-ttu-id="bf385-190">Prefiks jest usuwany, gdy pary klucz konfiguracji-wartość są odczytywane.</span><span class="sxs-lookup"><span data-stu-id="bf385-190">The prefix is stripped off when the configuration key-value pairs are read.</span></span>

<span data-ttu-id="bf385-191">Następujące polecenia testują prefiks niestandardowy:</span><span class="sxs-lookup"><span data-stu-id="bf385-191">The following commands test the custom prefix:</span></span>

```dotnetcli
set CustomPrefix__SecretKey="Secret key with CustomPrefix_ environment"
set CustomPrefix_TransientFaultHandlingOptions__Enabled=true
set CustomPrefix_TransientFaultHandlingOptions__AutoRetryDelay=00:00:21

dotnet run
```

<span data-ttu-id="bf385-192">Konfiguracja domyślna ładuje zmienne środowiskowe i argumenty wiersza polecenia poprzedzone prefiksem `DOTNET_` .</span><span class="sxs-lookup"><span data-stu-id="bf385-192">The default configuration loads environment variables and command-line arguments prefixed with `DOTNET_`.</span></span> <span data-ttu-id="bf385-193">`DOTNET_`Prefiks jest używany przez platformę .NET do [konfiguracji](generic-host.md#app-configuration) [hosta](generic-host.md#host-configuration) i aplikacji, ale nie do konfiguracji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bf385-193">The `DOTNET_` prefix is used by .NET for [host](generic-host.md#host-configuration) and [app configuration](generic-host.md#app-configuration), but not for user configuration.</span></span>

<span data-ttu-id="bf385-194">Aby uzyskać więcej informacji na temat konfiguracji hosta i aplikacji, zobacz [host ogólny programu .NET](generic-host.md).</span><span class="sxs-lookup"><span data-stu-id="bf385-194">For more information on host and app configuration, see [.NET Generic Host](generic-host.md).</span></span>

<span data-ttu-id="bf385-195">Na [Azure App Service](https://azure.microsoft.com/services/app-service)wybierz pozycję **nowe ustawienie aplikacji** na stronie **Konfiguracja > ustawienia** .</span><span class="sxs-lookup"><span data-stu-id="bf385-195">On [Azure App Service](https://azure.microsoft.com/services/app-service), select **New application setting** on the **Settings > Configuration** page.</span></span> <span data-ttu-id="bf385-196">Ustawienia aplikacji Azure App Service są następujące:</span><span class="sxs-lookup"><span data-stu-id="bf385-196">Azure App Service application settings are:</span></span>

- <span data-ttu-id="bf385-197">Szyfrowane i przesyłane przez zaszyfrowanego kanału.</span><span class="sxs-lookup"><span data-stu-id="bf385-197">Encrypted at rest and transmitted over an encrypted channel.</span></span>
- <span data-ttu-id="bf385-198">Uwidocznione jako zmienne środowiskowe.</span><span class="sxs-lookup"><span data-stu-id="bf385-198">Exposed as environment variables.</span></span>

### <a name="connection-string-prefixes"></a><span data-ttu-id="bf385-199">Prefiksy parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="bf385-199">Connection string prefixes</span></span>

<span data-ttu-id="bf385-200">Interfejs API konfiguracji ma specjalne reguły przetwarzania dla czterech zmiennych środowiskowych parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="bf385-200">The Configuration API has special processing rules for four connection string environment variables.</span></span> <span data-ttu-id="bf385-201">Te parametry połączenia są związane z konfigurowaniem parametrów połączenia platformy Azure dla środowiska aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bf385-201">These connection strings are involved in configuring Azure connection strings for the app environment.</span></span> <span data-ttu-id="bf385-202">Zmienne środowiskowe z prefiksami podanymi w tabeli są ładowane do aplikacji z konfiguracją domyślną lub gdy nie podano prefiksu `AddEnvironmentVariables` .</span><span class="sxs-lookup"><span data-stu-id="bf385-202">Environment variables with the prefixes shown in the table are loaded into the app with the default configuration or when no prefix is supplied to `AddEnvironmentVariables`.</span></span>

| <span data-ttu-id="bf385-203">Prefiks parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="bf385-203">Connection string prefix</span></span> | <span data-ttu-id="bf385-204">Dostawca</span><span class="sxs-lookup"><span data-stu-id="bf385-204">Provider</span></span>                                                                |
|--------------------------|-------------------------------------------------------------------------|
| `CUSTOMCONNSTR_`         | <span data-ttu-id="bf385-205">Dostawca niestandardowy</span><span class="sxs-lookup"><span data-stu-id="bf385-205">Custom provider</span></span>                                                         |
| `MYSQLCONNSTR_`          | [<span data-ttu-id="bf385-206">MySQL</span><span class="sxs-lookup"><span data-stu-id="bf385-206">MySQL</span></span>](https://www.mysql.com)                                          |
| `SQLAZURECONNSTR_`       | [<span data-ttu-id="bf385-207">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="bf385-207">Azure SQL Database</span></span>](https://azure.microsoft.com/services/sql-database) |
| `SQLCONNSTR_`            | [<span data-ttu-id="bf385-208">SQL Server</span><span class="sxs-lookup"><span data-stu-id="bf385-208">SQL Server</span></span>](https://www.microsoft.com/sql-server)                      |

<span data-ttu-id="bf385-209">Gdy zmienna środowiskowa zostanie odnaleziona i załadowana do konfiguracji z dowolnymi z czterech prefiksów pokazanych w tabeli:</span><span class="sxs-lookup"><span data-stu-id="bf385-209">When an environment variable is discovered and loaded into configuration with any of the four prefixes shown in the table:</span></span>

- <span data-ttu-id="bf385-210">Klucz konfiguracji jest tworzony przez usunięcie prefiksu zmiennej środowiskowej i dodanie sekcji klucza konfiguracji ( `ConnectionStrings` ).</span><span class="sxs-lookup"><span data-stu-id="bf385-210">The configuration key is created by removing the environment variable prefix and adding a configuration key section (`ConnectionStrings`).</span></span>
- <span data-ttu-id="bf385-211">Zostanie utworzona nowa para klucz-wartość konfiguracji, która reprezentuje dostawcę połączenia bazy danych (z wyjątkiem tego `CUSTOMCONNSTR_` , który nie ma określonego dostawcy).</span><span class="sxs-lookup"><span data-stu-id="bf385-211">A new configuration key-value pair is created that represents the database connection provider (except for `CUSTOMCONNSTR_`, which has no stated provider).</span></span>

| <span data-ttu-id="bf385-212">Klucz zmiennej środowiskowej</span><span class="sxs-lookup"><span data-stu-id="bf385-212">Environment variable key</span></span> | <span data-ttu-id="bf385-213">Przekonwertowany klucz konfiguracji</span><span class="sxs-lookup"><span data-stu-id="bf385-213">Converted configuration key</span></span> | <span data-ttu-id="bf385-214">Wpis konfiguracji dostawcy</span><span class="sxs-lookup"><span data-stu-id="bf385-214">Provider configuration entry</span></span>                                                    |
|--------------------------|-----------------------------|---------------------------------------------------------------------------------|
| `CUSTOMCONNSTR_{KEY}`    | `ConnectionStrings:{KEY}`   | <span data-ttu-id="bf385-215">Wpis konfiguracji nie został utworzony.</span><span class="sxs-lookup"><span data-stu-id="bf385-215">Configuration entry not created.</span></span>                                                |
| `MYSQLCONNSTR_{KEY}`     | `ConnectionStrings:{KEY}`   | <span data-ttu-id="bf385-216">Klucz: `ConnectionStrings:{KEY}_ProviderName` :</span><span class="sxs-lookup"><span data-stu-id="bf385-216">Key: `ConnectionStrings:{KEY}_ProviderName`:</span></span><br><span data-ttu-id="bf385-217">Wartość: `MySql.Data.MySqlClient`</span><span class="sxs-lookup"><span data-stu-id="bf385-217">Value: `MySql.Data.MySqlClient`</span></span> |
| `SQLAZURECONNSTR_{KEY}`  | `ConnectionStrings:{KEY}`   | <span data-ttu-id="bf385-218">Klucz: `ConnectionStrings:{KEY}_ProviderName` :</span><span class="sxs-lookup"><span data-stu-id="bf385-218">Key: `ConnectionStrings:{KEY}_ProviderName`:</span></span><br><span data-ttu-id="bf385-219">Wartość: `System.Data.SqlClient`</span><span class="sxs-lookup"><span data-stu-id="bf385-219">Value: `System.Data.SqlClient`</span></span>  |
| `SQLCONNSTR_{KEY}`       | `ConnectionStrings:{KEY}`   | <span data-ttu-id="bf385-220">Klucz: `ConnectionStrings:{KEY}_ProviderName` :</span><span class="sxs-lookup"><span data-stu-id="bf385-220">Key: `ConnectionStrings:{KEY}_ProviderName`:</span></span><br><span data-ttu-id="bf385-221">Wartość: `System.Data.SqlClient`</span><span class="sxs-lookup"><span data-stu-id="bf385-221">Value: `System.Data.SqlClient`</span></span>  |

### <a name="environment-variables-set-in-launchsettingsjson"></a><span data-ttu-id="bf385-222">Zmienne środowiskowe ustawione w launchSettings.jsna</span><span class="sxs-lookup"><span data-stu-id="bf385-222">Environment variables set in launchSettings.json</span></span>

<span data-ttu-id="bf385-223">Zmienne środowiskowe ustawione w *launchSettings.jsna* zastępują te ustawienia w środowisku systemowym.</span><span class="sxs-lookup"><span data-stu-id="bf385-223">Environment variables set in *launchSettings.json* override those set in the system environment.</span></span>

## <a name="command-line-configuration-provider"></a><span data-ttu-id="bf385-224">Dostawca konfiguracji wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="bf385-224">Command-line configuration provider</span></span>

<span data-ttu-id="bf385-225">Korzystając z konfiguracji domyślnej, <xref:Microsoft.Extensions.Configuration.CommandLine.CommandLineConfigurationProvider> ładuje konfigurację z par klucz-wartość argumentu wiersza polecenia po następujących źródłach konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="bf385-225">Using the default configuration, the <xref:Microsoft.Extensions.Configuration.CommandLine.CommandLineConfigurationProvider> loads configuration from command-line argument key-value pairs after the following configuration sources:</span></span>

- <span data-ttu-id="bf385-226">*appsettings.jsna* i *AppSettings*. `Environment` . pliki *JSON* .</span><span class="sxs-lookup"><span data-stu-id="bf385-226">*appsettings.json* and *appsettings*.`Environment`.*json* files.</span></span>
- <span data-ttu-id="bf385-227">Wpisy tajne aplikacji (Secret Manager) w `Development` środowisku.</span><span class="sxs-lookup"><span data-stu-id="bf385-227">App secrets (Secret Manager) in the `Development` environment.</span></span>
- <span data-ttu-id="bf385-228">Zmienne środowiskowe.</span><span class="sxs-lookup"><span data-stu-id="bf385-228">Environment variables.</span></span>

<span data-ttu-id="bf385-229">Domyślnie wartości konfiguracyjne ustawione w wierszu polecenia przesłaniają wartości konfiguracyjne ustawione dla wszystkich innych dostawców konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="bf385-229">By default, configuration values set on the command line override configuration values set with all the other configuration providers.</span></span>

### <a name="command-line-arguments"></a><span data-ttu-id="bf385-230">Argumenty wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="bf385-230">Command-line arguments</span></span>

<span data-ttu-id="bf385-231">Następujące polecenie ustawia klucze i wartości przy użyciu `=` :</span><span class="sxs-lookup"><span data-stu-id="bf385-231">The following command sets keys and values using `=`:</span></span>

```dotnetcli
dotnet run SecretKey="Secret key from command line"
```

<span data-ttu-id="bf385-232">Następujące polecenie ustawia klucze i wartości przy użyciu `/` :</span><span class="sxs-lookup"><span data-stu-id="bf385-232">The following command sets keys and values using `/`:</span></span>

```dotnetcli
dotnet run /SecretKey "Secret key set from forward slash"
```

<span data-ttu-id="bf385-233">Następujące polecenie ustawia klucze i wartości przy użyciu `--` :</span><span class="sxs-lookup"><span data-stu-id="bf385-233">The following command sets keys and values using `--`:</span></span>

```dotnetcli
dotnet run --SecretKey "Secret key set from double hyphen"
```

<span data-ttu-id="bf385-234">Wartość klucza:</span><span class="sxs-lookup"><span data-stu-id="bf385-234">The key value:</span></span>

- <span data-ttu-id="bf385-235">Musi `=` być zgodna lub musi mieć prefiks lub, gdy wartość znajduje się w `--` `/` miejscu.</span><span class="sxs-lookup"><span data-stu-id="bf385-235">Must follow `=`, or the key must have a prefix of `--` or `/` when the value follows a space.</span></span>
- <span data-ttu-id="bf385-236">Nie jest wymagane, jeśli `=` jest używany.</span><span class="sxs-lookup"><span data-stu-id="bf385-236">Isn't required if `=` is used.</span></span> <span data-ttu-id="bf385-237">Na przykład `SomeKey=`.</span><span class="sxs-lookup"><span data-stu-id="bf385-237">For example, `SomeKey=`.</span></span>

<span data-ttu-id="bf385-238">W tym samym poleceniu nie należy mieszać par klucz-wartość argumentu wiersza polecenia, które są używane `=` z parami klucz-wartość, które używają spacji.</span><span class="sxs-lookup"><span data-stu-id="bf385-238">Within the same command, don't mix command-line argument key-value pairs that use `=` with key-value pairs that use a space.</span></span>

## <a name="key-per-file-configuration-provider"></a><span data-ttu-id="bf385-239">Dostawca konfiguracji klucza dla plików</span><span class="sxs-lookup"><span data-stu-id="bf385-239">Key-per-file configuration provider</span></span>

<span data-ttu-id="bf385-240"><xref:Microsoft.Extensions.Configuration.KeyPerFile.KeyPerFileConfigurationProvider>Używa plików katalogu jako par klucz konfiguracji i wartość.</span><span class="sxs-lookup"><span data-stu-id="bf385-240">The <xref:Microsoft.Extensions.Configuration.KeyPerFile.KeyPerFileConfigurationProvider> uses a directory's files as configuration key-value pairs.</span></span> <span data-ttu-id="bf385-241">Kluczem jest nazwa pliku.</span><span class="sxs-lookup"><span data-stu-id="bf385-241">The key is the file name.</span></span> <span data-ttu-id="bf385-242">Wartość jest zawartością pliku.</span><span class="sxs-lookup"><span data-stu-id="bf385-242">The value is the file's contents.</span></span> <span data-ttu-id="bf385-243">Dostawca konfiguracji klucza dla plików jest używany w scenariuszach hostingu platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="bf385-243">The Key-per-file configuration provider is used in Docker hosting scenarios.</span></span>

<span data-ttu-id="bf385-244">Aby uaktywnić konfigurację klucza dla plików, wywołaj <xref:Microsoft.Extensions.Configuration.KeyPerFileConfigurationBuilderExtensions.AddKeyPerFile%2A> metodę rozszerzenia w wystąpieniu <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder> .</span><span class="sxs-lookup"><span data-stu-id="bf385-244">To activate key-per-file configuration, call the <xref:Microsoft.Extensions.Configuration.KeyPerFileConfigurationBuilderExtensions.AddKeyPerFile%2A> extension method on an instance of <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder>.</span></span> <span data-ttu-id="bf385-245">`directoryPath`Do plików musi być ścieżką bezwzględną.</span><span class="sxs-lookup"><span data-stu-id="bf385-245">The `directoryPath` to the files must be an absolute path.</span></span>

<span data-ttu-id="bf385-246">Przeciążania Zezwalaj na określanie:</span><span class="sxs-lookup"><span data-stu-id="bf385-246">Overloads permit specifying:</span></span>

- <span data-ttu-id="bf385-247">`Action<KeyPerFileConfigurationSource>`Delegat, który konfiguruje źródło.</span><span class="sxs-lookup"><span data-stu-id="bf385-247">An `Action<KeyPerFileConfigurationSource>` delegate that configures the source.</span></span>
- <span data-ttu-id="bf385-248">Określa, czy katalog jest opcjonalny, i ścieżkę do katalogu.</span><span class="sxs-lookup"><span data-stu-id="bf385-248">Whether the directory is optional and the path to the directory.</span></span>

<span data-ttu-id="bf385-249">Podwójny znak podkreślenia ( `__` ) jest używany jako ogranicznik klucza konfiguracji w nazwach plików.</span><span class="sxs-lookup"><span data-stu-id="bf385-249">The double-underscore (`__`) is used as a configuration key delimiter in file names.</span></span> <span data-ttu-id="bf385-250">Na przykład nazwa pliku `Logging__LogLevel__System` generuje klucz konfiguracji `Logging:LogLevel:System` .</span><span class="sxs-lookup"><span data-stu-id="bf385-250">For example, the file name `Logging__LogLevel__System` produces the configuration key `Logging:LogLevel:System`.</span></span>

<span data-ttu-id="bf385-251">Wywołaj `ConfigureAppConfiguration` podczas kompilowania hosta, aby określić konfigurację aplikacji:</span><span class="sxs-lookup"><span data-stu-id="bf385-251">Call `ConfigureAppConfiguration` when building the host to specify the app's configuration:</span></span>

```csharp
.ConfigureAppConfiguration((_, configuration) =>
{
    var path = Path.Combine(
        Directory.GetCurrentDirectory(), "path/to/files");

    configuration.AddKeyPerFile(directoryPath: path, optional: true);
})
```

## <a name="memory-configuration-provider"></a><span data-ttu-id="bf385-252">Dostawca konfiguracji pamięci</span><span class="sxs-lookup"><span data-stu-id="bf385-252">Memory configuration provider</span></span>

<span data-ttu-id="bf385-253"><xref:Microsoft.Extensions.Configuration.Memory.MemoryConfigurationProvider>Używa kolekcji w pamięci jako par klucz konfiguracji-wartość.</span><span class="sxs-lookup"><span data-stu-id="bf385-253">The <xref:Microsoft.Extensions.Configuration.Memory.MemoryConfigurationProvider> uses an in-memory collection as configuration key-value pairs.</span></span>

<span data-ttu-id="bf385-254">Poniższy kod dodaje kolekcję pamięci do systemu konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="bf385-254">The following code adds a memory collection to the configuration system:</span></span>

:::code language="csharp" source="snippets/configuration/console-memory/Program.cs" highlight="16-23":::

<span data-ttu-id="bf385-255">W powyższym kodzie program <xref:Microsoft.Extensions.Configuration.MemoryConfigurationBuilderExtensions.AddInMemoryCollection(Microsoft.Extensions.Configuration.IConfigurationBuilder,System.Collections.Generic.IEnumerable{System.Collections.Generic.KeyValuePair{System.String,System.String}})?displayProperty=nameWithType> dodaje dostawcę pamięci po domyślnych dostawcach konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="bf385-255">In the preceding code, <xref:Microsoft.Extensions.Configuration.MemoryConfigurationBuilderExtensions.AddInMemoryCollection(Microsoft.Extensions.Configuration.IConfigurationBuilder,System.Collections.Generic.IEnumerable{System.Collections.Generic.KeyValuePair{System.String,System.String}})?displayProperty=nameWithType> adds the memory provider after the default configuration providers.</span></span> <span data-ttu-id="bf385-256">Przykład określania kolejności dostawców konfiguracji można znaleźć w temacie [dostawca konfiguracji XML](#xml-configuration-provider).</span><span class="sxs-lookup"><span data-stu-id="bf385-256">For an example of ordering the configuration providers, see [XML configuration provider](#xml-configuration-provider).</span></span>

## <a name="see-also"></a><span data-ttu-id="bf385-257">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="bf385-257">See also</span></span>

- [<span data-ttu-id="bf385-258">Konfiguracja w programie .NET</span><span class="sxs-lookup"><span data-stu-id="bf385-258">Configuration in .NET</span></span>](configuration.md)
- [<span data-ttu-id="bf385-259">Host ogólny .NET</span><span class="sxs-lookup"><span data-stu-id="bf385-259">.NET Generic Host</span></span>](generic-host.md)
- [<span data-ttu-id="bf385-260">Implementowanie niestandardowego dostawcy konfiguracji</span><span class="sxs-lookup"><span data-stu-id="bf385-260">Implement a custom configuration provider</span></span>](custom-configuration-provider.md)