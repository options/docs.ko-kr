---
title: "혼합 된 선언적 코드 명령적 코드 버그 (LINQ to XML) (Visual Basic) | Microsoft 문서"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: f12b1ab4-bb92-4b92-a648-0525e45b3ce7
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 08edcabc3f0238c499f87c713f205ee5a517a1ea
ms.lasthandoff: 03/13/2017

---
# <a name="mixed-declarative-codeimperative-code-bugs-linq-to-xml-visual-basic"></a>혼합 된 선언적 코드/명령적 코드 버그 (LINQ to XML) (Visual Basic)
[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]에는 XML 트리를 직접 수정하는 데 사용할 수 있는 다양한 메서드가 포함되어 있습니다. 요소를 추가 및 삭제하고, 요소의 내용을 변경하고, 특성을 추가하는 등의 작업을 수행할 수 있습니다. 이 프로그래밍 인터페이스에 설명 된 [XML 트리 수정 (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/modifying-xml-trees-linq-to-xml.md)합니다. 경우 반복 하는 축 중 하나를 통해 같은 <xref:System.Xml.Linq.XContainer.Elements%2A>, 및 축 반복 하면서 XML 트리를 수정 하는, 결국 이상한 버그가 발생할 수 있습니다.</xref:System.Xml.Linq.XContainer.Elements%2A>  
  
 이 문제를 "할로윈 문제"라고도 합니다.  
  
## <a name="definition-of-the-problem"></a>문제에 대한 정의  
 LINQ를 사용하여 컬렉션을 반복하는 코드를 작성하는 경우 선언적 스타일로 코드를 작성할 수 있습니다. 하는 것을 설명 하는 것과 유사 *어떤* 아니라 원하는 *어떻게* 작업을 수행 하려면. 1) 첫 번째 요소를 가져오고 2) 특정 조건에 대해 테스트한 다음 3) 요소를 수정하고 4) 요소를 다시 목록에 배치하는 코드를 작성하는 경우 코드는 명령적 코드일 수 있습니다. 컴퓨터에 지시 하면 *어떻게* 를 수행할 수 있습니다.  
  
 이러한 스타일의 코드를 동일한 작업에서 혼합하면 문제가 발생할 수 있습니다. 다음을 살펴보세요.  
  
 세 항목(a, b 및 c)이 포함된 연결된 목록이 있는 경우를 생각해 보겠습니다.  
  
 `a -> b -> c`  
  
 이제 연결된 목록을 이동하여 세 항목(a', b' 및 c')을 새로 추가한다고 가정해 보겠습니다. 다음과 같은 연결된 목록을 생성하려고 합니다.  
  
 `a -> a' -> b -> b' -> c -> c'`  
  
 따라서 목록을 반복하고 각 항목의 바로 뒤에 새 항목을 추가하는 코드를 작성합니다. 코드에서는 먼저 `a` 요소를 찾고 그 뒤에 `a'`를 삽입합니다. 그런 다음 목록의 다음 노드로 이동합니다. 하지만 다음 노드는 이제 `a'`입니다. 코드에서는 새 항목 `a''`를 목록에 추가합니다.  
  
 실제 상황에서 이 문제를 어떻게 해결하시겠습니까? 연결된 원래 목록의 복사본을 만들고 완전히 새로운 목록을 만들 수도 있습니다. 또는 순전히 명령적 코드를 작성하는 경우 첫 번째 항목을 찾고 새 항목을 추가한 다음 연결된 목록에서 두 차례 이동하여 방금 추가한 요소를 건너뛸 수도 있습니다.  
  
## <a name="adding-while-iterating"></a>반복하는 동안 추가  
 예를 들어, 트리의 모든 요소에 대한 중복 요소를 만드는 코드를 작성하는 경우를 생각해 보겠습니다.  
  
```vb  
Dim root As XElement = _  
    <Root>  
        <A>1</A>  
        <B>2</B>  
        <C>3</C>  
    </Root>  
For Each e As XElement In root.Elements()  
    root.Add(New XElement(e.Name, e.Value))  
Next  
  
```  
  
 이 코드는 무한 루프에 들어갑니다. `foreach` 문은 `Elements()` 축을 반복하여 새 요소를 `doc` 요소에 추가합니다. 따라서 방금 추가한 요소도 반복하게 됩니다. 루프를 반복할 때마다 새 개체를 할당하기 때문에 결국 사용 가능한 모든 메모리를 사용하게 됩니다.  
  
 컬렉션에 사용 하 여 메모리에 가져오는 방법으로이 문제를 해결할 수는 <xref:System.Linq.Enumerable.ToList%2A>다음과 같이 표준 쿼리 연산자:</xref:System.Linq.Enumerable.ToList%2A>  
  
```vb  
Dim root As XElement = _  
    <Root>  
        <A>1</A>  
        <B>2</B>  
        <C>3</C>  
    </Root>  
For Each e As XElement In root.Elements().ToList()  
    root.Add(New XElement(e.Name, e.Value))  
Next  
Console.WriteLine(root)  
  
```  
  
 이제 코드가 제대로 작동합니다. 생성되는 XML 트리는 다음과 같습니다.  
  
```xml  
<Root>  
  <A>1</A>  
  <B>2</B>  
  <C>3</C>  
  <A>1</A>  
  <B>2</B>  
  <C>3</C>  
</Root>  
```  
  
## <a name="deleting-while-iterating"></a>반복하는 동안 삭제  
 특정 수준의 노드를 모두 삭제하려는 경우 다음과 같은 코드를 작성하려고 할 수 있습니다.  
  
```vb  
Dim root As XElement = _  
    <Root>  
        <A>1</A>  
        <B>2</B>  
        <C>3</C>  
    </Root>  
For Each e As XElement In root.Elements()  
    e.Remove()  
Next  
Console.WriteLine(root)  
  
```  
  
 그러나 이 코드는 원하는 작업을 수행하지 않습니다. 이 상황에서 첫 번째 요소 A를 제거하면 루트에 포함된 XML 트리에서 이 요소가 제거되고 반복을 수행하는 Elements 메서드의 코드에서 다음 요소를 찾을 수 없습니다.  
  
 위에 있는 코드의 결과는 다음과 같습니다.  
  
```xml  
<Root>  
  <B>2</B>  
  <C>3</C>  
</Root>  
```  
  
 솔루션 다시 호출 하는 <xref:System.Linq.Enumerable.ToList%2A>다음과 같이 컬렉션을 구체화 하는:</xref:System.Linq.Enumerable.ToList%2A>  
  
```vb  
Dim root As XElement = _  
    <Root>  
        <A>1</A>  
        <B>2</B>  
        <C>3</C>  
    </Root>  
For Each e As XElement In root.Elements().ToList()  
    e.Remove()  
Next  
Console.WriteLine(root)  
  
```  
  
 이 코드의 결과는 다음과 같습니다.  
  
```xml  
<Root />  
```  
  
 또는 모두 제거할 수 있습니다 반복 호출 하 여 <xref:System.Xml.Linq.XElement.RemoveAll%2A>부모 요소에:</xref:System.Xml.Linq.XElement.RemoveAll%2A>  
  
```vb  
Dim root As XElement = _  
    <Root>  
        <A>1</A>  
        <B>2</B>  
        <C>3</C>  
    </Root>  
root.RemoveAll()  
Console.WriteLine(root)  
  
```  
  
## <a name="why-cant-linq-automatically-handle-this"></a>LINQ를 사용하여 이 문제를 자동으로 처리할 수 없는 이유  
 한 가지 방법은 지연 계산을 수행하는 대신 항상 모든 항목을 메모리에 가져오는 것입니다. 그러나 이 방법은 성능과 메모리 사용 측면에서 비용이 매우 많이 듭니다. LINQ와 (LINQ to XML)이 이 방법을 사용한다면 실제 상황에서 제대로 작동하지 않을 것입니다.  
  
 또 다른 가능한 방법은 트랜잭션 구문을 LINQ에 삽입한 다음 컴파일러에서 코드를 분석하고 특정 컬렉션이 구체화되어야 했는지 확인하도록 하는 것입니다. 그러나 의도하지 않은 결과를 발생시키는 모든 코드를 확인하는 작업은 상당히 복잡합니다. 다음 코드를 살펴보세요.  
  
```vb  
Dim z = _  
    From e In root.Elements() _  
    Where (TestSomeCondition(e)) _  
    Select DoMyProjection(e)  
  
```  
  
 이러한 분석 코드에서는 TestSomeCondition 및 DoMyProjection 메서드를 분석하고 이러한 메서드가 호출한 모든 메서드를 분석하여 의도하지 않은 결과를 발생시킨 코드가 있는지 확인해야 합니다. 그러나 이 분석 코드에서는 의도하지 않은 결과를 발생시킨 코드를 찾기만 할 수는 없으며 이 상황에서 `root`의 자식 요소에 의도하지 않은 결과를 발생시킨 코드를 선택해야 합니다.  
  
 LINQ to XML에서는 이러한 분석을 수행하려고 하지 않습니다.  
  
 이러한 문제를 방지하는 것은 사용자의 책임입니다.  
  
## <a name="guidance"></a>지침  
 첫째, 선언적 코드와 명령적 코드를 혼합하지 마세요.  
  
 컬렉션의 의미와 XML 트리를 수정하는 메서드의 의미를 정확히 파악하고 이러한 범주의 문제를 방지하는 효과적인 코드를 작성하는 경우에도 향후 다른 개발자가 해당 코드를 유지 관리해야 할 때 이 문제를 명확히 이해하지 못할 수 있습니다. 선언적 코딩 스타일과 명령적 코딩 스타일을 혼합하면 코드가 더욱 불안정해집니다.  
  
 이러한 문제가 방지되도록 컬렉션을 구체화하는 코드를 작성하는 경우 코드에 이 문제에 대한 주석을 삽입하여 유지 관리 프로그래머가 이 문제를 이해하도록 해야 합니다.  
  
 둘째, 성능과 다른 고려 사항이 허용하는 경우 선언적 코드만 사용하세요. 기존 XML 트리는 수정하지 말고 새 XML 트리를 생성하세요.  
  
```vb  
Dim root As XElement = _  
    <Root>  
        <A>1</A>  
        <B>2</B>  
        <C>3</C>  
    </Root>  
Dim newRoot As XElement = New XElement("Root", _  
    root.Elements(), root.Elements())  
Console.WriteLine(newRoot)  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [고급 LINQ to XML 프로그래밍 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/advanced-linq-to-xml-programming.md)
