---
title: 'Samouczek: model klasyfikacji obrazów ML.NET z TensorFlow'
description: Dowiedz się, jak przenieść wiedzę z istniejącego modelu TensorFlow do nowego modelu klasyfikacji obrazów ML.NET. Model TensorFlow został przeszkolony do klasyfikowania obrazów do tysięcy kategorii. Model ML.NET wykorzystuje uczenie transferu do klasyfikowania obrazów do mniejszej liczby szerszej kategorii.
ms.date: 06/30/2020
ms.topic: tutorial
ms.custom: mvc, title-hack-0612
ms.openlocfilehash: a4c671816dce1fe2abdf77f81da0f27236136536
ms.sourcegitcommit: 97ce5363efa88179dd76e09de0103a500ca9b659
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/13/2020
ms.locfileid: "86282115"
---
# <a name="tutorial-generate-an-mlnet-image-classification-model-from-a-pre-trained-tensorflow-model"></a>Samouczek: Generowanie modelu klasyfikacji obrazów ML.NET na podstawie wstępnie nauczonego modelu TensorFlow

Dowiedz się, jak przenieść wiedzę z istniejącego modelu TensorFlow do nowego modelu klasyfikacji obrazów ML.NET.

Model TensorFlow został przeszkolony do klasyfikowania obrazów do tysięcy kategorii. Model ML.NET wykorzystuje część modelu TensorFlow w potoku do uczenia modelu do klasyfikowania obrazów do 3 kategorii.

Uczenie modelu [klasyfikacji obrazów](https://en.wikipedia.org/wiki/Outline_of_object_recognition) od podstaw wymaga ustawienia milionów parametrów, moc z etykietami danych szkoleniowych i ogromną ilość zasobów obliczeniowych (setki godzin procesora GPU). Chociaż nie jest tak wydajny, jak uczenie modelu niestandardowego od podstaw, uczenie przenoszenia pozwala na podjęcie tego procesu przez pracę z tysiącami obrazów i milionów obrazów z etykietami, a następnie szybko utworzyć dostosowany model (w ciągu godziny na maszynie bez procesora GPU). Ten samouczek skaluje się jeszcze bardziej dokładnie przy użyciu dziesiątych obrazów szkoleniowych.

Z tego samouczka dowiesz się, jak wykonywać następujące czynności:
> [!div class="checklist"]
>
> * Omówienie problemu
> * Uwzględnij wstępnie szkolony model TensorFlow do potoku ML.NET
> * Uczenie i szacowanie modelu ML.NET
> * Klasyfikowanie obrazu testowego

Kod źródłowy dla tego samouczka można znaleźć w repozytorium [dotnet/Samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/TransferLearningTF) . Należy pamiętać, że domyślnie konfiguracja projektu .NET dla tego samouczka dotyczy platformy .NET Core 2,2.

## <a name="what-is-transfer-learning"></a>Co to jest uczenie transferowe?

Nauka transferu to proces korzystania z wiedzy zdobytej podczas rozwiązywania jednego problemu i stosowania go do innego, ale związanego z nim problemu.

Na potrzeby tego samouczka należy użyć części TensorFlow model — przeszkolonej do klasyfikowania obrazów do tysięcy kategorii — w modelu ML.NET, który klasyfikuje obrazy do 3 kategorii.

## <a name="prerequisites"></a>Wymagania wstępne

* [Program Visual studio 2019](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) lub nowszy albo program visual Studio 2017 w wersji 15,6 lub nowszej z zainstalowanym obciążeniem "Programowanie dla wielu platform" platformy .NET Core.
* [Katalog zasobów samouczka. Plik ZIP](https://github.com/dotnet/samples/blob/master/machine-learning/tutorials/TransferLearningTF/image-classifier-assets.zip)
* [Model uczenia maszynowego InceptionV1](https://storage.googleapis.com/download.tensorflow.org/models/inception5h.zip)

## <a name="select-the-right-machine-learning-task"></a>Wybierz odpowiednie zadanie uczenia maszynowego

### <a name="deep-learning"></a>Uczenie głębokie

[Uczenie głębokie](https://en.wikipedia.org/wiki/Deep_learning) to podzbiór Machine Learning, które są obszarami revolutionizing, takimi jak przetwarzanie obrazów i rozpoznawanie mowy.

Modele uczenia głębokiego są przeszkolone przy użyciu dużych zestawów [danych z etykietami](https://en.wikipedia.org/wiki/Labeled_data) i [sieci neuronowych](https://en.wikipedia.org/wiki/Artificial_neural_network) , które zawierają wiele warstw szkoleniowych. Uczenie głębokie:

* Wykonuje lepsze zadania, takie jak przetwarzanie obrazów.
* Wymaga ogromnych ilości danych szkoleniowych.

Klasyfikacja obrazu to typowe zadanie Machine Learning, które pozwala nam na automatyczne klasyfikowanie obrazów do kategorii, takich jak:

* Wykrywanie ludzkiej twarz w obrazie.
* Wykrywanie kotów a psy.

 Lub jak na następujących ilustracjach, określenie, czy obraz jest (n) jedzeniem, Zabawka lub urządzeniem:

![obraz przedstawiający obraz przedstawiający zdjęcie z obrazu Pizza ](./media/image-classification/220px-Pepperoni_pizza.jpg)
 ![ Teddy ](./media/image-classification/119px-Nalle_-_a_small_brown_teddy_bear.jpg)
 ![](./media/image-classification/193px-Broodrooster.jpg)

>[!Note]
> Powyższe obrazy należą do Wikimedia Commons Attribution i są przypisywane w następujący sposób:
>
> * Domena publiczna "220px-Pepperoni_pizza.jpg", <https://commons.wikimedia.org/w/index.php?curid=79505> ,
> * "119px-Nalle_-_a_small_brown_teddy_bear.jpg" przez [Jonik](https://commons.wikimedia.org/wiki/User:Jonik) -własne grafy, CC według-sa 2,0, <https://commons.wikimedia.org/w/index.php?curid=48166> .
> * "193px-Broodrooster.jpg" według [Minderhoud](https://nl.wikipedia.org/wiki/Gebruiker:Michiel1972) pracy, CC według-sa 3,0,<https://commons.wikimedia.org/w/index.php?curid=27403>

`Inception model`Program jest szkolony do klasyfikowania obrazów do tysięcy kategorii, ale w tym samouczku należy sklasyfikować obrazy w mniejszym zestawie kategorii i tylko te kategorie. Wprowadź `transfer` część elementu `transfer learning` . Można przenieść `Inception model` możliwość rozpoznawania i klasyfikowania obrazów do nowych, ograniczonej kategorii klasyfikatora niestandardowego obrazu.

* Żywności
* Zabawki
* Wprowadzony

W tym samouczku jest [stosowany model uczenia głębokiego](https://storage.googleapis.com/download.tensorflow.org/models/inception5h.zip) "TensorFlow", popularny model rozpoznawania obrazów przeszkolony na `ImageNet` zestawie danych. Model TensorFlow klasyfikuje całe obrazy do tysięcy klas, takich jak "parasol", "Jersey" i "zmywarka".

Ponieważ `Inception model` program został już wstępnie przeszkolony na tysiącach różnych obrazów, wewnętrznie zawiera [funkcje obrazu](https://en.wikipedia.org/wiki/Feature_(computer_vision)) niezbędne do identyfikacji obrazu. Firma Microsoft może używać tych funkcji obrazu wewnętrznego w modelu do uczenia nowego modelu z znacznie mniejszą liczbą klas.

Jak pokazano na poniższym diagramie, należy dodać odwołanie do pakietów NuGet ML.NET w aplikacjach .NET Core lub .NET Framework. W obszarze okładki ML.NET obejmuje i odwołuje się do biblioteki natywnej, `TensorFlow` która umożliwia pisanie kodu ładującego istniejący plik z modelem wyszkolonym `TensorFlow` .

![Diagram TensorFlow transformacji ML.NET](./media/image-classification/tensorflow-mlnet.png)

### <a name="multiclass-classification"></a>Klasyfikacja wieloklasowa

Po użyciu modelu rozpoczęcia TensorFlow do wyodrębnienia funkcji odpowiednich jako dane wejściowe dla klasycznego algorytmu uczenia maszynowego dodaliśmy ML.NET [klasyfikatora wieloklasowego](../resources/tasks.md#multiclass-classification).

Konkretny Trainer używany w tym przypadku jest [algorytmem regresji logistycznej](https://en.wikipedia.org/wiki/Multinomial_logistic_regression).

Algorytm wdrożony przez ten Trainer działa dobrze w przypadku problemów z dużą liczbą funkcji, czyli dla modelu uczenia głębokiego działającego na danych obrazu.

### <a name="data"></a>Dane

Istnieją dwa źródła danych: `.tsv` plik i pliki obrazów.  `tags.tsv`Plik zawiera dwie kolumny: pierwszy jest zdefiniowany jako `ImagePath` , a drugi jest `Label` odpowiadający obrazowi. Następujący przykładowy plik nie ma wiersza nagłówka i wygląda następująco:

<!-- markdownlint-disable MD010 -->
```tsv
broccoli.jpg    food
pizza.jpg   food
pizza2.jpg  food
teddy2.jpg  toy
teddy3.jpg  toy
teddy4.jpg  toy
toaster.jpg appliance
toaster2.png    appliance
```
<!-- markdownlint-enable MD010 -->

Obrazy szkoleniowe i testowe znajdują się w folderach zasobów, które zostaną pobrane w pliku zip. Te obrazy należą do Wikimedia Commons Attribution.
> *[Wikimedia Commons Attribution](https://commons.wikimedia.org/w/index.php?title=Main_Page&oldid=313158208), repozytorium wolnych nośników.* Pobrano 10:48, 17 października 2018 z:<https://commons.wikimedia.org/wiki/Pizza>
> <https://commons.wikimedia.org/wiki/Toaster>
> <https://commons.wikimedia.org/wiki/Teddy_bear>

## <a name="setup"></a>Konfigurowanie

### <a name="create-a-project"></a>Tworzenie projektu

1. Utwórz **aplikację konsolową .NET Core** o nazwie "TransferLearningTF".

1. Zainstaluj **pakiet NuGet Microsoft.ml**:

    [!INCLUDE [mlnet-current-nuget-version](../../../includes/mlnet-current-nuget-version.md)]

    * W Eksplorator rozwiązań kliknij prawym przyciskiem myszy projekt i wybierz polecenie **Zarządzaj pakietami NuGet**.
    * Wybierz pozycję "nuget.org" jako źródło pakietu, wybierz kartę Przeglądaj, Wyszukaj pozycję **Microsoft.ml**.
    * Wybierz przycisk **Instaluj** .
    * Wybierz przycisk **OK** w oknie dialogowym **Podgląd zmian** .
    * Jeśli zgadzasz się z postanowieniami licencyjnymi dotyczącymi wymienionych pakietów, **Wybierz przycisk Akceptuję w oknie** dialogowym **akceptacji licencji** .
    * Powtórz te kroki dla **Microsoft. ml. ImageAnalytics**, **SciSharp. TensorFlow. Redist** i **Microsoft. ml. TensorFlow**.

### <a name="download-assets"></a>Pobierz zasoby

1. Pobierz [plik zip katalogu zasobów projektu](https://github.com/dotnet/samples/blob/master/machine-learning/tutorials/TransferLearningTF/image-classifier-assets.zip)i rozpakuj.

1. Skopiuj `assets` katalog do katalogu projektu *TransferLearningTF* . Ten katalog i jego podkatalogi zawierają pliki danych i obsługi (z wyjątkiem modelu, który zostanie pobrany i dodany w następnym kroku), co jest potrzebne w tym samouczku.

1. Pobierz [model rozpoczęcia](https://storage.googleapis.com/download.tensorflow.org/models/inception5h.zip)i rozpakuj.

1. Skopiuj zawartość `inception5h` katalogu w sposób niespakowany do katalogu projektu *TransferLearningTF* `assets/inception` . Ten katalog zawiera model i dodatkowe pliki pomocnicze, które są odpowiednie dla tego samouczka, jak pokazano na poniższej ilustracji:

   ![Zawartość katalogu początkowej](./media/image-classification/inception-files.png)

1. W Eksplorator rozwiązań kliknij prawym przyciskiem myszy każdy plik w katalogu zasobów i podkatalogach i wybierz polecenie **Właściwości**. W obszarze **Zaawansowane**Zmień wartość opcji **Kopiuj do katalogu wyjściowego** na Kopiuj, **jeśli nowszy**.

### <a name="create-classes-and-define-paths"></a>Tworzenie klas i Definiowanie ścieżek

1. Dodaj następujące dodatkowe `using` instrukcje na początku pliku *program.cs* :

    [!code-csharp[AddUsings](./snippets/image-classification/csharp/Program.cs#AddUsings)]

1. Dodaj następujący kod do wiersza bezpośrednio powyżej `Main` metody, aby określić ścieżki zasobów:

    [!code-csharp[DeclareGlobalVariables](./snippets/image-classification/csharp/Program.cs#DeclareGlobalVariables)]

1. Twórz klasy dla danych wejściowych i prognoz.

    [!code-csharp[DeclareImageData](./snippets/image-classification/csharp/Program.cs#DeclareImageData)]

    `ImageData`jest klasą danych obrazu wejściowego i ma następujące <xref:System.String> pola:

    * `ImagePath`zawiera nazwę pliku obrazu.
    * `Label`zawiera wartość etykiety obrazu.

1. Dodaj nową klasę do projektu dla `ImagePrediction` :

    [!code-csharp[DeclareImagePrediction](./snippets/image-classification/csharp/Program.cs#DeclareImagePrediction)]

    `ImagePrediction`jest klasą przewidywania obrazów i ma następujące pola:

    * `Score`zawiera procent zaufania dla danej klasyfikacji obrazu.
    * `PredictedLabelValue`zawiera wartość dla etykiety klasyfikacji predykcyjnej obrazu.

    `ImagePrediction`jest klasą używaną do przewidywania po przeszkoleniu modelu. Ma `string` ( `ImagePath` ) dla ścieżki obrazu. Służy `Label` do ponownego użycia i nauczenia modelu. `PredictedLabelValue`Jest używany podczas przewidywania i oceny. W celu dokonania oceny dane wejściowe z danymi szkoleniowymi, przewidywane wartości i model są używane.

### <a name="initialize-variables-in-main"></a>Inicjuj zmienne w głównym

1. Zainicjuj `mlContext` zmienną z nowym wystąpieniem `MLContext` .  Zamień `Console.WriteLine("Hello World!")` wiersz na następujący kod w `Main` metodzie:

    [!code-csharp[CreateMLContext](./snippets/image-classification/csharp/Program.cs#CreateMLContext)]

    [Klasa MLContext](xref:Microsoft.ML.MLContext) jest punktem początkowym dla wszystkich operacji ml.NET, a inicjowanie `mlContext` tworzy nowe środowisko ml.NET, które może być współużytkowane przez obiekty przepływu pracy tworzenia modelu. Jest to podobne, pojęciowo do `DBContext` w Entity Framework.

### <a name="create-a-struct-for-inception-model-parameters"></a>Tworzenie struktury dla parametrów modelu rozpoczęcia

1. Model rozpoczęcia zawiera kilka parametrów, które należy przekazać. Utwórz strukturę służącą do mapowania wartości parametrów na przyjazne nazwy o następującym kodzie, zaraz po `Main()` metodzie:

    [!code-csharp[InceptionSettings](./snippets/image-classification/csharp/Program.cs#InceptionSettings)]

### <a name="create-a-display-utility-method"></a>Utwórz metodę narzędzia do wyświetlania

Ponieważ wyświetlasz dane obrazu i powiązane przewidywania więcej niż raz, Utwórz metodę narzędzia do wyświetlania, aby obsłużyć wyświetlanie obrazu i wyników przewidywania.

1. Utwórz `DisplayResults()` metodę, tuż po `InceptionSettings` strukturze, przy użyciu następującego kodu:

    ```csharp
    private static void DisplayResults(IEnumerable<ImagePrediction> imagePredictionData)
    {

    }
    ```

1. Wypełnij treść `DisplayResults` metody:

    [!code-csharp[DisplayPredictions](./snippets/image-classification/csharp/Program.cs#DisplayPredictions)]

### <a name="create-a-tsv-file-utility-method"></a>Tworzenie metody narzędziowej pliku. tsv

1. Utwórz `ReadFromTsv()` metodę, tuż po `DisplayResults()` metodzie, przy użyciu następującego kodu:

    ```csharp
    public static IEnumerable<ImageData> ReadFromTsv(string file, string folder)
    {

    }
    ```

1. Wypełnij treść `ReadFromTsv` metody:

    [!code-csharp[ReadFromTsv](./snippets/image-classification/csharp/Program.cs#ReadFromTsv)]

    Kod analizuje `tags.tsv` plik, aby dodać ścieżkę pliku do nazwy pliku obrazu dla `ImagePath` właściwości i załadować ją oraz `Label` do `ImageData` obiektu.

### <a name="create-a-method-to-make-a-prediction"></a>Tworzenie metody do prognozowania

1. Utwórz `ClassifySingleImage()` metodę, tuż przed `DisplayResults()` metodą, przy użyciu następującego kodu:

    ```csharp
    public static void ClassifySingleImage(MLContext mlContext, ITransformer model)
    {

    }
    ```

1. Utwórz `ImageData` obiekt, który zawiera w pełni kwalifikowaną ścieżkę i nazwę pliku obrazu dla jednego `ImagePath` . Dodaj następujący kod jako następny wiersz w `ClassifySingleImage()` metodzie:

    [!code-csharp[LoadImageData](./snippets/image-classification/csharp/Program.cs#LoadImageData)]

1. Utwórz jedno prognozowanie, dodając następujący kod jako następny wiersz w `ClassifySingleImage` metodzie:

    [!code-csharp[PredictSingle](./snippets/image-classification/csharp/Program.cs#PredictSingle)]

    Aby uzyskać prognozę, użyj metody [przewidywania ()](xref:Microsoft.ML.PredictionEngine%602.Predict%2A) . [PredictionEngine](xref:Microsoft.ML.PredictionEngine%602) jest WYGODNYm interfejsem API, który umożliwia prognozowanie jednego wystąpienia danych. [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602)nie jest bezpieczny wątkowo. Jest to możliwe do użycia w środowiskach wielowątkowych lub prototypowych. Aby zwiększyć wydajność i bezpieczeństwo wątków w środowiskach produkcyjnych, należy użyć `PredictionEnginePool` usługi, która tworzy [`ObjectPool`](xref:Microsoft.Extensions.ObjectPool.ObjectPool%601) [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) obiekty do użycia w całej aplikacji. Zapoznaj się z tym przewodnikiem dotyczącym [korzystania `PredictionEnginePool` z programu w ASP.NET Core INTERNETowym interfejsie API](../how-to-guides/serve-model-web-api-ml-net.md#register-predictionenginepool-for-use-in-the-application).

    > [!NOTE]
    > `PredictionEnginePool`rozszerzenie usługi jest obecnie w wersji zapoznawczej.

1. Wyświetl wynik przewidywania jako następny wiersz kodu w `ClassifySingleImage()` metodzie:

   [!code-csharp[DisplayPrediction](./snippets/image-classification/csharp/Program.cs#DisplayPrediction)]

## <a name="construct-the-mlnet-model-pipeline"></a>Konstruowanie potoku modelu ML.NET

Potok modelu ML.NET jest łańcuchem szacowania. Należy pamiętać, że podczas konstruowania potoku nie jest wykonywane żadne wykonanie. Obiekty szacowania są tworzone, ale nie wykonywane.

1. Dodawanie metody w celu wygenerowania modelu

    Ta metoda jest sercem samouczka. Tworzy potok dla modelu i pociąga potok w celu utworzenia modelu ML.NET. Oblicza również model dla niektórych poprzednio niewidocznych danych testowych.

    Utwórz `GenerateModel()` metodę, tuż po `InceptionSettings` strukturze i tuż przed `DisplayResults()` metodą, używając następującego kodu:

    ```csharp
    public static ITransformer GenerateModel(MLContext mlContext)
    {

    }
    ```

1. Dodaj szacowania do ładowania, zmiany rozmiaru i wyodrębnienia pikseli z danych obrazu:

    [!code-csharp[ImageTransforms](./snippets/image-classification/csharp/Program.cs#ImageTransforms)]

    Dane obrazu należy przetworzyć w formacie, którego oczekuje model TensorFlow. W takim przypadku obrazy są ładowane do pamięci, zmieniono rozmiar do spójnego rozmiaru, a piksele są wyodrębniane do wektora liczbowego.

1. Dodaj szacowania, aby załadować model TensorFlow i wypróbować go:

    [!code-csharp[ScoreTensorFlowModel](./snippets/image-classification/csharp/Program.cs#ScoreTensorFlowModel)]

    Ten etap w potoku ładuje model TensorFlow do pamięci, a następnie przetwarza wektor wartości pikseli za pomocą sieci modelu TensorFlow. Zastosowanie danych wejściowych do modelu uczenia głębokiego i wygenerowanie danych wyjściowych przy użyciu modelu jest określane jako **ocenianie**. Gdy w całości korzystasz z modelu, ocenianie wykonuje wnioskowanie lub prognozowanie.

    W takim przypadku należy użyć wszystkich modeli TensorFlow z wyjątkiem ostatniej warstwy, czyli warstwy, która wykonuje wnioskowanie. Dane wyjściowe przedostatniej warstwy są oznaczone etykietami `softmax_2_preactivation` . Dane wyjściowe tej warstwy są efektywnie wektorami funkcji, które charakteryzują się oryginalnymi obrazami wejściowymi.

    Ten wektor funkcji generowany przez model TensorFlow będzie używany jako dane wejściowe do algorytmu szkolenia ML.NET.

1. Dodaj szacowania, aby zamapować etykiety ciągów w wartości klucza danych szkoleniowych do liczby całkowitej:

    [!code-csharp[MapValueToKey](./snippets/image-classification/csharp/Program.cs#MapValueToKey)]

    Dołączany dalej ML.NET Trainer wymaga, aby etykiety były w formacie, `key` a nie jako dowolne ciągi. Klucz to liczba, która ma jeden do jednego mapowania do wartości ciągu.

1. Dodaj algorytm szkoleniowy ML.NET:

    [!code-csharp[AddTrainer](./snippets/image-classification/csharp/Program.cs#AddTrainer)]

1. Dodaj szacowania, aby zamapować przewidywalną wartość klucza z powrotem na ciąg:

    [!code-csharp[MapKeyToValue](./snippets/image-classification/csharp/Program.cs#MapKeyToValue)]

## <a name="train-the-model"></a>Szkolenie modelu

1. Załaduj dane szkoleniowe przy użyciu otoki [LoadFromTextFile](xref:Microsoft.ML.TextLoaderSaverCatalog.LoadFromTextFile(Microsoft.ML.DataOperationsCatalog,System.String,Microsoft.ML.Data.TextLoader.Options)) . Dodaj następujący kod w następnym wierszu `GenerateModel()` metody:

    [!code-csharp[LoadData](./snippets/image-classification/csharp/Program.cs#LoadData "Load the data")]

    Dane w ML.NET są reprezentowane jako [Klasa IDataView](xref:Microsoft.ML.IDataView). `IDataView`to elastyczny i wydajny sposób opisywania danych tabelarycznych (liczbowych i tekstowych). Dane można ładować z pliku tekstowego lub w czasie rzeczywistym (na przykład bazy danych SQL lub plików dziennika) do `IDataView` obiektu.

1. Uczenie modelu z danymi załadowanymi powyżej:

    [!code-csharp[TrainModel](./snippets/image-classification/csharp/Program.cs#TrainModel)]

    `Fit()`Metoda pociąga za siebie model, stosując zestaw danych szkoleniowych do potoku.

## <a name="evaluate-the-accuracy-of-the-model"></a>Oceń dokładność modelu

1. Załaduj i Przekształć dane testowe, dodając następujący kod do następnego wiersza `GenerateModel` metody:

    [!code-csharp[LoadAndTransformTestData](./snippets/image-classification/csharp/Program.cs#LoadAndTransformTestData "Load and transform test data")]

    Istnieje kilka przykładowych obrazów, których można użyć do oszacowania modelu. Podobnie jak dane szkoleniowe, muszą zostać załadowane do `IDataView` , aby mogły być przekształcone przez model.

1. Dodaj następujący kod do `GenerateModel()` metody w celu obliczenia modelu:

    [!code-csharp[Evaluate](./snippets/image-classification/csharp/Program.cs#Evaluate)]

    Po wybraniu zestawu prognoz Metoda [szacowania ()](xref:Microsoft.ML.RecommendationCatalog.Evaluate%2A) :

    * Ocenia model (porównuje wartości przewidywane z testowym zestawem danych `labels` ).
    * Zwraca metryki wydajności modelu.

1. Wyświetl metryki dokładności modelu

    Użyj poniższego kodu, aby wyświetlić metryki, Udostępnij wyniki, a następnie wykonaj na nich czynności:

    [!code-csharp[DisplayMetrics](./snippets/image-classification/csharp/Program.cs#DisplayMetrics)]

    Następujące metryki są oceniane pod kątem klasyfikacji obrazów:

    * `Log-loss`-Zobacz [utrata dzienników](../resources/glossary.md#log-loss). Utrata dziennika powinna być jak najbliżej zera.
    * `Per class Log-loss`. Dla każdej klasy Dziennik ma być zbliżony do zera, jak to możliwe.

1. Dodaj następujący kod, aby zwrócić przeszkolony model jako następny wiersz:

    [!code-csharp[SaveModel](./snippets/image-classification/csharp/Program.cs#ReturnModel)]

## <a name="run-the-application"></a>Uruchom aplikację!

1. Dodaj wywołanie do `GenerateModel` w `Main` metodzie po utworzeniu klasy MLContext:

    [!code-csharp[CallGenerateModel](./snippets/image-classification/csharp/Program.cs#CallGenerateModel)]

1. Dodaj wywołanie do `ClassifySingleImage()` metody jako następny wiersz kodu w `Main` metodzie:

    [!code-csharp[CallClassifySingleImage](./snippets/image-classification/csharp/Program.cs#CallClassifySingleImage)]

1. Uruchom aplikację konsolową (Ctrl + F5). Wyniki powinny wyglądać podobnie do poniższych danych wyjściowych.  Mogą pojawić się ostrzeżenia lub komunikaty o przetwarzaniu, ale te komunikaty zostały usunięte z następujących wyników dla przejrzystości.

    ```console
    =============== Training classification model ===============
    Image: broccoli2.jpg predicted as: food with score: 0.8955513
    Image: pizza3.jpg predicted as: food with score: 0.9667718
    Image: teddy6.jpg predicted as: toy with score: 0.9797683
    =============== Classification metrics ===============
    LogLoss is: 0.0653774699265059
    PerClassLogLoss is: 0.110315812569315 , 0.0204391272836966 , 0
    =============== Making single image classification ===============
    Image: toaster3.jpg predicted as: appliance with score: 0.9646884
    ```

Gratulacje! Pomyślnie skompilowano model uczenia maszynowego na potrzeby klasyfikacji obrazów przez zastosowanie uczenia przeniesienia do `TensorFlow` modelu w ml.NET.

Kod źródłowy dla tego samouczka można znaleźć w repozytorium [dotnet/Samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/TransferLearningTF) .

W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:
> [!div class="checklist"]
>
> * Omówienie problemu
> * Uwzględnij wstępnie szkolony model TensorFlow do potoku ML.NET
> * Uczenie i szacowanie modelu ML.NET
> * Klasyfikowanie obrazu testowego

Zapoznaj się z przykładem Machine Learning przykładowe repozytorium GitHub, aby poznać rozszerzoną próbkę klasyfikacji obrazów.
> [!div class="nextstepaction"]
> [dotnet/machinelearning — przykłady repozytorium GitHub](https://github.com/dotnet/machinelearning-samples/)
