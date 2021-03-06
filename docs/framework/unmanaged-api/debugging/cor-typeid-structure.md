---
title: COR_TYPEID — Struktura
ms.date: 03/30/2017
api_name:
- COR_TYPEID
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- COR_TYPEID
helpviewer_keywords:
- COR_TYPEID structure [.NET Framework debugging]
ms.assetid: 1e172b14-ee22-4943-b3b8-3740e7bdcd2e
topic_type:
- apiref
ms.openlocfilehash: 4f6dbe8c17bd6a91078b87a87c1055fbf4977a88
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73132309"
---
# <a name="cor_typeid-structure"></a>COR_TYPEID — Struktura
Zawiera identyfikator typu.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
typedef struct COR_TYPEID{  
    UINT64 token1;  
    UINT64 token2;  
} COR_TYPEID;  
```  
  
## <a name="members"></a>Elementy członkowskie  
  
|Element członkowski|Opis|  
|------------|-----------------|  
|`token1`|Pierwszy token.|  
|`token2`|Drugi token.|  
  
## <a name="remarks"></a>Uwagi  
 Struktura `COR_TYPEID` jest zwracana przez wiele metod debugowania, które zapewniają informacje o obiektach, które mają być zbierane jako elementy bezużyteczne. Następnie można przekazać jako argument do innych metod debugowania, które zawierają dodatkowe informacje na temat tego elementu. Na przykład przez Wyliczenie obiektu [ICorDebugHeapEnum](icordebugheapenum-interface.md) można pobrać pojedyncze obiekty [COR_HEAPOBJECT](cor-heapobject-structure.md) , które reprezentują poszczególne obiekty na stercie zarządzanym. Następnie można przekazać wartość `COR_TYPEID` z pola `COR_HEAPOBJECT.type` do metody [ICorDebugProcess5:: GetTypeForTypeID —](icordebugprocess5-gettypefortypeid-method.md) , aby pobrać obiekt ICorDebugType, który zawiera informacje o typie obiektu.  
  
 Obiekt `COR_TYPEID` ma być nieprzezroczysty. Nie można uzyskać dostępu do poszczególnych pól ani manipulować nimi. Jego jedynym zastosowaniem jest jako identyfikator, który jest dostarczany jako parametr `out` w wywołaniu metody i który może z kolei być przekazywany do innych metod w celu dostarczenia dodatkowych informacji.  
  
## <a name="requirements"></a>Wymagania  
 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorDebug. idl, CorDebug. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **Wersje .NET Framework:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [Struktury debugowania](debugging-structures.md)
- [Debugowanie](index.md)
