---
title: "DataAdapter 매개 변수 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f21e6aba-b76d-46ad-a83e-2ad8e0af1e12
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# DataAdapter 매개 변수
<xref:System.Data.Common.DbDataAdapter>에는 데이터 소스에서 데이터를 검색하고 업데이트하는 데 사용되는 다음과 같은 네 가지 속성이 있습니다. <xref:System.Data.Common.DbDataAdapter.SelectCommand%2A> 속성은 데이터 소스에서 데이터를 반환하며 <xref:System.Data.Common.DbDataAdapter.InsertCommand%2A> , <xref:System.Data.Common.DbDataAdapter.UpdateCommand%2A> 및 <xref:System.Data.Common.DbDataAdapter.DeleteCommand%2A> 속성은 데이터 소스에서 변경 내용을 관리하는 데 사용됩니다.  `SelectCommand` 속성은 `DataAdapter`의 `Fill` 메서드를 호출하기 전에 설정해야 합니다.  `InsertCommand`, `UpdateCommand` 또는 `DeleteCommand` 속성은 `DataAdapter`의 `Update` 메서드가 호출되기 전에 설정해야 하며, <xref:System.Data.DataTable>의 데이터에 적용된 변경 내용에 따라 설정 값이 달라집니다.  예를 들어, 행이 추가되었으면 `Update`를 호출하기 전에 `InsertCommand`를 설정해야 합니다.  `Update`가 삽입, 업데이트 또는 삭제된 행을 처리하는 동안 `DataAdapter`는 해당 `Command` 속성을 사용하여 동작을 처리합니다.  수정된 행에 대한 현재 정보는 `Parameters` 컬렉션을 통해 `Command` 개체에 전달됩니다.  
  
 데이터 소스에서 행을 업데이트할 때는 업데이트된 테이블의 행을 고유 식별자로 식별하는 UPDATE 문을 호출합니다.  고유 식별자란 대개 기본 키 필드의 값을 말합니다.  UPDATE 문은 다음의 Transact\-SQL 문과 같이 고유 식별자와 업데이트된 열 및 값을 모두 포함하는 매개 변수를 사용합니다.  
  
```  
UPDATE Customers SET CompanyName = @CompanyName   
  WHERE CustomerID = @CustomerID  
```  
  
> [!NOTE]
>  매개 변수 자리 표시자의 구문은 데이터 소스에 따라 다릅니다.  이 예제에서는 SQL Server 데이터 소스용 자리 표시자를 보여 줍니다.  <xref:System.Data.OleDb> 및 <xref:System.Data.Odbc> 매개 변수의 경우 물음표\(?\) 자리 표시자를 사용합니다.  
  
 이 [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] 예제에서는 `CustomerID`가 `@CustomerID```매개 변수의 값과 동일한 행에 대해 `CompanyName` 필드가 `@CompanyName` 매개 변수의 값으로 업데이트됩니다.  이 매개 변수는 <xref:System.Data.SqlClient.SqlParameter> 개체의 <xref:System.Data.SqlClient.SqlParameter.SourceColumn%2A> 속성을 사용하여 수정된 행의 정보를 검색합니다.  다음은 앞에 나온 샘플 UPDATE 문에 대한 매개 변수입니다.  이 코드에서는 `adapter` 변수가 올바른 <xref:System.Data.SqlClient.SqlDataAdapter> 개체를 나타낸다고 가정합니다.  
  
```  
adapter.Parameters.Add( _  
  "@CompanyName", SqlDbType.NChar, 15, "CompanyName")  
Dim parameter As SqlParameter = _  
  adapter.UpdateCommand.Parameters.Add("@CustomerID", _  
  SqlDbType.NChar, 5, "CustomerID")  
parameter.SourceVersion = DataRowVersion.Original  
```  
  
 `Parameters` 컬렉션의 `Add` 메서드는 매개 변수 이름, 데이터 형식, 크기\(해당 형식에 적용되는 경우\) 및 `DataTable`의 <xref:System.Data.Common.DbParameter.SourceColumn%2A> 이름을 사용합니다.  `@CustomerID` 매개 변수의 <xref:System.Data.Common.DbParameter.SourceVersion%2A>은 `Original`로 설정됩니다.  그러면 식별하는 열 값이 수정된 <xref:System.Data.DataRow>에서 변경된 경우 데이터 소스의 기존 행이 업데이트됩니다.  이 경우 `Original` 행 값은 데이터 소스의 현재 값과 일치하고 `Current` 행 값에는 업데이트된 값이 포함됩니다.  `@CompanyName` 매개 변수의 `SourceVersion`은 설정되어 있지 않으므로 기본값인 `Current` 행 값을 사용합니다.  
  
> [!NOTE]
>  `DataAdapter`의 `Fill` 작업과 `DataReader`의 `Get` 메서드 모두에서 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 형식은 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 데이터 공급자로부터 반환된 형식에서 유추됩니다.  유추된 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 형식과 Microsoft SQL Server, OLE DB 및 ODBC 데이터 형식의 접근자 메서드는 [ADO.NET의 데이터 형식 매핑](../../../../docs/framework/data/adonet/data-type-mappings-in-ado-net.md)에 설명되어 있습니다.  
  
## Parameter.SourceColumn, Parameter.SourceVersion  
 `SourceColumn` 및 `SourceVersion`은 `Parameter` 생성자에 인수로 전달되거나 기존 `Parameter`의 속성으로 설정될 수 있습니다.  `SourceColumn`은 `Parameter` 값이 검색될 <xref:System.Data.DataRow>의 <xref:System.Data.DataColumn> 이름입니다.  `SourceVersion`에서는 `DataAdapter`가 값을 검색하기 위해 사용하는 `DataRow` 버전을 지정합니다.  
  
 다음 표에서는 `SourceVersion`에 사용할 수 있는 <xref:System.Data.DataRowVersion> 열거형 값을 보여 줍니다.  
  
|DataRowVersion 열거형|설명|  
|------------------------|--------|  
|`Current`|열의 현재 값을 사용하는 매개 변수입니다.  이 값이 기본값입니다.|  
|`Default`|열의 `DefaultValue`를 사용하는 매개 변수입니다.|  
|`Original`|열의 원래 값을 사용하는 매개 변수입니다.|  
|`Proposed`|제안된 값을 사용하는 매개 변수입니다.|  
  
 다음 단원의 `SqlClient` 코드 예제에서는 `CustomerID` 열이 두 매개 변수 `@CustomerID`\(`SET CustomerID = @CustomerID`\) 및 `@OldCustomerID` \(`WHERE CustomerID = @OldCustomerID`\)에 대한 `SourceColumn`으로 사용되는 <xref:System.Data.Common.DbDataAdapter.UpdateCommand%2A>의 매개 변수를 정의합니다.  `@CustomerID` 매개 변수는 **CustomerID** 열을 `DataRow`의 현재 값으로 업데이트하는 데 사용됩니다.  결과적으로 `SourceVersion`이 `Current`인 `CustomerID` `SourceColumn`이 사용됩니다.  *@OldCustomerID* 매개 변수는 데이터 소스에서 현재 행을 식별하는 데 사용됩니다.  행의 `Original` 버전에 일치하는 열 값이 있으므로 `SourceVersion`이 `Original`인 동일한 `SourceColumn`\(`CustomerID`\)이 사용됩니다.  
  
## SqlClient 매개 변수 사용  
 다음 예제에서는 데이터베이스에서 추가적인 스키마 정보를 검색하기 위해 <xref:System.Data.SqlClient.SqlDataAdapter>를 만들고 <xref:System.Data.Common.DataAdapter.MissingSchemaAction%2A>을 <xref:System.Data.MissingSchemaAction>로 설정하는 방법을 보여 줍니다.  <xref:System.Data.SqlClient.SqlDataAdapter.SelectCommand%2A>, <xref:System.Data.SqlClient.SqlDataAdapter.InsertCommand%2A>, <xref:System.Data.SqlClient.SqlDataAdapter.UpdateCommand%2A> 및 <xref:System.Data.SqlClient.SqlDataAdapter.DeleteCommand%2A> 속성이 설정되고 해당 <xref:System.Data.SqlClient.SqlParameter> 개체가 <xref:System.Data.SqlClient.SqlCommand.Parameters%2A> 컬렉션에 추가됩니다.  메서드에서 `SqlDataAdapter` 개체를 반환합니다.  
  
 [!code-csharp[Classic WebData SqlDataAdapter.SqlDataAdapter Example#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/Classic WebData SqlDataAdapter.SqlDataAdapter Example/CS/source.cs#1)]
 [!code-vb[Classic WebData SqlDataAdapter.SqlDataAdapter Example#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/Classic WebData SqlDataAdapter.SqlDataAdapter Example/VB/source.vb#1)]  
  
## OleDb 매개 변수 자리 표시자  
 <xref:System.Data.OleDb.OleDbDataAdapter> 및 <xref:System.Data.Odbc.OdbcDataAdapter> 개체의 경우 물음표\(?\) 자리 표시자를 사용하여 매개 변수를 식별해야 합니다.  
  
```vb  
Dim selectSQL As String = _  
  "SELECT CustomerID, CompanyName FROM Customers " & _  
  "WHERE CountryRegion = ? AND City = ?"  
Dim insertSQL AS String = _  
  "INSERT INTO Customers (CustomerID, CompanyName) VALUES (?, ?)"  
Dim updateSQL AS String = _  
  "UPDATE Customers SET CustomerID = ?, CompanyName = ? " & _  
  WHERE CustomerID = ?"  
Dim deleteSQL As String = "DELETE FROM Customers WHERE CustomerID = ?"  
```  
  
```csharp  
string selectSQL =   
  "SELECT CustomerID, CompanyName FROM Customers " +  
  "WHERE CountryRegion = ? AND City = ?";  
string insertSQL =   
  "INSERT INTO Customers (CustomerID, CompanyName) " +  
  "VALUES (?, ?)";  
string updateSQL =   
  "UPDATE Customers SET CustomerID = ?, CompanyName = ? " +  
  "WHERE CustomerID = ? ";  
string deleteSQL = "DELETE FROM Customers WHERE CustomerID = ?";  
```  
  
 매개 변수가 있는 쿼리 문에서는 만들어야 할 입력 및 출력 매개 변수를 정의합니다.  매개 변수를 만들려면 `Parameters.Add` 메서드나 `Parameter` 생성자를 사용하여 열 이름, 데이터 형식 및 크기를 지정합니다.  `Integer`와 같은 내장 데이터 형식의 경우 크기를 포함할 필요가 없거나 기본 크기를 지정할 수 있습니다.  
  
 다음 코드 예제에서는 SQL 문에 대한 매개 변수를 만들고 `DataSet`을 채웁니다.  
  
## OleDb 예제  
  
```vb  
' Assumes that connection is a valid OleDbConnection object.  
Dim adapter As OleDbDataAdapter = New OleDbDataAdapter   
  
Dim selectCMD AS OleDbCommand = New OleDbCommand(selectSQL, connection)  
adapter.SelectCommand = selectCMD  
  
' Add parameters and set values.  
selectCMD.Parameters.Add( _  
  "@CountryRegion", OleDbType.VarChar, 15).Value = "UK"  
selectCMD.Parameters.Add( _  
  "@City", OleDbType.VarChar, 15).Value = "London"  
  
Dim customers As DataSet = New DataSet  
adapter.Fill(customers, "Customers")  
  
```  
  
```csharp  
// Assumes that connection is a valid OleDbConnection object.  
OleDbDataAdapter adapter = new OleDbDataAdapter();  
  
OleDbCommand selectCMD = new OleDbCommand(selectSQL, connection);  
adapter.SelectCommand = selectCMD;  
  
// Add parameters and set values.  
selectCMD.Parameters.Add(  
  "@CountryRegion", OleDbType.VarChar, 15).Value = "UK";  
selectCMD.Parameters.Add(  
  "@City", OleDbType.VarChar, 15).Value = "London";  
  
DataSet customers = new DataSet();  
adapter.Fill(customers, "Customers");  
```  
  
## Odbc 매개 변수  
  
```vb  
' Assumes that connection is a valid OdbcConnection object.  
Dim adapter As OdbcDataAdapter = New OdbcDataAdapter  
  
Dim selectCMD AS OdbcCommand = New OdbcCommand(selectSQL, connection)  
adapter.SelectCommand = selectCMD  
  
' Add Parameters and set values.  
selectCMD.Parameters.Add("@CountryRegion", OdbcType.VarChar, 15).Value = "UK"  
selectCMD.Parameters.Add("@City", OdbcType.VarChar, 15).Value = "London"  
  
Dim customers As DataSet = New DataSet  
adapter.Fill(customers, "Customers")  
  
```  
  
```csharp  
// Assumes that connection is a valid OdbcConnection object.  
OdbcDataAdapter adapter = new OdbcDataAdapter();  
  
OdbcCommand selectCMD = new OdbcCommand(selectSQL, connection);  
adapter.SelectCommand = selectCMD;  
  
//Add Parameters and set values.  
selectCMD.Parameters.Add("@CountryRegion", OdbcType.VarChar, 15).Value = "UK";  
selectCMD.Parameters.Add("@City", OdbcType.VarChar, 15).Value = "London";  
  
DataSet customers = new DataSet();  
adapter.Fill(customers, "Customers");  
```  
  
> [!NOTE]
>  매개 변수에 이름을 지정하지 않으면 "Parameter1"로 시작하는 증분 기본 이름인 Parameter*N*이 매개 변수에 지정됩니다.  매개 변수 이름을 입력하는 경우에는 Parameter*N* 명명 규칙을 사용하지 않는 것이 좋습니다. 이 경우 `ParameterCollection`에 있는 기존의 기본 매개 변수 이름과 충돌이 발생할 수 있습니다.  이미 있는 이름을 입력하면 예외가 throw됩니다.  
  
## 참고 항목  
 [DataAdapters 및 DataReaders](../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)   
 [명령 및 매개 변수](../../../../docs/framework/data/adonet/commands-and-parameters.md)   
 [DataAdapters를 사용하여 데이터 소스 업데이트](../../../../docs/framework/data/adonet/updating-data-sources-with-dataadapters.md)   
 [저장 프로시저로 데이터 수정](../../../../docs/framework/data/adonet/modifying-data-with-stored-procedures.md)   
 [ADO.NET의 데이터 형식 매핑](../../../../docs/framework/data/adonet/data-type-mappings-in-ado-net.md)   
 [ADO.NET 관리되는 공급자 및 데이터 집합 개발자 센터](http://go.microsoft.com/fwlink/?LinkId=217917)