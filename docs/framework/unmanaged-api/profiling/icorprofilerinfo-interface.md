---
title: ICorProfilerInfo — Interfejs
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo
helpviewer_keywords:
- ICorProfilerInfo interface [.NET Framework profiling]
ms.assetid: eb4e4ce0-06e7-4469-bbc4-edc2eb5da4b1
topic_type:
- apiref
ms.openlocfilehash: cc8ab6f0c8115da4d74280023dc692b66846ed94
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/08/2020
ms.locfileid: "84497754"
---
# <a name="icorprofilerinfo-interface"></a>ICorProfilerInfo — Interfejs
Zapewnia metody do użycia przez program Code profilowas do komunikowania się ze środowiskiem uruchomieniowym języka wspólnego (CLR) w celu kontrolowania informacji o monitorowaniu zdarzeń i żądaniach.  
  
> [!NOTE]
> Każda metoda w `ICorProfilerInfo` interfejsie zwraca wynik HRESULT wskazujący powodzenie lub niepowodzenie. Zobacz CorError. h, aby uzyskać listę możliwych kodów powrotu.  
  
## <a name="methods"></a>Metody  
  
|Metoda|Opis|  
|------------|-----------------|  
|[BeginInprocDebugging, metoda](icorprofilerinfo-begininprocdebugging-method.md)|Inicjuje obsługę debugowania w procesie. Ta metoda jest przestarzała w .NET Framework w wersji 2,0.|  
|[EndInprocDebugging, metoda](icorprofilerinfo-endinprocdebugging-method.md)|Zamyka sesję debugowania w procesie. Ta metoda jest przestarzała w .NET Framework w wersji 2,0.|  
|[ForceGC, metoda](icorprofilerinfo-forcegc-method.md)|Wymusza wyrzucanie elementów bezużytecznych w czasie wykonywania.|  
|[GetAppDomainInfo, metoda](icorprofilerinfo-getappdomaininfo-method.md)|Pobiera informacje o określonej domenie aplikacji.|  
|[GetAssemblyInfo, metoda](icorprofilerinfo-getassemblyinfo-method.md)|Pobiera informacje o określonym zestawie.|  
|[GetClassFromObject, metoda](icorprofilerinfo-getclassfromobject-method.md)|Pobiera `ClassID` z<br /><br /> Obiekt, pod którym znajduje się `ObjectID` .|  
|[GetClassFromToken — Metoda](icorprofilerinfo-getclassfromtoken-method.md)|Pobiera identyfikator klasy, z uwzględnieniem tokenu metadanych. Ta metoda jest przestarzała w .NET Framework w wersji 2,0. Zamiast tego użyj metody [ICorProfilerInfo2:: GetClassFromTokenAndTypeArgs —](icorprofilerinfo2-getclassfromtokenandtypeargs-method.md) .|  
|[GetClassIDInfo, metoda](icorprofilerinfo-getclassidinfo-method.md)|Pobiera moduł nadrzędny i token metadanych dla określonej klasy.|  
|[GetCodeInfo, metoda](icorprofilerinfo-getcodeinfo-method.md)|Pobiera zakres kodu natywnego skojarzonego z określonym IDENTYFIKATORem funkcji. Ta metoda jest przestarzała. Zamiast tego użyj metody [ICorProfilerInfo2:: GetCodeInfo2 —](icorprofilerinfo2-getcodeinfo2-method.md) .|  
|[GetCurrentThreadID — Metoda](icorprofilerinfo-getcurrentthreadid-method.md)|Pobiera identyfikator bieżącego wątku, jeśli jest to wątek zarządzany.|  
|[GetEventMask, metoda](icorprofilerinfo-geteventmask-method.md)|Pobiera bieżące kategorie zdarzeń, dla których profiler chce otrzymywać powiadomienia o zdarzeniach z środowiska CLR.|  
|[GetFunctionFromIP, metoda](icorprofilerinfo-getfunctionfromip-method.md)|Mapuje wskaźnik zarządzanej instrukcji kodu na `FunctionID` .|  
|[GetFunctionFromToken — Metoda](icorprofilerinfo-getfunctionfromtoken-method.md)|Pobiera identyfikator funkcji. Ta metoda jest przestarzała w .NET Framework w wersji 2,0. Zamiast tego użyj metody [ICorProfilerInfo2:: GetFunctionFromTokenAndTypeArgs —](icorprofilerinfo2-getfunctionfromtokenandtypeargs-method.md) .|  
|[GetFunctionInfo, metoda](icorprofilerinfo-getfunctioninfo-method.md)|Pobiera klasę nadrzędną i token metadanych dla określonej funkcji.|  
|[GetHandleFromThread, metoda](icorprofilerinfo-gethandlefromthread-method.md)|Mapuje identyfikator wątku na dojście wątku Win32.|  
|[GetILFunctionBody, metoda](icorprofilerinfo-getilfunctionbody-method.md)|Pobiera wskaźnik do treści metody w kodzie języka pośredniego firmy Microsoft (MSIL), rozpoczynając od jego nagłówka.|  
|[GetILFunctionBodyAllocator, metoda](icorprofilerinfo-getilfunctionbodyallocator-method.md)|Pobiera interfejs, który zapewnia metodę przydzielenia pamięci do użycia podczas wymiany treści metody w kodzie MSIL.|  
|[GetILToNativeMapping — Metoda](icorprofilerinfo-getiltonativemapping-method.md)|Pobiera mapę z przesunięcia MSIL do natywnych przesunięć dla kodu zawartego w określonej funkcji.|  
|[GetInprocInspectionInterface, metoda](icorprofilerinfo-getinprocinspectioninterface-method.md)|Pobiera obiekt, który może być badany dla interfejsu ICorDebugProcess. Ta metoda jest przestarzała w .NET Framework w wersji 2,0.|  
|[GetInprocInspectionIThisThread, metoda](icorprofilerinfo-getinprocinspectionithisthread-method.md)|Pobiera obiekt, który może być badany dla interfejsu ICorDebugThread. Ta metoda jest przestarzała w .NET Framework w wersji 2,0.|  
|[GetModuleInfo, metoda](icorprofilerinfo-getmoduleinfo-method.md)|Podanym IDENTYFIKATORem modułu zwraca nazwę pliku modułu i identyfikator zestawu nadrzędnego modułu.|  
|[GetModuleMetaData, metoda](icorprofilerinfo-getmodulemetadata-method.md)|Pobiera wystąpienie interfejsu metadanych, które mapuje do określonego modułu.|  
|[GetObjectSize — Metoda](icorprofilerinfo-getobjectsize-method.md)|Pobiera rozmiar określonego obiektu.|  
|[GetThreadContext — Metoda](icorprofilerinfo-getthreadcontext-method.md)|Pobiera tożsamość kontekstu aktualnie skojarzoną z określonym wątkiem.|  
|[GetThreadInfo, metoda](icorprofilerinfo-getthreadinfo-method.md)|Pobiera bieżącą tożsamość wątku Win32 dla określonego wątku.|  
|[GetTokenAndMetadataFromFunction, metoda](icorprofilerinfo-gettokenandmetadatafromfunction-method.md)|Pobiera token metadanych i wystąpienie interfejsu metadanych, które mogą być używane w odniesieniu do tokenu określonej funkcji.|  
|[IsArrayClass, metoda](icorprofilerinfo-isarrayclass-method.md)|Określa, czy określona Klasa jest klasą Array.|  
|[SetEnterLeaveFunctionHooks, metoda](icorprofilerinfo-setenterleavefunctionhooks-method.md)|Określa funkcje zaimplementowane przez profiler, które mają być wywoływane w podpunktach "Enter", "urlop" i "tailcall" punktów zarządzanych funkcji.|  
|[SetEventMask, metoda](icorprofilerinfo-seteventmask-method.md)|Ustawia wartość określającą typy zdarzeń, dla których profiler chce otrzymywać powiadomienia z aparatu CLR.|  
|[SetFunctionIDMapper, metoda](icorprofilerinfo-setfunctionidmapper-method.md)|Określa funkcję zaimplementowaną przez profiler, która zostanie wywołana w celu mapowania `FunctionID` wartości na wartości alternatywne, które są przesyłane do punktów zaczepienia wejścia/wyjścia profilera.|  
|[SetFunctionReJIT, metoda](icorprofilerinfo-setfunctionrejit-method.md)|Nie zaimplementowano. Nie używaj.|  
|[SetILFunctionBody, metoda](icorprofilerinfo-setilfunctionbody-method.md)|Zastępuje treść określonej funkcji w określonym module.|  
|[SetILInstrumentedCodeMap, metoda](icorprofilerinfo-setilinstrumentedcodemap-method.md)|Określa sposób, w jaki przesunięcia oryginalnej mapy MSIL określonej funkcji są mapowane na nowe przesunięcia narzędzia MSIL modyfikowanego przez profiler funkcji.|  
  
## <a name="remarks"></a>Uwagi  
 Profiler wywołuje metodę w `ICorProfilerInfo` interfejsie, aby komunikować się z środowiskiem CLR w celu sterowania monitorowaniem zdarzeń i informacjami o żądaniu.  
  
 Metody `ICorProfilerInfo` interfejsu są implementowane przez środowisko CLR przy użyciu modelu dowolnego wątku. Każda metoda zwraca wynik HRESULT wskazujący powodzenie lub niepowodzenie. Zobacz CorError. h, aby uzyskać listę możliwych kodów powrotu.  
  
 Środowisko CLR przechodzi przez implementację profilera [ICorProfilerCallback:: Initialize](icorprofilercallback-initialize-method.md), `ICorProfilerInfo` interfejs do każdego profilera kodu podczas inicjalizacji. Profiler kodu może następnie wywołać metody `ICorProfilerInfo` interfejsu, aby uzyskać informacje o kodzie zarządzanym wykonywanym pod kontrolą środowiska CLR.  
  
## <a name="requirements"></a>Wymagania  
 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorProf. idl, CorProf. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [Interfejsy profilowania](profiling-interfaces.md)
- [ICorProfilerInfo2, interfejs](icorprofilerinfo2-interface.md)
