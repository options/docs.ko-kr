---
title: "메타데이터 아키텍처 개요 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "메타데이터 [WCF], 개요"
ms.assetid: 1d37645e-086d-4d68-a358-f3c5b6e8205e
caps.latest.revision: 24
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 24
---
# 메타데이터 아키텍처 개요
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]은 서비스 메타데이터의 내보내기, 게시, 검색 및 가져오기를 위한 풍부한 인프라를 제공합니다.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 서비스는 Svcutil.exe와 같은 도구가 서비스 액세스를 위해 클라이언트 코드에 자동으로 액세스할 수 있도록 메타데이터를 사용하여 서비스의 끝점과 상호 작용하는 방법을 설명합니다.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 메타데이터 인프라를 구성하는 대부분의 형식은 <xref:System.ServiceModel.Description> 네임스페이스에 있습니다.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]는 <xref:System.ServiceModel.Description.ServiceEndpoint> 클래스를 사용하여 서비스의 끝점을 설명합니다.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]를 사용하여 서비스 끝점에 대한 메타데이터를 생성하거나 서비스 메타데이터를 가져와서 <xref:System.ServiceModel.Description.ServiceEndpoint> 인스턴스를 생성할 수 있습니다.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]는 서비스에 대한 메타데이터를 <xref:System.ServiceModel.Description.MetadataSet> 형식의 인스턴스로 나타내는데, 이 형식의 구조체는 WS\-MetadataExchange에 정의된 메타데이터 serialization 형식에 강하게 연결되어 있습니다.<xref:System.ServiceModel.Description.MetadataSet> 형식은 WSDL\(웹 서비스 기술 언어\) 문서, XML 스키마 문서 또는 WS\-Policy 식과 같은 실제 서비스 메타데이터를 <xref:System.ServiceModel.Description.MetadataSection> 인스턴스의 컬렉션으로 묶습니다.<xref:System.ServiceModel.Description.MetadataSection?displayProperty=fullName> 인스턴스마다 특정 메타데이터 언어와 식별자가 포함되어 있습니다.<xref:System.ServiceModel.Description.MetadataSection?displayProperty=fullName>에는 해당 <xref:System.ServiceModel.Description.MetadataSection.Metadata%2A?displayProperty=fullName> 속성에 다음과 같은 항목이 포함될 수 있습니다.  
  
-   원시 메타데이터  
  
-   <xref:System.ServiceModel.Description.MetadataReference> 인스턴스  
  
-   <xref:System.ServiceModel.Description.MetadataLocation> 인스턴스  
  
 <xref:System.ServiceModel.Description.MetadataReference?displayProperty=fullName> 인스턴스는 다른 MEX\(메타데이터 교환\) 끝점을 가리키고 <xref:System.ServiceModel.Description.MetadataLocation?displayProperty=fullName> 인스턴스는 HTTP URL을 사용하여 메타데이터 문서를 가리킵니다.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 WSDL 문서를 사용하여 서비스에서 구현되는 서비스 끝점, 서비스 계약, 바인딩, 메시지 교환 패턴, 메시지 및 오류 메시지를 설명합니다.서비스에서 사용된 데이터 형식은 XML 스키마를 사용하여 WSDL 문서에 설명됩니다.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][스키마 가져오기 및 내보내기](../../../../docs/framework/wcf/feature-details/schema-import-and-export.md).[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]를 사용하여 서비스의 기능을 확장하는 서비스 동작, 계약 동작 및 바인딩 요소에 대한 WSDL 확장을 내보내고 가져올 수 있습니다.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][WCF 확장에 대한 사용자 지정 메타데이터 내보내기](../../../../docs/framework/wcf/extending/exporting-custom-metadata-for-a-wcf-extension.md).  
  
## 서비스 메타데이터 내보내기  
 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]에서 *메타데이터 내보내기*는 서비스 끝점을 설명하여 클라이언트에서 서비스 사용 방법을 이해할 수 있도록 병렬의 표준화된 표현으로 나타내는 프로세스입니다.<xref:System.ServiceModel.Description.ServiceEndpoint> 인스턴스에서 메타데이터를 내보내려면 <xref:System.ServiceModel.Description.MetadataExporter> 추상 클래스 구현을 사용합니다.<xref:System.ServiceModel.Description.MetadataExporter?displayProperty=fullName> 구현에서는 <xref:System.ServiceModel.Description.MetadataSet> 인스턴스에 캡슐화되는 메타데이터를 생성합니다.  
  
 <xref:System.ServiceModel.Description.MetadataExporter?displayProperty=fullName> 클래스는 끝점 바인딩의 기능 및 요구 사항과 관련 작업, 메시지 및 오류에 대해 설명하는 정책 식을 생성하는 데 필요한 프레임워크를 제공합니다.이러한 정책 식은 <xref:System.ServiceModel.Description.PolicyConversionContext> 인스턴스에 캡처됩니다.<xref:System.ServiceModel.Description.MetadataExporter?displayProperty=fullName> 구현에서는 생성되는 메타데이터에 이러한 정책 식을 연결할 수 있습니다.  
  
 <xref:System.ServiceModel.Description.MetadataExporter?displayProperty=fullName>는 사용할 <xref:System.ServiceModel.Description.MetadataExporter?displayProperty=fullName> 구현에 대한 <xref:System.ServiceModel.Description.PolicyConversionContext> 개체를 생성할 때 <xref:System.ServiceModel.Description.ServiceEndpoint>의 바인딩에서 <xref:System.ServiceModel.Description.IPolicyExportExtension> 인터페이스를 구현하는 각 <xref:System.ServiceModel.Channels.BindingElement?displayProperty=fullName>를 호출합니다.<xref:System.ServiceModel.Channels.BindingElement> 형식의 사용자 지정 구현에서 <xref:System.ServiceModel.Description.IPolicyExportExtension> 인터페이스를 구현하여 새 정책 어설션을 내보낼 수 있습니다.  
  
 <xref:System.ServiceModel.Description.WsdlExporter> 형식은 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에 포함된 <xref:System.ServiceModel.Description.MetadataExporter?displayProperty=fullName> 추상 클래스의 구현입니다.<xref:System.ServiceModel.Description.WsdlExporter> 형식은 연결된 정책 식을 사용하여 WSDL 메타데이터를 생성합니다.  
  
 서비스 끝점에서 끝점 동작, 계약 동작 또는 바인딩 요소에 대한 사용자 지정 WSDL 메타데이터 또는 WSDL 확장을 내보내려면 <xref:System.ServiceModel.Description.IWsdlExportExtension> 인터페이스를 구현합니다.<xref:System.ServiceModel.Description.WsdlExporter>는 WSDL 문서를 생성할 때 <xref:System.ServiceModel.Description.IWsdlExportExtension> 인터페이스를 구현하는 바인딩 요소, 작업 동작, 계약 동작 및 끝점 동작에 대한 <xref:System.ServiceModel.Description.ServiceEndpoint> 인스턴스를 조사합니다.  
  
## 서비스 메타데이터 게시  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 서비스는 하나 이상의 메타데이터 끝점을 노출하여 메타데이터를 게시합니다.서비스 메타데이터를 게시하면 MEX 및 HTTP\/GET 요청과 같이 표준화된 프로토콜을 통해 서비스 메타데이터를 사용할 수 있습니다.메타데이터 끝점은 주소, 바인딩 및 계약이 포함된 다른 서비스 끝점과 유사합니다.구성 또는 코드를 통해 서비스 호스트에 메타데이터 끝점을 추가할 수 있습니다.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 서비스의 메타데이터 끝점을 게시하려면 먼저 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 서비스 동작의 인스턴스를 해당 서비스에 추가해야 합니다.<xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=fullName> 인스턴스를 서비스에 추가하면 하나 이상의 메타데이터 끝점을 노출하여 메타데이터를 게시하는 기능으로 서비스가 보완됩니다.<xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=fullName> 서비스 동작을 추가하면 MEX 프로토콜을 지원하거나 HTTP\/GET 요청에 응답하는 메타데이터 끝점을 노출할 수 있습니다.  
  
 MEX 프로토콜을 사용하는 메타데이터 끝점을 추가하려면 IMetadataExchange라는 서비스 계약을 사용하는 서비스 호스트에 서비스 끝점을 추가합니다. [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]는 이 서비스 계약 이름을 갖는 <xref:System.ServiceModel.Description.IMetadataExchange> 인터페이스를 정의합니다.WS\-MetadataExchange 끝점 또는 MEX 끝점은 <xref:System.ServiceModel.Description.MetadataExchangeBindings> 클래스에서 정적 팩터리 메서드에 의해 노출되는 4개의 기본 바인딩 중 하나를 사용하여 Svcutil.exe와 같이 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 도구에서 사용하는 기본 바인딩과 일치시킬 수 있습니다.또한 사용자 지정 바인딩을 사용하여 MEX 메타데이터 끝점을 구성할 수도 있습니다.  
  
 <xref:System.ServiceModel.Description.ServiceMetadataBehavior>는 <xref:System.ServiceModel.Description.WsdlExporter?displayProperty=fullName>를 사용하여 서비스의 모든 서비스 끝점에 대한 메타데이터를 내보냅니다.서비스에서 메타데이터를 내보내는 방법에 대한 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]를 보려면 [메타데이터 내보내기 및 가져오기](../../../../docs/framework/wcf/feature-details/exporting-and-importing-metadata.md)를 참조하십시오.  
  
 <xref:System.ServiceModel.Description.ServiceMetadataBehavior>는 <xref:System.ServiceModel.Description.ServiceMetadataExtension> 인스턴스를 서비스 호스트에 대한 확장으로 추가하여 서비스 호스트를 보완합니다.<xref:System.ServiceModel.Description.ServiceMetadataExtension?displayProperty=fullName>은 메타데이터 게시 프로토콜에 대한 구현을 제공합니다.또한 <xref:System.ServiceModel.Description.ServiceMetadataExtension?displayProperty=fullName>을 통해 <xref:System.ServiceModel.Description.ServiceMetadataExtension.Metadata%2A> 속성에 액세스하여 서비스 메타데이터를 런타임에 가져올 수 있습니다.  
  
> [!CAUTION]
>  응용 프로그램 구성 파일에 MEX 끝점을 추가한 다음 코드에서 서비스 호스트에 <xref:System.ServiceModel.Description.ServiceMetadataBehavior>를 추가하려고 하면 다음과 같은 예외가 발생합니다.  
>   
>  System.InvalidOperationException: Service1 서비스에 의해 구현된 계약 목록에서 계약 이름 'IMetadataExchange'를 찾을 수 없습니다.ServiceMetadataBehavior를 구성 파일 또는 ServiceHost에 직접 추가하여 이 계약에 대한 지원을 활성화하십시오.  
>   
>  <xref:System.ServiceModel.Description.ServiceMetadataBehavior>를 구성 파일에 추가하거나 끝점과 <xref:System.ServiceModel.Description.ServiceMetadataBehavior>를 둘 다 코드에 추가하면 이 문제를 해결할 수 있습니다.  
>   
>  응용 프로그램 구성 파일에 <xref:System.ServiceModel.Description.ServiceMetadataBehavior>를 추가하는 방법에 대한 예를 보려면 [시작](../../../../docs/framework/wcf/samples/getting-started-sample.md)을 참조하십시오.코드에 <xref:System.ServiceModel.Description.ServiceMetadataBehavior>를 추가하는 방법에 대한 예를 보려면 [자체 호스팅](../../../../docs/framework/wcf/samples/self-host.md) 샘플을 참조하십시오.  
  
> [!CAUTION]
>  각각 같은 이름의 작업이 포함된 서로 다른 두 서비스 계약을 노출하는 서비스에 대해 메타데이터를 게시할 때는 예외가 throw됩니다.예를 들어 Get\(Car c\) 작업이 포함된 ICarService 서비스 계약을 노출하는 서비스가 Get\(Book b\) 작업이 포함된 IBookService 서비스 계약도 노출하는 경우에는 서비스 메타데이터를 생성할 때 예외가 throw되거나 오류 메시지가 표시됩니다.이 문제를 해결하려면 다음 중 하나를 수행합니다.  
>   
>  -   작업 중 하나의 이름을 바꿉니다.  
> -   <xref:System.ServiceModel.OperationContractAttribute.Name%2A>을 다른 이름으로 설정합니다.  
> -   <xref:System.ServiceModel.ServiceContractAttribute.Namespace%2A> 속성을 사용하여 작업 중 하나의 네임스페이스를 다른 네임스페이스로 설정합니다.  
  
## 서비스 메타데이터 검색  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 WS\-MetadataExchange 및 HTTP와 같은 표준화된 프로토콜을 통해 서비스 메타데이터를 검색할 수 있습니다.이러한 프로토콜은 모두 <xref:System.ServiceModel.Description.MetadataExchangeClient> 형식에서 지원합니다.주소 및 선택적 바인딩을 제공하여 <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=fullName> 형식을 사용한 서비스 메타데이터를 검색합니다.<xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=fullName> 인스턴스에서 사용되는 바인딩은 <xref:System.ServiceModel.Description.MetadataExchangeBindings> 정적 클래스의 기본 바인딩, 사용자 제공 바인딩 또는 `IMetadataExchange` 계약의 끝점 구성에서 로드된 바인딩 중 하나입니다.<xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=fullName>는 <xref:System.Net.HttpWebRequest> 형식을 통해 메타데이터에 대한 HTTP URL 참조를 확인할 수도 있습니다.  
  
 기본적으로 <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=fullName> 인스턴스는 하나의 <xref:System.ServiceModel.Channels.ChannelFactoryBase> 인스턴스에 연결됩니다.<xref:System.ServiceModel.Description.MetadataExchangeClient.GetChannelFactory%2A> 가상 메서드를 재정의하여 <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=fullName>에서 사용하는 <xref:System.ServiceModel.Channels.ChannelFactoryBase> 인스턴스를 변경하거나 바꿀 수 있습니다.마찬가지로 <xref:System.ServiceModel.Description.MetadataExchangeClient.GetWebRequest%2A?displayProperty=fullName> 가상 메서드를 재정의하여 HTTP\/GET 요청을 만들기 위해 <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=fullName>에서 사용하는 <xref:System.Net.HttpWebRequest?displayProperty=fullName> 인스턴스를 변경하거나 바꿀 수 있습니다.  
  
 Svcutil.exe 도구를 사용하고 **\/target:metadata** 스위치와 주소를 전달하여 WS\-MetadataExchange 또는 HTTP\/GET 요청을 통해 서비스 메타데이터를 검색할 수 있습니다.Svcutil.exe는 지정된 주소의 메타데이터를 다운로드하고 파일을 디스크에 저장합니다.Svcutil.exe는 <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=fullName> 인스턴스를 내부적으로 사용하고, Svcutil.exe가 있을 경우 Svcutil.exe에 전달된 주소 스키마와 이름이 같은 MEX 끝점 구성을 응용 프로그램 구성 파일에서 로드합니다.그렇지 않으면 Svcutil.exe는 기본적으로 <xref:System.ServiceModel.Description.MetadataExchangeBindings> 정적 팩터리 형식에 정의된 바인딩 중 하나를 사용합니다.  
  
## 서비스 메타데이터 가져오기  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서 메타데이터 가져오기는 해당 메타데이터에서 서비스 또는 해당 구성 요소 부분의 추상적 표현을 생성하는 프로세스입니다.예를 들면, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 <xref:System.ServiceModel.Description.ServiceEndpoint> 인스턴스, <xref:System.ServiceModel.Channels.Binding> 인스턴스 또는 <xref:System.ServiceModel.Description.ContractDescription> 인스턴스를 서비스의 WSDL 문서에서 가져올 수 있습니다.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서 서비스 메타데이터를 가져오려면 <xref:System.ServiceModel.Description.MetadataImporter> 추상 클래스의 구현을 사용합니다.<xref:System.ServiceModel.Description.MetadataImporter?displayProperty=fullName> 클래스에서 파생되는 형식은 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서 WS\-Policy 가져오기 논리를 사용하는 메타데이터 형식 가져오기에 대한 지원을 구현합니다.  
  
 <xref:System.ServiceModel.Description.MetadataImporter?displayProperty=fullName> 구현에서는 <xref:System.ServiceModel.Description.PolicyConversionContext> 개체의 서비스 메타데이터에 연결된 정책 식을 수집합니다.<xref:System.ServiceModel.Description.MetadataImporter?displayProperty=fullName>는 메타데이터를 가져올 때 <xref:System.ServiceModel.Description.MetadataImporter.PolicyImportExtensions%2A> 속성의 <xref:System.ServiceModel.Description.IPolicyImportExtension> 인터페이스 구현을 호출하여 정책을 처리합니다.  
  
 <xref:System.ServiceModel.Description.IPolicyImportExtension> 인터페이스의 사용자 지정 구현을 <xref:System.ServiceModel.Description.MetadataImporter?displayProperty=fullName> 인스턴스의 <xref:System.ServiceModel.Description.MetadataImporter.PolicyImportExtensions%2A> 컬렉션에 추가하여 <xref:System.ServiceModel.Description.MetadataImporter?displayProperty=fullName>로 새 정책 어설션 가져오기에 대한 지원을 추가할 수 있습니다.또는 클라이언트 응용 프로그램 구성 파일에 정책 가져오기 확장을 등록할 수 있습니다.  
  
 <xref:System.ServiceModel.Description.WsdlImporter?displayProperty=fullName> 형식은 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에 포함된 <xref:System.ServiceModel.Description.MetadataImporter?displayProperty=fullName> 추상 클래스의 구현입니다.<xref:System.ServiceModel.Description.WsdlImporter?displayProperty=fullName> 형식은 <xref:System.ServiceModel.Description.MetadataSet> 개체에 번들로 제공되는 연결된 정책과 함께 WSDL 메타데이터를 가져옵니다.  
  
 <xref:System.ServiceModel.Description.IWsdlImportExtension> 인터페이스를 구현한 다음 <xref:System.ServiceModel.Description.WsdlImporter?displayProperty=fullName> 인스턴스의 <xref:System.ServiceModel.Description.WsdlImporter.WsdlImportExtensions%2A> 속성에 이 구현을 추가하여 WSDL 확장 가져오기에 대한 지원을 추가할 수 있습니다.<xref:System.ServiceModel.Description.WsdlImporter?displayProperty=fullName>에서 클라이언트 응용 프로그램 구성 파일에 등록된 <xref:System.ServiceModel.Description.IWsdlImportExtension?displayProperty=fullName> 인터페이스의 구현을 로드할 수도 있습니다.  
  
## 동적 바인딩  
 끝점에 대한 바인딩이 변경된 경우 또는 같은 계약을 사용하지만 다른 바인딩이 있는 끝점에 대한 채널을 만들려는 경우 서비스 끝점에 대한 채널을 만드는 데 사용하는 바인딩을 동적으로 업데이트할 수 있습니다.<xref:System.ServiceModel.Description.MetadataResolver> 정적 클래스를 사용하여 특정 계약을 구현하는 서비스 끝점에 대한 메타데이터를 런타임에 검색하고 가져올 수 있습니다.그런 다음 가져온 <xref:System.ServiceModel.Description.ServiceEndpoint?displayProperty=fullName> 개체를 사용하여 원하는 끝점에 대한 클라이언트 또는 채널 팩터리를 만들 수 있습니다.  
  
## 참고 항목  
 <xref:System.ServiceModel.Description>   
 [메타데이터 형식](../../../../docs/framework/wcf/feature-details/metadata-formats.md)   
 [메타데이터 내보내기 및 가져오기](../../../../docs/framework/wcf/feature-details/exporting-and-importing-metadata.md)   
 [메타데이터 게시](../../../../docs/framework/wcf/feature-details/publishing-metadata.md)   
 [메타데이터 검색](../../../../docs/framework/wcf/feature-details/retrieving-metadata.md)   
 [메타데이터 사용](../../../../docs/framework/wcf/feature-details/using-metadata.md)   
 [메타데이터 관련 보안 고려 사항](../../../../docs/framework/wcf/feature-details/security-considerations-with-metadata.md)   
 [메타데이터 시스템 확장](../../../../docs/framework/wcf/extending/extending-the-metadata-system.md)