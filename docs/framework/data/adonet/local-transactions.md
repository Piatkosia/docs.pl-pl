---
title: Transakcje lokalne
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 8ae3712f-ef5e-41a1-9ea9-b3d0399439f1
ms.openlocfilehash: a0b713ab0b81cb2f0661212dae22db34b7f9f3ae
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91175398"
---
# <a name="local-transactions"></a>Transakcje lokalne

Transakcje w programie ADO.NET są używane, gdy chcesz powiązać wiele zadań w taki sposób, aby wykonywały one jako pojedynczą jednostkę pracy. Załóżmy na przykład, że aplikacja wykonuje dwa zadania. Najpierw aktualizuje tabelę z informacjami o zamówieniu. Następnie aktualizuje tabelę zawierającą informacje o zapasach, co oznacza, że elementy są uporządkowane. Jeśli jedno z zadań nie powiedzie się, obie aktualizacje zostaną wycofane.  
  
## <a name="determining-the-transaction-type"></a>Określanie typu transakcji  

 Transakcja jest traktowana jako transakcja lokalna, gdy jest to transakcja jednoetapowa i jest obsługiwana bezpośrednio przez bazę danych. Transakcja jest traktowana jako transakcja rozproszona, gdy jest koordynowana przez Monitor transakcji i używa mechanizmów awaryjnych (takich jak zatwierdzenie dwufazowe) do rozpoznawania transakcji.  
  
 Każdy dostawca danych .NET Framework ma własny `Transaction` obiekt do wykonywania transakcji lokalnych. Jeśli potrzebujesz transakcji do wykonania w bazie danych SQL Server, wybierz <xref:System.Data.SqlClient> transakcję. W przypadku transakcji Oracle Użyj <xref:System.Data.OracleClient> dostawcy. Ponadto istnieje <xref:System.Data.Common.DbTransaction> Klasa, która jest dostępna do pisania kodu niezależnego od dostawcy, który wymaga transakcji.  
  
> [!NOTE]
> Transakcje są najbardziej wydajne, gdy są wykonywane na serwerze. Jeśli pracujesz z SQL Server bazą danych, która wykonuje szerokie użycie jawnych transakcji, rozważ zapisanie ich jako procedur składowanych przy użyciu instrukcji języka Transact-SQL BEGIN TRANSACTION.
  
## <a name="performing-a-transaction-using-a-single-connection"></a>Wykonywanie transakcji przy użyciu jednego połączenia  

 W programie ADO.NET można kontrolować transakcje z `Connection` obiektem. Możesz zainicjować transakcję lokalną za pomocą `BeginTransaction` metody. Po rozpoczęciu transakcji można zarejestrować polecenie w tej transakcji z `Transaction` właściwością `Command` obiektu. Następnie możesz zatwierdzić lub cofnąć modyfikacje wprowadzone w źródle danych na podstawie sukcesu lub niepowodzenia składników transakcji.  
  
> [!NOTE]
> `EnlistDistributedTransaction`Metoda nie powinna być używana dla transakcji lokalnej.  
  
 Zakres transakcji jest ograniczony do połączenia. Poniższy przykład wykonuje jawną transakcję, która składa się z dwóch oddzielnych poleceń w `try` bloku. Polecenia Execute instrukcji INSERT odnoszą się do tabeli Product. ScrapReason w przykładowej bazie danych AdventureWorks SQL Server, które są zatwierdzone w przypadku niezgłaszania wyjątków. Kod w `catch` bloku Wycofuje transakcję w przypadku zgłoszenia wyjątku. Jeśli transakcja została przerwana lub połączenie zostanie zamknięte przed ukończeniem transakcji, zostanie automatycznie wycofane.  
  
## <a name="example"></a>Przykład  

 Wykonaj następujące kroki, aby wykonać transakcję.  
  
1. Wywołaj <xref:System.Data.SqlClient.SqlConnection.BeginTransaction%2A> metodę obiektu, <xref:System.Data.SqlClient.SqlConnection> Aby oznaczyć początek transakcji. <xref:System.Data.SqlClient.SqlConnection.BeginTransaction%2A>Metoda zwraca odwołanie do transakcji. To odwołanie jest przypisane do <xref:System.Data.SqlClient.SqlCommand> obiektów, które są zarejestrowane w transakcji.  
  
2. Przypisz `Transaction` obiekt do <xref:System.Data.SqlClient.SqlCommand.Transaction%2A> właściwości, która <xref:System.Data.SqlClient.SqlCommand> ma zostać wykonana. Jeśli polecenie jest wykonywane w ramach połączenia z aktywną transakcją, a `Transaction` obiekt nie został przypisany do `Transaction` właściwości `Command` obiektu, zostanie zgłoszony wyjątek.  
  
3. Wykonaj wymagane polecenia.  
  
4. Wywołaj <xref:System.Data.SqlClient.SqlTransaction.Commit%2A> metodę <xref:System.Data.SqlClient.SqlTransaction> obiektu, aby zakończyć transakcję, lub wywołaj <xref:System.Data.SqlClient.SqlTransaction.Rollback%2A> metodę, aby zakończyć transakcję. Jeśli połączenie jest zamknięte lub zlikwidowane przed <xref:System.Data.SqlClient.SqlTransaction.Commit%2A> <xref:System.Data.SqlClient.SqlTransaction.Rollback%2A> wykonaniem metody lub, transakcja zostanie wycofana.  
  
 Poniższy przykład kodu demonstruje logikę transakcyjną przy użyciu ADO.NET z Microsoft SQL Server.  
  
 [!code-csharp[DataWorks SqlTransaction.Local#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlTransaction.Local/CS/source.cs#1)]
 [!code-vb[DataWorks SqlTransaction.Local#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlTransaction.Local/VB/source.vb#1)]  
  
## <a name="see-also"></a>Zobacz też

- [Transakcje i współbieżność](transactions-and-concurrency.md)
- [Transakcje rozproszone](distributed-transactions.md)
- [Integracja System.Transactions z programem SQL Server](system-transactions-integration-with-sql-server.md)
- [Omówienie ADO.NET](ado-net-overview.md)
