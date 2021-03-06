---
title: Metoda ICorDebugILFrame4::GetLocalVariableEx
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- ICorDebugILFrame4.GetCodeEx
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: 0c8676f8-ca0d-4998-b64d-fefac7e38912
topic_type:
- apiref
ms.openlocfilehash: 7c43c32e10d8e10b0f843795bbc3f0f3bc20529c
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90544248"
---
# <a name="icordebugilframe4getlocalvariableex-method"></a>Metoda ICorDebugILFrame4::GetLocalVariableEx
[Obsługiwane w .NET Framework 4.5.2 i nowszych wersjach]  
  
 Pobiera wartość określonej zmiennej lokalnej w ramce stosu języka pośredniego (IL) i opcjonalnie uzyskuje dostęp do zmiennej dodanej w instrumentacji profilera ReJIT.  
  
## <a name="syntax"></a>Składnia  
  
```cpp
HRESULT GetLocalVariableEx(  
   [in] ILCodeKind flags,
   [in] DWORD dwIndex,
   [out] ICorDebugValue **ppValue  
);  
```  
  
## <a name="parameters"></a>Parametry  
 `flags`  
 podczas Element członkowski wyliczenia [ILCodeKind](ilcodekind-enumeration.md) , który określa, czy zmienna dodana w Instrumentacji ReJIT profilera jest uwzględniona w ramce.  
  
 `dwIndex`  
 podczas Indeks zmiennej lokalnej w ramce stosu IL.  
  
 `ppValue`  
 określoną Wskaźnik do adresu obiektu "ICorDebugValue", który reprezentuje pobraną wartość.  
  
## <a name="remarks"></a>Uwagi  
 Ta metoda jest podobna do metody [GetLocalVariable —](icordebugilframe-getlocalvariable-method.md) , z tą różnicą, że opcjonalnie uzyskuje dostęp do zmiennej dodanej w Instrumentacji ReJIT profilera. Wywołanie tej metody z `flags` wartością `ILCODE_ORIGINAL_IL` jest równoznaczne z wywołaniem metody [GetLocalVariable —](icordebugilframe-getlocalvariable-method.md); Jeśli metoda jest Instrumentacją przy użyciu dodatkowych zmiennych lokalnych, nie można uzyskać dostępu do tych zmiennych. `ILCODE_REJIT_IL` zezwala debugerowi na dostęp do zmiennych lokalnych dodanych w Instrumentacji ReJIT profilera. Jeśli IL nie jest Instrumentacją, metoda zwraca `E_INVALIDARG` .  
  
## <a name="requirements"></a>Wymagania  
 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorDebug. idl, CorDebug. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [Interfejs ICorDebugILFrame4](icordebugilframe4-interface.md)
- [Debugowanie — Interfejsy](debugging-interfaces.md)
- [ReJIT: Przewodnik po poradniku](/archive/blogs/davbr/rejit-a-how-to-guide)
