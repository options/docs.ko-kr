---
title: "&lt;gcServer&gt; 요소 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/gcServer"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#gcServer"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<gcServer> 요소"
  - "gcServer 요소"
ms.assetid: 8d25b80e-2581-4803-bd87-a59528e3cb03
caps.latest.revision: 17
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 17
---
# &lt;gcServer&gt; 요소
공용 언어 런타임이 서버 가비지 수집을 실행하는지 여부를 지정합니다.  
  
## 구문  
  
```  
<gcServer    
   enabled="true|false"/>  
```  
  
## 특성 및 요소  
 다음 단원에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### 특성  
  
|특성|설명|  
|--------|--------|  
|`enabled`|필수 특성입니다.<br /><br /> 런타임이 서버 가비지 수집을 실행하는지 여부를 지정합니다.|  
  
## enabled 특성  
  
|값|설명|  
|-------|--------|  
|`false`|서버 가비지 수집을 실행하지 않습니다.  이 값이 기본값입니다.|  
|`true`|서버 가비지 수집을 실행합니다.|  
  
### 자식 요소  
 없음  
  
### 부모 요소  
  
|요소|설명|  
|--------|--------|  
|`configuration`|공용 언어 런타임 및 .NET Framework 응용 프로그램에서 사용하는 모든 구성 파일의 루트 요소입니다.|  
|`runtime`|어셈블리 바인딩 및 가비지 수집에 대한 정보를 포함합니다.|  
  
## 설명  
 CLR\(공용 언어 런타임\)에서는 두 가지 유형의 가비지 수집을 지원합니다. 워크스테이션 가비지 수집은 모든 시스템에서 사용할 수 있고, 서버 가비지 수집은 다중 프로세서 시스템에서 사용할 수 있습니다.  `<gcServer>` 요소를 사용하여 CLR에서 수행하는 가비지 수집 유형을 제어합니다.  <xref:System.Runtime.GCSettings.IsServerGC%2A?displayProperty=fullName> 속성을 사용하여 서버 가비지 수집이 사용하도록 설정되었는지 확인합니다.  
  
 단일 프로세서 컴퓨터의 경우 기본 워크스테이션 가비지 수집이 가장 빠른 옵션입니다.  두 개의 프로세서가 있는 컴퓨터에는 워크스테이션 또는 서버를 사용할 수 있습니다.  세 개 이상 프로세서의 경우 서버 가비지 수집이 가장 빠른 옵션입니다.  
  
 이 요소는 응용 프로그램 구성 파일에만 사용할 수 있습니다. 컴퓨터 구성 파일에 있는 경우 무시됩니다.  
  
> [!NOTE]
>  .NET Framework 4 및 이전 버전에서, 서버 가비지 수집이 사용되는 경우에는 동시 가비지 수집을 사용할 수 없습니다.  [!INCLUDE[net_v45](../../../../../includes/net-v45-md.md)]부터 서버 가비지 수집이 동시에 이루어집니다.  비동시 가비지 수집을 사용하려면 `<gcServer>` 요소를 `true`로 설정하고, [\<gcConcurrent\> 요소](../../../../../docs/framework/configure-apps/file-schema/runtime/gcconcurrent-element.md)를 `false`로 설정합니다.  
  
## 예제  
 다음 예제에서는 서버 가비지 수집을 사용하도록 설정합니다.  
  
```  
  
<configuration>  
   <runtime>  
      <gcServer enabled="true"/>  
   </runtime>  
</configuration>  
  
```  
  
## 참고 항목  
 <xref:System.Runtime.GCSettings.IsServerGC%2A?displayProperty=fullName>   
 [런타임 설정 스키마](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [구성 파일 스키마](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [How to: Disable Concurrent Garbage Collection](http://msdn.microsoft.com/ko-kr/ba2c6c67-5778-497c-9fac-5f793b5500c7)