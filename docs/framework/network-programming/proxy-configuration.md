---
title: "프록시 구성 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "적응 프록시"
  - "인터넷, 프록시 구성"
  - "네트워크 리소스"
  - "네트워크, 프록시 구성"
  - "네트워킹"
  - "프록시"
  - "프록시, 구성"
  - "정적 프록시"
ms.assetid: 353c0a8b-4cee-44f6-8e65-60e286743df9
caps.latest.revision: 14
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 14
---
# 프록시 구성
프록시 서버는 리소스에 대한 클라이언트 요청을 처리합니다.  프록시는 해당 캐시에서 요청한 리소스를 반환하거나 리소스가 있는 서버로 요청을 전달할 수 있으며,  원격 서버로 전송되는 요청 수를 줄여 네트워크 성능을 개선할 수 있습니다.  프록시를 사용하여 리소스에 대한 액세스를 제한할 수도 있습니다.  
  
## 적응 프록시  
 .NET Framework에서 프록시는 적응 및 정적의 두 가지 형식으로 제공됩니다.  적응 프록시는 네트워크 구성이 변경되면 설정을 조정합니다.  예를 들어 랩톱 사용자가 전화 접속 네트워크 연결을 시작하면 적응 프록시가 해당 변경을 인식하여 새 구성 스크립트를 검색 및 실행하고 설정을 적절하게 조정합니다.  
  
 구성 스크립트를 통해 적응 프록시를 구성합니다\([자동 프록시 검색](../../../docs/framework/network-programming/automatic-proxy-detection.md) 참조\).  스크립트는 응용 프로그램 프로토콜 집합과 각 프로토콜용 프록시를 생성합니다.  
  
 구성 스크립트 실행 방식은 여러 옵션으로 제어됩니다.  다음을 지정할 수 있습니다.  
  
-   구성 스크립트 다운로드 및 실행 빈도  
  
-   스크립트가 다운로드를 대기할 시간  
  
-   시스템에서 프록시에 액세스하는 데 사용해야 하는 자격 증명  
  
-   시스템에서 구성 스크립트를 다운로드하는 데 사용해야 하는 자격 증명  
  
 네트워크 환경이 변경되는 경우에는 시스템에서 새 프록시 집합을 사용해야 할 수 있습니다.  네트워크 연결이 다운되거나 새 네트워크 연결이 초기화되면 시스템은 새 환경에서 적절한 구성 스크립트 소스를 찾아 새 스크립트를 실행해야 합니다.  
  
 다음 테이블에는 적응 프록시의 구성 옵션이 나와 있습니다.  
  
|특성, 속성 또는 구성 파일 설정|설명|  
|------------------------|--------|  
|`scriptDownloadInterval`|스크립트 다운로드 간에 경과된 시간\(초\)입니다.|  
|`scriptDownloadTimeout`|스크립트 다운로드를 대기할 시간\(초\)입니다.|  
|`useDefaultCredentials` 또는 <xref:System.Net.WebProxy.UseDefaultCredentials>|시스템이 기본 네트워크 자격 증명을 사용하여 프록시에 액세스하는지 여부를 제어합니다.|  
|`useDefaultCredentialForScriptDownload`|시스템이 기본 네트워크 자격 증명을 사용하여 구성 스크립트를 다운로드하는지 여부를 제어합니다.|  
|`usesystemdefaults`|정적 프록시 설정\(프록시 주소, 바이패스 목록, 로컬에서 바이패스\)을 사용자의 Internet Explorer 프록시 설정에서 읽어야 하는지 여부를 제어합니다.  이 값을 "true"로 설정하면 Internet Explorer의 정적 프록시 설정을 사용합니다.<br /><br /> 이 값을 "false"로 설정하거나 설정하지 않으면 구성에서 정적 프록시 설정을 지정할 수 있으며 Internet Explorer 프록시 설정은 재정의됩니다.  적응 프록시를 사용하도록 설정하려는 경우에도 이 값을 "false"로 설정하거나 설정하지 않아야 합니다.|  
  
 다음 예제에서는 일반적인 적응 프록시 구성을 보여 줍니다.  
  
```  
<system.net>  
    <defaultProxy>  
      <proxy  scriptDownloadInterval="600"  
              scriptDownloadTimeout="30"  
              useDefaultCredentials="true"  
              usesystemdefaults="true"  
      />  
    </defaultProxy>  
</system.net>  
```  
  
## 정적 프록시  
 정적 프록시는 보통 응용 프로그램에 의해 명시적으로 구성되거나 응용 프로그램 또는 시스템에서 구성 파일을 호출할 때 구성됩니다.  정적 프록시는 회사 네트워크에 연결된 데스크톱 컴퓨터와 같이 토폴로지가 자주 변경되지 않는 네트워크에서 유용합니다.  
  
 정적 프록시 작동 방식은 여러 옵션으로 제어됩니다.  다음을 지정할 수 있습니다.  
  
-   프록시의 주소  
  
-   로컬 주소에 대해 프록시를 바이패스해야 하는지 여부  
  
-   주소 집합에 대해 프록시를 바이패스해야 하는지 여부  
  
 다음 테이블에는 정적 프록시의 구성 옵션이 나와 있습니다.  
  
|특성, 속성 또는 구성 파일 설정|설명|  
|------------------------|--------|  
|`proxyaddress` 또는 <xref:System.Net.WebProxy.Address>|사용할 프록시의 주소입니다.|  
|`bypassonlocal` 또는 <xref:System.Net.WebProxy.BypassProxyOnLocal>|로컬 주소에 대해 프록시를 바이패스하는지 여부를 제어합니다.|  
|`bypasslist` 또는 <xref:System.Net.WebProxy.BypassArrayList>|정규식을 사용하여 프록시를 바이패스하는 주소 집합을 설명합니다.|  
|`usesystemdefaults`|정적 프록시 설정\(프록시 주소, 바이패스 목록, 로컬에서 바이패스\)을 사용자의 Internet Explorer 프록시 설정에서 읽어야 하는지 여부를 제어합니다.  이 값을 "true"로 설정하면 Internet Explorer의 정적 프록시 설정을 사용합니다.  .NET Framework 2.0에서는 이 값을 "true"로 설정하면 Internet Explorer 프록시 설정이 구성 파일의 다른 프록시 설정으로 재정의되지 않습니다.  .NET Framework 1.1에서는 구성 파일의 다른 프록시 설정으로 Internet Explorer 프록시 설정을 재정의할 수 있습니다.<br /><br /> 이 값을 "false"로 설정하거나 설정하지 않으면 구성에서 정적 프록시 설정을 지정할 수 있으며 Internet Explorer 프록시 설정은 재정의됩니다.  적응 프록시를 사용하도록 설정하려는 경우에도 이 값을 "false"로 설정하거나 설정하지 않아야 합니다.|  
  
 다음 예제에서는 일반적인 정적 프록시 구성을 보여 줍니다.  
  
```  
<system.net>  
    <defaultProxy>  
        <proxy  proxyaddress="http://proxy.contoso.com:3128"  
                bypassonlocal="true"  
        />  
        <bypasslist>  
            <add address="[a-z]+.blueyonderairlines.com$" />  
        </bypasslist>  
    </defaultProxy>  
</system.net>  
```  
  
## 참고 항목  
 <xref:System.Net.WebProxy>   
 <xref:System.Net.GlobalProxySelection>   
 [자동 프록시 검색](../../../docs/framework/network-programming/automatic-proxy-detection.md)