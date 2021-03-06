---
title: Wyrażenia inicjowania
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 98daef1f-15d4-483e-985c-d78ea3abe8c8
ms.openlocfilehash: 93f590e1c177adf541baca85a48fee5f9eb8d1d0
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91203634"
---
# <a name="initialization-expressions"></a>Wyrażenia inicjowania

Wyrażenie inicjowania inicjuje nowy obiekt. Obsługiwane są większość wyrażeń inicjujących, w tym większość nowych wyrażeń inicjacji C# 3,0 i Visual Basic 9,0. Następujące typy można zainicjować i zwrócić przez zapytanie LINQ to Entities:  
  
- Kolekcja obiektów jednostek typu "zero" lub "rzutowanie typów złożonych", które są zdefiniowane w modelu koncepcyjnym.  
  
- Typy CLR obsługiwane przez Entity Framework.
  
- Kolekcje wbudowane.  
  
- Typy anonimowe.  
  
 Inicjalizacja typu anonimowego jest pokazana w poniższym przykładzie w składni wyrażenia zapytania:  
  
 [!code-csharp[DP L2E Conceptual Examples#AnonymousTypeInitialization](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#anonymoustypeinitialization)]
 [!code-vb[DP L2E Conceptual Examples#AnonymousTypeInitialization](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#anonymoustypeinitialization)]  
  
 W poniższym przykładzie w składni zapytania opartej na metodzie są wyświetlane anonimowe inicjalizacje typu:  
  
 [!code-csharp[DP L2E Conceptual Examples#AnonymousTypeInitialization_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#anonymoustypeinitialization_mq)]
 [!code-vb[DP L2E Conceptual Examples#AnonymousTypeInitialization_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#anonymoustypeinitialization_mq)]  
  
 Inicjowanie klasy zdefiniowanej przez użytkownika również jest obsługiwane. Wzorzec inicjowania języka C# 3,0 i Visual Basic 9,0 jest obsługiwany i zakłada, że metody pobierającej i ustawiającej właściwości są symetryczne. Poniższy przykład w składni wyrażenia zapytania pokazuje klasę niestandardową, która jest inicjowana w zapytaniu:  
  
 [!code-csharp[DP L2E Conceptual Examples#MyOrder](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#myorder)]
 [!code-vb[DP L2E Conceptual Examples#MyOrder](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#myorder)]  
  
 [!code-csharp[DP L2E Conceptual Examples#TypeInitialization](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#typeinitialization)]
 [!code-vb[DP L2E Conceptual Examples#TypeInitialization](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#typeinitialization)]  
  
 Poniższy przykład w składni zapytania opartej na metodzie przedstawia klasę niestandardową, która jest inicjowana w zapytaniu:  
  
 [!code-csharp[DP L2E Conceptual Examples#TypeInitialization_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#typeinitialization_mq)]
 [!code-vb[DP L2E Conceptual Examples#TypeInitialization_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#typeinitialization_mq)]  
  
## <a name="see-also"></a>Zobacz też

- [Wyrażenia w zapytaniach składnika LINQ to Entities](expressions-in-linq-to-entities-queries.md)
