---
title: "방법: finally를 사용하여 정리 코드 실행(C# 프로그래밍 가이드) | Microsoft 문서"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- try/finally blocks [C#]
- exceptions [C#], try/finally block
- exception handling [C#], try/finally block
ms.assetid: 1b1e5aef-3f32-4a88-9d39-b5fffb33bdaf
caps.latest.revision: 21
author: BillWagner
ms.author: wiwagn
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
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: b9c22ca8ee9c83e6f1808520530c6d1912d8f4f1
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-execute-cleanup-code-using-finally-c-programming-guide"></a>방법: finally를 사용하여 정리 코드 실행(C# 프로그래밍 가이드)
`finally` 문은 예외가 throw된 경우에도 개체, 일반적으로 외부 리소스를 포함하는 개체의 필요한 정리가 즉시 수행되도록 합니다. 이러한 정리 작업의 한 가지 예로 다음과 같이 개체가 공용 언어 런타임에 의해 수집될 때까지 기다리지 않고 사용 후 즉시 <xref:System.IO.FileStream>에 대해 <xref:System.IO.Stream.Close%2A>를 호출하는 것입니다.  
  
 [!code-cs[csProgGuideExceptions#16](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/how-to-execute-cleanup-code-using-finally_1.cs)]  
  
## <a name="example"></a>예제  
 이전 코드를 `try-catch-finally` 문으로 바꾸려면 다음과 같이 정리 코드와 작업 코드를 구분합니다.  
  
 [!code-cs[csProgGuideExceptions#17](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/how-to-execute-cleanup-code-using-finally_2.cs)]  
  
 `OpenWrite()` 호출 또는 `OpenWrite()` 호출 자체가 실패하기 전에 `try` 블록 내에서 언제든지 예외가 발생할 수 있으므로 파일을 닫으려고 할 때 열려 있다는 보장은 없습니다. `finally` 블록은 <xref:System.IO.Stream.Close%2A> 메서드를 호출하기 전에 <xref:System.IO.FileStream> 개체가 `null`이 아닌지 확인하는 검사를 추가합니다. `null` 검사가 없으면 `finally` 블록에서 고유한 <xref:System.NullReferenceException>을 throw할 수 있지만 가능하면 `finally` 블록에서 예외를 throw하지 않도록 해야 합니다.  
  
 데이터베이스 연결은 `finally` 블록에서 닫기에 적합한 또 다른 후보입니다. 데이터베이스 서버에 허용되는 연결 수가 제한된 경우도 있으므로 최대한 빨리 데이터베이스 연결을 닫아야 합니다. 연결을 닫기 전에 예외가 throw되는 경우에도 `finally` 블록 사용이 가비지 수집을 기다리는 것보다 더 낫습니다.  
  
## <a name="see-also"></a>참고 항목  
 [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)   
 [예외 및 예외 처리](../../../csharp/programming-guide/exceptions/index.md)   
 [예외 처리](../../../csharp/programming-guide/exceptions/exception-handling.md)   
 [using 문](../../../csharp/language-reference/keywords/using-statement.md)   
 [try-catch](../../../csharp/language-reference/keywords/try-catch.md)   
 [try-finally](../../../csharp/language-reference/keywords/try-finally.md)   
 [try-catch-finally](../../../csharp/language-reference/keywords/try-catch-finally.md)
