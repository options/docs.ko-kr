---
title: "WCF 서비스에서 REST 스타일 서비스 호출 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 77df81d8-7f53-4daf-8d2d-bf7996e94d5a
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# WCF 서비스에서 REST 스타일 서비스 호출
일반\(SOAP 기반\) WCF 서비스에서 REST 스타일의 서비스를 호출할 때 서비스 메서드의 작업 컨텍스트\(들어오는 요청에 대한 정보 포함\)가 나가는 요청에 사용되는 컨텍스트를 재정의합니다.  따라서 HTTP GET 요청이 HTTP POST 요청으로 변경됩니다.  WCF 서비스가 REST 스타일 서비스를 호출하는 데 올바른 컨텍스트를 사용하도록 적용하려면 새 <xref:System.ServiceModel.OperationContextScope>를 만들고 작업 컨텍스트 범위 내에서 REST 스타일 서비스를 호출합니다.  이 항목에서는 이러한 기술을 설명하는 간단한 예제를 만드는 방법에 대해 설명합니다.  
  
## REST 스타일 서비스 계약 정의  
 간단한 REST 스타일 서비스 계약 정의:  
  
```  
[ServiceContract]  
        public interface IRestInterface  
        {  
            [OperationContract, WebGet]  
            int Add(int x, int y);  
            [OperationContract, WebGet]  
            string Echo(string input);  
        }  
```  
  
## REST 스타일 서비스 계약 구현  
 REST 스타일 서비스 계약 구현:  
  
```  
public class RestService : IRestInterface  
        {  
            public int Add(int x, int y)  
            {  
                return x + y;  
            }  
  
            public string Echo(string input)  
            {  
                return input;  
            }  
        }  
  
```  
  
## WCF 서비스 계약 정의  
 REST 스타일 서비스를 호출하는 데 사용되는 WCF 서비스 계약 정의:  
  
```  
[ServiceContract]  
 public interface INormalInterface  
 {  
     [OperationContract]  
     int CallAdd(int x, int y);  
     [OperationContract]  
     string CallEcho(string input);  
 }  
```  
  
## WCF 서비스 계약 구현  
 WCF 서비스 계약 구현:  
  
```  
public class NormalService : INormalInterface  
        {  
            static MyRestClient client = new MyRestClient(RestServiceBaseAddress);  
            public int CallAdd(int x, int y)  
            {  
                return client.Add(x, y);  
            }  
  
            public string CallEcho(string input)  
            {  
                return client.Echo(input);  
            }  
        }  
```  
  
## REST 스타일 서비스에 대한 클라이언트 프록시 만들기  
 <xref:System.ServiceModel.ClientBase%60>를 사용하여 클라이언트 프록시를 구현합니다.  호출되는 각 메서드에 대해 새로운 <xref:System.ServiceModel.OperationContextScope>가 생성되고 작업 호출에 사용됩니다.  
  
```  
public class MyRestClient : ClientBase<IRestInterface>, IRestInterface  
        {  
            public MyRestClient(string address)  
                : base(new WebHttpBinding(), new EndpointAddress(address))  
            {  
                this.Endpoint.Behaviors.Add(new WebHttpBehavior());  
            }  
  
            public int Add(int x, int y)  
            {  
                using (new OperationContextScope(this.InnerChannel))  
                {  
                    return base.Channel.Add(x, y);  
                }  
            }  
  
            public string Echo(string input)  
            {  
                using (new OperationContextScope(this.InnerChannel))  
                {  
                    return base.Channel.Echo(input);  
                }  
            }  
        }  
```  
  
## 서비스 호스트 및 호출  
 필요한 끝점 및 동작을 추가하여 콘솔 응용 프로그램에서 두 서비스를 모두 호스트합니다.  그런 후 일반 WCF 서비스를 호출합니다.  
  
```  
public static void Main()  
        {  
            ServiceHost restHost = new ServiceHost(typeof(RestService), new Uri(RestServiceBaseAddress));  
            restHost.AddServiceEndpoint(typeof(IRestInterface), new WebHttpBinding(), "").Behaviors.Add(new WebHttpBehavior());  
            restHost.Open();  
  
            ServiceHost normalHost = new ServiceHost(typeof(NormalService), new Uri(NormalServiceBaseAddress));  
            normalHost.AddServiceEndpoint(typeof(INormalInterface), new BasicHttpBinding(), "");  
            normalHost.Open();  
  
            Console.WriteLine("Hosts opened");  
  
            ChannelFactory<INormalInterface> factory = new ChannelFactory<INormalInterface>(new BasicHttpBinding(), new EndpointAddress(NormalServiceBaseAddress));  
            INormalInterface proxy = factory.CreateChannel();  
  
            Console.WriteLine(proxy.CallAdd(123, 456));  
            Console.WriteLine(proxy.CallEcho("Hello world"));  
        }  
```  
  
## 전체 코드 목록  
 다음은 이 항목에서 구현된 예제의 전체 목록입니다.  
  
```  
public class CallingRESTSample  
    {  
        static readonly string RestServiceBaseAddress = "http://" + Environment.MachineName + ":8008/Service";  
        static readonly string NormalServiceBaseAddress = "http://" + Environment.MachineName + ":8000/Service";  
  
        [ServiceContract]  
        public interface IRestInterface  
        {  
            [OperationContract, WebGet]  
            int Add(int x, int y);  
            [OperationContract, WebGet]  
            string Echo(string input);  
        }  
  
        [ServiceContract]  
        public interface INormalInterface  
        {  
            [OperationContract]  
            int CallAdd(int x, int y);  
            [OperationContract]  
            string CallEcho(string input);  
        }  
  
        public class RestService : IRestInterface  
        {  
            public int Add(int x, int y)  
            {  
                return x + y;  
            }  
  
            public string Echo(string input)  
            {  
                return input;  
            }  
        }  
  
        public class MyRestClient : ClientBase<IRestInterface>, IRestInterface  
        {  
            public MyRestClient(string address)  
                : base(new WebHttpBinding(), new EndpointAddress(address))  
            {  
                this.Endpoint.Behaviors.Add(new WebHttpBehavior());  
            }  
  
            public int Add(int x, int y)  
            {  
                using (new OperationContextScope(this.InnerChannel))  
                {  
                    return base.Channel.Add(x, y);  
                }  
            }  
  
            public string Echo(string input)  
            {  
                using (new OperationContextScope(this.InnerChannel))  
                {  
                    return base.Channel.Echo(input);  
                }  
            }  
        }  
  
        public class NormalService : INormalInterface  
        {  
            static MyRestClient client = new MyRestClient(RestServiceBaseAddress);  
            public int CallAdd(int x, int y)  
            {  
                return client.Add(x, y);  
            }  
  
            public string CallEcho(string input)  
            {  
                return client.Echo(input);  
            }  
        }  
        public static void Main()  
        {  
            ServiceHost restHost = new ServiceHost(typeof(RestService), new Uri(RestServiceBaseAddress));  
            restHost.AddServiceEndpoint(typeof(IRestInterface), new WebHttpBinding(), "").Behaviors.Add(new WebHttpBehavior());  
            restHost.Open();  
  
            ServiceHost normalHost = new ServiceHost(typeof(NormalService), new Uri(NormalServiceBaseAddress));  
            normalHost.AddServiceEndpoint(typeof(INormalInterface), new BasicHttpBinding(), "");  
            normalHost.Open();  
  
            Console.WriteLine("Hosts opened");  
  
            ChannelFactory<INormalInterface> factory = new ChannelFactory<INormalInterface>(new BasicHttpBinding(), new EndpointAddress(NormalServiceBaseAddress));  
            INormalInterface proxy = factory.CreateChannel();  
  
            Console.WriteLine(proxy.CallAdd(123, 456));  
            Console.WriteLine(proxy.CallEcho("Hello world"));  
        }  
    }  
```  
  
## 참고 항목  
 [방법: 기본 WCF 웹 HTTP 서비스 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-basic-wcf-web-http-service.md)   
 [WCF 웹 HTTP 프로그래밍 개체 모델](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-object-model.md)