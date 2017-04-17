---
title: "관계 간 쿼리 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 297878d0-685b-4c01-b2e0-9d731b7322bc
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# 관계 간 쿼리
클래스 정의에서 다른 개체 또는 다른 개체의 컬렉션에 대한 참조는 데이터베이스의 외래 키 관계에 직접적으로 해당합니다.  점 표기법을 사용하여 쿼리할 때 이러한 관계를 사용하여 관계 속성에 액세스하고 한 개체에서 다른 개체로 이동할 수 있습니다.  이러한 액세스 작업은 해당 SQL에서 더 복잡한 조인이나 연관된 하위 쿼리로 변환됩니다.  
  
 예를 들어 다음 쿼리는 런던에 있는 고객의 주문으로만 결과를 제한하기 위한 방법으로 주문에서 고객으로 이동합니다.  
  
 [!code-csharp[DLinqQueryConcepts#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#3)]
 [!code-vb[DLinqQueryConcepts#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#3)]  
  
 관계 속성이 없을 경우에는 다음 코드와 같이 SQL 쿼리에서처럼 관계 속성을 *조인*으로 직접 작성해야 합니다.  
  
 [!code-csharp[DLinqQueryConcepts#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#4)]
 [!code-vb[DLinqQueryConcepts#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#4)]  
  
 *관계* 속성을 사용하여 이 특정 관계를 한 번 정의한 다음  더 편리한 점 구문을 사용할 수 있습니다.  그러나 관계 속성이 존재하는 더 중요한 이유는 도메인 관련 개체 모델이 일반적으로 계층 구조나 그래프로 정의되기 때문입니다.  사용자가 프로그래밍하는 개체는 다른 개체에 대한 참조를 가집니다.  운이 좋다면 개체 간의 관계와 데이터베이스의 외래 키 스타일 관계가 일치할 수도 있습니다.  그런 다음 속성 액세스를 통해 조인을 편리하게 작성할 수 있습니다.  
  
 이와 관련하여 관계 속성은 쿼리 자체의 일부보다는 쿼리의 결과 측면에서 더 중요합니다.  쿼리에서 특정 고객에 대한 데이터를 검색한 후 클래스 정의에서는 고객이 주문을 갖고 있다는 것을 나타냅니다.  즉, 특정 고객의 `Orders` 속성은 해당 고객의 모든 주문으로 채워지는 컬렉션으로 간주됩니다.  실제로 이 방식으로 클래스를 정의하여 계약이 선언됩니다  쿼리가 주문을 요청하지 않은 경우에도 주문을 보게 될 것입니다.  또한 개체 모델은 즉시 사용 가능한 관련 개체가 있는 데이터베이스의 메모리 내 확장이라는 가정을 유지합니다.  
  
 이제 관계가 존재하므로 클래스에 정의된 관계 속성을 참조하여 쿼리를 작성할 수 있습니다.  이러한 관계 참조는 데이터베이스의 외래 키 관계에 해당합니다.  이러한 관계를 사용하는 작업은 해당 SQL에서 더 복잡한 조인으로 변환됩니다.  <xref:System.Data.Linq.Mapping.AssociationAttribute> 특성을 사용하여 관계를 정의한 경우 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서 명시적 조인을 코딩할 필요가 없습니다.  
  
 이 가정을 유지하는 데 도움이 되도록 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]은 *지연된 로드*라는 기술을 구현합니다.  자세한 내용은 [지연된 로드와 즉시 로드 비교](../../../../../../docs/framework/data/adonet/sql/linq/deferred-versus-immediate-loading.md)를 참조하세요.  
  
 `CustomerID`\-`OrderID` 쌍의 목록을 반환하기 위한 다음 SQL 쿼리를 살펴보세요.  
  
```  
SELECT t0.CustomerID, t1.OrderID  
FROM   Customers AS t0 INNER JOIN  
          Orders AS t1 ON t0.CustomerID = t1.CustomerID  
WHERE  (t0.City = @p0)  
```  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]을 사용하여 동일한 결과를 얻으려면 이미 `Orders` 클래스에 있는 `Customer` 속성 참조를 사용합니다.  `Orders` 참조는 다음 코드와 같이 쿼리를 실행하고 `CustomerID`\-`OrderID` 쌍을 반환하는 데 필요한 정보를 제공합니다.  
  
 [!code-csharp[DLinqQueryConcepts#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#5)]
 [!code-vb[DLinqQueryConcepts#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#5)]  
  
 반대로 할 수도 있습니다.  즉, `Orders`를 쿼리하고 해당 `Customer` 관계 참조를 사용하여 연관된 `Customer` 개체에 대한 정보에 액세스할 수 있습니다.  다음 코드는 앞의 경우와 동일한 `CustomerID`\-`OrderID` 쌍을 반환하지만 `Orders` 대신 `Customers`를 쿼리합니다.  
  
 [!code-csharp[DLinqQueryConcepts#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#6)]
 [!code-vb[DLinqQueryConcepts#6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#6)]  
  
## 참고 항목  
 [쿼리 개념](../../../../../../docs/framework/data/adonet/sql/linq/query-concepts.md)