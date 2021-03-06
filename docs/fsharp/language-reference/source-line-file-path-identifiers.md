---
title: Identyfikatory wiersza źródłowego, pliku i ścieżki
description: Dowiedz się, jak używać wbudowanych F# wartości identyfikatorów, które umożliwiają uzyskiwanie dostępu do numeru wiersza źródłowego, katalogu i nazwy pliku w kodzie.
ms.date: 05/16/2016
ms.openlocfilehash: f22c3dfb3cb106fbe45883ffd7de01feac30db00
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2019
ms.locfileid: "71216747"
---
# <a name="source-line-file-and-path-identifiers"></a>Identyfikatory wiersza źródłowego, pliku i ścieżki

Identyfikatory `__LINE__` `__SOURCE_DIRECTORY__` i sąwbudowanymiwartościami,któreumożliwiajądostępdonumeruwierszaźródłowego,kataloguinazwyplikuwkodzie.`__SOURCE_FILE__`

## <a name="syntax"></a>Składnia

```fsharp
__LINE__
__SOURCE_DIRECTORY__
__SOURCE_FILE__
```

## <a name="remarks"></a>Uwagi

Każda z tych wartości ma typ `string`.

Poniższa tabela zawiera podsumowanie identyfikatorów wiersza źródłowego, pliku i ścieżki, które są dostępne w programie F#. Te identyfikatory nie są makrami preprocesora; są to wbudowane wartości, które są rozpoznawane przez kompilator.

|Wstępnie zdefiniowany identyfikator|Opis|
|---------------------|-----------|
|`__LINE__`|Oblicza bieżący numer wiersza, rozważając `#line` dyrektywy.|
|`__SOURCE_DIRECTORY__`|Oblicza bieżącą pełną ścieżkę katalogu źródłowego, rozważając `#line` dyrektywy.|
|`__SOURCE_FILE__`|Oblicza bieżącą nazwę pliku źródłowego bez jego ścieżki, rozważając `#line` dyrektywy.|

Aby uzyskać więcej informacji na `#line` temat dyrektywy, zobacz [dyrektywy kompilatora](compiler-directives.md).

## <a name="example"></a>Przykład

Poniższy przykład kodu demonstruje użycie tych wartości.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet7401.fs)]

Dane wyjściowe:

```console
Line: 4
Source Directory: C:\Users\username\Documents\Visual Studio 2017\Projects\SourceInfo\SourceInfo
Source File: Program.fs
```

## <a name="see-also"></a>Zobacz także

- [Dyrektywy kompilatora](compiler-directives.md)
- [Dokumentacja języka F#](index.md)
