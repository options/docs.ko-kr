---
title: "&lt;basicHttpBinding&gt;의 &lt;transport&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4c5ba293-3d7e-47a6-b84e-e9022857b7e5
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 18
---
# &lt;basicHttpBinding&gt;의 &lt;transport&gt;
HTTP 전송의 인증 매개 변수를 제어하는 속성을 정의합니다.  
  
## 구문  
  
```  
<basicHttpBinding>  
    <binding>  
        <security  
        mode="None|Transport|Message|TransportWithMessageCredential|TransportCredentialOnly">  
            <transport clientCredentialType="None|Basic|Digest|Ntlm|Windows"  
             proxyCredentialType="None|Basic|Digest|Ntlm|Windows" realm="string" >  
                <extendedProtectionPolicy  
                     policyEnforcement="Never|WhenSupported|Always"  
                     protectionScenario="TransportSelected|TrustedProxy">  
                    <customServiceNames></customServiceNames>  
                        </extendedProtectionPolicy>  
            </transport>  
        </security>  
    </binding>  
</basicHttpBinding>  
```  
  
## 특성 및 요소  
 다음 단원에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### 특성  
  
|특성|설명|  
|--------|--------|  
|clientCredentialType|-   HTTP 인증을 사용하여 클라이언트 인증을 수행할 때 사용할 자격 증명의 형식을 지정합니다.  기본값은 `None`입니다.  이 특성은 <xref:System.ServiceModel.HttpClientCredentialType> 형식입니다.|  
|proxyCredentialType|-   HTTP를 통한 프록시를 사용하여 도메인 내에서 클라이언트 인증을 수행할 때 사용되는 자격 증명의 형식을 지정합니다.  이 특성은 부모 `security` 요소의 `mode` 특성이 `Transport` 또는 `TransportCredentialsOnly`일 때만 적용할 수 있습니다.  이 특성은 <xref:System.ServiceModel.HttpProxyCredentialType> 형식입니다.|  
|realm|다이제스트 또는 기본 인증의 HTTP 인증 체계에 사용되는 영역을 지정하는 문자열입니다.  기본값은 빈 문자열입니다.|  
|policyEnforcement|이 열거형은 <xref:System.Security.Authentication.ExtendedProtectionPolicy>가 적용되는 경우를 지정합니다.<br /><br /> 1.  Never \- 정책이 적용되지 않습니다\(확장 보호가 사용되지 않음\).<br />2.  WhenSupported – 클라이언트에서 확장 보호를 지원하는 경우에만 정책이 적용됩니다.<br />3.  Always – 정책이 항상 적용됩니다.  확장 보호를 지원하지 않는 클라이언트는 인증되지 않습니다.|  
|protectionScenario|이 열거형은 정책을 통해 적용되는 보호 시나리오를 지정합니다.|  
  
## clientCredentialType 특성  
  
|값|설명|  
|-------|--------|  
|없음|메시지가 전송 중에 보호되지 않습니다.|  
|Basic|기본 인증을 지정합니다.|  
|Digest|다이제스트 인증을 지정합니다.|  
|Ntlm|Windows 인증이 실패할 경우 가능하면 NTLM 인증을 지정합니다.|  
|Windows|Windows 통합 인증을 지정합니다.|  
  
## proxyCredentialType 특성  
  
|값|설명|  
|-------|--------|  
|없음|-   메시지가 전송 중에 보호되지 않습니다.|  
|Basic|RFC 2617 – HTTP 인증: 기본 및 다이제스트 인증에 정의된 대로 기본 인증을 지정합니다.|  
|Digest|RFC 2617 – HTTP 인증: 기본 및 다이제스트 인증에 정의된 대로 다이제스트 인증을 지정합니다.|  
|Ntlm|Windows 인증이 실패할 경우 가능하면 NTLM 인증을 지정합니다.|  
|Windows|Windows 통합 인증을 지정합니다.|  
|인증서|인증서를 사용하여 클라이언트 인증을 수행합니다.  이 옵션은 부모 `security` 요소의 `Mode` 특성이 Transport로 설정되어 있을 때만 작동하며 TransportCredentialOnly로 설정된 경우에는 작동하지 않습니다.|  
  
### 자식 요소  
 없음  
  
### 부모 요소  
  
|요소|설명|  
|--------|--------|  
|[\<security\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-basichttpbinding.md)|[\<basicHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md)의 보안 기능을 정의합니다.|  
  
## 예제  
 다음 예제에서는 기본 바인딩이 있는 SSL 전송 보안을 사용하는 방법을 보여 줍니다.  기본적으로 기본 바인딩은 HTTP 통신을 지원합니다.  
  
```  
<system.serviceModel>  
   <services>  
      <service   
          type="Microsoft.ServiceModel.Samples.CalculatorService"  
          behaviorConfiguration="CalculatorServiceBehavior">  
         <endpoint address=""  
               binding="basicHttpBinding"  
               bindingConfiguration="Binding1"   
               contract="Microsoft.ServiceModel.Samples.ICalculator" />  
      </service>  
   </services>  
    <bindings>  
        <basicHttpBinding>  
        <!-- Configure basicHttpBinding with Transport security -- >  
        <!-- mode and clientCredentialType set to None.-->  
           <binding name="Binding1">  
               <security mode="Transport">  
                   <transport clientCredentialType="None"  
                              proxyCredentialType="None">  
                       <extendedProtectionPolicy  
                          policyEnforcement="WhenSupported"  
                          protectionScenario="TransportSelected">  
                    <customServiceNames></customServiceNames>  
                       </extendedProtectionPolicy>  
               </security>  
           </binding>  
        </basicHttpBinding>  
    </bindings>  
</system.serviceModel>  
```  
  
## 참고 항목  
 <xref:System.ServiceModel.Configuration.BasicHttpSecurityElement.Transport%2A>   
 <xref:System.ServiceModel.BasicHttpSecurity.Transport%2A>   
 <xref:System.ServiceModel.Configuration.HttpTransportSecurityElement>   
 <xref:System.ServiceModel.HttpTransportSecurity>   
 [서비스 및 클라이언트에 보안 설정](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [바인딩](../../../../../docs/framework/wcf/bindings.md)   
 [시스템 제공 바인딩 구성](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/ko-kr/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<binding\>](../../../../../docs/framework/misc/binding.md)