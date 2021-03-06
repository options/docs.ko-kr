---
title: "| 연산자(C# 참조) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "|_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "| 연산자[C#]"
  - "이항 연산자(|)[C#]"
  - "비트 OR 연산자[C#]"
ms.assetid: 82d6bb78-54c8-40bf-b679-531180ddaf70
caps.latest.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 15
---
# | 연산자(C# 참조)
Binary        `|`  연산자는 정수 계열 형식과 `bool`에 대해 미리 정의되어 있습니다.  정수 계열 형식의 경우  `|`연산자는 피연산자에 대한 비트 OR를 계산합니다.  `bool` 피연산자의 경우  `|` 연산자는 피연산자에 대한 논리 OR를 계산합니다. 즉, 두 피연산자가 모두 `false`인 경우에만 결과가 `false`입니다.  
  
## 설명  
 사용자 정의 형식으로          `|` 연산자를 오버로드할 수 있습니다\([operator](../../../csharp/language-reference/keywords/operator.md) 참조\).  
  
## 예제  
 [!code-cs[csRefOperators#31](../../../csharp/language-reference/operators/codesnippet/CSharp/or-operator_1.cs)]  
  
## 참고 항목  
 [C\# 참조](../../../csharp/language-reference/index.md)   
 [C\# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)   
 [C\# 연산자](../../../csharp/language-reference/operators/index.md)