---
title: <disableCommitThreadStack> Element
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/disableCommitThreadStack
- http://schemas.microsoft.com/.NetConfiguration/v2.0#disableCommitThreadStack
helpviewer_keywords:
- <disableCommitThreadStack> element
- disableCommitThreadStack element
ms.assetid: 3559d46a-7640-4c72-9a11-7e980768929e
ms.openlocfilehash: f717f57fe8670b126ed1468713a2114aaa772762
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91198993"
---
# <a name="disablecommitthreadstack-element"></a>\<disableCommitThreadStack> Element

Określa, czy pełny stos wątków jest zatwierdzany podczas uruchamiania wątku.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<runtime>**](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<disableCommitThreadStack>**  
  
## <a name="syntax"></a>Składnia  
  
```xml  
<disableCommitThreadStack enabled="0|1"/>  
```  
  
## <a name="attributes-and-elements"></a>Atrybuty i elementy  

 W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|  
|---------------|-----------------|  
|enabled|Atrybut wymagany.<br /><br /> Określa, czy zatwierdzanie pełnego stosu wątków podczas uruchamiania wątku (zachowanie domyślne) jest wyłączone.|  
  
## <a name="enabled-attribute"></a>Atrybut włączony  
  
|Wartość|Opis|  
|-----------|-----------------|  
|0|Nie należy wyłączać domyślnego zachowania środowiska uruchomieniowego języka wspólnego, czyli zatwierdzić pełny stos wątków podczas uruchamiania wątku.|  
|1|Wyłączenie domyślnego zachowania środowiska uruchomieniowego języka wspólnego, które polega na zatwierdzeniu pełnego stosu wątków podczas uruchamiania wątku.|  
  
### <a name="child-elements"></a>Elementy podrzędne  

 Brak.  
  
### <a name="parent-elements"></a>Elementy nadrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|`configuration`|Element główny w każdym pliku konfiguracji używanym przez środowisko uruchomieniowe języka wspólnego i aplikacje programu .NET Framework.|  
|`runtime`|Zawiera informacje dotyczące powiązania zestawu oraz wyrzucania elementów bezużytecznych.|  
  
## <a name="remarks"></a>Uwagi  

 Domyślne zachowanie środowiska uruchomieniowego języka wspólnego polega na zatwierdzeniu pełnego stosu wątków podczas uruchamiania wątku. Jeśli na serwerze, który ma ograniczoną ilość pamięci, należy utworzyć dużą liczbę wątków, a większość z nich będzie używać bardzo małej ilości miejsca na stosie, serwer może działać lepiej, jeśli środowisko uruchomieniowe języka wspólnego nie zatwierdzi pełnego stosu wątków natychmiast po rozpoczęciu wątku.  
  
> [!NOTE]
> Hosty niezarządzane mogą używać `STARTUP_DISABLE_COMMITTHREADSTACK` flagi uruchamiania w wyliczeniu [STARTUP_FLAGS](../../../unmanaged-api/hosting/startup-flags-enumeration.md) , aby osiągnąć ten sam wynik.  
  
## <a name="example"></a>Przykład  

 Poniższy przykład pokazuje, jak wyłączyć domyślne zachowanie środowiska uruchomieniowego języka wspólnego, czyli zatwierdzić pełny stos wątków podczas uruchamiania wątku.  
  
```xml  
<configuration>  
   <runtime>  
      <disableCommitThreadStack enabled="1" />  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>Zobacz też

- [Schemat ustawień środowiska uruchomieniowego](index.md)
- [Schemat pliku konfiguracji](../index.md)
