---
title: "Microsoft.Transactions.TransactionBridge.CoordinatorStateMachineFinished | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 16cb428d-d886-4789-a961-6fded4b0dbba
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Microsoft.Transactions.TransactionBridge.CoordinatorStateMachineFinished
코디네이터 인리스트먼트를 위한 상태 시스템이 완료 상태가 되었습니다.  
  
## 설명  
 로컬 트랜잭션 관리자가 상위 코디네이터 인리스트먼트에서 2PC\(2단계 커밋\) 처리를 완료한 것으로 간주할 때 추적됩니다.인리스트먼트 결과는 커밋됨 또는 중단됨 또는 잊어버림입니다.로컬 트랜잭션 관리자가 준비 과정에서 ReadOnly를 선택하는 경우에도 추적됩니다.  
  
## 참고 항목  
 [추적](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [추적을 사용하여 응용 프로그램 문제 해결](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)   
 [관리 및 진단](../../../../../docs/framework/wcf/diagnostics/index.md)