---
title: "보안 확장 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "보안 [WCF], 확장"
ms.assetid: a015a040-9fdf-4147-9ea9-f83b570be1d4
caps.latest.revision: 23
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 23
---
# 보안 확장
새 클레임 형식 및 사용자 지정 토큰을 적용하기 위해 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]의 보안 인프라를 확장할 수 있습니다.이 단원의 각 항목에서는 이를 수행하는 방법을 보여 줍니다.  
  
## 단원 내용  
 [Security Architecture](http://msdn.microsoft.com/ko-kr/16593476-d36a-408d-808c-ae6fd483e28f)  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 보안 시스템의 아키텍처에 대해 설명합니다.  
  
 [사용자 지정 자격 증명 및 자격 증명 유효성 검사](../../../../docs/framework/wcf/extending/custom-credential-and-credential-validation.md)  
 사용자 지정 자격 증명의 유효성을 검사할 때 ID 모델을 사용하는 방법에 대해 설명합니다.  
  
 [사용자 지정 토큰](../../../../docs/framework/wcf/extending/custom-tokens.md)  
 일반적으로 STS\(보안 토큰 서비스\)에서 발행된 토큰은 SAML 토큰입니다.이 항목에서는 사용자 지정 토큰 형식에 대해 설명합니다.  
  
 [사용자 지정 권한 부여](../../../../docs/framework/wcf/extending/custom-authorization.md)  
 사용자 지정 인증을 구현하는 방법에 대해 설명합니다.  
  
 [인증을 위해 서비스 ID 재정의](../../../../docs/framework/wcf/extending/overriding-the-identity-of-a-service-for-authentication.md)  
 인증을 위해 서비스의 ID를 재지정하는 방법에 대해 설명합니다.  
  
 [방법: 사용자 지정 클라이언트 ID 검증 도구 만들기](../../../../docs/framework/wcf/extending/how-to-create-a-custom-client-identity-verifier.md)  
 사용자 지정 끝점 ID의 유효성을 검사하는 방법을 보여 줍니다.  
  
 [방법: 서명 및 암호화에 별도의 X.509 인증서 사용](../../../../docs/framework/wcf/extending/how-to-use-separate-x-509-certificates-for-signing-and-encryption.md)  
 일반적으로 메시지는 단일 인증서를 사용하여 서명되고 암호화됩니다.이 항목에서는 필요한 경우 두 가지 인증서를 사용하는 방법에 대해 설명합니다.  
  
 [방법: X.509 인증서의 개인 키에 대한 암호화 공급자 변경](../../../../docs/framework/wcf/extending/change-cryptographic-provider-x509-certificate-private-key.md)  
 X.509 인증서의 개인 키를 제공하는 데 사용되는 암호화 공급자를 변경하는 방법 및 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 프레임워크에 공급자를 통합하는 방법에 대해 설명합니다.  
  
## 참조  
 <xref:System.ServiceModel.ServiceAuthorizationManager>  
  
 <xref:System.ServiceModel.Security>  
  
 <xref:System.IdentityModel.Claims>  
  
 <xref:System.IdentityModel.Policy>  
  
 <xref:System.IdentityModel.Tokens>  
  
 <xref:System.IdentityModel.Selectors>  
  
## 관련 단원  
 [보안](../../../../docs/framework/wcf/feature-details/security.md)  
  
 [기본 WCF 프로그래밍](../../../../docs/framework/wcf/basic-wcf-programming.md)  
  
## 참고 항목  
 [보안 개요](../../../../docs/framework/wcf/feature-details/security-overview.md)