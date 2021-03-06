---
title: 'Porady: kompilowanie warunkowe ze śledzeniem i debugowaniem'
description: Dowiedz się, jak kompilować warunkowo przy użyciu atrybutów warunkowych TRACE i DEBUG podczas kompilowania aplikacji .NET.
ms.date: 03/30/2017
helpviewer_keywords:
- trace compiler options
- trace statements
- compiling source code, trace statements
- tracing [.NET Framework], enabling or disabling
- tracing [.NET Framework], compiling conditionally
- TRACE directive
- conditional compilation, tracing code
ms.assetid: 56d051c3-012c-42c1-9a58-7270edc624aa
ms.openlocfilehash: 8758b793866ec0317f91d636476d33bd001ddd78
ms.sourcegitcommit: 0edbeb66d71b8df10fcb374cfca4d731b58ccdb2
ms.contentlocale: pl-PL
ms.lasthandoff: 07/07/2020
ms.locfileid: "86051223"
---
# <a name="how-to-compile-conditionally-with-trace-and-debug"></a>Porady: kompilowanie warunkowe ze śledzeniem i debugowaniem
Podczas debugowania aplikacji podczas opracowywania dane wyjściowe śledzenia i debugowania są przechodzą do okna danych wyjściowych w programie Visual Studio. Aby jednak uwzględnić funkcje śledzenia we wdrożonej aplikacji, należy skompilować aplikacje Instrumentacji przy włączonej dyrektywie kompilatora **śledzenia** . Pozwala to na skompilowanie kodu śledzenia w wydanej wersji aplikacji. Jeśli nie włączysz dyrektywy **Trace** , cały kod śledzenia zostanie zignorowany podczas kompilacji i nie zostanie uwzględniony w kodzie wykonywalnym, który zostanie wdrożony.  
  
 Obie metody śledzenia i debugowania mają skojarzone atrybuty warunkowe. Na przykład jeśli atrybut Conditional dla śledzenia ma **wartość true**, wszystkie instrukcje śledzenia są zawarte w zestawie (skompilowany plik exe lub. dll); Jeśli atrybut Conditional **śledzenia** ma **wartość false**, instrukcje Trace nie są uwzględniane.  
  
 Można mieć włączony atrybut warunkowy **Trace** lub **Debug** dla kompilacji lub obu tych wartości. W tym celu istnieją cztery typy kompilacji: **Debug**, **Trace**, Both lub nie. Niektóre kompilacje wydania dla wdrożenia produkcyjnego mogą nie zawierać żadnego z nich; Większość kompilacji debugowania zawiera oba elementy.  
  
 Ustawienia kompilatora dla aplikacji można określić na kilka sposobów:  
  
- Strony właściwości  
  
- Wiersz polecenia  
  
- **#CONST** (Visual Basic) i **#define** (dla języka C#)  
  
### <a name="to-change-compile-settings-from-the-property-pages-dialog-box"></a>Aby zmienić ustawienia kompilacji w oknie dialogowym strony właściwości  
  
1. Kliknij prawym przyciskiem myszy węzeł projektu w **Eksplorator rozwiązań**.  
  
2. Wybierz **Właściwości** z menu skrótów.  
  
    - W Visual Basic kliknij kartę **kompilacja** w lewym okienku strony właściwości, a następnie kliknij przycisk **Zaawansowane opcje kompilacji** , aby wyświetlić okno dialogowe **Zaawansowane ustawienia kompilatora** . Zaznacz pola wyboru dla ustawień kompilatora, które chcesz włączyć. Usuń zaznaczenie pól wyboru dla ustawień, które chcesz wyłączyć.  
  
    - W języku C# kliknij kartę **kompilacja** w lewym okienku strony właściwości, a następnie zaznacz pola wyboru dla ustawień kompilatora, które chcesz włączyć. Usuń zaznaczenie pól wyboru dla ustawień, które chcesz wyłączyć.  
  
### <a name="to-compile-instrumented-code-using-the-command-line"></a>Aby skompilować kod Instrumentacji przy użyciu wiersza polecenia  
  
1. Ustaw przełącznik kompilatora warunkowego w wierszu polecenia. Kompilator będzie zawierać kod śledzenia lub debugowania w pliku wykonywalnym.  
  
     Na przykład następująca instrukcja kompilatora wprowadzona w wierszu polecenia będzie zawierać kod śledzenia w skompilowanym pliku wykonywalnym:  
  
     W przypadku Visual Basic: **vbc -r:System.dll-d:Trace = true-d:Debug = false WebApplication. vb**  
  
     Dla języka C#: **csc -r:System.dll-d:Trace-d:Debug = FALSE MyApplication.cs**  
  
    > [!TIP]
    > Aby skompilować więcej niż jeden plik aplikacji, pozostaw puste miejsce między nazwami plików, na przykład **MyApplication1. vb MyApplication2. vb MyApplication3. vb** lub **MyApplication1.cs MyApplication2.cs MyApplication3.cs**.  
  
     Znaczenie dyrektyw kompilacji warunkowej używanych w powyższych przykładach jest następujące:  
  
    |Dyrektywę|Znaczenie|  
    |---------------|-------------|  
    |`vbc`|kompilator Visual Basic|  
    |`csc`|Kompilator języka C#|  
    |`-r:`|Odwołuje się do zestawu zewnętrznego (EXE lub DLL)|  
    |`-d:`|Definiuje symbol kompilacji warunkowej|  
  
    > [!NOTE]
    > Należy sprawdzić poprawność śledzenia lub debugowania przy użyciu wielkich liter. Aby uzyskać więcej informacji na temat poleceń kompilacji warunkowej, wprowadź `vbc /?` (dla Visual Basic) lub `csc /?` (dla języka C#) w wierszu polecenia. Aby uzyskać więcej informacji, zobacz [Kompilowanie z wiersza polecenia](../../csharp/language-reference/compiler-options/how-to-set-environment-variables-for-the-visual-studio-command-line.md) (C#) lub [wywoływanie kompilatora wiersza polecenia](../../visual-basic/reference/command-line-compiler/how-to-invoke-the-command-line-compiler.md) (Visual Basic).  
  
### <a name="to-perform-conditional-compilation-using-const-or-define"></a>Aby przeprowadzić kompilację warunkową przy użyciu #CONST lub #define  
  
1. Wpisz odpowiednią instrukcję dla języka programowania w górnej części pliku kodu źródłowego.  
  
    |Język|Instrukcja|Wynik|  
    |--------------|---------------|------------|  
    |**Visual Basic**|**Śledzenie #CONST = true**|Włącza śledzenie|  
    ||**Śledzenie #CONST = FAŁSZ**|Wyłącza śledzenie|  
    ||**#CONST DEBUGUJ = true**|Włącza debugowanie|  
    ||**Debugowanie #CONST = FAŁSZ**|Wyłącza debugowanie|  
    |**C#**|**Śledzenie #define**|Włącza śledzenie|  
    ||**Śledzenie #undef**|Wyłącza śledzenie|  
    ||**Debugowanie #define**|Włącza debugowanie|  
    ||**Debugowanie #undef**|Wyłącza debugowanie|  
  
### <a name="to-disable-tracing-or-debugging"></a>Aby wyłączyć śledzenie lub debugowanie  
  
Usuń dyrektywę kompilatora z kodu źródłowego.  
  
\-oraz  
  
Dodaj komentarz do dyrektywy kompilatora.  
  
> [!NOTE]
> Gdy wszystko będzie gotowe do skompilowania, możesz wybrać opcję **Kompiluj** z menu **kompilacja** lub użyć metody wiersza polecenia, ale bez wpisywania znaków **d:** , aby zdefiniować symbole kompilacji warunkowej.  
  
## <a name="see-also"></a>Zobacz także

- [Śledzenie i instrumentacja aplikacji](tracing-and-instrumenting-applications.md)
- [Instrukcje: tworzenie, inicjowanie i konfigurowanie przełączników śledzenia](how-to-create-initialize-and-configure-trace-switches.md)
- [Przełączniki śledzenia](trace-switches.md)
- [Obiekty nasłuchujące śledzenia](trace-listeners.md)
- [Porady: dodawanie instrukcji śledzenia do kodu aplikacji](how-to-add-trace-statements-to-application-code.md)
- [Porada: ustawianie zmiennych środowiskowych dla wiersza polecenia programu Visual Studio](../../csharp/language-reference/compiler-options/how-to-set-environment-variables-for-the-visual-studio-command-line.md)
- [Instrukcje: Wywoływanie kompilatora z wiersza polecenia](../../visual-basic/reference/command-line-compiler/how-to-invoke-the-command-line-compiler.md)
