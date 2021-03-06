---
title: SqlMetal.exe (Narzędzie generowania kodu)
description: Poznaj SqlMetal.exe narzędzia generowania kodu. Użyj narzędzia, aby wygenerować kod i mapowanie dla składnika LINQ to SQL platformy .NET.
ms.date: 03/30/2017
helpviewer_keywords:
- SQLMetal [LINQ to SQL]
- code generation tool
- SQLMetal.exe
- LINQ to SQL, serialization
- LINQ to SQL, DBML files
- LINQ to SQL, SQLMetal
ms.assetid: 819e5a96-7646-4fdb-b14b-fe31221b0614
ms.openlocfilehash: 84cad85a7a9fc4b420b57543b7f258607be4ab52
ms.sourcegitcommit: b4f8849c47c1a7145eb26ce68bc9f9976e0dbec3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2020
ms.locfileid: "87517051"
---
# <a name="sqlmetalexe-code-generation-tool"></a>SqlMetal.exe (Narzędzie generowania kodu)
Narzędzie wiersza polecenia SqlMetal generuje kod i mapowanie dla [!INCLUDE[vbtecdlinq](../../../includes/vbtecdlinq-md.md)] składnika .NET Framework. Stosując opisane w dalszej części tego tematu opcje, można za pomocą programu SqlMetal wykonać kilka różnych akcji, takich jak:  
  
- Na podstawie bazy danych — generowanie kodu źródłowego i atrybutów mapowania lub pliku mapowania.  
  
- Na podstawie bazy danych — generowanie pliku języka Intermediate Database Markup Language (dbml) na potrzeby dostosowywania.  
  
- Na podstawie pliku dbml — generowanie kodu i atrybutów mapowania lub pliku mapowania.  
  
 To narzędzie jest instalowane automatycznie z programem Visual Studio. Domyślnie plik znajduje się w `drive` folderze: \Program Files\Microsoft SDKs\Windows\v `n.nn` \Bin. Jeśli program Visual Studio nie zostanie zainstalowany, można również pobrać plik SQLMetal, pobierając [Windows SDK](https://go.microsoft.com/fwlink/?LinkId=142225).  
  
> [!NOTE]
> Deweloperzy, którzy korzystają z programu Visual Studio, mogą również generować klasy jednostek przy użyciu Object Relational Designer. Podejście z użyciem wiersza polecenia dobrze sprawdza się w przypadku dużych baz danych. Program SqlMetal to narzędzie wiersza polecenia, więc można użyć go w procesie kompilacji.  
  
 Aby uruchomić narzędzie, użyj wiersz polecenia dla deweloperów dla programu Visual Studio (lub wiersza polecenia programu Visual Studio w systemie Windows 7). Aby uzyskać więcej informacji, zobacz [wiersza polecenia](developer-command-prompt-for-vs.md). W wierszu polecenia wpisz następujące polecenie:  
  
## <a name="syntax"></a>Składnia  
  
```console  
sqlmetal [options] [<input file>]  
```  
  
## <a name="options"></a>Opcje  
 Aby wyświetlić najbardziej aktualną listę opcji, wpisz `sqlmetal /?` w wierszu polecenia z zainstalowanej lokalizacji.  
  
 **Opcje połączenia**  
  
|Opcja|Opis|  
|------------|-----------------|  
|**/Server:***\<name>*|Określa nazwę serwera bazy danych.|  
|**/Database:***\<name>*|Określa wykaz baz danych na serwerze.|  
|**/User:***\<name>*|Określa identyfikator logowania użytkownika. Wartość domyślna: Użyj uwierzytelniania systemu Windows.|  
|**/Password:***\<password>*|Określa hasło logowania. Wartość domyślna: Użyj uwierzytelniania systemu Windows.|  
|**/Conn:***\<connection string>*|Określa parametry połączenia z bazą danych. Nie można używać z opcjami **/Server**, **/Database**, **/User**i **/Password** .<br /><br /> W parametrach połączenia nie można umieszczać nazwy pliku. Zamiast tego należy określić nazwę pliku w wierszu polecenia jako plik wejściowy. Na przykład poniższy wiersz określa "c:\northwnd.mdf" jako plik wejściowy: **SQLMetal/Code: "c:\Northwind.cs"/Language: CSharp "c:\northwnd.mdf"**.|  
|**/timeout:***\<seconds>*|Określa wartość limitu czasu używaną, gdy program SqlMetal uzyskuje dostęp do bazy danych. Wartość domyślna: 0 (czyli brak limitu czasu).|  
  
 **Opcje wyodrębniania**  
  
|Opcja|Opis|  
|------------|-----------------|  
|**/views**|Wyodrębnia widoki bazy danych.|  
|**/functions**|Wyodrębnia funkcje bazy danych.|  
|**/sprocs**|Wyodrębnia procedury składowane.|  
  
 **Opcje wyjściowe**  
  
|Opcja|Opis|  
|------------|-----------------|  
|**/DBML** *[: plik]*|Wysyła dane wyjściowe w postaci pliku dbml. Nie można używać z opcją **/map** .|  
|**/Code** *[: plik]*|Wysyła dane wyjściowe w postaci kodu źródłowego. Nie można używać z opcją **/DBML** .|  
|**/map** *[: plik]*|Generuje plik mapowania XML zamiast atrybutów. Nie można używać z opcją **/DBML** .|  
  
 **Różne**  
  
|Opcja|Opis|  
|------------|-----------------|  
|**/Language:***\<language>*|Określa język kodu źródłowego.<br /><br /> Prawidłowy *\<language>* : VB, CSharp.<br /><br /> Wartość domyślna: pochodzi z rozszerzeniem nazwy pliku kodu.|  
|**/Namespace:***\<name>*|Określa przestrzeń nazw wygenerowanego kodu. Wartość domyślna: brak przestrzeni nazw.|  
|**/Context:***\<type>*|Określa nazwę klasy kontekstu danych. Wartość domyślna: pochodzi z nazwy bazy danych.|  
|**/entitybase:***\<type>*|Określa klasę bazową klas obiektów w generowanym kodzie. Wartość domyślna: obiekty nie mają klasy bazowej.|  
|**/Pluralize**|Automatycznie zmienia nazwy klas i składowych na liczbę mnogą lub pojedynczą.<br /><br /> Ta opcja jest dostępna tylko w wersji angielskiej (USA).|  
|**/Serialization:***\<option>*|Generuje klasy, które można serializować.<br /><br /> Prawidłowy *\<option>* : brak, jednokierunkowe. Wartość domyślna: None.<br /><br /> Aby uzyskać więcej informacji, zobacz [serializacji](../data/adonet/sql/linq/serialization.md).|  
  
 **Plik wejściowy**  
  
|Opcja|Opis|  
|------------|-----------------|  
|**\<input file>**|Określa plik. mdf SQL Server Express, plik SQL Server Compact 3,5. sdf lub plik pośredni. dbml.|  
  
## <a name="remarks"></a>Uwagi  
 Działanie programu SqlMetal w rzeczywistości obejmuje wykonanie dwóch kroków:  
  
- Wyodrębnienie metadanych bazy danych do pliku dbml.  
  
- Wygenerowanie pliku wyjściowego z kodem.  
  
     Korzystając z odpowiednich opcji wiersza polecenia, można utworzyć kod źródłowy Visual Basic lub C# lub utworzyć plik mapowania XML.  
  
 Aby wyodrębnić metadane z pliku mdf, należy określić nazwę pliku mdf po wszystkich innych opcjach.  
  
 Jeśli **/Server** nie jest określony, zakłada się **localhost/SQLExpress** .  
  
 Microsoft SQL Server 2005 zgłasza wyjątek, jeśli spełnione są co najmniej jeden z następujących warunków:  
  
- Program SqlMetal próbuje wyodrębnić procedurę składowaną, którą sam wywołuje.  
  
- Poziom zagnieżdżenia procedury składowanej, funkcji lub widoku przekracza 32.  
  
     Program SqlMetal przechwytuje ten wyjątek i zgłasza go jako ostrzeżenie.  
  
 Aby określić nazwę pliku wejściowego, należy dodać ją do wiersza polecenia jako plik wejściowy. Dołączenie nazwy pliku w parametrach połączenia (przy użyciu opcji **/Conn** ) nie jest obsługiwane.  
  
## <a name="examples"></a>Przykłady  
 Generuje plik dbml zawierający wyodrębnione metadane SQL:  
  
 **SQLMetal/Server:/Database o identyfikatorze northwind/dbml: meta. dbml**  
  
 Generuje plik dbml zawierający metadane SQL wyodrębnione z pliku mdf przy użyciu programu SQL Server Express:  
  
 **SQLMetal/dbml: meta. dbml mydbfile. mdf**  
  
 Generuje plik dbml zawierający metadane SQL wyodrębnione z programu SQL Server Express:  
  
 **SQLMetal/Server: .\SQLEXPRESS/dbml: meta. dbml/Database: Northwind**  
  
 Generuje kod źródłowy na podstawie pliku metadanych dbml:  
  
 **SQLMetal/Namespace: NWIND/Code: NWIND. cs/Language: CSharp. dbml**  
  
 Generuje kod źródłowy bezpośrednio na podstawie metadanych SQL:  
  
 **SQLMetal/Server: KSW/Database: Northwind/Namespace: NWIND/Code: NWIND. cs/Language: CSharp**  
  
> [!NOTE]
> W przypadku korzystania z opcji **/pluralize** z przykładową bazą danych Northwind należy zwrócić uwagę na następujące zachowanie. Gdy program SqlMetal tworzy nazwy tabel typu wiersz, nazwy tabel mają liczbę pojedynczą. Gdy udostępnia <xref:System.Data.Linq.DataContext> Właściwości tabel, nazwy tabel są w liczbie mnogiej. Przypadkowo nazwy tabel w przykładowej bazie danych Northwind mają już liczbę mnogą. Dlatego też nie widać działania tej części opcji. Popularną praktyką jest nadawanie tabelom w bazie danych nazw w liczbie pojedynczej, ale równie popularną praktyką na platformie .NET jest nadawanie kolekcjom nazw w liczbie mnogiej.  
  
## <a name="see-also"></a>Zobacz także

- [Instrukcje: Generowanie modelu obiektu w języku Visual Basic lub C#](../data/adonet/sql/linq/how-to-generate-the-object-model-in-visual-basic-or-csharp.md)
- [Generowanie kodu w składniku LINQ to SQL](../data/adonet/sql/linq/code-generation-in-linq-to-sql.md)
- [Mapowanie zewnętrzne](../data/adonet/sql/linq/external-mapping.md)
