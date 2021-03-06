---
title: "방법: 클래스를 사용하여 Windows Communication Foundation 계약 만들기 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
ms.assetid: 1ad69393-3915-4e7f-9b91-b6fc59c6f5ba
caps.latest.revision: 17
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 17
---
# 방법: 클래스를 사용하여 Windows Communication Foundation 계약 만들기
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 계약을 만드는 기본 방법은 인터페이스를 사용하는 것입니다.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][방법: 서비스 계약 정의](../../../../docs/framework/wcf/how-to-define-a-wcf-service-contract.md).또는 다음에 요약한 대로 클래스를 만든 후 <xref:System.ServiceModel.ServiceContractAttribute> 특성을 직접 해당 클래스에 적용하고 <xref:System.ServiceModel.OperationContractAttribute> 특성을 계약의 일부인 클래스의 각 메서드에 적용합니다.  
  
> [!WARNING]
>  `[ServiceContract]` 및 `[ServiceContractAttribute]` 에 대해 동일한 작업을 수행합니다.같은 기준이 `[OperationContract]` 및 `[OperationContractAttribute]`에도 적용됩니다.각 경우 전자가 후자보다 빠릅니다.  
  
 서비스 계약[!INCLUDE[crabout](../../../../includes/crabout-md.md)][서비스 계약 디자인](../../../../docs/framework/wcf/designing-service-contracts.md)을 참조하십시오.  
  
### 클래스를 사용하여 Windows Communication Foundation 계약 만들기  
  
1.  [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)], C\# 또는 기타 공용 언어 런타임 언어를 사용하여 새 클래스를 만듭니다.  
  
2.  이 클래스에 <xref:System.ServiceModel.ServiceContractAttribute> 클래스를 적용합니다.  
  
3.  클래스에 메서드를 만듭니다.  
  
4.  공용 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 계약의 일부로서 노출해야 하는 각 메서드에 <xref:System.ServiceModel.OperationContractAttribute> 클래스를 적용합니다.  
  
## 예제  
 다음 코드 예제에서는 서비스 계약을 정의하는 클래스를 보여 줍니다.  
  
 [!code-csharp[c_HowTo_CreateContractWithClass#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_createcontractwithclass/cs/source.cs#1)]
 [!code-vb[c_HowTo_CreateContractWithClass#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_createcontractwithclass/vb/source.vb#1)]  
  
 <xref:System.ServiceModel.OperationContractAttribute> 클래스가 적용된 메서드는 기본적으로 요청\-회신 메시지 패턴을 사용합니다.이 메시지 패턴에 대한 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]는 [방법: 요청\-회신 계약 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-request-reply-contract.md)를 참조하십시오.특성의 속성을 설정하여 다른 메시지 패턴을 만들고 사용할 수도 있습니다.예제에 대해서는 [방법: 단방향 계약 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-one-way-contract.md) 및 [방법: 이중 계약 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-duplex-contract.md)를 참조하십시오.  
  
## 참고 항목  
 <xref:System.ServiceModel.ServiceContractAttribute>   
 <xref:System.ServiceModel.OperationContractAttribute>