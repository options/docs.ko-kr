---
title: "채널 팩터리 및 캐싱 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 954f030e-091c-4c0e-a7a2-10f9a6b1f529
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 채널 팩터리 및 캐싱
WCF 클라이언트 응용 프로그램은 <xref:System.ServiceModel.ChannelFactory%601> 클래스를 사용하여 WCF 서비스와 통신 채널을 만듭니다.<xref:System.ServiceModel.ChannelFactory%601> 인스턴스를 만들면 다음 작업이 필요하기 때문에 약간의 오버헤드가 발생합니다.  
  
-   <xref:System.ServiceModel.Description.ContractDescription> 트리 생성  
  
-   필요한 모든 CLR 형식 반영  
  
-   채널 스택 생성  
  
-   리소스 해제  
  
 이 오버헤드를 최소화하기 위해 사용자가 WCF 클라이언트 프록시를 사용할 때 WCF가 채널 팩터리를 캐싱할 수 있습니다.  
  
> [!TIP]
>  <xref:System.ServiceModel.ChannelFactory%601> 클래스를 직접 사용하면 채널 팩터리 생성을 직접 제어할 수 있습니다.  
  
 [ServiceModel Metadata 유틸리티 도구\(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)을 사용하여 생성된 WCF 클라이언트 프록시는 <xref:System.ServiceModel.ClientBase%601>에서 파생됩니다.<xref:System.ServiceModel.ClientBase%601>는 채널 팩터리 캐싱 동작을 정의하는 정적 <xref:System.ServiceModel.ClientBase%601.CacheSetting%2A> 속성을 정의합니다.캐시 설정은 특정 형식에 대해 지정합니다.예를 들어 `ClientBase<ITest>.CacheSettings`를 아래 정의된 값 중 하나로 설정하면 형식이 `ITest`인 프록시\/ClientBase에만 영향을 미칩니다.특정 <xref:System.ServiceModel.ClientBase%601>에 대한 캐시 설정은 첫 번째 프록시\/ClientBase 인스턴스가 만들어지는 즉시 변경할 수 없게 됩니다.  
  
## 캐싱 동작 지정  
 캐싱 동작은 <xref:System.ServiceModel.ClientBase%601.CacheSetting> 속성을 다음 값 중 하나로 설정하여 지정할 수 있습니다.  
  
|캐시 설정 값|설명|  
|-------------|--------|  
|<xref:System.ServiceModel.CacheSetting.AlwaysOn>|응용 프로그램 도메인 안의 모든 <xref:System.ServiceModel.ClientBase%601> 인스턴스가 캐싱에 참여할 수 있습니다.개발자는 캐싱에 대해 보안 상의 문제가 없는 것으로 판단했습니다.<xref:System.ServiceModel.ClientBase%601>에서 "보안과 관련된" 속성을 액세스하더라도 캐싱은 해제되지 않습니다."보안과 관련된" <xref:System.ServiceModel.ClientBase%601> 속성은 <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A>, <xref:System.ServiceModel.ClientBase%601.Endpoint%2A> 및 <xref:System.ServiceModel.ClientBase%601.ChannelFactory%2A>입니다.|  
|<xref:System.ServiceModel.CacheSetting.Default>|구성 파일에 정의된 끝점에서 만든 <xref:System.ServiceModel.ClientBase%601> 인스턴스만 응용 프로그램 도메인 안의 캐싱에 참여할 수 있습니다.해당 응용 프로그램 도메인에서 프로그래밍 방식으로 생성된 모든 <xref:System.ServiceModel.ClientBase%601> 인스턴스는 캐싱에 참여하지 않습니다.또한, "보안과 관련된" 임의의 속성을 액세스하면 <xref:System.ServiceModel.ClientBase%601> 인스턴스에 대한 캐싱이 비활성화됩니다.|  
|<xref:System.ServiceModel.CacheSetting.AlwaysOff>|해당 응용 프로그램 도메인 안에서 특정 형식의 <xref:System.ServiceModel.ClientBase%601>의 모든 인스턴스에 대한 캐싱이 해제됩니다.|  
  
 다음 코드 조각에서는 <xref:System.ServiceModel.ClientBase%601.CacheSetting%2A> 속성을 사용하는 방법을 보여 줍니다.  
  
```  
class Program   
{   
   static void Main(string[] args)   
   {   
      ClientBase<ITest>.CacheSettings = CacheSettings.AlwaysOn;   
      foreach (string msg in messages)   
      {   
         using (TestClient proxy = new TestClient (new BasicHttpBinding(), new EndpointAddress(address)))   
         {   
            // ...  
            proxy.Test(msg);   
            // ...  
         }   
      }   
   }   
}  
// Generated by SvcUtil.exe     
public partial class TestClient : System.ServiceModel.ClientBase, ITest { }  
  
```  
  
 위 코드에서 `TestClient`의 모든 인스턴스는 같은 채널 팩터리를 사용합니다.  
  
```  
class Program   
{   
   static void Main(string[] args)   
   {   
      ClientBase.CacheSettings = CacheSettings.Default;   
      int i = 1;   
      foreach (string msg in messages)   
      {   
         using (TestClient proxy = new TestClient (“MyEndpoint”, new EndpointAddress(address)))   
         {   
            if (i == 4)   
            {   
               ServiceEndpoint endpoint = proxy.Endpoint;   
               ... // use endpoint in some way   
            }   
            proxy.Test(msg);   
         }   
         i++;   
   }   
}   
  
// Generated by SvcUtil.exe     
public partial class TestClient : System.ServiceModel.ClientBase, ITest {}  
```  
  
 위 예제에서 `TestClient`의 모든 인스턴스는 \#4 인스턴스를 제외하고 같은 채널 팩터리를 사용합니다.인스턴스 \#4는 전용으로 특수하게 만들어진 채널 팩터리를 사용합니다.이 설정은 특정 끝점이 같은 채널 팩터리 형식\(이 경우 `ITest`\)의 다른 끝점과 다른 보안 설정이 필요한 시나리오에 적용됩니다.  
  
```  
class Program   
{   
   static void Main(string[] args)   
   {   
      ClientBase.CacheSettings = CacheSettings.AlwaysOff;   
      foreach (string msg in messages)   
      {   
         using (TestClient proxy = new TestClient (“MyEndpoint”, new EndpointAddress(address)))   
         {   
            proxy.Test(msg);   
         }           
      }   
   }  
}  
  
// Generated by SvcUtil.exe   
public partial class TestClient : System.ServiceModel.ClientBase, ITest {}  
```  
  
 위 예제에서 `TestClient`의 모든 인스턴스는 다른 채널 팩터리를 사용합니다.이는 각 끝점이 다른 보안 요구사항을 가지고 있고 캐싱하는 의미가 없을 때 유용합니다.  
  
## 참고 항목  
 <xref:System.ServiceModel.ClientBase%601>   
 [클라이언트 빌드](../../../../docs/framework/wcf/building-clients.md)   
 [클라이언트](../../../../docs/framework/wcf/feature-details/clients.md)   
 [WCF 클라이언트를 사용하여 서비스 액세스](../../../../docs/framework/wcf/accessing-services-using-a-wcf-client.md)   
 [방법: ChannelFactory 사용](../../../../docs/framework/wcf/feature-details/how-to-use-the-channelfactory.md)