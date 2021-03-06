---
title: "SpinWait | Microsoft Docs"
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
  - "synchronization primitives, SpinWait"
ms.assetid: 36012f42-34e5-4f86-adf4-973f433ed6c6
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# SpinWait
<xref:System.Threading.SpinWait?displayProperty=fullName>는 하위 수준 시나리오에서 커널 이벤트에 필요한 부담이 큰 컨텍스트 전환 및 커널 전환을 대신하기 위해 사용할 수 있는 간단한 동기화 형식입니다.  다중 코어 컴퓨터에서 리소스가 오랫동안 보관될 것으로 예상되지 않는 경우 사용자 모드에서 대기 중인 스레드를 수십 또는 수백 차례 더 회전한 다음 리소스 확보를 다시 시도하는 것이 더 효율적일 수 있습니다.  회전 후 리소스를 사용할 수 있으면 수천 차례 저장한 것입니다.  아직 리소스를 사용할 수 없으면 하나의 사이클만 사용되었고 여전히 커널 기반 대기에 들어갈 수 있습니다.  이 회전 후 대기 조합은 *2단계 대기 작업*이라고도 합니다.  
  
 <xref:System.Threading.SpinWait>는 <xref:System.Threading.ManualResetEvent>와 같은 커널 이벤트를 래핑하는 .NET Framework 형식과 함께 사용되도록 설계되었습니다.  또한 <xref:System.Threading.SpinWait>는 기본 회전 기능을 제공하기 위해 하나의 프로그램에서 단독으로 사용할 수도 있습니다.  
  
 <xref:System.Threading.SpinWait>는 빈 루프 이상의 기능을 수행합니다.  즉, 일반적인 경우에는 올바른 회전 동작을 제공할 수 있도록 신중하게 구현되어 있으며, 충분히 회전한 경우\(즉, 커널 전환에 필요한 시간 만큼 회전한 경우\)에는 컨텍스트 전환을 시작합니다.  예를 들어 단일 코어 컴퓨터에서는 모든 스레드에서 회전 블록이 앞으로 진행되기 때문에 <xref:System.Threading.SpinWait>가 스레드의 시간 간격을 즉시 계산합니다.  또한 <xref:System.Threading.SpinWait>는 다중 코어 컴퓨터에서도 대기 스레드가 우선 순위가 더 높은 스레드나 가비지 수집기를 차단하는 것을 방지하기 위해 시간 간격을 계산합니다.  따라서 2단계 대기 작업에서 <xref:System.Threading.SpinWait>를 사용하는 경우에는 <xref:System.Threading.SpinWait>가 컨텍스트 전환을 시작하기 전에 커널 대기를 호출하는 것이 좋습니다.  <xref:System.Threading.SpinWait>는 <xref:System.Threading.SpinWait.SpinOnce%2A>가 호출될 때마다 그전에 확인할 수 있는 <xref:System.Threading.SpinWait.NextSpinWillYield%2A> 속성을 제공합니다.  이 속성이 `true`를 반환하면 사용자 고유의 대기 작업을 시작합니다.  예제를 보려면 [How to: Use SpinWait to Implement a Two\-Phase Wait Operation](../../../docs/standard/threading/how-to-use-spinwait-to-implement-a-two-phase-wait-operation.md)를 참조하십시오.  
  
 2단계 대기 작업을 수행하지 않고 특정 조건이 true가 될 때까지 단순히 회전하고 있는 경우 <xref:System.Threading.SpinWait>가 컨텍스트 전환을 수행하여 Windows 운영 체제 환경에서 제대로 작동하도록 설정할 수 있습니다.  다음 기본 예제에서는 잠금이 필요 없는 스택에 있는 <xref:System.Threading.SpinWait>를 보여 줍니다.  스레드로부터 안전한 고성능 스택이 필요하면 <xref:System.Collections.Concurrent.ConcurrentStack%601?displayProperty=fullName>을 사용하는 것이 좋습니다.  
  
 [!code-csharp[CDS_SpinWait#05](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_spinwait/cs/spinwait.cs#05)]
 [!code-vb[CDS_SpinWait#05](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_spinwait/vb/cds_spinwait1.vb#05)]  
  
## 참고 항목  
 <xref:System.Threading.Thread.SpinWait%2A>   
 [Threading Objects and Features](../../../docs/standard/threading/threading-objects-and-features.md)