---
title: "암시적 형식 지역 변수(C# 프로그래밍 가이드) | Microsoft 문서"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- implicitly-typed local variables [C#]
- var [C#]
ms.assetid: b9218fb2-ef5d-4814-8a8e-2bc29b0bbc9b
caps.latest.revision: 23
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
ms.openlocfilehash: 59bb61d8dd530e87f342d38acb131fab5e25febf
ms.lasthandoff: 03/13/2017

---
# <a name="implicitly-typed-local-variables-c-programming-guide"></a>암시적으로 형식화된 지역 변수(C# 프로그래밍 가이드)
지역 변수에 명시적 형식 대신 유추된 "형식" `var`을 지정할 수 있습니다. `var` 키워드는 초기화 문의 오른쪽에 있는 식에서 변수의 형식을 유추하도록 컴파일러에 지시합니다. 유추된 형식은 기본 제공 형식, 무명 형식, 사용자 정의 형식 또는 .NET Framework 클래스 라이브러리에 정의된 형식일 수 있습니다. `var`을 사용하여 배열을 초기화하는 방법에 대한 자세한 내용은 [암시적으로 형식화된 배열](../../../csharp/programming-guide/arrays/implicitly-typed-arrays.md)을 참조하세요.  
  
 다음 예제에서는 `var`을 사용하여 지역 변수를 선언하는 다양한 방법을 보여 줍니다.  
  
 [!code-cs[csProgGuideLINQ#43](../../../csharp/programming-guide/arrays/codesnippet/CSharp/implicitly-typed-local-variables_1.cs)]  
  
 `var` 키워드는 "variant"를 의미하지 않고 변수가 느슨하게 형식화되었거나 런타임에 바인딩되었음을 나타내지도 않습니다. 단지 컴파일러가 가장 적절한 형식을 결정하고 할당함을 의미합니다.  
  
 `var` 키워드는 다음과 같은 컨텍스트에서 사용할 수 있습니다.  
  
-   앞의 예제와 같이 지역 변수(메서드 범위에서 선언된 변수)에 대해 사용  
  
-   [for](../../../csharp/language-reference/keywords/for.md) 초기화 문에서 사용  
  
    ```  
    for(var x = 1; x < 10; x++)  
    ```  
  
-   [foreach](../../../csharp/language-reference/keywords/foreach-in.md) 초기화 문에서 사용  
  
    ```  
    foreach(var item in list){...}  
    ```  
  
-   [using](../../../csharp/language-reference/keywords/using-statement.md) 문에서 사용  
  
    ```  
    using (var file = new StreamReader("C:\\myfile.txt")) {...}  
    ```  
  
 자세한 내용은 [방법: 쿼리 식에서 암시적 형식 지역 변수 및 배열 사용](../../../csharp/programming-guide/classes-and-structs/how-to-use-implicitly-typed-local-variables-and-arrays-in-a-query-expression.md)을 참조하세요.  
  
## <a name="var-and-anonymous-types"></a>var 및 무명 형식  
 대부분의 경우 `var` 사용은 선택 사항이며 단지 편리한 구문을 위해 사용됩니다. 그러나 변수가 무명 형식을 사용하여 초기화된 경우 나중에 개체의 속성에 액세스해야 하면 변수를 `var`로 선언해야 합니다. 이것이 [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq_md.md)] 쿼리 식의 일반적인 시나리오입니다. 자세한 내용은 [무명 형식](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)을 참조하세요.  
  
 소스 코드의 관점에서 무명 형식에는 이름이 없습니다. 따라서 쿼리 변수가 `var`로 초기화된 경우 반환된 개체 시퀀스의 속성에 액세스하는 유일한 방법은 `var`을 `foreach` 문의 반복 변수 형식으로 사용하는 것입니다.  
  
 [!code-cs[csProgGuideLINQ#44](../../../csharp/programming-guide/arrays/codesnippet/CSharp/implicitly-typed-local-variables_2.cs)]  
  
## <a name="remarks"></a>설명  
 암시적 형식 변수 선언에는 다음과 같은 제한 사항이 적용됩니다.  
  
-   지역 변수가 동일한 문에서 선언 및 초기화된 경우에만 `var`을 사용할 수 있습니다. 변수를 null이나 메서드 그룹 또는 익명 함수로 초기화할 수는 없습니다.  
  
-   클래스 범위의 필드에는 `var`을 사용할 수 없습니다.  
  
-   `var`을 사용하여 선언된 변수는 초기화 식에 사용할 수 없습니다. 즉, `: int i = (i = 20);` 식은 유효하지만 `var i = (i = 20);` 식은 컴파일 시간 오류를 생성합니다.  
  
-   동일한 문에서 여러 개의 암시적 형식 변수를 초기화할 수 없습니다.  
  
-   `var`라는 형식이 범위 내에 있으면 `var` 키워드가 해당 형식 이름으로 확인되고 암시적 형식 지역 변수 선언의 일부로 처리되지 않습니다.  
  
 `var`은 생성된 쿼리 변수 형식을 정확하게 확인하기 어려운 쿼리 식에서도 유용할 수 있습니다. 그룹화 및 정렬 작업에서 이러한 경우가 발생할 수 있습니다.  
  
 또한 `var` 키워드는 변수의 특정 형식이 키보드에서 입력하기 번거롭거나, 명확하거나, 코드의 가독성에 도움이 되지 않는 경우에 유용할 수 있습니다. 이런 방식으로 `var`이 유용한 한 가지 예로 그룹 작업에 사용되는 경우 등의 중첩된 제네릭 형식이 있습니다. 다음 쿼리에서 쿼리 변수의 형식은 `IEnumerable<IGrouping<string, Student>>`입니다. 사용자나 코드를 유지 관리해야 하는 다른 사용자가 이 점을 이해하기만 하면 편리하고 간단하도록 암시적 형식을 사용하는 데 문제가 없습니다.  
  
 [!code-cs[cscsrefQueryKeywords#13](../../../csharp/language-reference/keywords/codesnippet/CSharp/implicitly-typed-local-variables_3.cs)]  
  
 그러나 `var`을 사용하면 최소한 다른 개발자가 코드를 이해하기 더 어려워질 수 있습니다. 이런 이유로, C# 문서에서는 일반적으로 필요한 경우에만 `var`을 사용합니다.  
  
## <a name="see-also"></a>참고 항목  
 [C# 참조](../../../csharp/language-reference/index.md)   
 [암시적으로 형식화된 배열](../../../csharp/programming-guide/arrays/implicitly-typed-arrays.md)   
 [방법: 쿼리 식에서 암시적 형식 지역 변수 및 배열 사용](../../../csharp/programming-guide/classes-and-structs/how-to-use-implicitly-typed-local-variables-and-arrays-in-a-query-expression.md)   
 [무명 형식](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)   
 [개체 이니셜라이저 및 컬렉션 이니셜라이저](../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md)   
 [var](../../../csharp/language-reference/keywords/var.md)   
 [LINQ 쿼리 식](../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [LINQ(Language-Integrated Query)](http://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d)   
 [for](../../../csharp/language-reference/keywords/for.md)   
 [foreach, in](../../../csharp/language-reference/keywords/foreach-in.md)   
 [using 문](../../../csharp/language-reference/keywords/using-statement.md)
