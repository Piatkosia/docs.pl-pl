---
ms.openlocfilehash: 19002cce40fdc929716a761a5e01303be4decb35
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90537834"
---
Nie trzeba uruchamiać programu [`dotnet restore`](~/docs/core/tools/dotnet-restore.md) , ponieważ jest on uruchamiany niejawnie przez wszystkie polecenia, które wymagają wykonania przywracania, takie jak,,,, `dotnet new` `dotnet build` `dotnet run` `dotnet test` `dotnet publish` i `dotnet pack` . Aby wyłączyć Przywracanie niejawne, użyj `--no-restore` opcji.

`dotnet restore`Polecenie jest nadal przydatne w niektórych scenariuszach, w których jawne jest przywracanie, takie jak [kompilacje ciągłej integracji w Azure DevOps Services](/azure/devops/build-release/apps/aspnet/build-aspnet-core) lub w systemach kompilacji, które muszą jawnie kontrolować po wystąpieniu przywracania.

Informacje o sposobach zarządzania źródłami danych NuGet znajdują się w [ `dotnet restore` dokumentacji](../docs/core/tools/dotnet-restore.md).

To polecenie obsługuje `dotnet restore` Opcje, gdy są przesyłane w postaci długiej (na przykład `--source` ). Opcje krótkiej formy, takie jak `-s` , nie są obsługiwane.
