---
title: 'NETSDK1005 i NETSDK1047: brak elementu docelowego w pliku zasobów'
description: Jak rozwiązać problem braku elementu docelowego w pliku zasobu.
author: sfoslund
ms.topic: error-reference
ms.date: 10/09/2020
f1_keywords:
- NETSDK1005
- NETSDK1047
ms.openlocfilehash: 6c22fd8c79c2ac6e024b46b4f67e08011d42efc6
ms.sourcegitcommit: b59237ca4ec763969a0dd775a3f8f39f8c59fe24
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/12/2020
ms.locfileid: "91957171"
---
# <a name="netsdk1005-and-netsdk1047-asset-file-is-missing-target"></a>NETSDK1005 i NETSDK1047: brak elementu docelowego w pliku zasobów

**Ten artykuł ma zastosowanie do:** ✔️ .NET 2.1.100 SDK i nowszych wersji

Gdy zestaw SDK programu .NET wystawia błąd NETSDK1005 lub NETSDK1047, w pliku zasobów projektu brakuje informacji o jednej z platform docelowych. Może to być zwykle ustalone przez zagwarantowanie, że przywracanie jest uruchomione i że brakująca wartość docelowa jest uwzględniona we `TargetFrameworks` właściwości projektu.

> [!NOTE]
> Wystąpił znany problem z wczesnymi kompilacjami programu .NET 5 Preview 8, gdy jest używany z wersjami wersji zapoznawczych programu Visual Studio 16,8, co spowodowało błąd. W przypadku braku elementu docelowego `net5.0-windows7.0` lub upewnij się, `net5.0` że Zaktualizowano do najnowszych wersji programu Visual Studio i zestawu SDK programu .NET 5.
