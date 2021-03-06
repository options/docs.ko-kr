---
title: "&lt;ws2007HttpBinding&gt;의 &lt;transport&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 692befa3-8b0b-4ec5-b601-755874e98eb0
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# &lt;ws2007HttpBinding&gt;의 &lt;transport&gt;
HTTP 전송의 인증 설정을 정의합니다.  
  
## 구문  
  
```  
  
transport clientCredentialType =   
       "Basic/Certificate/Digest/None/Ntlm/Windows"  
       proxyCredentialType="Basic/Digest/None/Ntlm/Windows"  
       realm="string"   
```  
  
## 형식  
 <xref:System.ServiceModel.HttpTransportSecurity>  
  
## 특성 및 요소  
 다음 단원에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### 특성  
  
|특성|설명|  
|--------|--------|  
|`clientCredentialType`|클라이언트를 서비스에 인증할 때 사용되는 자격 증명을 지정합니다.  이 특성은 <xref:System.ServiceModel.HttpClientCredentialType> 형식입니다.|  
|`proxyCredentialType`|클라이언트를 도메인 프록시에 인증할 때 사용되는 자격 증명을 지정합니다.  이 특성은 <xref:System.ServiceModel.HttpProxyCredentialType> 형식입니다.|  
|`realm`|다이제스트 또는 기본 인증을 위한 인증 영역입니다.  기본값은 빈 문자열입니다.<br /><br /> 인증 영역은 최소한, 인증을 수행하는 호스트의 이름을 지정하며,  액세스 권한을 가진 사용자 컬렉션을 지정할 수도 있습니다.  사용자는 여러 개의 사용자 이름 및 암호 중에서 사용할 수 있는 하나를 알아내기 위해 인증 영역을 쿼리할 수 있습니다.|  
  
## clientCredentialType 특성  
  
|값|설명|  
|-------|--------|  
|없음|보안이 해제되어 있습니다.|  
|Basic|기본 인증을 사용합니다.|  
|Digest|다이제스트 인증을 사용합니다.|  
|Ntlm|Windows 도메인에 대한 대체\(fallback\)로 NTLM 인증을 사용합니다.|  
|Windows|Windows 통합 인증을 사용합니다.|  
|인증서|X.509 인증서를 사용하여 클라이언트를 인증합니다.|  
  
## proxyCredentialType 특성  
  
|값|설명|  
|-------|--------|  
|없음|보안이 해제되어 있습니다.|  
|Basic|기본 인증을 사용합니다.|  
|Digest|다이제스트 인증을 사용합니다.|  
|Ntlm|Windows 도메인에 대한 대체\(fallback\)로 NTLM을 사용합니다.|  
|Windows|Windows 통합 인증을 사용합니다.|  
|인증서|X.509 인증서를 사용하여 클라이언트를 인증합니다.|  
  
### 자식 요소  
 없음  
  
### 부모 요소  
  
|요소|설명|  
|--------|--------|  
|[\<security\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-ws2007httpbinding.md)|[\<ws2007HttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/ws2007httpbinding.md) 요소의 보안 기능을 나타냅니다.|  
  
## 참고 항목  
 <xref:System.ServiceModel.HttpTransportSecurity>   
 <xref:System.ServiceModel.Configuration.BasicHttpSecurityElement.Transport%2A>   
 <xref:System.ServiceModel.WSHttpSecurity.Transport%2A>   
 <xref:System.ServiceModel.Configuration.WSHttpTransportSecurityElement>   
 [서비스 및 클라이언트에 보안 설정](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [바인딩](../../../../../docs/framework/wcf/bindings.md)   
 [시스템 제공 바인딩 구성](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/ko-kr/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<binding\>](../../../../../docs/framework/misc/binding.md)