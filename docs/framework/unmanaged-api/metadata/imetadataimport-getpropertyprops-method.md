---
title: IMetaDataImport::GetPropertyProps — Metoda
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetPropertyProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetPropertyProps
helpviewer_keywords:
- GetPropertyProps method [.NET Framework metadata]
- IMetaDataImport::GetPropertyProps method [.NET Framework metadata]
ms.assetid: dc0ff3e6-7e7d-4f6c-948d-52b28f5cb78c
topic_type:
- apiref
ms.openlocfilehash: cac5aaa7ed13b6a48b36ad550da8b73d0deb2ee7
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/08/2020
ms.locfileid: "84491046"
---
# <a name="imetadataimportgetpropertyprops-method"></a>IMetaDataImport::GetPropertyProps — Metoda
Pobiera metadane dla właściwości reprezentowanej przez określony token.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT GetPropertyProps (  
   [in]  mdProperty        prop,  
   [out] mdTypeDef         *pClass,
   [out] LPCWSTR           szProperty,
   [in]  ULONG             cchProperty,
   [out] ULONG             *pchProperty,
   [out] DWORD             *pdwPropFlags,
   [out] PCCOR_SIGNATURE   *ppvSig,
   [out] ULONG             *pbSig,
   [out] DWORD             *pdwCPlusTypeFlag,
   [out] UVCP_CONSTANT     *ppDefaultValue,  
   [out] ULONG             *pcchDefaultValue,  
   [out] mdMethodDef       *pmdSetter,
   [out] mdMethodDef       *pmdGetter,
   [out] mdMethodDef       rmdOtherMethod[],  
   [in]  ULONG             cMax,
   [out] ULONG             *pcOtherMethod
);  
```  
  
## <a name="parameters"></a>Parametry  
 `prop`  
 podczas Token reprezentujący właściwość, dla której ma zostać zwrócona wartość metadanych.  
  
 `pClass`  
 określoną Wskaźnik do tokenu TypeDef, który reprezentuje typ implementujący właściwość.  
  
 `szProperty`  
 określoną Bufor służący do przechowywania nazwy właściwości.  
  
 `cchProperty`  
 podczas Rozmiar w postaci znaków dwubajtowych `szProperty` .  
  
 `pchProperty`  
 określoną Liczba znaków dwubajtowych zwracana w `szProperty` .  
  
 `pdwPropFlags`  
 określoną Wskaźnik do dowolnych flag atrybutów zastosowanych do właściwości. Ta wartość jest maska bitowa z wyliczenia [CorPropertyAttr —](corpropertyattr-enumeration.md) .  
  
 `ppvSig`  
 określoną Wskaźnik do sygnatury metadanych właściwości.  
  
 `pbSig`  
 określoną Liczba bajtów zwróconych w `ppvSig` .  
  
 `pdwCPlusTypeFlag`  
 określoną Flaga określająca typ stałej, która jest wartością domyślną właściwości. Ta wartość pochodzi z wyliczenia CorElementType —.  
  
 `ppDefaultValue`  
 określoną Wskaźnik do bajtów przechowujących wartość domyślną dla tej właściwości.  
  
 `pcchDefaultValue`  
 określoną Rozmiar w postaci znaków dwubajtowych `ppDefaultValue` , jeśli `pdwCPlusTypeFlag` jest ELEMENT_TYPE_STRING; w przeciwnym razie ta wartość nie jest istotna. W takim przypadku długość `ppDefaultValue` jest wywnioskowana z typu, który jest określony przez `pdwCPlusTypeFlag` .  
  
 `pmdSetter`  
 określoną Wskaźnik do tokenu MethodDef, który reprezentuje metodę dostępu set dla właściwości.  
  
 `pmdGetter`  
 określoną Wskaźnik do tokenu MethodDef, który reprezentuje metodę get akcesora dla właściwości.  
  
 `rmdOtherMethod`  
 określoną Tablica tokenów MethodDef, która reprezentuje inne metody skojarzone z właściwością.  
  
 `cMax`  
 podczas Maksymalny rozmiar `rmdOtherMethod` tablicy. Jeśli tablica nie jest wystarczająco duża, aby pomieścić wszystkie metody, są one pomijane bez ostrzeżenia.  
  
 `pcOtherMethod`  
 określoną Liczba tokenów MethodDef zwróconych w `rmdOtherMethod` .  
  
## <a name="requirements"></a>Wymagania  
 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** Cor. h  
  
 **Biblioteka:** Uwzględnione jako zasób w bibliotece MsCorEE. dll  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [IMetaDataImport — Interfejs](imetadataimport-interface.md)
- [IMetaDataImport2, interfejs](imetadataimport2-interface.md)
