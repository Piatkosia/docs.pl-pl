---
title: Typy kopiowalne i niekopiowalne
description: Dowiedz się więcej o typach danych kopiowalnych i innych niż danych kopiowalnych. Typy danych danych kopiowalnych są często reprezentowane w pamięci zarządzanej i niezarządzanej i nie wymagają specjalnej obsługi.
ms.date: 03/30/2017
helpviewer_keywords:
- interop marshaling, blittable types
- blittable types, interop marshaling
ms.assetid: d03b050e-2916-49a0-99ba-f19316e5c1b3
ms.openlocfilehash: 8bbf9c72143033cec22b38cc26cbe8ceb44f790b
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90556274"
---
# <a name="blittable-and-non-blittable-types"></a>Typy kopiowalne i niekopiowalne
Większość typów danych ma wspólną reprezentację w pamięci zarządzanej i niezarządzanej i nie wymaga specjalnej obsługi przez organizatora międzyoperacyjności. Typy te są nazywane *danych kopiowalnychmi* , ponieważ nie wymagają konwersji podczas przekazywania między zarządzanym i niezarządzanym kodem.  
  
 Struktury zwracane z wywołań wywołania platformy muszą być typami danych kopiowalnych. Wywołanie platformy nie obsługuje struktur innych niż danych kopiowalnych jako typów zwracanych.  
  
 Następujące typy z <xref:System> przestrzeni nazw są typami danych kopiowalnych:  
  
- <xref:System.Byte?displayProperty=nameWithType>  
  
- <xref:System.SByte?displayProperty=nameWithType>  
  
- <xref:System.Int16?displayProperty=nameWithType>  
  
- <xref:System.UInt16?displayProperty=nameWithType>  
  
- <xref:System.Int32?displayProperty=nameWithType>  
  
- <xref:System.UInt32?displayProperty=nameWithType>  
  
- <xref:System.Int64?displayProperty=nameWithType>  
  
- <xref:System.UInt64?displayProperty=nameWithType>  
  
- <xref:System.IntPtr?displayProperty=nameWithType>  
  
- <xref:System.UIntPtr?displayProperty=nameWithType>  
  
- <xref:System.Single?displayProperty=nameWithType>  
  
- <xref:System.Double?displayProperty=nameWithType>  
  
 Następujące typy złożone są również danych kopiowalnych:  
  
- Jednowymiarowe tablice typów danych kopiowalnych, takie jak tablica liczb całkowitych. Jednak typ, który zawiera zmienną tablicę typów danych kopiowalnych, nie należy do siebie danych kopiowalnych.  
  
- Sformatowane typy wartości, które zawierają tylko typy danych kopiowalnych (i klasy, jeśli są organizowane jako sformatowane typy). Aby uzyskać więcej informacji na temat sformatowanych typów wartości, zobacz [domyślne kierowanie dla typów wartości](default-marshaling-behavior.md#default-marshaling-for-value-types).  
  
 Odwołania do obiektów nie są danych kopiowalnych. Obejmuje to tablicę odwołań do obiektów, które są danych kopiowalnych przez siebie. Na przykład można zdefiniować strukturę danych kopiowalnych, ale nie można zdefiniować typu danych kopiowalnych, który zawiera tablicę odwołań do tych struktur.  
  
 Jako Optymalizacja, tablice typów danych kopiowalnych i klas, które zawierają tylko składowe danych kopiowalnych, są [przypięte](copying-and-pinning.md) zamiast kopiowane podczas organizowania. Te typy mogą być organizowane jako parametry wejściowe/out, gdy wywołujący i wywoływany są w tym samym elemencie Apartment. Jednak te typy są faktycznie organizowane jako parametry i należy zastosować <xref:System.Runtime.InteropServices.InAttribute> atrybuty i, <xref:System.Runtime.InteropServices.OutAttribute> Jeśli chcesz zorganizować argument jako parametr in/out.  
  
 Niektóre typy danych zarządzanych wymagają innej reprezentacji w niezarządzanym środowisku. Te typy danych inne niż danych kopiowalnych muszą zostać przekonwertowane na formularz, który może być zorganizowany. Na przykład, zarządzanymi ciągami są typy inne niż danych kopiowalnych, ponieważ muszą one być konwertowane do obiektów String, zanim będą mogły być organizowane.  
  
 Poniższa tabela zawiera listę typów innych niż danych kopiowalnych z <xref:System> przestrzeni nazw. [Delegaty](default-marshaling-behavior.md#default-marshaling-for-delegates), które są strukturami danych, które odwołują się do metody statycznej lub do wystąpienia klasy, również nie są danych kopiowalnych.  
  
|Typ inny niż danych kopiowalnych|Opis|  
|-------------------------|-----------------|  
|[System. Array](default-marshaling-for-arrays.md)|Konwertuje na tablicę w stylu C lub `SAFEARRAY` .|  
|[System. Boolean](/previous-versions/dotnet/netframework-4.0/t2t3725f(v=vs.100))|Konwertuje do wartości 1, 2 lub 4-bajtowej na wartość `true` 1 lub-1.|  
|[System. Char](/previous-versions/dotnet/netframework-4.0/6tyybbf2(v=vs.100))|Konwertuje na znak Unicode lub ANSI.|  
|[System. Class](/previous-versions/dotnet/netframework-4.0/s0968xy8(v=vs.100))|Konwertuje do interfejsu klasy.|  
|[System.Object](default-marshaling-for-objects.md)|Konwertuje na wariant lub interfejs.|  
|[System. Mdarray](default-marshaling-for-arrays.md)|Konwertuje na tablicę w stylu C lub `SAFEARRAY` .|  
|[System. String](default-marshaling-for-strings.md)|Konwertuje na ciąg kończący się w odwołaniu o wartości null lub w postaci BSTR.|  
|[System. ValueType](/previous-versions/dotnet/netframework-4.0/0t2cwe11(v=vs.100))|Konwertuje na strukturę ze stałym układem pamięci.|  
|[System. Szarray](default-marshaling-for-arrays.md)|Konwertuje na tablicę w stylu C lub `SAFEARRAY` .|  
  
 Typy klas i obiektów są obsługiwane tylko przez międzyoperacyjność modelu COM. Aby uzyskać odpowiednie typy w Visual Basic, C# i C++, zobacz [Omówienie biblioteki klas](../../standard/class-library-overview.md).  
  
## <a name="see-also"></a>Zobacz także

- [Domyślne zachowanie marshalingu](default-marshaling-behavior.md)
