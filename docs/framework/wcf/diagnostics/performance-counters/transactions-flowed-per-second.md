---
title: "Transactions Flowed Per Second | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b9f661e1-576c-48fc-9fdf-91853e0749e8
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Transactions Flowed Per Second
카운터 이름: Transactions Flowed Per Second  
  
## 설명  
 이 작업에 적용된 초당 트랜잭션의 수입니다.  작업에 전송된 메시지에 트랜잭션 ID가 있을 때마다 이 카운터가 증가합니다.  
  
 이 카운터는 성능 카운터 형식 [PERF\_COUNTER\_COUNTER](http://go.microsoft.com/fwlink/?LinkID=94649)\(영문\)로 되어 있습니다. 이 형식의 값은 다음과 같은 수식으로 계산됩니다.  
  
 \(N 1 \- N 0 \) \/ \( \(D 1 \-D 0 \) \/ F\)