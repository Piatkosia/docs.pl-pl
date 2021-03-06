---
ms.openlocfilehash: 2edb06106283c26573863f230e5e9956728cdfa3
ms.sourcegitcommit: b1442669f1982d3a1cb18ea35b5acfb0fc7d93e4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2020
ms.locfileid: "93135572"
---

### <a name="install-the-sdk"></a>Instalacja zestawu SDK

Zestaw .NET Core SDK umożliwia tworzenie aplikacji przy użyciu platformy .NET Core. W przypadku zainstalowania zestaw .NET Core SDK nie trzeba instalować odpowiedniego środowiska uruchomieniowego. Aby zainstalować zestaw .NET Core SDK, uruchom następujące polecenia:

```bash
sudo dnf install dotnet-sdk-3.1
```

### <a name="install-the-runtime"></a>Instalowanie środowiska uruchomieniowego

Środowisko uruchomieniowe programu .NET Core umożliwia uruchamianie aplikacji, które zostały wykonane przy użyciu platformy .NET Core, które nie zawierały środowiska uruchomieniowego. Następujące polecenia instalują środowisko uruchomieniowe ASP.NET Core, które jest najbardziej zgodnym środowiskiem uruchomieniowym dla platformy .NET Core. W terminalu uruchom następujące polecenia.

```bash
sudo dnf install aspnetcore-runtime-3.1
```

Jako alternatywę dla środowiska uruchomieniowego ASP.NET Core można zainstalować środowisko uruchomieniowe programu .NET Core, które nie obejmuje ASP.NET Core Support: Zastąp `aspnetcore-runtime-3.1` w poprzednim poleceniu poleceniem `dotnet-runtime-3.1` .

```bash
sudo dnf install dotnet-runtime-3.1
```
