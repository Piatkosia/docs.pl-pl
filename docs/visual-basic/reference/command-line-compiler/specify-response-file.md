---
title: '@ (określenie pliku odpowiedzi)'
ms.date: 03/13/2018
helpviewer_keywords:
- '@ (Specify Response File) compiler option [Visual Basic]'
ms.assetid: a6847eaa-e5f9-4303-9421-45b55484b9ca
ms.openlocfilehash: 91cf1b5a55d16ab47a83fbd259dd1d83d8e9c31a
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403099"
---
# <a name="-specify-response-file-visual-basic"></a>@ (Określ plik odpowiedzi) (Visual Basic)

Określa plik, który zawiera opcje kompilatora i pliki kodu źródłowego do skompilowania.

## <a name="syntax"></a>Składnia

```console
@response_file
```

## <a name="arguments"></a>Argumenty

`response_file`  
Wymagany. Plik, który zawiera listę opcji kompilatora lub plików kodu źródłowego do skompilowania. Nazwa pliku należy ująć w cudzysłów (""), jeśli zawiera spację.

## <a name="remarks"></a>Uwagi

Kompilator przetwarza opcje kompilatora i pliki kodu źródłowego określone w pliku odpowiedzi, tak jakby zostały określone w wierszu polecenia.

Aby określić więcej niż jeden plik odpowiedzi w kompilacji, określ wiele opcji pliku odpowiedzi, takich jak poniższe.

```console
@file1.rsp @file2.rsp
```

W pliku odpowiedzi w jednym wierszu mogą znajdować się wiele opcji kompilatora i plików kodu źródłowego. Pojedyncza Specyfikacja kompilatora-Option musi znajdować się w jednym wierszu (nie może obejmować wielu wierszy). Pliki odpowiedzi mogą mieć komentarze zaczynające się od `#` symbolu.

Opcje określone w wierszu polecenia można połączyć z opcjami określonymi w jednym lub kilku plikach odpowiedzi. Kompilator przetwarza opcje polecenia w miarę ich występowania. W związku z tym argumenty wiersza polecenia mogą przesłonić wcześniej wymienione opcje w plikach odpowiedzi. Z kolei opcje w pliku odpowiedzi opcje przesłaniają się wcześniej w wierszu polecenia lub w innych plikach odpowiedzi.

Visual Basic udostępnia plik VBC. rsp, który znajduje się w tym samym katalogu, co plik VBC. exe. Plik VBC. rsp jest uwzględniany domyślnie, jeśli `-noconfig` opcja jest używana. Aby uzyskać więcej informacji, zobacz [-noconfig](noconfig.md).

> [!NOTE]
> `@`Opcja jest niedostępna w środowisku deweloperskim programu Visual Studio. jest ona dostępna tylko podczas kompilowania z wiersza polecenia.

## <a name="example"></a>Przykład

Poniższe wiersze pochodzą z przykładowego pliku odpowiedzi.

```console
# build the first output file
-target:exe
-out:MyExe.exe
source1.vb
source2.vb
```

## <a name="example"></a>Przykład

W poniższym przykładzie pokazano, jak użyć `@` opcji z plikiem odpowiedzi o nazwie `File1.rsp` .

```console
vbc @file1.rsp
```

## <a name="see-also"></a>Zobacz też

- [Kompilator wiersza polecenia Visual Basic](index.md)
- [-noconfig](noconfig.md)
- [Przykłady kompilacji — wiersze poleceń](sample-compilation-command-lines.md)
