---
ms.openlocfilehash: dc9f37ae0cd6eef2c67e62421571290bba1c2233
ms.sourcegitcommit: 2e95559d957a1a942e490c5fd916df04b39d73a9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/16/2019
ms.locfileid: "72393983"
---
### <a name="mvc-async-suffix-trimmed-from-controller-action-names"></a>MVC: sufiks Async został przycięty z nazw akcji kontrolera

W ramach adresowania [ASPNET/AspNetCore # 4849](https://github.com/aspnet/AspNetCore/issues/4849), ASP.NET Core MVC domyślnie przycina sufiks `Async` z nazw akcji. Począwszy od ASP.NET Core 3,0, ta zmiana ma wpływ na generowanie routingu i linków.

#### <a name="version-introduced"></a>Wprowadzona wersja

3.0

#### <a name="old-behavior"></a>Stare zachowanie

Rozważmy następujący kontroler ASP.NET Core MVC:

```csharp
public class ProductController : Controller
{
    public async IActionResult ListAsync()
    {
        var model = await DbContext.Products.ToListAsync();
        return View(model);
    }
}
```

Akcja polega na włączeniu routingu za pośrednictwem `Product/ListAsync`. Generowanie linku wymaga określenia sufiksu `Async`. Na przykład:

```cshtml
<a asp-controller="Product" asp-action="ListAsync">List</a>
```

#### <a name="new-behavior"></a>Nowe zachowanie

W ASP.NET Core 3,0 akcja polega na włączeniu routingu za pośrednictwem `Product/List`. Kod generacji łącza powinien pominąć sufiks `Async`. Na przykład:

```cshtml
<a asp-controller="Product" asp-action="List">List</a>
```

Ta zmiana nie ma wpływu na nazwy określone przy użyciu atrybutu `[ActionName]`. Nowe zachowanie można wyłączyć, ustawiając `MvcOptions.SuppressAsyncSuffixInActionNames` do `false` w `Startup.ConfigureServices`:

```csharp
services.AddMvc(options =>
{
   options.SuppressAsyncSuffixInActionNames = false; 
});
```

#### <a name="reason-for-change"></a>Przyczyna zmiany

Zgodnie z Konwencją asynchroniczne metody .NET są sufiksem z `Async`. Jednak jeśli metoda definiuje akcję MVC, nie można użyć sufiksu `Async`.

#### <a name="recommended-action"></a>Zalecana akcja

Jeśli aplikacja zależy od akcji MVC z zachowaniem sufiksu `Async`, wybierz jedno z następujących środków zaradczych:

- Użyj atrybutu `[ActionName]`, aby zachować oryginalną nazwę.
- Wyłącz zmianę nazwy poprzez ustawienie `MvcOptions.SuppressAsyncSuffixInActionNames` na `false` w `Startup.ConfigureServices`:

```csharp
services.AddMvc(options =>
{
   options.SuppressAsyncSuffixInActionNames = false; 
});
```

#### <a name="category"></a>Kategoria

ASP.NET Core

#### <a name="affected-apis"></a>Dotyczy interfejsów API

Brak

<!-- 

#### Affected APIs

Not detectable via API analysis

-->