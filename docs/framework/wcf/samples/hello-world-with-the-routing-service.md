---
title: "Hello World 라우팅 서비스 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0f4b0d5b-6522-4ad5-9f3a-baa78316d7d1
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# Hello World 라우팅 서비스
이 샘플에서는 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 라우팅 서비스를 보여 줍니다.라우팅 서비스는 응용 프로그램에 내용 기반 라우터를 손쉽게 포함할 수 있게 해 주는 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 구성 요소입니다.이 샘플에서는 라우팅 서비스를 사용하여 통신하도록 표준 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] Calculator 샘플을 조정합니다.이 샘플에서 계산기 클라이언트는 라우터에 의해 노출된 끝점으로 메시지를 보내도록 구성되어 있습니다.라우팅 서비스는 전송된 모든 메시지를 승인하고 이를 계산기 서비스에 해당하는 끝점에 전달하도록 구성되어 있습니다.따라서 클라이언트에서 보내는 메시지는 라우터가 받아 실제 계산기 서비스로 다시 라우트합니다.계산기 서비스에서 보내는 메시지는 다시 라우터로 전송되고 라우터는 이를 다시 계산기 클라이언트에 전달합니다.  
  
### 이 샘플을 사용하려면  
  
1.  [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)]에서 HelloRoutingService.sln을 엽니다.  
  
2.  F5 또는 Ctrl\+Shift\+B를 누릅니다.  
  
    > [!NOTE]
    >  F5 키를 누르면 계산기 클라이언트가 자동으로 시작됩니다.Ctrl\+Shift\+B\(빌드\)를 누를 경우에는 다음 응용 프로그램을 직접 시작해야 합니다.  
    >   
    >  1.  계산기 클라이언트\(.\/CalculatorClient\/bin\/client.exe\)  
    > 2.  계산기 서비스\(.\/CalculatorService\/bin\/service.exe\)  
    > 3.  라우팅 서비스\(.\/RoutingService\/bin\/RoutingService.exe\)  
  
3.  Enter 키를 눌러 클라이언트를 시작합니다.  
  
     다음과 같은 내용이 출력됩니다.  
  
     Add\(100,15.99\) \= 115.99  
  
     Subtract\(145,76.54\) \= 68.46  
  
     Multiply\(9,81.25\) \= 731.25  
  
     Divide\(22,7\) \= 3.14285714285714  
  
## 코드 또는 App.Config를 통해 구성 가능  
 이 샘플은 App.config 파일을 사용하여 라우터 동작을 정의하도록 구성되어 있습니다.App.config 파일이 인식되지 않도록 이 파일의 이름을 다른 이름으로 바꾸고 ConfigureRouterViaCode\(\) 메서드 호출의 주석 처리를 제거할 수도 있습니다.어떤 방법을 사용하든 라우터 동작은 동일합니다.  
  
### 시나리오  
 이 샘플에서는 기본 메시지 펌프 역할을 하는 라우터를 보여 줍니다.라우팅 서비스는 미리 구성된 대상 끝점 집합에 직접 메시지를 전달하도록 구성된 투명 프록시 노드 역할을 합니다.  
  
### 실제 시나리오  
 Contoso에서는 서비스의 명명, 주소 지정, 구성 및 보안과 관련하여 유연성을 향상시키려고 합니다.이를 위해 Contoso에서는 공개 끝점 역할을 할 서비스 앞에 기본 메시지 펌프를 배치합니다.이렇게 하면 실제 서비스 앞에 추가 보안 기능을 배치할 수 있으며 나중에 확장된 솔루션이나 서비스 버전 관리를 보다 쉽게 구현할 수 있습니다.  
  
> [!IMPORTANT]
>  컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다.계속하기 전에 다음\(기본\) 디렉터리를 확인하십시오.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  이 디렉터리가 없으면 [Windows Communication Foundation \(WCF\) and Windows Workflow Foundation \(WF\) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780)로 이동하여 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 모두 다운로드하십시오.이 샘플은 다음 디렉터리에 있습니다.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\RoutingServices\HelloRoutingService`  
  
## 참고 항목  
 [AppFabric 호스팅 및 지속성 샘플](http://go.microsoft.com/fwlink/?LinkId=193961)