---
title: "Microsoft.Transactions.TransactionBridge.VolatileOutcomeTimeout | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2dbe34c5-57c7-4b64-9257-63021911d03c
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Microsoft.Transactions.TransactionBridge.VolatileOutcomeTimeout
일시 참가자의 결과 메시지에 대한 응답을 기다리는 동안 WS\-AT 프로토콜 서비스의 시간 제한이 초과되었습니다.참가자가 반환되면 트랜잭션 결과가 확실하지 않을 수 있습니다.  
  
## 설명  
 일시 참가자가 커밋 또는 중단으로 결정했지만 주어진 시간 내에 커밋 또는 롤백 요청에 대해 응답하지 않을 때 추적됩니다.  
  
## 문제 해결  
 주어진 시간 내에 모든 일시 참가자가 응답할 수 있는지 확인합니다.기본 시간은 180초입니다.이 시간이 충분하지 않으면 WS\-AT에 대한 `VolatileOutcomeDelay` 타이머 정책을 증가시킵니다.  
  
## 참고 항목  
 [추적](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [추적을 사용하여 응용 프로그램 문제 해결](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)   
 [관리 및 진단](../../../../../docs/framework/wcf/diagnostics/index.md)