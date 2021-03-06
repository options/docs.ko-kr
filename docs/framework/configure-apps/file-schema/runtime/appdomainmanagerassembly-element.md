---
title: "&lt;appDomainManagerAssembly&gt; 요소 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<appDomainManagerAssembly> 요소"
  - "appDomainManagerAssembly 요소"
ms.assetid: c7c56e39-a700-44f5-b94e-411bfce339d9
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# &lt;appDomainManagerAssembly&gt; 요소
프로세스의 기본 응용 프로그램 도메인에 대한 응용 프로그램 도메인 관리자를 제공하는 어셈블리를 지정합니다.  
  
## 구문  
  
```  
<appDomainManagerAssembly   
   value="assembly display name" />  
```  
  
## 특성 및 요소  
 다음 단원에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### 특성  
  
|특성|설명|  
|--------|--------|  
|`value`|필수 특성입니다.  프로세스의 기본 응용 프로그램 도메인에 대한 응용 프로그램 도메인 관리자를 제공하는 어셈블리의 표시 이름을 지정합니다.|  
  
### 자식 요소  
 없음  
  
### 부모 요소  
  
|요소|설명|  
|--------|--------|  
|`configuration`|공용 언어 런타임 및 .NET Framework 응용 프로그램에서 사용하는 모든 구성 파일의 루트 요소입니다.|  
|`runtime`|어셈블리 바인딩 및 가비지 수집에 대한 정보를 포함합니다.|  
  
## 설명  
 응용 프로그램 도메인 관리자의 형식을 지정하려면 이 요소와 [\<appDomainManagerType\>](../../../../../docs/framework/configure-apps/file-schema/runtime/appdomainmanagertype-element.md)요소를 모두 지정해야 합니다.  이러한 요소 중 하나를 지정하지 않으면 다른 한 요소가 무시됩니다.  
  
 기본 응용 프로그램 도메인이 로드된 경우 지정된 어셈블리가 없거나 어셈블리에 [\<appDomainManagerType\>](../../../../../docs/framework/configure-apps/file-schema/runtime/appdomainmanagertype-element.md) 요소로 지정한 형식이 포함되어 있지 않으면 <xref:System.TypeLoadException>이 throw되고 프로세스를 시작하지 못합니다.  어셈블리가 있지만 버전 정보가 일치하지 않으면 <xref:System.IO.FileLoadException>이 throw됩니다.  
  
 기본 응용 프로그램 도메인의 응용 프로그램 도메인 관리자를 지정하면 기본 응용 프로그램 도메인에서 만든 다른 응용 프로그램 도메인은 이 응용 프로그램 도메인 관리자 형식을 상속합니다.  새 응용 프로그램 도메인에 다른 응용 프로그램 도메인 관리자를 지정하려면 <xref:System.AppDomainSetup.AppDomainManagerType%2A?displayProperty=fullName> 및 <xref:System.AppDomainSetup.AppDomainManagerAssembly%2A?displayProperty=fullName> 속성을 사용합니다.  
  
 응용 프로그램 도메인 관리자 형식을 지정하려면 응용 프로그램이 완전히 신뢰되어야 합니다. 예를 들어, 데스크톱에서 실행되는 응용 프로그램은 완전히 신뢰된 응용 프로그램입니다. 응용 프로그램이 완전히 신뢰된 응용 프로그램이 아니면 <xref:System.TypeLoadException>이 throw됩니다.  
  
 어셈블리 표시 이름의 형식은 <xref:System.Reflection.Assembly.FullName%2A?displayProperty=fullName> 속성을 참조하십시오.  
  
 이 구성 요소는 [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)] 이상에서만 사용할 수 있습니다.  
  
## 예제  
 다음 예제에서는 프로세스의 기본 응용 프로그램 도메인에 대한 응용 프로그램 도메인 관리자가 `AdMgrExample` 어셈블리의 `MyMgr` 형식이 되도록 지정하는 방법을 보여 줍니다.  
  
```  
<configuration>  
   <runtime>  
      <appDomainManagerType value="MyMgr" />  
      <appDomainManagerAssembly   
         value="AdMgrExample, Version=1.0.0.0, Culture=neutral, PublicKeyToken=6856bccf150f00b3" />  
   </runtime>  
</configuration>  
```  
  
## 참고 항목  
 <xref:System.AppDomainSetup.AppDomainManagerType%2A?displayProperty=fullName>   
 <xref:System.AppDomainSetup.AppDomainManagerAssembly%2A?displayProperty=fullName>   
 [\<appDomainManagerType\> 요소](../../../../../docs/framework/configure-apps/file-schema/runtime/appdomainmanagertype-element.md)   
 [런타임 설정 스키마](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [구성 파일 스키마](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [SetAppDomainManagerType 메서드](../Topic/ICLRControl::SetAppDomainManagerType%20Method.md)