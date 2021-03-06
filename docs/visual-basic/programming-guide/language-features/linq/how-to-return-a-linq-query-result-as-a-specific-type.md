---
title: "방법: LINQ 쿼리 결과 특정 형식 (Visual Basic)으로 반환 | Microsoft 문서"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- queries [LINQ in Visual Basic], specific type returned
- projection [LINQ in Visual Basic]
- anonymous types [Visual Basic]
- querying databases [LINQ]
- queries [LINQ in Visual Basic], how-to topics
- query samples [Visual Basic]
ms.assetid: 621bb10a-e5d7-44fb-a025-317964b19d92
caps.latest.revision: 8
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 2031e24ca0fe5aa86ca6c0bcd0e0e4f27238c8ae
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-return-a-linq-query-result-as-a-specific-type-visual-basic"></a>방법: LINQ 쿼리 결과를 특정 형식으로 반환(Visual Basic)
언어 통합 쿼리 (LINQ)를 사용 하면 쉽게 데이터베이스 정보에 액세스 하 고 쿼리를 실행할 수 있습니다. LINQ 쿼리는 기본적으로 익명 형식으로 개체 목록을 반환 합니다. 쿼리에서 사용 하 여 특정 형식의 목록을 반환 하도록 지정할 수도 있습니다는 `Select` 절.  
  
 다음 예제에는 SQL Server 데이터베이스에 대 한 쿼리를 수행 하 고 특정 명명 된 형식으로 결과 프로젝션 하는 새 응용 프로그램을 만드는 방법을 보여 줍니다. 자세한 내용은 참조 [익명 형식](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md) 및 [Select 절](../../../../visual-basic/language-reference/queries/select-clause.md)합니다.  
  
 이 항목의 예제는 Northwind 샘플 데이터베이스를 사용합니다. 개발 컴퓨터에 Northwind 샘플 데이터베이스가 없는 경우 있습니다에서 다운로드할 수는 [Microsoft 다운로드 센터](http://go.microsoft.com/fwlink/?LinkID=98088) 웹 사이트입니다. 자세한 내용은 [샘플 데이터베이스 다운로드](https://msdn.microsoft.com/library/bb399411)합니다.  
  
[!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
### <a name="to-create-a-connection-to-a-database"></a>데이터베이스에 연결을 만들려면  
  
1.  Visual Studio에서 열고 **서버 탐색기**/**데이터베이스 탐색기** 클릭 하 여 **서버 탐색기**/**데이터베이스 탐색기** 에 **보기** 메뉴.  
  
2.  마우스 오른쪽 단추로 클릭 **데이터 연결** 에서 **서버 탐색기**/**데이터베이스 탐색기** 클릭 하 고 **연결 추가**합니다.  
  
3.  Northwind 샘플 데이터베이스에 올바른 연결을 지정 합니다.  
  
### <a name="to-add-a-project-that-contains-a-linq-to-sql-file"></a>LINQ to SQL 파일을 포함 하는 프로젝트를 추가 하려면  
  
1.  Visual Studio에서에 **파일** 메뉴에서 **새로** 클릭 하 고 **프로젝트**합니다. Visual basic **Windows Forms 응용 프로그램** 프로젝트 유형으로 합니다.  
  
2.  **프로젝트** 메뉴에서 **새 항목 추가**를 클릭합니다. 선택 된 **LINQ to SQL 클래스** 항목 템플릿.  
  
3.  파일 이름을 `northwind.dbml`합니다. **추가**를 클릭합니다. 개체 관계형 디자이너 (O/R 디자이너) northwind.dbml 파일이 열립니다.  
  
### <a name="to-add-tables-to-query-to-the-or-designer"></a>O/R 디자이너를 쿼리 하는 테이블을 추가 하려면  
  
1.  **서버 탐색기**/**데이터베이스 탐색기**, Northwind 데이터베이스에 연결을 확장 합니다. 확장 된 **테이블** 폴더입니다.  
  
     O/R 디자이너를 닫은 경우 앞에 추가 되는 northwind.dbml 파일을 두 번 클릭 하 여 다시 열 수 있습니다.  
  
2.  Customers 테이블을 클릭 하 고 디자이너의 왼쪽된 창에 놓습니다.  
  
     디자이너에서는 새 `Customer` 프로젝트에 대 한 개체입니다. 쿼리 결과를 프로젝션 할 수는 `Customer` 형식 또는 사용자가 만드는 유형에. 이 예제를 이후 절차에서 새 형식을 만들어 해당 형식으로 쿼리 결과 합니다.  
  
3.  변경 내용을 저장 하 고 디자이너를 닫습니다.  
  
4.  프로젝트를 저장합니다.  
  
### <a name="to-add-code-to-query-the-database-and-display-the-results"></a>데이터베이스를 쿼리하고 결과 표시 하는 코드를 추가 하려면  
  
1.  **도구 상자**를 끌어 한 <xref:System.Windows.Forms.DataGridView>Form1 프로젝트에 대 한 기본 Windows Form 컨트롤을.</xref:System.Windows.Forms.DataGridView>  
  
2.  Form1 Form1 클래스를 수정 하려면 두 번 클릭 합니다.  
  
3.  이후에 `End Class` 를 만드는 다음 코드를 추가 하는 문을 Form1 클래스의는 `CustomerInfo` 이 샘플에 대 한 쿼리 결과 보유 하는 형식을 합니다.  
  
     [!code-vb[VbLINQToSQLHowTos #&16;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/how-to-return-a-linq-query-result-as-a-specific-type_1.vb)]  
  
4.  O/R 디자이너에 테이블을 추가한 경우 디자이너 추가 <xref:System.Data.Linq.DataContext>프로젝트에는 개체입니다.</xref:System.Data.Linq.DataContext> 이 개체는 해당 테이블에 액세스 하 고 개별 개체 및 각 테이블에 대 한 컬렉션에 액세스할 수 있어야 하는 코드를 포함 합니다. <xref:System.Data.Linq.DataContext>.dbml 파일의 이름에 따라 프로젝트에 대 한 개체입니다.</xref:System.Data.Linq.DataContext> 이 프로젝트는 <xref:System.Data.Linq.DataContext>개체의 이름은 `northwindDataContext`.</xref:System.Data.Linq.DataContext>  
  
     인스턴스를 만들 수는 <xref:System.Data.Linq.DataContext>O/R 디자이너에서 지정 된 테이블에 프로그램 코드를 쿼리 합니다.</xref:System.Data.Linq.DataContext>  
  
     에 `Load` Form1 클래스의 이벤트 데이터 컨텍스트의 속성으로 노출 되는 테이블을 쿼리 하는 다음 코드를 추가 합니다. `Select` 쿼리 절에 새 만들어집니다 `CustomerInfo` 쿼리 결과의 각 항목에 대 한 익명 형식 대신 형식입니다.  
  
     [!code-vb[VbLINQToSQLHowTos #&15;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/how-to-return-a-linq-query-result-as-a-specific-type_2.vb)]  
  
5.  F5 키를 눌러 프로젝트를 실행 하 고 결과 확인 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [쿼리](../../../../visual-basic/language-reference/queries/queries.md)   
 [LINQ to SQL](https://msdn.microsoft.com/library/bb386976)   
 [DataContext 메서드 (O/R 디자이너)](https://docs.microsoft.com/visualstudio/data-tools/datacontext-methods-o-r-designer)

