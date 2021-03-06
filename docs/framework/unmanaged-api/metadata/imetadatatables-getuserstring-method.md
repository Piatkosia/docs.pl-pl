---
title: IMetaDataTables::GetUserString — Metoda
ms.date: 03/30/2017
api_name:
- IMetaDataTables.GetUserString
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataTables::GetUserString
helpviewer_keywords:
- IMetaDataTables::GetUserString method [.NET Framework metadata]
- GetUserString method, IMetaDataTables interface [.NET Framework metadata]
ms.assetid: 35b8f0d6-9aba-4714-adb2-62020a38fb7e
topic_type:
- apiref
ms.openlocfilehash: 21ce66722e069573b651ada950b64ef6d97220fb
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501147"
---
# <a name="imetadatatablesgetuserstring-method"></a>IMetaDataTables::GetUserString — Metoda

Pobiera zakodowany ciąg o określonym indeksie w kolumnie ciąg w bieżącym zakresie.

## <a name="syntax"></a>Składnia

```cpp
HRESULT GetUserString (
    [in]  ULONG       ixUserString,
    [out] ULONG       *pcbData,
    [out] const void  **ppData
);
```

## <a name="parameters"></a>Parametry

`ixUserString`\
podczas Wartość indeksu, z której zostanie pobrany zakodowany ciąg.

`pcbData`\
określoną Wskaźnik do rozmiaru `ppData` .

`ppData`\
określoną Wskaźnik do wskaźnika do zwracanego ciągu.

## <a name="requirements"></a>Wymagania

**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).

**Nagłówek:** Cor. h

**Biblioteka:** Używany jako zasób w bibliotece MsCorEE. dll

**.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]

## <a name="see-also"></a>Zobacz także

- [IMetaDataTables, interfejs](imetadatatables-interface.md)
- [IMetaDataTables2 — Interfejs](imetadatatables2-interface.md)
