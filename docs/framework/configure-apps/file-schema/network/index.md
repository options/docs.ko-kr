---
title: "네트워크 설정 스키마 | Microsoft Docs"
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
  - "구성 설정[.NET Framework], 네트워크"
  - "연결[.NET Framework], 네트워크 구성 요소"
  - "요소[.NET Framework], 네트워크 구성 요소"
  - "인터넷, 네트워크 구성 요소"
  - "네트워크 구성 요소"
  - "네트워크 리소스, 네트워크 구성 요소"
  - "네트워크 설정"
  - "데이터 받기, 네트워크 구성 요소"
  - "데이터 보내기, 네트워크 구성 요소"
ms.assetid: f1de5a0f-76c5-4833-819f-5222b8146340
caps.latest.revision: 14
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 14
---
# 네트워크 설정 스키마
네트워크 설정은 .NET Framework의 인터넷 연결 방법을 지정하는 방법을 지정합니다.  다음 표에서는 [\<system.Net\> 요소\(네트워크 설정\)](../../../../../docs/framework/configure-apps/file-schema/network/system-net-element-network-settings.md)에서 각 하위 구성 요소의 기능에 대해 설명합니다.  
  
|요소|설명|  
|--------|--------|  
|[\<authenticationModules\> 요소\(네트워크 설정\)](../../../../../docs/framework/configure-apps/file-schema/network/authenticationmodules-element-network-settings.md)|인터넷 요청을 인증하는 데 사용되는 모듈을 지정합니다.|  
|[\<connectionManagement\> 요소\(네트워크 설정\)](../../../../../docs/framework/configure-apps/file-schema/network/connectionmanagement-element-network-settings.md)|인터넷 호스트에 대한 최대 연결 수를 지정합니다.|  
|[\<defaultProxy\> 요소\(네트워크 설정\)](../../../../../docs/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings.md)|인터넷에서 HTTP 요청에 사용되는 프록시 서버를 지정합니다.|  
|[\<mailSettings\> 요소\(네트워크 설정\)](../../../../../docs/framework/configure-apps/file-schema/network/mailsettings-element-network-settings.md)|메일 보내기 옵션 설정을 포함합니다.|  
|[\<requestCaching\> 요소\(네트워크 설정\)](../../../../../docs/framework/configure-apps/file-schema/network/requestcaching-element-network-settings.md)|인터넷 호스트에서 정보를 요청하는 데 사용되는 모듈을 지정합니다.|  
|[\<requestCaching\> 요소\(네트워크 설정\)](../../../../../docs/framework/configure-apps/file-schema/network/requestcaching-element-network-settings.md)|<xref:System.Net?displayProperty=fullName> 네임스페이스에 대한 기본 네트워크 옵션을 구성합니다.|  
|[\<webRequestModules\> 요소\(네트워크 설정\)](../../../../../docs/framework/configure-apps/file-schema/network/webrequestmodules-element-network-settings.md)|인터넷 호스트에서 정보를 요청하는 데 사용되는 모듈을 지정합니다.|  
  
 Uri 설정은 uniform resource identifiers \(URIs\)를 사용하여 표현된 웹 주소를 .NET Framework에서 처리하는 방법을 지정합니다.  다음 표에서는 [\<Uri\> 요소\(Uri 설정\)](../../../../../docs/framework/configure-apps/file-schema/network/uri-element-uri-settings.md)에서 각 하위 구성 요소의 기능에 대해 설명합니다.  
  
|요소|설명|  
|--------|--------|  
|[\<idn\> 요소\(Uri 설정\)](../../../../../docs/framework/configure-apps/file-schema/network/idn-element-uri-settings.md)|IDN\(Internationalized Domain Name\) 구문 분석이 도메인 이름에 적용되는 경우 지정합니다.|  
|[\<iriParsing\> 요소\(Uri 설정\)](../../../../../docs/framework/configure-apps/file-schema/network/iriparsing-element-uri-settings.md)|IDN\(Internationalized Domain Name\) 구문 분석이 <xref:System.Uri>에 적용되는 경우 IRI 구문 분석 규칙이 적용되어야 하는지 여부를 지정합니다.|  
|[\<schemeSettings\> 요소\(URI 설정\)](../../../../../docs/framework/configure-apps/file-schema/network/schemesettings-element-uri-settings.md)|특정 스키마에 대해 <xref:System.Uri>가 구문 분석되는 방식을 지정합니다.|  
  
## 참고 항목  
 [인터넷 응용 프로그램 구성](../../../../../docs/framework/network-programming/configuring-internet-applications.md)   
 [구성 파일 스키마](../../../../../docs/framework/configure-apps/file-schema/index.md)