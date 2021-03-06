---
title: "How to: Access XML Child Elements (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "XML axis [Visual Basic], child"
  - "child axis property [Visual Basic]"
  - "XML child axis property [Visual Basic]"
  - "XML [Visual Basic], accessing"
ms.assetid: 6689eb36-c471-469f-a82d-099ab8197b25
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# How to: Access XML Child Elements (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

이 예제에서는 자식 축 속성을 사용하여 XML 요소에 지정한 이름이 있는 모든 XML 자식 요소에 액세스하는 방법을 보여 줍니다.  특히 <xref:System.Xml.Linq.XElement.Value%2A> 속성을 사용하여 `name` 자식 축 속성에서 반환하는 컬렉션의 첫 번째 요소 값을 가져옵니다.  `name` 자식 축 속성은 `contact` 개체에서 `phone`이라는 모든 자식 요소를 가져옵니다.  또한 이 예제에서는 `phone` 자식 축 속성을 사용하여 `contact` 개체에 포함된 `phone`이라는 모든 자식 요소에 액세스합니다.  
  
## 예제  
 [!code-vb[VbXMLSamples#10](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-access-xml-child-elements_1.vb)]  
  
## 코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
-   <xref:System.Xml.Linq> 네임스페이스에 대한 참조  
  
## 참고 항목  
 <xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=fullName>   
 [XML Child Axis Property](../../../../visual-basic/language-reference/xml-axis/xml-child-axis-property.md)   
 [XML Value Property](../../../../visual-basic/language-reference/xml-axis/xml-value-property.md)   
 [Accessing XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/accessing-xml.md)   
 [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)