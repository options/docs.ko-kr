---
title: "방법: BlockingCollection에서 개별적으로 항목 추가 및 가져오기 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "스레드로부터 안전한 컬렉션, 차단 사전"
ms.assetid: 38f2f3d8-15e5-4bf4-9c83-2b5b6f22bad1
caps.latest.revision: 7
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 7
---
# 방법: BlockingCollection에서 개별적으로 항목 추가 및 가져오기
이 예제에서는 차단 및 비차단 방식으로 <xref:System.Collections.Concurrent.BlockingCollection%601>에서 항목을 추가하고 제거하는 방법을 보여 줍니다.<xref:System.Collections.Concurrent.BlockingCollection%601>에 대한 자세한 내용은 [BlockingCollection 개요](../../../../docs/standard/collections/thread-safe/blockingcollection-overview.md)을 참조하세요.  
  
 빈 상태가 되고 더 이상 요소가 추가되지 않을 때까지 <xref:System.Collections.Concurrent.BlockingCollection%601>을 열거하는 방법의 예제는 [방법: ForEach를 사용하여 BlockingCollection의 항목 제거](../../../../docs/standard/collections/thread-safe/how-to-use-foreach-to-remove.md)을 참조하세요.  
  
## 예제  
 이 첫 번째 예제에서는 컬렉션이 일시적으로 비어있거나\(가져올 때\) 최대 용량일 경우\(추가할 때\) 또는 지정된 제한 시간이 경과되었을 경우 작업이 차단되도록 항목을 추가하거나 가져오는 방법을 보여 줍니다. 최대 용량에서 차단은 생성자에서 최대 용량이 지정된 상태에서 BlockingCollection이 만들어졌을 때에만 사용하도록 설정됩니다.  
  
 [!code-csharp[CDS_BlockingCollection#01](../../../../samples/snippets/csharp/VS_Snippets_Misc/cds_blockingcollection/cs/example01.cs#01)]
 [!code-vb[CDS_BlockingCollection#01](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_blockingcollection/vb/simpleblocking.vb#01)]  
  
## 예제  
 이 두 번째 예제에서는 작업이 차단되지 않도록 항목을 추가하고 가져오는 방법을 보여 줍니다. 항목이 없거나 바인딩된 컬렉션에서 최대 용량에 도달했을 경우 또는 제한 시간이 경과한 경우 <xref:System.Collections.Concurrent.BlockingCollection%601.TryAdd%2A> 또는 <xref:System.Collections.Concurrent.BlockingCollection%601.TryTake%2A> 작업에서 False를 반환합니다. 이를 통해 스레드는 잠시 동안 다른 몇 가지 유용한 작업을 수행한 다음 나중에 다시 한 번 새 항목을 검색하거나 이전에 추가할 수 없었던 동일한 항목을 추가하려고 시도할 수 있습니다. 프로그램은 또한 <xref:System.Collections.Concurrent.BlockingCollection%601>에 액세스할 때 취소를 구현하는 방법을 보여 줍니다.  
  
 [!code-csharp[CDS_BlockingCollection#02](../../../../samples/snippets/csharp/VS_Snippets_Misc/cds_blockingcollection/cs/example02.cs#02)]
 [!code-vb[CDS_BlockingCollection#02](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_blockingcollection/vb/nonblockingbc.vb#02)]  
  
## 참고 항목  
 <xref:System.Collections.Concurrent?displayProperty=fullName>   
 [BlockingCollection 개요](../../../../docs/standard/collections/thread-safe/blockingcollection-overview.md)