---
title: "AspNetRouteIntegration | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0638ce0e-d053-47df-a447-688e447a03fb
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# AspNetRouteIntegration
이 샘플에서는 ASP.NET 경로를 사용하여 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] REST 서비스를 호스팅하는 방법을 보여 줍니다.[기본 리소스 서비스](../../../../docs/framework/wcf/samples/basic-resource-service.md) 샘플에서는 이 시나리오의 자체 호스팅 버전을 보여 주고 서비스 구현에 대해 자세히 설명합니다.이 항목에서는 ASP.NET 통합 기능을 중점적으로 설명합니다.ASP.NET 라우팅[!INCLUDE[crabout](../../../../includes/crabout-md.md)]<xref:System.Web.Routing>을 참조하십시오.  
  
## 샘플 세부 정보  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 서비스는 리소스 지향\/REST 방식으로 고객 컬렉션을 노출합니다.SOAP 기반 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 서비스와 마찬가지로 이 서비스는 .svc 파일을 사용하여 ASP.NET에서 호스팅할 수 있습니다.그러나 서비스에 대한 URL에 .svc를 포함해야 하므로 HTTP 시나리오의 경우에는 이 서비스가 적절하지 않을 수도 있습니다.또한 .svc 파일을 서비스 라이브러리와 함께 배포해야 합니다.이 샘플에서와 같이 ASP.NET 경로를 사용하여 서비스를 호스팅하면 이러한 제한을 피할 수 있습니다.  
  
 이 샘플에서는 Global.asax 파일에 <xref:System.ServiceModel.Activation.ServiceRoute>를 추가하여 ASP.NET에서 서비스를 호스팅합니다.<xref:System.ServiceModel.Activation.ServiceRoute>는 서비스 유형\(이 경우 ‘Service’\), 서비스에 사용할 서비스 호스트 팩터리의 유형\(이 경우 <xref:System.ServiceModel.Activation.WebServiceHostFactory>\) 및 서비스의 HTTP 기본 주소\(이 경우 ‘~\/Customers’\)를 지정합니다.  
  
 또한 이 샘플에는 <xref:System.Web.Routing.UrlRoutingModule>을 추가하여 ASP.NET 경로를 설정하는 Web.config와 서비스에 대한 구성이 포함되어 있습니다.특히 이 구성에서는 <xref:System.ServiceModel.Description.WebHttpEndpoint.HelpEnabled%2A>가 `true`로 설정된 기본 <xref:System.ServiceModel.Description.WebHttpEndpoint>로 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 서비스를 구성합니다.따라서 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 인프라에서는 `http://localhost/Customers/help`에 자동 HTML 기반 도움말 페이지를 만듭니다. 이 페이지에서는 서비스에 대한 HTTP 요청을 생성하고 서비스의 HTTP 응답에 액세스하는 방법에 대한 정보가 제공됩니다. 예를 들어 고객 세부 정보를 XML 또는 JSON으로 표현하는 방법에 대한 예제가 제공됩니다.  
  
 이러한 방식으로 고객 컬렉션\(보다 일반적으로는 모든 리소스\)을 노출하면 클라이언트가 URI와 HTTP `GET`, `PUT`, `DELETE` 및 `POST`를 사용하여 일관된 방식으로 서비스와 상호 작용할 수 있습니다.  
  
 Client 프로젝트의 Program.cs에서는 <xref:System.Net.HttpWebRequest>를 사용하여 이러한 클라이언트를 작성하는 방법을 보여 줍니다.이 방법은 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 서비스에 액세스하는 여러 방법 중 하나일 뿐입니다.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 채널 팩터리 및 <xref:System.Net.WebClient>와 같은 다른 .NET Framework 클래스를 사용하여 서비스에 액세스할 수도 있습니다.[기본 HTTP 서비스](../../../../docs/framework/wcf/samples/basic-http-service.md) 샘플 및 [자동 포맷 선택](../../../../docs/framework/wcf/samples/automatic-format-selection.md) 샘플과 같은 SDK의 다른 샘플에서는 이러한 클래스를 사용하여 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 서비스와 통신하는 방법을 보여 줍니다.  
  
 이 샘플은 다음의 세 프로젝트로 구성되어 있습니다.  
  
 Service  
 ASP.NET에서 호스팅되는 WCF HTTP 서비스가 포함된 웹 응용 프로그램 프로젝트입니다.  
  
 Client  
 서비스를 호출하는 콘솔 응용 프로그램 프로젝트입니다.  
  
 Common  
 클라이언트 및 서비스에서 사용되는 `Customer` 형식이 포함된 공유 라이브러리입니다.클라이언트 콘솔 응용 프로그램이 실행되면 클라이언트에서는 서비스로 요청을 보내고 응답의 관련 정보를 콘솔 창에 씁니다.  
  
#### 이 샘플을 사용하려면  
  
1.  [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)]에서 ASP.NET Routes Integration 샘플의 솔루션을 엽니다.  
  
2.  Ctrl\+Shift\+B를 눌러 솔루션을 빌드합니다.  
  
3.  **솔루션 탐색기** 창이 아직 열려 있지 않은 경우 "Ctrl\+W, S"를 눌러 엽니다.  
  
4.  **솔루션 탐색기** 창에서 **Service** 프로젝트를 마우스 오른쪽 단추로 클릭하고 커서를 상황에 맞는 메뉴의 **디버그** 옵션 위에 놓아 **새 인스턴스 시작** 상황에 맞는 메뉴가 표시되면 **새 인스턴스 시작**을 선택합니다.그러면 ASP.NET Development Server가 시작되어 서비스를 호스팅합니다.  
  
5.  **솔루션 탐색기** 창에서 **Client** 프로젝트를 마우스 오른쪽 단추로 클릭하고 커서를 상황에 맞는 메뉴의 **디버그** 옵션 위에 놓아 **새 인스턴스 시작** 상황에 맞는 메뉴가 표시되면 **새 인스턴스 시작**을 선택합니다.  
  
6.  클라이언트 콘솔 창이 나타나고 실행 중인 서비스의 URI와 실행 중인 서비스에 대한 HTML 도움말 페이지의 URI가 제공됩니다.언제든지 브라우저에서 HTML 도움말 페이지의 URI를 입력하면 해당 도움말 페이지를 볼 수 있습니다.샘플이 실행되면 클라이언트에서는 현재 활동의 상태를 씁니다.  
  
7.  아무 키나 눌러 클라이언트 콘솔 응용 프로그램을 종료합니다.  
  
8.  Shift\+F5를 눌러 서비스 디버깅을 중지하고 Windows 알림 영역에서 ASP.NET Development Server 아이콘을 마우스 오른쪽 단추로 클릭한 다음 상황에 맞는 메뉴에서 **중지**를 선택합니다.  
  
> [!IMPORTANT]
>  컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다.계속하기 전에 다음\(기본\) 디렉터리를 확인하십시오.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  이 디렉터리가 없으면 [Windows Communication Foundation \(WCF\) and Windows Workflow Foundation \(WF\) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780)로 이동하여 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 모두 다운로드하십시오.이 샘플은 다음 디렉터리에 있습니다.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Web\AspNetRouteIntegration`  
  
## 참고 항목