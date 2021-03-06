---
title: "피어 투 피어 공동 작업 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: b6216d88-bccb-4a59-9f1c-9f751708e811
caps.latest.revision: 7
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 7
---
# 피어 투 피어 공동 작업
피어\-투\-피어 네트워킹 사용률 보다 단순한 클라이언트 기반 컴퓨팅 작업에 대 한 인터넷의 가장자리에 있는 비교적 강력한 컴퓨터 \(개인용 컴퓨터\)입니다.  현대 개인용 컴퓨터 \(PC\)에 고속 프로세서, 대용량 메모리 및 완전 하가 게 전자 메일 및 웹 브라우징과 같은 일반적인 컴퓨팅 작업을 수행할 때 사용 되는 대용량 하드 디스크를 했습니다.  요즘 PC 클라이언트와 서버 \(피어\) 여러 종류의 응용 프로그램으로 쉽게 작동할 수 있습니다.  
  
-   피어\-투\-피어 공동 작업 인프라는 주변 사람 찾기 Windows Vista 및 이후 플랫폼에 서비스를 활용 하는 Microsoft Windows 피어\-투\-피어 인프라를 단순화 된 구현입니다.  피어 지원 응용 프로그램 내의 서브넷에 대 한 최상의 사용을 주변 사람 찾기 서비스 작동, 인터넷 끝점 또는 연락처도 서비스를 제공할 수 있지만.  공용 연락처 라이브 메신저 및 기타 Live 인식 응용 프로그램에서 연락처 끝점, 가용성 및 현재 상태를 확인 하는 데 사용 되 관리자를 통합 합니다.  
  
## 공동 작업 응용 프로그램  
 일반적인 피어\-투\-피어 공동 작업 응용 프로그램에는 다음 단계로 구성 됩니다.  
  
-   피어 피어 공동 작업 세션을 호스트 하는 데 관심이 있는 사용자의 id를 확인 합니다.  
  
-   세션 호스트 요청, 어떻게든, 전송 되 고 호스트 피어 공동 작업을 관리 하겠다고.  
  
-   호스트 서브넷 등 요청자 연락처 세션에 초대 합니다.  
  
-   공동 작업 하려는 모든 피어는 호스트 연락처 관리자에 추가할 수 있습니다.  
  
-   대부분의 동료 초대 응답을 수락 또는 거절 호스트 피어에 시기에 다시 보냅니다.  
  
-   공동 작업 하려는 모든 피어는 호스트 피어에 등록 합니다.  
  
-   피어가 초기 공동 작업을 수행 하는 동안 호스트 피어는 원격 피어 자신의 연락처 관리자에 추가할 수 있습니다.  또한 모든 초대 응답을 확인 하 게 누가 거절 했습니다 고 답한 사람이 없습니다 수락 했습니다 처리 합니다.  답하지는 초대를 취소 하거나 일부 다른 작업을 수행할 수 있습니다.  
  
-   이 시점에서 호스트 피어 초대 모든 동료 들과 공동 작업 세션을 시작 하거나 응용 프로그램이 공동 작업 인프라에 등록 합니다.  P2P 응용 프로그램에서 피어\-투\-피어 공동 작업 인프라를 사용 하는 <xref:System.Net.PeerToPeer.Collaboration> 네임 스페이스 게임, 게시판, 회 및 기타 상태를 사용 하지 않는 응용 프로그램에 대 한 통신을 조정 합니다.  
  
## 피어\-투\-피어 네트워킹 보안  
 Active Directory 도메인에 도메인 컨트롤러가 Kerberos를 사용 하 여 인증 서비스를 제공 합니다.  사용 하지 않는 피어 환경에서 피어는 자체 인증을 제공 해야 합니다.  피어\-투\-피어 네트워킹에 대 한, 모든 노드가 각 피어의 신뢰할 수 있는 루트 저장소에 루트 인증서의 요구 사항이 제거 된 CA로 작동할 수 있습니다.  포맷으로 X.509 인증서는 자체 서명된 인증서를 사용 하 여 인증을 제공 합니다.  개인 키를 사용 하 여 서명 된 인증서 및 공개 키\/개인 키 쌍을 생성 하는 각 피어가 만들어진 인증서입니다.  자체 서명 된 인증서 피어 엔터티에 대 한 정보를 제공 하 고 인증에 사용 됩니다.  X.509 인증 처럼 피어 네트워킹 인증의 인증서 체인에 신뢰할 수 있는 공용 키 다시 추적에 의존 합니다.  
  
## 참고 항목  
 <xref:System.Net.PeerToPeer.Collaboration>   
 [System.Net.PeerToPeer.Collaboration 네임스페이스 정보](../../../docs/framework/network-programming/about-the-system-net-peertopeer-collaboration-namespace.md)