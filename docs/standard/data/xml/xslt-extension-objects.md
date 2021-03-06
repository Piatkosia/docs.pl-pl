---
title: Obiekty rozszerzeń XSLT
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: a4ebdbad-087c-4cfe-acc0-17c48142f81a
ms.openlocfilehash: ff50cbb561f9da5ea0877ded1de6fd3d5c424a7e
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90555962"
---
# <a name="xslt-extension-objects"></a>Obiekty rozszerzeń XSLT
Obiekty rozszerzeń służą do rozszerzania funkcjonalności arkuszy stylów. Obiekty rozszerzeń są obsługiwane przez <xref:System.Xml.Xsl.XsltArgumentList> klasę.  
  
 Poniżej przedstawiono zalety użycia obiektu rozszerzenia zamiast skryptu osadzonego:  
  
- Zapewnia lepszą hermetyzację i ponowne użycie klas.  
  
- Zezwala na mniejsze i łatwiejsze w obsłudze arkusze stylów.  
  
 Obiekty rozszerzeń XSLT są dodawane do <xref:System.Xml.Xsl.XsltArgumentList> obiektu za pomocą <xref:System.Xml.Xsl.XsltArgumentList.AddExtensionObject%2A> metody. Kwalifikowana nazwa i identyfikator URI przestrzeni nazw są skojarzone z obiektem rozszerzenia w tym czasie.  
  
> [!NOTE]
> Zestaw uprawnień FullTrust jest wymagany do wywołania <xref:System.Xml.Xsl.XsltArgumentList.AddExtensionObject%2A> metody. Aby uzyskać więcej informacji, zobacz [zabezpieczenia dostępu kodu](../../../framework/misc/code-access-security.md) i [nazwane zestawy uprawnień](/previous-versions/dotnet/netframework-4.0/4652tyx7(v=vs.100)).  
  
 Typy danych zwracane z obiektów rozszerzeń to jeden z czterech podstawowych typów danych XPath,,, `number` `string` `Boolean` i `node set` .  
  
 Każda metoda, która jest zdefiniowana za pomocą `params` słowa kluczowego, umożliwiająca nieokreśloną liczbę parametrów do przesłania, nie jest obecnie obsługiwana przez <xref:System.Xml.Xsl.XslCompiledTransform> klasę. Arkusze stylów XSLT używające dowolnej metody zdefiniowanej za pomocą `params` słowa kluczowego nie będą działały prawidłowo. Aby uzyskać szczegółowe informacje, zobacz [params](../../../csharp/language-reference/keywords/params.md).  
  
### <a name="to-use-an-xslt-extension-object"></a>Aby użyć obiektu rozszerzenia XSLT  
  
1. Utwórz <xref:System.Xml.Xsl.XsltArgumentList> obiekt i Dodaj obiekt rozszerzenia za pomocą <xref:System.Xml.Xsl.XsltArgumentList.AddExtensionObject%2A> metody.  
  
2. Wywołaj obiekt rozszerzenia z arkusza stylów.  
  
3. Przekaż <xref:System.Xml.Xsl.XsltArgumentList> obiekt do <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> metody.  
  
## <a name="see-also"></a>Zobacz także

- [Przekształcenia XSLT](xslt-transformations.md)
- [Zagadnienia dotyczące bezpieczeństwa danych XSLT](xslt-security-considerations.md)
