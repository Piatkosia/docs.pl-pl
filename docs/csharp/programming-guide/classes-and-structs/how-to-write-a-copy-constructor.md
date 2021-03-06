---
title: Jak napisać Konstruktor kopiujący — Przewodnik programowania w języku C#
description: Dowiedz się, jak napisać Konstruktor kopiujący w języku C#, który przyjmuje wystąpienie klasy i zwraca nowe wystąpienie z wartościami wejściowymi.
ms.date: 07/20/2015
helpviewer_keywords:
- C# Language, copy constructor
- copy constructor [C#]
ms.assetid: fba899b5-fc41-428e-a745-3ebdbf37990a
ms.openlocfilehash: 52fd5aedea6a0e3b7c22e20db523329a00bba9ad
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91204011"
---
# <a name="how-to-write-a-copy-constructor-c-programming-guide"></a>Jak napisać Konstruktor kopiujący (Przewodnik programowania w języku C#)

Język C# nie udostępnia konstruktora kopiującego dla obiektów, ale można napisać jeden siebie.  
  
## <a name="example"></a>Przykład  

 W poniższym przykładzie `Person` [Klasa](../../language-reference/keywords/class.md) definiuje Konstruktor kopiujący, który przyjmuje, jako argument, wystąpienie `Person` . Wartości właściwości argumentu są przypisywane do właściwości nowego wystąpienia `Person` . Kod zawiera alternatywny Konstruktor kopiujący, który wysyła `Name` `Age` właściwości i wystąpienia, które chcesz skopiować do konstruktora wystąpienia klasy.  
  
 [!code-csharp[csProgGuideObjects#16](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#16)]  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.ICloneable>
- [Przewodnik programowania w języku C#](../index.md)
- [Klasy i struktury](./index.md)
- [Konstruktory](./constructors.md)
- [Finalizatory](./destructors.md)
