---
title: Uzupełnianie ciągów w programie .NET
description: Dowiedz się, jak uzupełniać ciągi w programie .NET. Użyj metod String. PadLeft i String. PadRight, aby dodać znaki wiodące lub końcowe w celu osiągnięcia określonej całkowitej długości.
ms.date: 03/15/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- strings [.NET], padding
- white space
- PadRight method
- PadLeft method
- padding strings
ms.assetid: 84a9f142-3244-4c90-ba02-21af9bbaff71
ms.openlocfilehash: f90a95f0ceb5ad7cc32d451897544fffe56afb6d
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/28/2020
ms.locfileid: "92889052"
---
# <a name="padding-strings-in-net"></a>Uzupełnianie ciągów w programie .NET

Użyj jednej z następujących <xref:System.String> metod, aby utworzyć nowy ciąg, który składa się z oryginalnego ciągu, który jest uzupełniony znakami początkowymi lub końcowymi do określonej całkowitej długości. Znak uzupełniania może być spacją lub określonym znakiem. Ciąg wyników wydaje się być wyrównany do prawej lub wyrównany do lewej. Jeśli pierwotna długość ciągu jest już równa lub większa od żądanej całkowitej długości, metody uzupełniania zwracają oryginalny ciąg niezmieniony; Aby uzyskać więcej informacji, zobacz sekcje **zwraca** dwa przeciążenia <xref:System.String.PadLeft%2A?displayProperty=nameWithType> <xref:System.String.PadRight%2A?displayProperty=nameWithType> metod i.
  
|Nazwa metody|Zastosowanie|  
|-----------------|---------|  
|<xref:System.String.PadLeft%2A?displayProperty=nameWithType>|Tworzy w postaci ciągu znaki wiodące z określoną łączną długością.|  
|<xref:System.String.PadRight%2A?displayProperty=nameWithType>|Tworzy w postaci ciągu znaki końcowe z określoną całkowitą długością.|  
  
## <a name="padleft"></a>PadLeft  
 <xref:System.String.PadLeft%2A?displayProperty=nameWithType>Metoda tworzy nowy ciąg przez złączenie wystarczającej liczby wiodących znaków pad do oryginalnego ciągu, aby osiągnąć określoną łączną długość. <xref:System.String.PadLeft%28System.Int32%29?displayProperty=nameWithType>Metoda używa odstępu jako znaku uzupełniania, a <xref:System.String.PadLeft%28System.Int32%2CSystem.Char%29?displayProperty=nameWithType> Metoda umożliwia określenie własnego znaku uzupełniania.  
  
 Poniższy przykład kodu używa metody, <xref:System.String.PadLeft%2A> Aby utworzyć nowy ciąg o długości dwudziestu znaków. W przykładzie zostanie wyświetlony komunikat " `--------Hello World!` " w konsoli programu.  
  
 [!code-cpp[Conceptual.String.BasicOps#3](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/padding.cpp#3)]
 [!code-csharp[Conceptual.String.BasicOps#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/padding.cs#3)]
 [!code-vb[Conceptual.String.BasicOps#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/padding.vb#3)]  
  
## <a name="padright"></a>PadRight  
 <xref:System.String.PadRight%2A?displayProperty=nameWithType>Metoda tworzy nowy ciąg, łącząc wystarczającą liczbę końcową znaków uzupełniających do oryginalnego ciągu, aby osiągnąć określoną łączną długość. <xref:System.String.PadRight%28System.Int32%29?displayProperty=nameWithType>Metoda używa odstępu jako znaku uzupełniania, a <xref:System.String.PadRight%28System.Int32%2CSystem.Char%29?displayProperty=nameWithType> Metoda umożliwia określenie własnego znaku uzupełniania.  
  
 Poniższy przykład kodu używa metody, <xref:System.String.PadRight%2A> Aby utworzyć nowy ciąg o długości dwudziestu znaków. W przykładzie zostanie wyświetlony komunikat " `Hello World!--------` " w konsoli programu.  
  
 [!code-cpp[Conceptual.String.BasicOps#4](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/padding.cpp#4)]
 [!code-csharp[Conceptual.String.BasicOps#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/padding.cs#4)]
 [!code-vb[Conceptual.String.BasicOps#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/padding.vb#4)]  
  
## <a name="see-also"></a>Zobacz także

- [Podstawowe operacje na ciągach](basic-string-operations.md)
