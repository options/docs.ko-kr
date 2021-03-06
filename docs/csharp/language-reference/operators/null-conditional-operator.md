---
title: "?? 연산자(C# 참조) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "??_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "?? 연산자[C#]"
  - "병합 연산자[C#]"
  - "조건부 AND 연산자(&&)[C#]"
ms.assetid: 088b1f0d-c1af-4fe1-b4b8-196fd5ea9132
caps.latest.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 17
---
# ?? 연산자(C# 참조)
`??` 연산자는 null 병합 연산자라고 합니다.  이 연산자는 피연산자가 null이 아닐 경우 왼쪽 피연산자를 반환하고 null일 경우 오른쪽 피연산자를 반환합니다.  
  
## 설명  
 nullable 형식은 형식 도메인의 값을 나타낼 수 있거나 값을 정의하지 않을 수 있습니다\(이 경우 값은 null\).  왼쪽 연산자에 값이 null인 null 허용 형식이 있는 경우 `??` 연산자의 구문 표현을 사용하여 적절한 값을 반환할 수 있습니다\(오른쪽 피연산자\).  `??` 연산자를 사용하지 않고 nullable 값 형식을 nullable이 아닌 값 형식에 할당하려고 하면 컴파일 타임 오류가 발생합니다.  캐스트를 사용할 때 nullable 값 형식이 현재 정의되어 있지 않으면 `InvalidOperationException` 예외가 throw됩니다.  
  
 자세한 내용은 [nullable 형식](../../../csharp/programming-guide/nullable-types/index.md)을 참조하십시오.  
  
 ?? 연산자의 결과는 두 인수가 상수인 경우에도 상수가 될 수 없습니다.  
  
## 예제  
 [!code-cs[csRefOperators#53](../../../csharp/language-reference/operators/codesnippet/CSharp/null-conditional-operator_1.cs)]  
  
## 참고 항목  
 [C\# 참조](../../../csharp/language-reference/index.md)   
 [C\# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)   
 [C\# 연산자](../../../csharp/language-reference/operators/index.md)   
 [nullable 형식](../../../csharp/programming-guide/nullable-types/index.md)   
 ['리프트'란 정확히 어떤 의미입니까?](http://go.microsoft.com/fwlink/?LinkID=112382)