---
title: "System.ServiceModel.MessageClosedAgain | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 24c274d4-65cd-4c91-9869-bc6eb34ef979
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# System.ServiceModel.MessageClosedAgain
System.ServiceModel.MessageClosedAgain  
  
## 설명  
 메시지가 다시 닫혔습니다.  
  
 메시지는 한 번만 닫혀야 합니다.사용자 확장 코드에서 이 추적을 내보낸다는 것은 사용자 확장 코드가 이미 닫힌 메시지를 닫고 있음을 나타냅니다.제품 코드를 통해 이 추적을 내보낸다는 것은 사용자 확장 코드가 메시지를 너무 일찍 닫을 가능성이 있다는 것을 나타냅니다.  
  
## 참고 항목  
 [추적](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [추적을 사용하여 응용 프로그램 문제 해결](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)   
 [관리 및 진단](../../../../../docs/framework/wcf/diagnostics/index.md)