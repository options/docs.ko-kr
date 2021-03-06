---
title: "방법: 디지털 서명을 암호화하지 않도록 설정 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fd174313-ad81-4dca-898a-016ccaff8187
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 방법: 디지털 서명을 암호화하지 않도록 설정
기본적으로 메시지는 서명되며 서명은 디지털 방식으로 암호화됩니다.  이 작업은 <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement> 또는 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>의 인스턴스가 포함된 사용자 지정 바인딩을 만든 다음, 해당 클래스의 `MessageProtectionOrder` 속성을 <xref:System.ServiceModel.Security.MessageProtectionOrder> 열거형 값으로 설정하여 제어합니다.  기본값은 <xref:System.ServiceModel.Security.MessageProtectionOrder>입니다.  이 프로세스에서는 전체 메시지 크기를 기반으로 서명하고 암호화하는 경우보다 최대 30%의 시간이 더 소요됩니다. 메시지가 작을수록 성능에 미치는 영향이 더 큽니다.  하지만 서명 암호화를 사용하지 않으면 공격자가 메시지 내용을 추측할 수 있습니다.  서명 요소에는 메시지의 서명된 모든 부분에 대한 일반 텍스트의 해시 코드가 들어 있기 때문입니다.  예를 들어, 메시지 본문이 기본적으로 암호화되어 있더라도 암호화되어 있지 않은 서명에는 암호화 이전의 메시지 본문에 대한 해시 코드가 포함되어 있습니다.  서명 및 암호화된 부품에 사용 가능한 값이 작은 경우 공격자는 해시 값을 조사하여 내용을 추론할 수 있습니다.  서명을 암호화하면 이러한 공격 벡터를 완화할 수 있습니다.  
  
 따라서 내용 값이 작거나 가능한 내용 값이 크고 불명확하지만 위에서 설명한 공격을 줄이는 것보다 성능 향상이 더 중요한 경우에만 서명 암호화를 비활성화하세요.  
  
> [!NOTE]
>  메시지에 암호화된 내용이 없는 경우에는 <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement.MessageProtectionOrder%2A?displayProperty=fullName> 또는 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement.MessageProtectionOrder%2A?displayProperty=fullName> 속성이 <xref:System.ServiceModel.Security.MessageProtectionOrder>로 설정되어 있더라도 서명 요소가 암호화되지 않습니다.  이 동작은 시스템 제공 바인딩에서도 발생합니다. 모든 시스템 제공 바인딩에서는 메시지 보호 순서가 `SignBeforeEncryptAndEncryptSignature`로 설정되어 있습니다.  그러나 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서 생성되는 WSDL\(웹 서비스 기술 언어\)은 `<sp:EncryptSignature>` 어설션을 계속해서 포함합니다.  
  
### 디지털 서명을 사용하지 않도록 설정하려면  
  
1.  <xref:System.ServiceModel.Channels.CustomBinding>를 만듭니다.  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [방법: SecurityBindingElement를 사용하여 사용자 지정 바인딩 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md).  
  
2.  <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement> 또는 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>를 바인딩 컬렉션에 추가합니다.  
  
3.  <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement.MessageProtectionOrder%2A?displayProperty=fullName> 속성을 <xref:System.ServiceModel.Security.MessageProtectionOrder>로 설정하거나 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement.MessageProtectionOrder%2A?displayProperty=fullName> 속성을 <xref:System.ServiceModel.Security.MessageProtectionOrder>로 설정합니다.  
  
## 참고 항목  
 [사용자 지정 바인딩을 사용하는 보안 기능](../../../../docs/framework/wcf/feature-details/security-capabilities-with-custom-bindings.md)