---
title: "제네릭 형식 매개 변수(C# 프로그래밍 가이드) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "제네릭[C#], 형식 매개 변수"
  - "형식 매개 변수[C#]"
ms.assetid: a03b0ab2-0606-4b41-b7bf-e64d5bb4d18f
caps.latest.revision: 23
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 23
---
# 제네릭 형식 매개 변수(C# 프로그래밍 가이드)
제네릭 형식 또는 메서드 정의에서 형식 매개 변수는 클라이언트가 제네릭 형식의 변수를 인스턴스화할 때 지정하는 특정 형식에 대한 자리 표시자입니다.  [제네릭 소개](../../../csharp/programming-guide/generics/introduction-to-generics.md)에 나열된 `GenericList<T>` 등의 제네릭 클래스는 실제로 형식이 아니고 형식에 대한 청사진과 같으므로 있는 그대로 사용할 수는 없습니다.  클라이언트 코드에서 `GenericList<T>`를 사용하려면 꺾쇠괄호 내에 형식 매개 변수를 지정하는 방법으로 생성된 형식을 선언하고 인스턴스화해야 합니다.  이 특정 클래스에 대한 형식 매개 변수의 형식은 컴파일러에서 인식하는 모든 형식이 될 수 있습니다.  만들 수 있는 생성된 형식 인스턴스의 수에는 제한이 없고, 각 인스턴스에서는 다음과 같이 서로 다른 형식 매개 변수를 사용할 수 있습니다.  
  
 [!code-cs[csProgGuideGenerics#7](../../../csharp/programming-guide/generics/codesnippet/csharp/generic-type-parameters_1.cs)]  
  
 `GenericList<T>`의 각 인스턴스에서 클래스에 있는 모든 `T`는 런타임에 형식 매개 변수로 대체됩니다.  이러한 대체를 통해 단일 클래스 정의를 사용하여 세 개의 형식 안전적이고 효율적인 개체를 개별적으로 만들 수 있습니다.  CLR에서 이러한 대체를 수행하는 방식에 대한 자세한 내용은 [런타임의 제네릭](../../../csharp/programming-guide/generics/generics-in-the-run-time.md)을 참조하십시오.  
  
## 형식 매개 변수 명명 지침  
  
-   **필수적** 단일 문자 이름으로도 자체 설명이 가능하여 설명적인 이름을 굳이 사용할 필요가 없는 경우가 아니면 제네릭 형식 매개 변수 이름을 설명적인 이름으로 지정하십시오.  
  
     [!code-cs[csProgGuideGenerics#8](../../../csharp/programming-guide/generics/codesnippet/csharp/generic-type-parameters_2.cs)]  
  
-   **선택적** 단일 문자 형식 매개 변수를 사용하는 형식에는 형식 매개 변수 이름으로 T를 사용하십시오.  
  
     [!code-cs[csProgGuideGenerics#9](../../../csharp/programming-guide/generics/codesnippet/csharp/generic-type-parameters_3.cs)]  
  
-   **필수적** 설명적인 형식 매개 변수 이름 앞에 “T”를 붙이십시오.  
  
     [!code-cs[csProgGuideGenerics#10](../../../csharp/programming-guide/generics/codesnippet/csharp/generic-type-parameters_4.cs)]  
  
-   **선택적** 매개 변수 이름 안에서 형식 매개 변수에 적용되는 제약 조건을 나타내십시오.  예를 들어 `ISession`으로 제한되는 매개 변수의 이름은 `TSession`이 될 수 있습니다.  
  
## 참고 항목  
 <xref:System.Collections.Generic>   
 [C\# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)   
 [제네릭](../../../csharp/programming-guide/generics/index.md)   
 [C\+\+ 템플릿과 C\# 제네릭의 차이점](../../../csharp/programming-guide/generics/differences-between-cpp-templates-and-csharp-generics.md)