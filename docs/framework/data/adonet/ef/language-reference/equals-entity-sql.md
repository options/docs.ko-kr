---
title: "= (같음) (Entity SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
ms.assetid: 948eb588-7080-4046-bb48-633b007393bf
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# = (같음) (Entity SQL)
두 식이 같은지 비교합니다.  
  
## 구문  
  
```  
  
          expression  
          =  
          expression  
or   
expression==expression  
```  
  
## 인수  
 `expression`  
 모든 유효한 식입니다. 비교할 두 식 모두 데이터 형식이 암시적으로 변환 가능해야 합니다.  
  
## 결과 형식  
 왼쪽 식의 값이 오른쪽 식의 값과 같으면 `true`이고, 그렇지 않으면 `false`입니다.  
  
## 설명  
 \=\= 연산자는 \= 연산자와 동일합니다.  
  
## 예제  
 다음 Entity SQL 쿼리에서는 \= 비교 연산자를 사용하여 두 식이 같은지 비교합니다. 쿼리는 AdventureWorks Sales 모델을 기반으로 합니다. 이 쿼리를 컴파일하고 실행하려면 다음 단계를 수행하세요.  
  
1.  [방법: StructuralType 결과를 반환하는 쿼리 실행](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-structuraltype-results.md)의 절차를 따릅니다.  
  
2.  다음 쿼리를 `ExecuteStructuralTypeQuery` 메서드에 인수로 전달합니다.  
  
 [!code-csharp[DP EntityServices Concepts 2#EQUALS](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#equals)]  
  
## 참고 항목  
 [Entity SQL 참조](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)