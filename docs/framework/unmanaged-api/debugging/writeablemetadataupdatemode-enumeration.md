---
title: Wyliczenie WriteableMetadataUpdateMode
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- WriteableMetadataUpdateMode
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: 6758f4d3-6bc7-4c99-8582-e9be00566784
topic_type:
- apiref
ms.openlocfilehash: 0793dcbe4d080da83cf507e04303d66fbbb56b85
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/15/2020
ms.locfileid: "83420646"
---
# <a name="writeablemetadataupdatemode-enumeration"></a>Wyliczenie WriteableMetadataUpdateMode
[Obsługiwane w .NET Framework 4.5.2 i nowszych wersjach]  
  
 Zawiera wartości, które określają, czy aktualizacje w pamięci mają być widoczne dla debugera.  
  
## <a name="syntax"></a>Składnia  
  
```cpp
typedef enum WriteableMetadataUpdateMode {  
   LegacyCompatPolicy,  
   AlwaysShowUpdates  
} WriteableMetadataUpdateMode;  
```  
  
## <a name="members"></a>Elementy członkowskie  
  
|Nazwa elementu członkowskiego|Opis|  
|-----------------|-----------------|  
|`LegacyCompatPolicy`|Zachowaj zgodność z poprzednimi wersjami .NET Framework, gdy aktualizacje w pamięci mają być widoczne dla metadanych. Zobacz sekcję Spostrzeżenia, aby uzyskać więcej informacji.|  
|`AlwaysShowUpdates`|Wprowadź aktualizacje w pamięci do metadanych widocznych dla debugera.|  
  
## <a name="remarks"></a>Uwagi  
 Element członkowski `WriteableMetadataUpdateMode` wyliczenia można przesłać do metody [SetWriteableMetadataUpdateMode](icordebugprocess7-setwriteablemetadataupdatemode-method.md) w celu określenia, czy aktualizacje w pamięci w procesie docelowym są widoczne dla debugera.  
  
 `LegacyCompatPolicy`Opcja wymusza takie samo zachowanie jak w wersjach .NET Framework przed 4.5.2. Często oznacza to, że metadane z aktualizacji nie są widoczne. Jednak wywołania do wielu metod debugowania niejawnie przekształcenie debugera w celu udostępnienia aktualizacji. Jeśli na przykład debuger przekaże [ICorDebugILFrame:: GetLocalVariable —](icordebugilframe-getlocalvariable-method.md) indeks zmiennej nie został znaleziony w oryginalnych metadanych metody, wszystkie metadane modułu zostaną zaktualizowane do migawki zgodnej z bieżącym stanem procesu. Innymi słowy, z `LegacyCompatPolicy` opcją debuger może zobaczyć Brak, niektóre lub wszystkie dostępne aktualizacje metadanych w zależności od tego, w jaki sposób używa innych części niezarządzanego interfejsu API debugowania.  
  
## <a name="requirements"></a>Wymagania  
 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorDebug. idl, CorDebug. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [Debugowanie — wyliczenia](debugging-enumerations.md)
- [SetWriteableMetadataUpdateMode, metoda](icordebugprocess7-setwriteablemetadataupdatemode-method.md)
