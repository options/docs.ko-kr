---
title: ".NET Framework의 버전 호환성 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - ".NET Framework 4.5, 이전 버전과의 호환성"
  - ".NET Framework 버전, 호환성"
  - ".NET Framework, 버전 호환성"
ms.assetid: 2f25e522-456a-48c3-8a53-e5f39275649f
caps.latest.revision: 35
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 30
---
# .NET Framework의 버전 호환성
이전 버전과의 호환성은 특정 버전의 플랫폼용으로 개발된 앱이 해당 플랫폼의 다음 버전에서도 실행되는 것을 의미합니다.  .NET Framework에서는 이전 버전과의 호환성을 최대한 지원하려고 합니다. 한 버전의 .NET Framework용으로 작성된 소스 코드는 다음 버전의 .NET Framework에서 컴파일되어야 하며 한 버전의 .NET Framework에서 실행되는 이진 파일은 다음 버전의 .NET Framework에서 동일하게 작동해야 합니다.  
  
<a name="Apps"></a>   
## 앱의 버전 호환성  
 기본적으로 앱은 빌드에 사용된 .NET Framework 버전에서 실행됩니다.  해당 버전이 없고 앱 구성 파일에 지원되는 버전이 정의되지 않은 경우 .NET Framework 초기화 오류가 발생할 수 있습니다.  이 경우 앱을 실행하지 못합니다.  
  
 앱이 실행되는 특정 버전을 정의하려면 하나 이상의 [\<supportedRuntime\>](../../../docs/framework/configure-apps/file-schema/startup/supportedruntime-element.md) 요소를 앱의 구성 파일에 추가합니다.  각 `<supportedRuntime>` 요소에는 지원되는 런타임 버전이 나열됩니다. 우선 순위가 가장 높은 버전이 처음에 지정되고 우선 순위가 가장 낮은 버전이 마지막에 지정됩니다.  자세한 내용은 [방법: .NET Framework 4 또는 4.5를 지원하도록 응용 프로그램 구성](../../../docs/framework/migration-guide/how-to-configure-an-app-to-support-net-framework-4-or-4-5.md)을 참조하세요.  
  
## 구성 요소의 버전 호환성  
 앱에서는 실행되는 .NET Framework의 버전을 자체적으로 제어할 수 있지만, 구성 요소는 제어할 수 없습니다.  구성 요소 및 클래스 라이브러리는 특정 앱의 컨텍스트에서 로드되므로 앱이 실행되는 .NET Framework 버전에서 자동으로 실행됩니다.  
  
 이러한 제한 사항 때문에 구성 요소에서 호환성 보장은 특히 중요합니다.  .NET Framework 4부터 <xref:System.Runtime.Versioning.ComponentGuaranteesAttribute?displayProperty=fullName> 특성을 해당 구성 요소에 적용하여 구성 요소가 여러 버전 간 호환성을 유지해야 하는 수준을 지정할 수 있습니다.  여러 도구에서는 이 특성을 사용하여 이후 버전의 구성 요소에서 호환성 보장을 잠재적으로 위반할 수 있는 가능성을 검색할 수 있습니다.  
  
## 이전 버전과의 호환성과 .NET Framework 4.5  
 .NET Framework 4.5 및 해당 포인트 릴리스는 이전 버전의 .NET Framework로 빌드된 앱과 호환됩니다.  즉, 이전 버전으로 빌드된 앱과 구성 요소는 수정하지 않아도 .NET Framework 4.5에서 작동합니다.  그러나 앱은 기본적으로 해당 앱을 위해 개발된 공용 언어 런타임 버전에서 실행되기 때문에 .NET Framework 4.5에서 앱을 실행하려면 구성 파일을 제공해야 할 수 있습니다.  자세한 내용은 이 문서 앞부분의 [앱의 버전 호환성](#Apps) 섹션을 참조하십시오.  
  
 실제 상황에서 .NET Framework의 외견상 중요하지 않은 변경 사항 및 프로그래밍 기술 변경 사항에 의해 이 호환성이 손상될 수 있습니다.  예를 들어 .NET Framework 4의 성능 향상 기능이 이전 버전에서 발생하지 않은 경합 상태를 발생시킬 수 있습니다.  마찬가지로 .NET Framework 어셈블리에 하드 코드된 경로 사용, 특정 버전의 .NET Framework와 같음 비교 수행, 리플렉션을 사용한 전용 필드 값 가져오기는 이전 버전과 호환되지 않습니다.  또한 각 .NET Framework 버전에는 일부 앱 및 구성 요소의 호환성에 영향을 줄 수 있는 버그 수정 내용 및 보안 관련 변경 사항이 포함되어 있습니다.  
  
 앱이나 구성 요소가 .NET Framework 4.5, 4.5.1, 4.5.2 또는 4.6에서 제대로 작동하지 않는 경우 다음 검사 목록을 사용합니다.  
  
-   이러한 항목에 대해 앱에 영향을 줄 수 있는 모든 변경 사항을 확인하고 설명된 해결 방법을 적용하십시오.  
  
    -   [.NET Framework 4 마이그레이션 문제](http://go.microsoft.com/fwlink/p/?LinkId=248212)  
  
    -   [4.5의 응용 프로그램 호환성](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-5.md)  
  
    -   [4.5.1의 응용 프로그램 호환성](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-5-1.md)  
  
    -   [4.5.2의 응용 프로그램 호환성](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-5-2.md)  
  
    -   [4.6의 응용 프로그램 호환성](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-6.md)  
  
-   .NET Framework 1.1 앱이 있는 경우 다음 항목도 검토하십시오.  
  
    -   [.NET Framework 2.0의 변경 내용](http://go.microsoft.com/fwlink/?LinkID=125263)  
  
    -   [.NET Framework 3.5 SP1의 변경 내용](http://go.microsoft.com/fwlink/?LinkId=186989)  
  
-   .NET Framework 4.5에서 실행하기 위해 기존 소스 코드를 다시 컴파일하거나 기존 소스 코드 기반의 버전 4.5를 대상으로 하는 새 버전의 앱 또는 구성 요소를 개발하는 경우 [클래스 라이브러리의 사용되지 않는 기능](../../../docs/framework/whats-new/whats-obsolete.md)에서 사용되지 않는 형식과 멤버를 확인하고 설명된 해결 방법을 적용합니다.  이전에 컴파일된 코드는 사용되지 않는 것으로 표시된 형식과 멤버에 대해 계속해서 실행됩니다.  
  
-   [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]가 변경되어 앱이 손상된 것으로 확인된 경우 [런타임 설정 스키마](../../../docs/framework/configure-apps/file-schema/runtime/index.md)에서 앱 구성 파일의 런타임 설정을 사용하여 이전 동작을 복원할 수 있는지 여부를 확인합니다.  
  
-   문서화되지 않은 문제가 발생한 경우 [Microsoft Connect](http://go.microsoft.com/fwlink/?LinkID=154815)에 버그를 등록하고 해당 버그 번호로 [netfxcf@microsoft.com](mailto:netfxcf@microsoft.com)에 문의하세요.  
  
## 호환성 및 Side\-By\-Side 실행  
 문제에 대한 적합한 해결 방법을 찾지 못한 경우 .NET Framework 4.5가 버전 1.1, 2.0 및 3.5와 side\-by\-side 실행된다는 것과 버전 4.5는 버전 4를 대체하는 내부 업데이트임을 기억하십시오.  버전 1.1, 2.0 및 3.5를 대상으로 하는 앱의 경우 대상 컴퓨터에 적절한 .NET Framework 버전을 설치하여 앱을 가장 적합한 환경에서 실행할 수 있습니다.  Side\-by\-Side 실행에 대한 자세한 내용은 [Side\-by\-Side 실행](../../../docs/framework/deployment/side-by-side-execution.md)을 참조하세요.  
  
## 참고 항목  
 [새로운 기능](../../../docs/framework/whats-new/index.md)   
 [클래스 라이브러리의 사용되지 않는 기능](../../../docs/framework/whats-new/whats-obsolete.md)   
 [응용 프로그램 호환성](../../../docs/framework/migration-guide/application-compatibility.md)   
 [Microsoft .NET Framework 지원 주기 정책](http://go.microsoft.com/fwlink/p/?LinkId=248212)   
 [.NET Framework 4 마이그레이션 문제](http://go.microsoft.com/fwlink/p/?LinkId=248212)