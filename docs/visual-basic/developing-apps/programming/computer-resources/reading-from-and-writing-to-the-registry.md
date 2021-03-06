---
title: Odczytywanie z rejestru i zapisywanie w nim
ms.date: 07/20/2015
helpviewer_keywords:
- My.Computer.Registry object, tasks
- registry [Visual Basic], writing to
- registry [Visual Basic], reading
ms.assetid: a13da106-185b-41d7-b23c-416da65e21e4
ms.openlocfilehash: fe0714f25cd41ca9ce4eabf135c82d1dbb1fe524
ms.sourcegitcommit: 74d05613d6c57106f83f82ce8ee71176874ea3f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2020
ms.locfileid: "93282220"
---
# <a name="reading-from-and-writing-to-the-registry-visual-basic"></a>Odczytywanie z oraz zapisywanie do rejestru (Visual Basic)

W tym temacie opisano tematy dotyczące zadań i pojęć, które są skojarzone z rejestrem.  
  
 Podczas programowania w Visual Basic można wybrać dostęp do rejestru za pomocą funkcji udostępnianych przez Visual Basic lub klasy rejestru .NET. Rejestr zawiera informacje z systemu operacyjnego oraz informacje z aplikacji hostowanych na komputerze. Praca z rejestrem może naruszyć bezpieczeństwo przez umożliwienie nieodpowiedniego dostępu do zasobów systemowych lub chronionych informacji.  
  
## <a name="in-this-section"></a>W tej sekcji  

 [Instrukcje: tworzenie klucza rejestru i określanie jego wartości](how-to-create-a-registry-key-and-set-its-value.md)  
 Opisuje sposób użycia `CreateSubKey` `SetValue` metod i `My.Computer.Registry` obiektu do utworzenia klucza rejestru i ustawienia jego wartości.  
  
 [Instrukcje: odczytywanie wartości z klucza rejestru](how-to-read-a-value-from-a-registry-key.md)  
 Opisuje sposób użycia `GetValue` metody `My.Computer.Registry` obiektu do odczytania wartości z klucza rejestru.  
  
 [Instrukcje: usuwanie klucza rejestru](how-to-delete-a-registry-key.md)  
 Opisuje sposób użycia `DeleteSubKey` metody `My.Computer.Registry.CurrentUser` właściwości w celu usunięcia klucza rejestru.  
  
 [Odczytywanie z rejestru i zapisywanie w nim za pomocą przestrzeni nazw Microsoft.Win32](reading-from-and-writing-to-the-registry-using-the-microsoft-win32-namespace.md)  
 Opisuje sposób używania `Registry` klas i programu `RegistryKey` .NET do uzyskiwania dostępu do rejestru.  
  
 [Bezpieczeństwo i rejestr](security-and-the-registry.md)  
 Omawia problemy z zabezpieczeniami związane z rejestrem.  
  
## <a name="related-sections"></a>Sekcje pokrewne  

 <xref:Microsoft.VisualBasic.MyServices.RegistryProxy>  
 Wyświetla listę i objaśnia elementy członkowskie `My.Computer.Registry` obiektu.  
  
 <xref:Microsoft.Win32.Registry>  
 Przedstawia przegląd `Registry` klasy wraz z łączami do poszczególnych kluczy i członków.
