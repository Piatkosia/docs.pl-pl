---
title: 'Instrukcje: Tworzenie otok COM'
description: Tworzenie otok Component Object Model (COM) przy użyciu programu Visual Studio lub narzędzi .NET (Tlbimp.exe i Regasm.exe). Obie metody generują dwa typy otok COM.
ms.date: 03/30/2017
helpviewer_keywords:
- COM,wrappers creating
- COM,wrappers Visual Studio
ms.assetid: bdf89bea-1623-45ee-a57b-cf7c90395efa
ms.openlocfilehash: 286526c710287e6efa3e49a7f7c55e3687076e29
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/01/2020
ms.locfileid: "85617395"
---
# <a name="how-to-create-com-wrappers"></a>Instrukcje: Tworzenie otok COM

Otoki Component Object Model (COM) można tworzyć za pomocą funkcji programu Visual Studio 2005 lub narzędzi .NET Framework Tlbimp.exe i Regasm.exe. Obie metody generują dwa typy otok COM:

- Wywoływanie [otoki środowiska uruchomieniowego](../../standard/native-interop/runtime-callable-wrapper.md) z biblioteki typów w celu uruchomienia obiektu com w kodzie zarządzanym.

- Wywoływany przez [com otokę](../../standard/native-interop/com-callable-wrapper.md) z wymaganymi ustawieniami rejestru w celu uruchomienia obiektu zarządzanego w aplikacji natywnej.

W programie Visual Studio 2005 można dodać otokę COM jako odwołanie do projektu.

## <a name="wrap-com-objects-in-a-managed-application"></a>Zawijanie obiektów COM w aplikacji zarządzanej

### <a name="to-create-a-runtime-callable-wrapper-using-visual-studio"></a>Aby utworzyć oddzielną otokę środowiska uruchomieniowego przy użyciu programu Visual Studio

1. Otwórz projekt dla aplikacji zarządzanej.

2. W menu **projekt** kliknij polecenie **Pokaż wszystkie pliki**.

3. W menu **projekt** kliknij polecenie **Dodaj odwołanie**.

4. W oknie dialogowym Dodaj odwołanie kliknij kartę **com** , wybierz składnik, którego chcesz użyć, a następnie kliknij przycisk **OK**.

     W **Eksplorator rozwiązań**Zwróć uwagę, że składnik com jest dodawany do folderu References w projekcie.

Teraz można napisać kod, aby uzyskać dostęp do obiektu COM. Można rozpocząć od zadeklarowania obiektu, takiego jak `Imports` instrukcja Visual Basic lub `Using` instrukcji dla języka C#.

> [!NOTE]
> Jeśli chcesz programować Microsoft Office składniki, najpierw zainstaluj [pakiet redystrybucyjny podstawowych zestawów Międzyoperacyjnych Microsoft Office](https://www.microsoft.com/Download/details.aspx?id=3508).
  
### <a name="to-create-a-runtime-callable-wrapper-using-net-framework-tools"></a>Aby utworzyć oddzielną otokę środowiska uruchomieniowego przy użyciu narzędzi .NET Framework  
  
- Uruchom narzędzie [Tlbimp.exe (Importer biblioteki typów)](../tools/tlbimp-exe-type-library-importer.md) .  
  
 To narzędzie tworzy zestaw zawierający metadane czasu wykonywania dla typów zdefiniowanych w oryginalnej bibliotece typów.  
  
## <a name="wrap-managed-objects-in-a-native-application"></a>Zawijaj obiekty zarządzane w aplikacji natywnej  
  
### <a name="to-create-a-com-callable-wrapper-using-visual-studio"></a>Aby utworzyć zawywoływaną przez COM otokę przy użyciu programu Visual Studio  
  
1. Utwórz projekt biblioteki klas dla zarządzanej klasy, która ma być uruchamiana w kodzie natywnym. Klasa musi mieć konstruktora bez parametrów.  
  
     Sprawdź, czy dla Twojego zestawu w pliku AssemblyInfo masz pełny numer wersji z czterema częścią. Ta liczba jest wymagana do obsługi wersji w rejestrze systemu Windows. Aby uzyskać więcej informacji o numerach wersji, zobacz [wersja zestawu](../../standard/assembly/versioning.md).  
  
2. W menu **projekt** kliknij polecenie **Właściwości**.  
  
3. Kliknij kartę **kompilacja** .  
  
4. Zaznacz pole wyboru **Zarejestruj dla międzyoperacyjności modelu COM** .  
  
 Podczas kompilowania projektu zestaw jest automatycznie rejestrowany pod kątem współdziałania z modelem COM. Jeśli tworzysz aplikację natywną w programie Visual Studio 2005, możesz użyć zestawu, klikając pozycję **Dodaj odwołanie** w menu **projekt** .  
  
### <a name="to-create-a-com-callable-wrapper-using-net-framework-tools"></a>Aby utworzyć zawywoływaną przez COM otokę przy użyciu narzędzi .NET Framework  
  
Uruchom narzędzie [Regasm.exe (Narzędzie rejestracji zestawów)](../tools/regasm-exe-assembly-registration-tool.md) .  
  
To narzędzie odczytuje metadane zestawu i dodaje niezbędne wpisy do rejestru. W związku z tym klienci modelu COM mogą w niewidoczny sposób tworzyć klasy .NET Framework. Zestawu można użyć tak, jakby był natywną klasą COM.  
  
Można uruchomić Regasm.exe w zestawie znajdującym się w dowolnym katalogu, a następnie uruchomić [Gacutil.exe (Global Assembly Cache Tool)](../tools/gacutil-exe-gac-tool.md) , aby przenieść go do globalnej pamięci podręcznej zestawów. Przeniesienie zestawu nie unieważnia wpisów rejestru lokalizacji, ponieważ globalna pamięć podręczna zestawów jest zawsze sprawdzana, jeśli zestaw nie został znaleziony w innym miejscu.  
  
## <a name="see-also"></a>Zobacz także

- [Wywoływana otoka środowiska uruchomieniowego](../../standard/native-interop/runtime-callable-wrapper.md)
- [Wywoływana otoka COM](../../standard/native-interop/com-callable-wrapper.md)
