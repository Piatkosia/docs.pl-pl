---
title: Wdróż platformę .NET dla Apache Spark procesów roboczych i plików binarnych funkcji zdefiniowanych przez użytkownika
description: Dowiedz się, jak wdrożyć platformę .NET dla Apache Spark procesów roboczych i plików binarnych funkcji zdefiniowanych przez użytkownika.
ms.date: 01/21/2019
ms.topic: conceptual
ms.custom: mvc,how-to
ms.openlocfilehash: f9197ca3cf8066f0849ebbe70d7757c9035d02f6
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/24/2020
ms.locfileid: "76748532"
---
# <a name="deploy-net-for-apache-spark-worker-and-user-defined-function-binaries"></a><span data-ttu-id="667a2-103">Wdróż platformę .NET dla Apache Spark procesów roboczych i plików binarnych funkcji zdefiniowanych przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="667a2-103">Deploy .NET for Apache Spark worker and user-defined function binaries</span></span>

<span data-ttu-id="667a2-104">Ten opis zawiera ogólne instrukcje dotyczące wdrażania programu .NET dla Apache Spark procesów roboczych i plików binarnych funkcji zdefiniowanych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="667a2-104">This how-to provides general instructions on how to deploy .NET for Apache Spark worker and user-defined function binaries.</span></span> <span data-ttu-id="667a2-105">Dowiesz się, które zmienne środowiskowe mają być skonfigurowane, a także kilka często używanych parametrów do uruchamiania aplikacji przy użyciu `spark-submit`.</span><span class="sxs-lookup"><span data-stu-id="667a2-105">You learn which Environment Variables to set up, as well as some commonly used parameters for launching applications with `spark-submit`.</span></span>

## <a name="configurations"></a><span data-ttu-id="667a2-106">Konfiguracje</span><span class="sxs-lookup"><span data-stu-id="667a2-106">Configurations</span></span>
<span data-ttu-id="667a2-107">Konfiguracje zawierają ogólne ustawienia zmiennych środowiskowych i parametrów w celu wdrożenia platformy .NET dla Apache Spark procesów roboczych i plików binarnych funkcji zdefiniowanych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="667a2-107">Configurations show the general environment variables and parameters settings in order to deploy .NET for Apache Spark worker and user-defined function binaries.</span></span>

### <a name="environment-variables"></a><span data-ttu-id="667a2-108">Zmienne środowiskowe</span><span class="sxs-lookup"><span data-stu-id="667a2-108">Environment variables</span></span>
<span data-ttu-id="667a2-109">Podczas wdrażania procesów roboczych i pisania UDF istnieje kilka często używanych zmiennych środowiskowych, które mogą być konieczne do ustawienia:</span><span class="sxs-lookup"><span data-stu-id="667a2-109">When deploying workers and writing UDFs, there are a few commonly used environment variables that you may need to set:</span></span> 

| <span data-ttu-id="667a2-110">Zmienna środowiskowa</span><span class="sxs-lookup"><span data-stu-id="667a2-110">Environment Variable</span></span>         | <span data-ttu-id="667a2-111">Opis</span><span class="sxs-lookup"><span data-stu-id="667a2-111">Description</span></span>
| :--------------------------- | :---------- 
| <span data-ttu-id="667a2-112">DOTNET_WORKER_DIR</span><span class="sxs-lookup"><span data-stu-id="667a2-112">DOTNET_WORKER_DIR</span></span>            | <span data-ttu-id="667a2-113">Ścieżka, w której Wygenerowano <code>Microsoft.Spark.Worker</code> plik binarny.</span><span class="sxs-lookup"><span data-stu-id="667a2-113">Path where the <code>Microsoft.Spark.Worker</code> binary has been generated.</span></span></br><span data-ttu-id="667a2-114">Jest ona używana przez sterownik Spark i zostanie przeniesiona do modułów wykonujących testy platformy Spark.</span><span class="sxs-lookup"><span data-stu-id="667a2-114">It's used by the Spark driver and will be passed to Spark executors.</span></span> <span data-ttu-id="667a2-115">Jeśli ta zmienna nie jest skonfigurowana, program wykonujący testy programu Spark przeszuka ścieżkę określoną w zmiennej środowiskowej <code>PATH</code>.</span><span class="sxs-lookup"><span data-stu-id="667a2-115">If this variable is not set up, the Spark executors will search the path specified in the <code>PATH</code> environment variable.</span></span></br><span data-ttu-id="667a2-116">_np. "C:\bin\Microsoft.Spark.Worker"_</span><span class="sxs-lookup"><span data-stu-id="667a2-116">_e.g. "C:\bin\Microsoft.Spark.Worker"_</span></span>
| <span data-ttu-id="667a2-117">DOTNET_ASSEMBLY_SEARCH_PATHS</span><span class="sxs-lookup"><span data-stu-id="667a2-117">DOTNET_ASSEMBLY_SEARCH_PATHS</span></span> | <span data-ttu-id="667a2-118">Ścieżki oddzielone przecinkami, w których <code>Microsoft.Spark.Worker</code> będą ładować zestawy.</span><span class="sxs-lookup"><span data-stu-id="667a2-118">Comma-separated paths where <code>Microsoft.Spark.Worker</code> will load assemblies.</span></span></br><span data-ttu-id="667a2-119">Należy pamiętać, że jeśli ścieżka zaczyna się od ".", katalog roboczy zostanie poprzedzony.</span><span class="sxs-lookup"><span data-stu-id="667a2-119">Note that if a path starts with ".", the working directory will be prepended.</span></span> <span data-ttu-id="667a2-120">Jeśli w **trybie przędzenia**, "." będzie reprezentować katalog roboczy kontenera.</span><span class="sxs-lookup"><span data-stu-id="667a2-120">If in **yarn mode**, "." would represent the container's working directory.</span></span></br><span data-ttu-id="667a2-121">_na przykład "C:\Users\\&lt;nazwa użytkownika&gt;\\&lt;mysparkapp&gt;\bin\Debug\\&lt;dotnet Version&gt;"_</span><span class="sxs-lookup"><span data-stu-id="667a2-121">_e.g. "C:\Users\\&lt;user name&gt;\\&lt;mysparkapp&gt;\bin\Debug\\&lt;dotnet version&gt;"_</span></span>
| <span data-ttu-id="667a2-122">DOTNET_WORKER_DEBUG</span><span class="sxs-lookup"><span data-stu-id="667a2-122">DOTNET_WORKER_DEBUG</span></span>          | <span data-ttu-id="667a2-123">Jeśli chcesz debugować funkcję <a href="https://github.com/dotnet/spark/blob/master/docs/developer-guide.md#debugging-user-defined-function-udf">UDF</a>, ustaw tę zmienną środowiskową na <code>1</code> przed uruchomieniem <code>spark-submit</code>.</span><span class="sxs-lookup"><span data-stu-id="667a2-123">If you want to <a href="https://github.com/dotnet/spark/blob/master/docs/developer-guide.md#debugging-user-defined-function-udf">debug a UDF</a>, then set this environment variable to <code>1</code> before running <code>spark-submit</code>.</span></span>

### <a name="parameter-options"></a><span data-ttu-id="667a2-124">Opcje parametrów</span><span class="sxs-lookup"><span data-stu-id="667a2-124">Parameter options</span></span>
<span data-ttu-id="667a2-125">Po dodaniu aplikacji platformy [](https://spark.apache.org/docs/latest/submitting-applications.html#bundling-your-applications-dependencies)Spark można ją uruchomić przy użyciu `spark-submit`.</span><span class="sxs-lookup"><span data-stu-id="667a2-125">Once the Spark application is [bundled](https://spark.apache.org/docs/latest/submitting-applications.html#bundling-your-applications-dependencies), you can launch it using `spark-submit`.</span></span> <span data-ttu-id="667a2-126">W poniższej tabeli przedstawiono niektóre z najczęściej używanych opcji:</span><span class="sxs-lookup"><span data-stu-id="667a2-126">The following table shows some of the commonly used options:</span></span> 

| <span data-ttu-id="667a2-127">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="667a2-127">Parameter Name</span></span>        | <span data-ttu-id="667a2-128">Opis</span><span class="sxs-lookup"><span data-stu-id="667a2-128">Description</span></span>
| :---------------------| :---------- 
| <span data-ttu-id="667a2-129">--Klasa</span><span class="sxs-lookup"><span data-stu-id="667a2-129">--class</span></span>               | <span data-ttu-id="667a2-130">Punkt wejścia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="667a2-130">The entry point for your application.</span></span></br><span data-ttu-id="667a2-131">_np. org. Apache. Spark. deploy. dotnet. DotnetRunner_</span><span class="sxs-lookup"><span data-stu-id="667a2-131">_e.g. org.apache.spark.deploy.dotnet.DotnetRunner_</span></span>
| <span data-ttu-id="667a2-132">--Master</span><span class="sxs-lookup"><span data-stu-id="667a2-132">--master</span></span>              | <span data-ttu-id="667a2-133"><a href="https://spark.apache.org/docs/latest/submitting-applications.html#master-urls">Główny adres URL</a> klastra.</span><span class="sxs-lookup"><span data-stu-id="667a2-133">The <a href="https://spark.apache.org/docs/latest/submitting-applications.html#master-urls">master URL</a> for the cluster.</span></span></br><span data-ttu-id="667a2-134">_np. przędza_</span><span class="sxs-lookup"><span data-stu-id="667a2-134">_e.g. yarn_</span></span>
| <span data-ttu-id="667a2-135">--Tryb wdrażania</span><span class="sxs-lookup"><span data-stu-id="667a2-135">--deploy-mode</span></span>         | <span data-ttu-id="667a2-136">Czy wdrożyć sterownik na węzłach procesu roboczego (<code>cluster</code>) czy lokalnie jako Klient zewnętrzny (<code>client</code>).</span><span class="sxs-lookup"><span data-stu-id="667a2-136">Whether to deploy your driver on the worker nodes (<code>cluster</code>) or locally as an external client (<code>client</code>).</span></span></br><span data-ttu-id="667a2-137">Wartość domyślna: <code>client</code></span><span class="sxs-lookup"><span data-stu-id="667a2-137">Default: <code>client</code></span></span>
| <span data-ttu-id="667a2-138">--conf</span><span class="sxs-lookup"><span data-stu-id="667a2-138">--conf</span></span>                | <span data-ttu-id="667a2-139">Dowolnych właściwości konfiguracji platformy Spark w formacie <code>key=value</code>.</span><span class="sxs-lookup"><span data-stu-id="667a2-139">Arbitrary Spark configuration property in <code>key=value</code> format.</span></span></br><span data-ttu-id="667a2-140">_na przykład Spark. przędz. appMasterEnv. DOTNET_WORKER_DIR = .\worker\Microsoft.Spark.Worker_</span><span class="sxs-lookup"><span data-stu-id="667a2-140">_e.g. spark.yarn.appMasterEnv.DOTNET_WORKER_DIR=.\worker\Microsoft.Spark.Worker_</span></span>
| <span data-ttu-id="667a2-141">--pliki</span><span class="sxs-lookup"><span data-stu-id="667a2-141">--files</span></span>               | <span data-ttu-id="667a2-142">Rozdzielana przecinkami lista plików, które mają zostać umieszczone w katalogu roboczym każdego wykonawcy.</span><span class="sxs-lookup"><span data-stu-id="667a2-142">Comma-separated list of files to be placed in the working directory of each executor.</span></span><br/><ul><li><span data-ttu-id="667a2-143">Należy pamiętać, że ta opcja ma zastosowanie tylko w przypadku trybu przędzy.</span><span class="sxs-lookup"><span data-stu-id="667a2-143">Please note that this option is only applicable for yarn mode.</span></span></li><li><span data-ttu-id="667a2-144">Obsługuje ona Określanie nazw plików przy użyciu # podobnego do usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="667a2-144">It supports specifying file names with # similar to Hadoop.</span></span></br></ul><span data-ttu-id="667a2-145">_np. <code>myLocalSparkApp.dll#appSeen.dll</code>. Aplikacja powinna używać nazwy jako <code>appSeen.dll</code> do odwoływania się do <code>myLocalSparkApp.dll</code> podczas uruchamiania w ramach PRZĘDZy._</span><span class="sxs-lookup"><span data-stu-id="667a2-145">_e.g. <code>myLocalSparkApp.dll#appSeen.dll</code>. Your application should use the name as <code>appSeen.dll</code> to reference <code>myLocalSparkApp.dll</code> when running on YARN._</span></span></li>
| <span data-ttu-id="667a2-146">--Archiwa</span><span class="sxs-lookup"><span data-stu-id="667a2-146">--archives</span></span>          | <span data-ttu-id="667a2-147">Rozdzielana przecinkami lista archiwów, które mają zostać wyodrębnione do katalogu roboczego każdego wykonawcy.</span><span class="sxs-lookup"><span data-stu-id="667a2-147">Comma-separated list of archives to be extracted into the working directory of each executor.</span></span></br><ul><li><span data-ttu-id="667a2-148">Należy pamiętać, że ta opcja ma zastosowanie tylko w przypadku trybu przędzy.</span><span class="sxs-lookup"><span data-stu-id="667a2-148">Please note that this option is only applicable for yarn mode.</span></span></li><li><span data-ttu-id="667a2-149">Obsługuje ona Określanie nazw plików przy użyciu # podobnego do usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="667a2-149">It supports specifying file names with # similar to Hadoop.</span></span></br></ul><span data-ttu-id="667a2-150">_np. <code>hdfs://&lt;path to your worker file&gt;/Microsoft.Spark.Worker.zip#worker</code>. Spowoduje to skopiowanie i wyodrębnienie pliku zip do folderu <code>worker</code>._</span><span class="sxs-lookup"><span data-stu-id="667a2-150">_e.g. <code>hdfs://&lt;path to your worker file&gt;/Microsoft.Spark.Worker.zip#worker</code>. This will copy and extract the zip file to <code>worker</code> folder._</span></span></li>
| <span data-ttu-id="667a2-151">Aplikacja — jar</span><span class="sxs-lookup"><span data-stu-id="667a2-151">application-jar</span></span>       | <span data-ttu-id="667a2-152">Ścieżka do powiązanego jar, w tym aplikacji i wszystkich zależności.</span><span class="sxs-lookup"><span data-stu-id="667a2-152">Path to a bundled jar including your application and all dependencies.</span></span></br><span data-ttu-id="667a2-153">_np. hdfs://&lt;ścieżka do&gt;jar/Microsoft-Spark-&lt;wersja&gt;. jar_</span><span class="sxs-lookup"><span data-stu-id="667a2-153">_e.g. hdfs://&lt;path to your jar&gt;/microsoft-spark-&lt;version&gt;.jar_</span></span>
| <span data-ttu-id="667a2-154">argumenty aplikacji</span><span class="sxs-lookup"><span data-stu-id="667a2-154">application-arguments</span></span> | <span data-ttu-id="667a2-155">Argumenty przekazane do metody Main klasy głównej, jeśli istnieją.</span><span class="sxs-lookup"><span data-stu-id="667a2-155">Arguments passed to the main method of your main class, if any.</span></span></br><span data-ttu-id="667a2-156">_np. hdfs://&lt;ścieżkę do aplikacji&gt;/&lt;aplikacji&gt;. zip &lt;nazwę aplikacji&gt; &lt;argumenty aplikacji&gt;_</span><span class="sxs-lookup"><span data-stu-id="667a2-156">_e.g. hdfs://&lt;path to your app&gt;/&lt;your app&gt;.zip &lt;your app name&gt; &lt;app args&gt;_</span></span>

> [!NOTE]
> <span data-ttu-id="667a2-157">Określ wszystkie `--options` przed `application-jar` podczas uruchamiania aplikacji za pomocą `spark-submit`, w przeciwnym razie zostaną one zignorowane.</span><span class="sxs-lookup"><span data-stu-id="667a2-157">Specify all the `--options` before `application-jar` when launching applications with `spark-submit`, otherwise they will be ignored.</span></span> <span data-ttu-id="667a2-158">Aby uzyskać więcej informacji, zobacz [`spark-submit` opcje](https://spark.apache.org/docs/latest/submitting-applications.html) i [Uruchamianie platformy Spark z informacjami o przędze](https://spark.apache.org/docs/latest/running-on-yarn.html).</span><span class="sxs-lookup"><span data-stu-id="667a2-158">For more information, see [`spark-submit` options](https://spark.apache.org/docs/latest/submitting-applications.html) and [running spark on YARN details](https://spark.apache.org/docs/latest/running-on-yarn.html).</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="667a2-159">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="667a2-159">Frequently asked questions</span></span>
### <a name="when-i-run-a-spark-app-with-udfs-i-get-a-filenotfoundexception-error-what-should-i-do"></a><span data-ttu-id="667a2-160">Gdy uruchamiam aplikację Spark przy użyciu programu UDF, otrzymuję błąd "FileNotFoundException".</span><span class="sxs-lookup"><span data-stu-id="667a2-160">When I run a spark app with UDFs, I get a \`FileNotFoundException' error.</span></span> <span data-ttu-id="667a2-161">Co mam zrobić?</span><span class="sxs-lookup"><span data-stu-id="667a2-161">What should I do?</span></span>
> <span data-ttu-id="667a2-162">**Błąd:** [błąd] [TaskRunner] [0] ProcessStream () nie powiodło się. wyjątek: System. IO. FileNotFoundException: zestaw ' MySparkApp, Version = 1.0.0.0, Culture = neutral, PublicKeyToken = null ' nie znaleziono pliku: ' mySparkApp. dll '</span><span class="sxs-lookup"><span data-stu-id="667a2-162">**Error:** [Error] [TaskRunner] [0] ProcessStream() failed with exception: System.IO.FileNotFoundException: Assembly 'mySparkApp, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null' file not found: 'mySparkApp.dll'</span></span>

<span data-ttu-id="667a2-163">**Odpowiedź:** Sprawdź, czy zmienna środowiskowa `DOTNET_ASSEMBLY_SEARCH_PATHS` jest prawidłowo ustawiona.</span><span class="sxs-lookup"><span data-stu-id="667a2-163">**Answer:** Check that the `DOTNET_ASSEMBLY_SEARCH_PATHS` environment variable is set correctly.</span></span> <span data-ttu-id="667a2-164">Powinna to być ścieżka zawierająca `mySparkApp.dll`.</span><span class="sxs-lookup"><span data-stu-id="667a2-164">It should be the path that contains your `mySparkApp.dll`.</span></span>

### <a name="after-i-upgraded-my-net-for-apache-spark-version-and-reset-the-dotnet_worker_dir-environment-variable-why-do-i-still-get-the-following-ioexception-error"></a><span data-ttu-id="667a2-165">Dlaczego po uaktualnieniu wersji platformy .NET dla Apache Spark i zresetowaniu zmiennej środowiskowej `DOTNET_WORKER_DIR` nadal pojawia się następujący błąd `IOException`?</span><span class="sxs-lookup"><span data-stu-id="667a2-165">After I upgraded my .NET for Apache Spark version and reset the `DOTNET_WORKER_DIR` environment variable, why do I still get the following `IOException` error?</span></span>
> <span data-ttu-id="667a2-166">**Błąd:** Utracono zadanie 0,0 w fazie 11,0 (TID 24, localhost, sterownik wykonujący): Java. IO. IOException: nie można uruchomić programu "Microsoft. Spark. Worker. exe": błąd CreateProcess = 2, system nie może odnaleźć określonego pliku.</span><span class="sxs-lookup"><span data-stu-id="667a2-166">**Error:** Lost task 0.0 in stage 11.0 (TID 24, localhost, executor driver): java.io.IOException: Cannot run program "Microsoft.Spark.Worker.exe": CreateProcess error=2, The system cannot find the file specified.</span></span>

<span data-ttu-id="667a2-167">**Odpowiedź:** Spróbuj ponownie uruchomić okno programu PowerShell (lub inne okna poleceń), aby można było pobrać najnowsze wartości zmiennych środowiskowych.</span><span class="sxs-lookup"><span data-stu-id="667a2-167">**Answer:** Try restarting your PowerShell window (or other command windows) first so that it can take the latest environment variable values.</span></span> <span data-ttu-id="667a2-168">Następnie uruchom program.</span><span class="sxs-lookup"><span data-stu-id="667a2-168">Then start your program.</span></span>

### <a name="after-submitting-my-spark-application-i-get-the-error-systemtypeloadexception-could-not-load-type-systemruntimeremotingcontextscontext"></a><span data-ttu-id="667a2-169">Po przesłaniu aplikacji platformy Spark otrzymuję błąd `System.TypeLoadException: Could not load type 'System.Runtime.Remoting.Contexts.Context'`.</span><span class="sxs-lookup"><span data-stu-id="667a2-169">After submitting my Spark application, I get the error `System.TypeLoadException: Could not load type 'System.Runtime.Remoting.Contexts.Context'`.</span></span>
> <span data-ttu-id="667a2-170">**Błąd:** [błąd] [TaskRunner] [0] ProcessStream () nie powiodło się. wyjątek: System. TypeLoadException: nie można załadować typu "System. Runtime. Komunikacja zdalna. Contexts. kontekst" z zestawu "mscorlib, Version = 4.0.0.0, Culture = neutral, PublicKeyToken =...".</span><span class="sxs-lookup"><span data-stu-id="667a2-170">**Error:** [Error] [TaskRunner] [0] ProcessStream() failed with exception: System.TypeLoadException: Could not load type 'System.Runtime.Remoting.Contexts.Context' from assembly 'mscorlib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=...'.</span></span>

<span data-ttu-id="667a2-171">**Odpowiedź:** Sprawdź używaną wersję `Microsoft.Spark.Worker`.</span><span class="sxs-lookup"><span data-stu-id="667a2-171">**Answer:** Check the `Microsoft.Spark.Worker` version you are using.</span></span> <span data-ttu-id="667a2-172">Istnieją dwie wersje: **.NET Framework 4.6.1** i **.NET Core 2.1. x**.</span><span class="sxs-lookup"><span data-stu-id="667a2-172">There are two versions: **.NET Framework 4.6.1** and **.NET Core 2.1.x**.</span></span> <span data-ttu-id="667a2-173">W takim przypadku należy użyć `Microsoft.Spark.Worker.net461.win-x64-<version>` (którą można [pobrać](https://github.com/dotnet/spark/releases)), ponieważ `System.Runtime.Remoting.Contexts.Context` ma tylko .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="667a2-173">In this case, `Microsoft.Spark.Worker.net461.win-x64-<version>` (which you can [download](https://github.com/dotnet/spark/releases)) should be used since `System.Runtime.Remoting.Contexts.Context` is only for .NET Framework.</span></span>

### <a name="how-do-i-run-my-spark-application-with-udfs-on-yarn-which-environment-variables-and-parameters-should-i-use"></a><span data-ttu-id="667a2-174">Jak mogę uruchomić moją aplikację Spark z UDF na PRZĘDZę?</span><span class="sxs-lookup"><span data-stu-id="667a2-174">How do I run my spark application with UDFs on YARN?</span></span> <span data-ttu-id="667a2-175">Których zmiennych środowiskowych i parametrów należy użyć?</span><span class="sxs-lookup"><span data-stu-id="667a2-175">Which environment variables and parameters should I use?</span></span>

<span data-ttu-id="667a2-176">**Odpowiedź:** Aby uruchomić aplikację Spark w ramach PRZĘDZy, zmienne środowiskowe należy określić jako `spark.yarn.appMasterEnv.[EnvironmentVariableName]`.</span><span class="sxs-lookup"><span data-stu-id="667a2-176">**Answer:** To launch the spark application on YARN, the environment variables should be specified as `spark.yarn.appMasterEnv.[EnvironmentVariableName]`.</span></span> <span data-ttu-id="667a2-177">Poniżej przedstawiono przykład użycia `spark-submit`:</span><span class="sxs-lookup"><span data-stu-id="667a2-177">Please see below as an example using `spark-submit`:</span></span>

```powershell
spark-submit \
--class org.apache.spark.deploy.dotnet.DotnetRunner \
--master yarn \
--deploy-mode cluster \
--conf spark.yarn.appMasterEnv.DOTNET_WORKER_DIR=./worker/Microsoft.Spark.Worker-<version> \
--conf spark.yarn.appMasterEnv.DOTNET_ASSEMBLY_SEARCH_PATHS=./udfs \
--archives hdfs://<path to your files>/Microsoft.Spark.Worker.net461.win-x64-<version>.zip#worker,hdfs://<path to your files>/mySparkApp.zip#udfs \
hdfs://<path to jar file>/microsoft-spark-2.4.x-<version>.jar \
hdfs://<path to your files>/mySparkApp.zip mySparkApp
```

## <a name="next-steps"></a><span data-ttu-id="667a2-178">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="667a2-178">Next steps</span></span>

* [<span data-ttu-id="667a2-179">Wprowadzenie do platformy .NET dla Apache Spark</span><span class="sxs-lookup"><span data-stu-id="667a2-179">Get started with .NET for Apache Spark</span></span>](../tutorials/get-started.md)
* [<span data-ttu-id="667a2-180">Debugowanie aplikacji .NET dla Apache Spark w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="667a2-180">Debug a .NET for Apache Spark application on Windows</span></span>](../how-to-guides/debug.md)