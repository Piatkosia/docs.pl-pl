---
title: Rozszerzalność metadanych
ms.date: 03/30/2017
ms.assetid: f92fcc76-0806-4c84-9d63-7aae0d3899de
ms.openlocfilehash: 1e8e7f511b38cf3326b9abbca57df769317a26a4
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2020
ms.locfileid: "84584626"
---
# <a name="metadata-extensibility"></a>Rozszerzalność metadanych
Ta sekcja zawiera przykłady demonstrujące niestandardowe metadane.  
  
## <a name="in-this-section"></a>W tej sekcji  
 [Niestandardowy bezpieczny punkt końcowy metadanych](custom-secure-metadata-endpoint.md)  
 Pokazuje, jak wdrożyć usługę z bezpiecznym punktem końcowym metadanych, który używa jednego z powiązań wymiany niebędących metadanymi i jak skonfigurować narzędzie do obsługi [metadanych ServiceModel (Svcutil. exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md) lub klientów, aby pobrać metadane z takiego punktu końcowego metadanych.  
  
 [Niestandardowa publikacja WSDL](custom-wsdl-publication.md)  
 Pokazuje, jak zaimplementować <xref:System.ServiceModel.Description.IWsdlExportExtension?displayProperty=nameWithType> w atrybucie niestandardowym <xref:System.ServiceModel.Description.IContractBehavior?displayProperty=nameWithType> , aby eksportować właściwości atrybutów jako adnotacje WSDL, między innymi.
