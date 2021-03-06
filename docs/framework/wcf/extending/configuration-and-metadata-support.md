---
title: "구성 및 메타데이터 지원 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 27c240cb-8cab-472c-87f8-c864f4978758
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# 구성 및 메타데이터 지원
이 항목에서는 바인딩 및 바인딩 요소에 대한 구성 및 메타데이터 지원을 사용하도록 설정하는 방법에 대해 설명합니다.  
  
## 구성 및 메타데이터 개요  
 이 항목에서는 [채널 개발](../../../../docs/framework/wcf/extending/developing-channels.md) 작업 목록의 선택적 항목 1, 2,4에 해당하는 다음 작업에 대해 설명합니다.  
  
-   바인딩 요소에 대해 구성 파일 지원을 사용하도록 설정합니다.  
  
-   바인딩에 대해 구성 파일 지원을 사용하도록 설정합니다.  
  
-   바인딩 요소에 대해 WSDL 및 정책 어설션을 내보냅니다.  
  
-   바인딩 또는 바인딩 요소를 삽입하고 구성하기 위해 WSDL 및 정책 어설션을 식별합니다.  
  
 사용자 정의 바인딩 및 바인딩 요소 만들기에 대한 자세한 내용은 [사용자 정의 바인딩 만들기](../../../../docs/framework/wcf/extending/creating-user-defined-bindings.md) 및 [BindingElement 만들기](../../../../docs/framework/wcf/extending/creating-a-bindingelement.md)를 각각 참조하십시오.  
  
## 구성 지원 추가  
 채널에 대해 구성 파일 지원을 사용하도록 설정하려면 두 개의 구성 섹션, 즉, 바인딩 요소에 대해 구성 지원을 사용하도록 설정하는 <xref:System.ServiceModel.Configuration.BindingElementExtensionElement?displayProperty=fullName>와 바인딩에 대해 구성 지원을 사용하도록 설정하는 <xref:System.ServiceModel.Configuration.StandardBindingElement?displayProperty=fullName> 및 <xref:System.ServiceModel.Configuration.StandardBindingCollectionElement%602?displayProperty=fullName>를 구현해야 합니다.  
  
 이 작업을 더 쉽게 수행하려면 [ConfigurationCodeGenerator](../../../../docs/framework/wcf/samples/configurationcodegenerator.md) 샘플 도구를 사용하여 바인딩 및 바인딩 요소에 대해 구성 코드를 생성합니다.  
  
### BindingElementExtensionElement 확장  
 다음 예제 코드는 [전송: UDP](../../../../docs/framework/wcf/samples/transport-udp.md) 샘플에서 가져온 것입니다.`UdpTransportElement`는 구성 시스템에 `UdpTransportBindingElement`를 노출하는 <xref:System.ServiceModel.Configuration.BindingElementExtensionElement>입니다.샘플에서는 몇 가지 기본 재정의를 통해 구성 섹션 이름, 바인딩 요소의 형식 및 바인딩 요소를 만드는 방법을 정의합니다.그러면 사용자는 다음과 같이 구성 파일에서 확장 섹션을 등록할 수 있습니다.  
  
```  
<configuration>  
  <system.serviceModel>  
    <extensions>  
      <bindingElementExtensions>  
      <add name="udpTransport" type="Microsoft.ServiceModel.Samples.UdpTransportElement, UdpTransport />  
      </bindingElementExtensions>  
    </extensions>  
  </system.serviceModel>  
</configuration>  
  
```  
  
 사용자 지정 바인딩에서는 UDP를 전송으로 사용하기 위해 확장을 참조할 수 있습니다.  
  
```  
<configuration>  
  <system.serviceModel>  
    <bindings>  
      <customBinding>  
       <binding configurationName="UdpCustomBinding">  
         <udpTransport/>  
       </binding>  
      </customBinding>  
    </bindings>  
  </system.serviceModel>  
</configuration>  
  
```  
  
### 바인딩에 대해 구성 추가  
 `SampleProfileUdpBindingCollectionElement` 섹션은 구성 시스템에 `SampleProfileUdpBinding`을 노출하는 <xref:System.ServiceModel.Configuration.StandardBindingCollectionElement%602>입니다.대량의 구현은 <xref:System.ServiceModel.Configuration.StandardBindingElement>로부터 파생되는 `SampleProfileUdpBindingConfigurationElement`에 위임됩니다.`SampleProfileUdpBindingConfigurationElement`에는 `SampleProfileUdpBinding`의 속성에 해당하는 속성과 `ConfigurationElement` 바인딩에서 매핑하는 함수가 있습니다.마지막으로 `OnApplyConfiguration` 메서드는 다음 샘플 코드에서처럼 `SampleProfileUdpBinding`에서 재정의됩니다.  
  
```  
protected override void OnApplyConfiguration(string configurationName)  
{  
            if (binding == null)  
                throw new ArgumentNullException("binding");  
  
            if (binding.GetType() != typeof(SampleProfileUdpBinding))  
            {  
                throw new ArgumentException(string.Format(CultureInfo.CurrentCulture,  
                    "Invalid type for binding. Expected type: {0}. Type passed in: {1}.",  
                    typeof(SampleProfileUdpBinding).AssemblyQualifiedName,  
                    binding.GetType().AssemblyQualifiedName));  
            }  
            SampleProfileUdpBinding udpBinding = (SampleProfileUdpBinding)binding;  
  
            udpBinding.OrderedSession = this.OrderedSession;  
            udpBinding.ReliableSessionEnabled = this.ReliableSessionEnabled;  
            udpBinding.SessionInactivityTimeout = this.SessionInactivityTimeout;  
            if (this.ClientBaseAddress != null)  
                   udpBinding.ClientBaseAddress = ClientBaseAddress;  
}  
  
```  
  
 구성 시스템을 사용하여 이 처리기를 등록하려면 관련 구성 파일에 다음 섹션을 추가합니다.  
  
```  
<configuration>  
  <configSections>  
     <sectionGroup name="system.serviceModel">  
         <sectionGroup name="bindings">  
                 <section name="sampleProfileUdpBinding" type="Microsoft.ServiceModel.Samples.SampleProfileUdpBindingCollectionElement, UdpTransport />  
         </sectionGroup>  
     </sectionGroup>  
  </configSections>  
</configuration>  
```  
  
 이렇게 하면 [\<system.serviceModel\>](../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md) 구성 섹션에서 이 처리기를 참조할 수 있습니다.  
  
```  
<configuration>  
  <system.serviceModel>  
    <client>  
      <endpoint configurationName="calculator"  
                address="soap.udp://localhost:8001/"   
                bindingConfiguration="CalculatorServer"  
                binding="sampleProfileUdpBinding"   
                contract= "Microsoft.ServiceModel.Samples.ICalculatorContract">  
      </endpoint>  
    </client>  
  </system.serviceModel>  
</configuration>  
  
```  
  
## 바인딩 요소에 대해 메타데이터 지원 추가  
 채널을 메타데이터 시스템으로 통합하려면 채널이 정책 가져오기와 내보내기를 모두 지원해야 합니다.두 가지를 모두 지원하면 [ServiceModel Metadata 유틸리티 도구\(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 등의 도구를 사용하여 바인딩 요소의 클라이언트를 생성할 수 있습니다.  
  
### WSDL 지원 추가  
 바인딩의 전송 바인딩 요소는 메타데이터에서 주소 지정 정보를 내보내고 가져옵니다.또한 전송 바인딩 요소는 SOAP 바인딩을 사용할 때 메타데이터에서 올바른 전송 URI을 내보낼 수 있어야 합니다.다음 예제 코드는 [전송: UDP](../../../../docs/framework/wcf/samples/transport-udp.md) 샘플에서 가져온 것입니다.  
  
#### WSDL 내보내기  
 주소 지정 정보를 내보내기 위해 `UdpTransportBindingElement`는 <xref:System.ServiceModel.Description.IWsdlExportExtension?displayProperty=fullName>인터페이스를 구현합니다.<xref:System.ServiceModel.Description.IWsdlExportExtension.ExportEndpoint%2A?displayProperty=fullName>메서드는 WSDL 포트에 올바른 주소 지정 정보를 추가합니다.  
  
```  
if (context.WsdlPort != null)  
{  
    AddAddressToWsdlPort(context.WsdlPort, context.Endpoint.Address, encodingBindingElement.MessageVersion.Addressing);  
}  
```  
  
 끝점이 SOAP 바인딩을 사용할 때 <xref:System.ServiceModel.Description.IWsdlExportExtension.ExportEndpoint%2A> 메서드의 `UdpTransportBindingElement` 구현이 전송 URI도 내보냅니다.  
  
```  
WsdlNS.SoapBinding soapBinding = GetSoapBinding(context, exporter);  
if (soapBinding != null)  
{  
    soapBinding.Transport = UdpPolicyStrings.UdpNamespace;  
}  
```  
  
#### WSDL 가져오기  
 주소 가져오기를 처리하기 위해 WSDL 가져오기 시스템을 확장하려면 Svcutil.exe.config 파일에서처럼 Svcutil.exe에 대한 구성 파일에 다음 구성을 추가합니다.  
  
```  
<configuration>  
  <system.serviceModel>  
    <client>  
      <metadata>  
        <wsdlImporters>  
          <extension type=" Microsoft.ServiceModel.Samples.UdpBindingElementImporter, UdpTransport" />  
        </policyImporters>  
      </metadata>  
    </client>  
  </system.serviceModel>  
</configuration>  
```  
  
 Svcutil.exe를 실행하는 경우 Svcutil.exe에서 WSDL 가져오기 확장을 로드하는 방법은 두 가지가 있습니다.  
  
1.  \/SvcutilConfig:\<파일\>을 사용하여 Svcutil.exe를 구성 파일에 지정합니다.  
  
2.  Svcutil.exe와 동일한 디렉터리에 있는 Svcutil.exe.config에 구성 섹션을 추가합니다.  
  
 `UdpBindingElementImporter` 형식은 <xref:System.ServiceModel.Description.IWsdlImportExtension?displayProperty=fullName>인터페이스를 구현합니다.`ImportEndpoint` 메서드는 WSDL 포트로부터 주소를 가져옵니다.  
  
```  
BindingElementCollection bindingElements = context.Endpoint.Binding.CreateBindingElements();  
TransportBindingElement transportBindingElement = bindingElements.Find<TransportBindingElement>();  
if (transportBindingElement is UdpTransportBindingElement)  
{  
    ImportAddress(context);  
}  
```  
  
### 정책 지원 추가  
 사용자 지정 바인딩 요소는 서비스 끝점이 해당 바인딩 요소의 기능을 표현하도록 WSDL 바인딩에서 정책 어설션을 내보낼 수 있습니다.다음 예제 코드는 [전송: UDP](../../../../docs/framework/wcf/samples/transport-udp.md) 샘플에서 가져온 것입니다.  
  
#### 정책 내보내기  
 `UdpTransportBindingElement` 형식은``<xref:System.ServiceModel.Description.IPolicyExportExtension?displayProperty=fullName>을구현하여 정책 내보내기 지원을 추가합니다.그 결과, <xref:System.ServiceModel.Description.MetadataExporter?displayProperty=fullName>는 이를 포함하는 모든 바인딩에 대한 정책 생성에 `UdpTransportBindingElement`를 포함합니다.  
  
 <xref:System.ServiceModel.Description.IPolicyExportExtension.ExportPolicy%2A?displayProperty=fullName>에서는 채널이 멀티캐스트 모드인 경우 UDP용 어설션 및 다른 어설션을 추가합니다.이는 멀티캐스트 모드가 통신 스택의 구성 방법에 영향을 주므로 양쪽 모두에서 조정되어야 하기 때문입니다.  
  
```  
ICollection<XmlElement> bindingAssertions = context.GetBindingAssertions();  
XmlDocument xmlDocument = new XmlDocument();  
bindingAssertions.Add(xmlDocument.CreateElement(  
UdpPolicyStrings.Prefix, UdpPolicyStrings.TransportAssertion, UdpPolicyStrings.UdpNamespace));  
if (Multicast)  
{  
    bindingAssertions.Add(xmlDocument.CreateElement(  
UdpPolicyStrings.Prefix, UdpPolicyStrings.MulticastAssertion,     UdpPolicyStrings.UdpNamespace));  
}  
```  
  
 사용자 지정 전송 바인딩 요소가 주소 지정을 처리하기 때문에 `UdpTransportBindingElement`에서의 <xref:System.ServiceModel.Description.IPolicyExportExtension?displayProperty=fullName> 구현 역시 사용 중인 WS\-Addressing의 버전을 나타내기 위해 적절한 WS\-Addressing 정책 어설션 내보내기를 처리해야 합니다.  
  
```  
AddWSAddressingAssertion(context, encodingBindingElement.MessageVersion.Addressing);  
```  
  
#### 정책 가져오기  
 정책 가져오기 시스템을 확장하려면 Svcutil.exe.config 파일에서처럼 Svcutil.exe에 대한 구성 파일에 다음 구성을 추가합니다.  
  
```  
<configuration>  
  <system.serviceModel>  
    <client>  
      <metadata>  
        <policyImporters>  
          <extension type=" Microsoft.ServiceModel.Samples.UdpBindingElementImporter, UdpTransport" />  
        </policyImporters>  
      </metadata>  
    </client>  
  </system.serviceModel>  
</configuration>  
```  
  
 그런 다음 등록된 클래스\(`UdpBindingElementImporter`\)로부터 <xref:System.ServiceModel.Description.IPolicyImportExtension?displayProperty=fullName>을 구현합니다.<xref:System.ServiceModel.Description.IPolicyImportExtension.ImportPolicy%2A?displayProperty=fullName>에서는 적절한 네임스페이스에서 어설션을 검사하고, 어셜션 중 하나를 처리하여 전송을 생성하고 멀티캐스트인지 여부를 확인합니다.또한 가져오기가 바인딩 어설션 목록으로부터 처리하는 어설션을 제거합니다.다시 한 번 말하지만 Svcutil.exe를 실행할 때 통합하는 방법은 두 가지가 있습니다.  
  
1.  \/SvcutilConfig:\<파일\>을 사용하여 Svcutil.exe를 구성 파일에 지정합니다.  
  
2.  Svcutil.exe와 동일한 디렉터리에 있는 Svcutil.exe.config에 구성 섹션을 추가합니다.  
  
### 사용자 지정 표준 바인딩 가져오기 추가  
 기본적으로 Svcutil.exe 및 <xref:System.ServiceModel.Description.WsdlImporter?displayProperty=fullName> 형식은 시스템 제공 바인딩을 인식하고 가져옵니다.그렇지 않을 경우, 해당 바인딩을 <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=fullName> 인스턴스로 가져옵니다.Svcutil.exe 및 <xref:System.ServiceModel.Description.WsdlImporter>를 사용하도록 설정하여 `SampleProfileUdpBinding`을 가져오기 위해 `UdpBindingElementImporter`가 사용자 지정 표준 바인딩 가져오기도 수행합니다.  
  
 사용자 지정 표준 바인딩 가져오기는 <xref:System.ServiceModel.Description.IWsdlImportExtension?displayProperty=fullName> 인터페이스에서 `ImportEndpoint` 메서드를 구현하여 특정 표준 바인딩에 의해 생성되었는지 확인하기 위해 메타데이터로부터 가져온 <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=fullName>인스턴스를 검사합니다.  
  
```  
if (context.Endpoint.Binding is CustomBinding)  
{  
    Binding binding;  
    if (transportBindingElement is UdpTransportBindingElement)  
    {  
        //if TryCreate is true, the CustomBinding will be replace by a SampleProfileUdpBinding in the  
        //generated config file for better typed generation.  
        if (SampleProfileUdpBinding.TryCreate(bindingElements, out binding))  
        {  
            binding.Name = context.Endpoint.Binding.Name;  
            binding.Namespace = context.Endpoint.Binding.Namespace;  
            context.Endpoint.Binding = binding;  
        }  
    }  
}  
```  
  
 일반적으로 사용자 지정 표준 바인딩 가져오기를 구현하면 가져온 바인딩 요소의 속성을 확인하여 표준 바인딩에 의해 설정될 수 있는 속성만 변경되고, 다른 모든 속성은 기본값인지를 확인하는 작업이 포함됩니다.표준 바인딩 가져오기를 구현하기 위한 기본 전략은 표준 바인딩의 인스턴스를 만들고, 바인딩 요소의 속성을 표준 바인딩이 지원하는 표준 바인딩 인스턴스로 전파하고, 가져온 바인딩 요소를 표준 바인딩의 바인딩 요소와 비교하는 것입니다.