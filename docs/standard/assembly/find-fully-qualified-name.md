---
title: 'Instrukcje: Znajdowanie w pełni kwalifikowanej nazwy zestawu'
description: W tym artykule pokazano, jak uzyskać w pełni kwalifikowaną nazwę zestawu platformy .NET.
ms.date: 08/20/2019
helpviewer_keywords:
- names [.NET], fully qualified type names
- names [.NET], assemblies
- assemblies [.NET], names
ms.assetid: 009dae23-e1f6-4a64-9a9a-32e4c34802b0
dev_langs:
- csharp
- vb
- cpp
ms.openlocfilehash: 223def7d992f5fae64c95aa6886f20980184eddc
ms.sourcegitcommit: 279fb6e8d515df51676528a7424a1df2f0917116
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/27/2020
ms.locfileid: "92687617"
---
# <a name="how-to-find-an-assemblys-fully-qualified-name"></a>Instrukcje: Znajdowanie w pełni kwalifikowanej nazwy zestawu

Aby odnaleźć w pełni kwalifikowaną nazwę zestawu .NET Framework w globalnej pamięci podręcznej zestawów, użyj narzędzia globalnej pamięci podręcznej zestawów ([Gacutil.exe](../../framework/tools/gacutil-exe-gac-tool.md)). Zobacz [jak to zrobić: wyświetlanie zawartości globalnej pamięci podręcznej zestawów](../../framework/app-domains/how-to-view-the-contents-of-the-gac.md).

W przypadku zestawów .NET Core i dla zestawów .NET Framework, które nie znajdują się w globalnej pamięci podręcznej zestawów, można uzyskać w pełni kwalifikowaną nazwę zestawu na wiele sposobów:

- Można użyć kodu do wyprowadzania informacji do konsoli lub do zmiennej. można też użyć [Ildasm.exe (Il dezasembler)](../../framework/tools/ildasm-exe-il-disassembler.md) do sprawdzenia metadanych zestawu, który zawiera w pełni kwalifikowaną nazwę.

- Jeśli zestaw jest już załadowany przez aplikację, możesz pobrać wartość <xref:System.Reflection.Assembly.FullName%2A?displayProperty=nameWithType> właściwości, aby uzyskać w pełni kwalifikowaną nazwę. Możesz użyć <xref:System.Type.Assembly> właściwości <xref:System.Type> zdefiniowanej w tym zestawie, aby pobrać odwołanie do <xref:System.Reflection.Assembly> obiektu. Przykład stanowi ilustrację.

- Jeśli znasz ścieżkę systemu plików zestawu, możesz wywołać `static` metodę (C#) lub `Shared` (Visual Basic), <xref:System.Reflection.AssemblyName.GetAssemblyName%2A?displayProperty=nameWithType> Aby uzyskać w pełni kwalifikowaną nazwę zestawu. Poniżej przedstawiono prosty przykład.

  ```csharp
  using System;
  using System.Reflection;

  public class Example
  {
     public static void Main()
     {
        Console.WriteLine(AssemblyName.GetAssemblyName(@".\UtilityLibrary.dll"));
     }
  }
  // The example displays output like the following:
  //   UtilityLibrary, Version=1.1.0.0, Culture=neutral, PublicKeyToken=null
  ```

  ```vb
  Imports System.Reflection

  Public Module Example
     Public Sub Main
        Console.WriteLine(AssemblyName.GetAssemblyName(".\UtilityLibrary.dll"))
     End Sub
  End Module
  ' The example displays output like the following:
  '   UtilityLibrary, Version=1.1.0.0, Culture=neutral, PublicKeyToken=null
  ```

- Można użyć [Ildasm.exe (Il dezasembler)](../../framework/tools/ildasm-exe-il-disassembler.md) do sprawdzenia metadanych zestawu, który zawiera w pełni kwalifikowaną nazwę.

Aby uzyskać więcej informacji na temat ustawiania atrybutów zestawu, takich jak wersja, kultura i nazwa zestawu, zobacz [Ustawianie atrybutów zestawu](set-attributes.md). Aby uzyskać więcej informacji na temat nadawania silnej nazwy zestawu, zobacz [Tworzenie i używanie zestawów o silnej nazwie](create-use-strong-named.md).

## <a name="example"></a>Przykład

Poniższy przykład pokazuje, jak wyświetlić w pełni kwalifikowaną nazwę zestawu zawierającego określoną klasę w konsoli programu. Używa właściwości, <xref:System.Type.Assembly?displayProperty=nameWithType> Aby pobrać odwołanie do zestawu z typu, który jest zdefiniowany w tym zestawie.

```cpp
#using <System.dll>
#using <System.Data.dll>

using namespace System;
using namespace System::Reflection;

ref class asmname
{
public:
    static void Main()
    {
        Type^ t = System::Data::DataSet::typeid;
        String^ s = t->Assembly->FullName->ToString();
        Console::WriteLine("The fully qualified assembly name " +
            "containing the specified class is {0}.", s);
    }
};

int main()
{
    asmname::Main();
}
```

```csharp
using System;
using System.Reflection;

class asmname
{
    public static void Main()
    {
        Type t = typeof(System.Data.DataSet);
        string s = t.Assembly.FullName.ToString();
        Console.WriteLine("The fully qualified assembly name " +
            "containing the specified class is {0}.", s);
    }
}
```

```vb
Imports System.Reflection

Class asmname
    Public Shared Sub Main()
        Dim t As Type = GetType(System.Data.DataSet)
        Dim s As String = t.Assembly.FullName.ToString()
        Console.WriteLine("The fully qualified assembly name " +
            "containing the specified class is {0}.", s)
    End Sub
End Class
```

## <a name="see-also"></a>Zobacz także

- [Nazwy zestawów](names.md)
- [Tworzenie zestawów](create.md)
- [Tworzenie i używanie zestawów o silnej nazwie](create-use-strong-named.md)
- [Globalna pamięć podręczna zestawów](../../framework/app-domains/gac.md)
- [Jak środowisko uruchomieniowe lokalizuje zestawy](../../framework/deployment/how-the-runtime-locates-assemblies.md)
