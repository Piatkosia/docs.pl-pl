---
title: <parameter>
ms.date: 03/30/2017
ms.assetid: 0fb41e2d-64f7-44ab-993e-05892eac6d82
ms.openlocfilehash: 2ef674dc8601bc9afaf6b547265988bb8a99f943
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91170171"
---
# \<parameter>

Określa parametr generyczny, gdy zadeklarowany typ jest typem ogólnym.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.runtime.serialization>**](system-runtime-serialization.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<dataContractSerializer>**](datacontractserializer.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<declaredTypes>**](declaredtypes.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<add>**](add-of-declaredtypes-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<knownType>**](knowntype.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<parameter>**  
  
## <a name="syntax"></a>Składnia  
  
```xml  
<parameter index="Integer"
           type="String" />
```  
  
## <a name="attributes-and-elements"></a>Atrybuty i elementy  

 W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|  
|---------------|-----------------|  
|index|Gdy zadeklarowany typ jest typem ogólnym, określa parametr generyczny, który zwróci znany typ.|  
|typ|Ciąg opisujący znany typ używany do serializacji i deserializacji.|  
  
## <a name="index-attribute"></a>Atrybut indeksu  
  
|Wartość|Opis|  
|-----------|-----------------|  
|„0”|Pierwszy parametr w typie ogólnym. Na przykład <xref:System.Collections.Generic.List%601> ma tylko jeden parametr. Jeśli jest używany jako zadeklarowany typ, indeks zostanie ustawiony na wartość "0".|  
|„1”|Drugi parametr w typie ogólnym. Na przykład <xref:System.Collections.Generic.Dictionary%602> ma dwa parametry. Jeśli znany typ jest zwracany przez drugi parametr, ustaw atrybut index na wartość "1".|  
  
### <a name="child-elements"></a>Elementy podrzędne  

 Brak.  
  
### <a name="parent-elements"></a>Elementy nadrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|[\<knownType>](knowntype.md)|Określa znany typ, który może być zwracany przez pole lub właściwość zadeklarowanego typu.|  
  
## <a name="remarks"></a>Uwagi  

 Aby uzyskać więcej informacji na temat znanych typów, zobacz [znane typy kontraktu danych](../../../wcf/feature-details/data-contract-known-types.md) i <xref:System.Runtime.Serialization.DataContractSerializer> .  
  
 Zobacz, [\<dataContractSerializer>](datacontractserializer-element.md) Aby zapoznać się z przykładem użycia tego elementu.  
  
 Ten element konfiguracji nie może jednocześnie mieć obu atrybutów. Jeśli oba atrybuty są ustawione, <xref:System.Configuration.ConfigurationErrorsException> występuje.  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.Runtime.Serialization.DataContractSerializer>
- [Znane typy kontraktów danych](../../../wcf/feature-details/data-contract-known-types.md)
- [\<dataContractSerializer>](datacontractserializer-element.md)
- [\<add>](add-of-declaredtypes-element.md)
