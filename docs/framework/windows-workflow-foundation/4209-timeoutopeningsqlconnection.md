---
title: "4209 - TimeoutOpeningSqlConnection | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f0e56518-9758-41dc-a760-50d1a10fba6e
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 4209 - TimeoutOpeningSqlConnection
## 속성  
  
|||  
|-|-|  
|ID|4209|  
|키워드|WFInstanceStore|  
|수준|오류|  
|채널|Microsoft\-Windows\-응용 프로그램 서버\-응용 프로그램\/디버그|  
  
## 설명  
 SQL 연결을 여는 동안 시간 초과가 발생했음을 나타냅니다.  
  
## 메시지  
 SQL 연결을 열려는 중 시간이 초과했습니다.  할당된 시간 제한인 %1 내에 작업을 완료하지 못했습니다.  이 작업에 할당된 시간은 더 긴 시간 제한의 일부였을 수 있습니다.  
  
## 설명  
  
|데이터 항목 이름|데이터 항목 형식|설명|  
|---------------|---------------|--------|  
|시간 제한|xs:string|SQL 연결을 열기 위한 시간 제한 값입니다.|  
|AppDomain|xs:string|AppDomain.CurrentDomain.FriendlyName에서 반환되는 문자열입니다.|