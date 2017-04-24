---
title: "ServiceModel 등록 도구(ServiceModelReg.exe) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
ms.assetid: 396ec5ae-e34f-4c64-a164-fcf50e86b6ac
caps.latest.revision: 26
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 26
---
# ServiceModel 등록 도구(ServiceModelReg.exe)
이 명령줄 도구는 단일 컴퓨터에서 WCF 및 WF 구성 요소 등록을 관리하는 기능을 제공합니다.일반적인 경우에는 설치 시 WCF 및 WF 구성 요소가 구성되므로 이 도구를 사용할 필요가 없습니다.하지만 서비스 활성화 문제가 있는 경우 이 도구를 사용하여 구성 요소를 등록해 볼 수 있습니다.  
  
## 구문  
  
```  
  
ServiceModelReg.exe[(-ia|-ua|-r)|((-i|-u) -c:<command>)] [-v|-q] [-nologo] [-?]  
```  
  
## 설명  
 이 도구는 다음 위치에 있습니다.  
  
 %SystemRoot%\\Microsoft.Net\\Framework\\v3.0\\Windows Communication Foundation\\  
  
> [!NOTE]
>  ServiceModel 등록 도구가 [!INCLUDE[wv](../../../includes/wv-md.md)]에서 실행되는 경우 **Windows 기능** 대화 상자는 **Microsoft .NET Framework 3.0**의 **Windows Communication Foundation HTTP 활성화** 옵션이 켜져 있음을 나타내지 않을 수도 있습니다.**Windows 기능** 대화 상자에 액세스하려면 **시작**, **실행**을 차례로 클릭한 다음 **OptionalFeatures**를 입력합니다.  
  
 다음 표에서는 ServiceModelReg.exe와 함께 사용할 수 있는 옵션을 보여 줍니다.  
  
|옵션|설명|  
|--------|--------|  
|`-ia`|모든 WCF 및 WF 구성 요소를 설치합니다.|  
|`-ua`|모든 WCF 및 WF 구성 요소를 삭제합니다.|  
|`-r`|모든 WCF 및 WF 구성 요소를 복구합니다.|  
|`-i`|\-c로 지정된 WCF 및 WF 구성 요소를 설치합니다.|  
|`-u`|\-c로 지정된 WCF 및 WF 구성 요소를 삭제합니다.|  
|`-c`|구성 요소를 설치 또는 삭제합니다.<br /><br /> -   httpnamespace – HTTP 네임스페이스 예약<br />-   tcpportsharing – TCP 포트 공유 서비스<br />-   tcpactivation – TCP 활성화 서비스\(.NET 4 클라이언트 프로필에 지원되지 않음\)<br />-   namedpipeactivation – 명명된 파이프 활성화 서비스\(.NET 4 클라이언트 프로필에 지원되지 않음<br />-   msmqactivation – MSMQ 활성화 서비스\(.NET 4 클라이언트 프로필에 지원되지 않음<br />-   etw – ETW 이벤트 추적 매니페스트\(Windows Vista 이상\)|  
|`-q`|자동 모드\(오류 기록만 표시함\)|  
|`-v`|자세한 정보 표시 모드.|  
|`-nologo`|저작권 및 배너 메시지를 표시하지 않습니다.|  
|`-?`|도움말 텍스트 표시|  
  
## FileLoadException 오류 수정  
 컴퓨터에 이전 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 버전을 설치한 경우 새 설치를 등록하기 위해 ServiceModelReg 도구를 실행할 때 `FileLoadFoundException` 오류가 발생할 수 있습니다.이전 설치에서 파일을 수동으로 제거했지만 machine.config 설정이 그대로 남아 있으면 이 오류가 발생할 수 있습니다.  
  
 다음과 유사한 오류 메시지가 표시됩니다.  
  
```  
Error: System.IO.FileLoadException: Could not load file or assembly 'System.ServiceModel, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089' or one of its dependencies. The located assembly's manifest definition does not match the assembly reference. (Exception from HRESULT: 0x80131040)  
File name: 'System.ServiceModel, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089'  
```  
  
 오류 메시지에 따르면 System.ServiceModel 버전 2.0.0.0 어셈블리가 초기 CTP\(Customer Technology Preview\) 릴리스에 의해 설치되었습니다.릴리스된 System.ServiceModel 어셈블리의 현재 버전은 3.0.0.0입니다.따라서 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]의 초기 CTP 릴리스가 설치되었지만 완전히 제거되지 않은 컴퓨터에 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]의 공식 릴리스를 설치하려는 경우 이 문제가 발생합니다.  
  
 ServiceModelReg.exe는 이전 버전의 항목을 정리할 수 없으며 새 버전의 항목을 등록할 수도 없습니다.유일한 해결 방법은 수동으로 machine.config를 편집하는 것입니다.다음 위치에서 이 파일을 찾을 수 있습니다.  
  
```  
%windir%\Microsoft.NET\Framework\v2.0.50727\config\machine.config   
```  
  
 또한 64비트 컴퓨터에서 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]를 실행하는 경우 이 위치에서 동일한 파일을 편집해야 합니다.  
  
```  
%windir%\Microsoft.NET\Framework64\v2.0.50727\config\machine.config   
```  
  
 이 파일에서 "System.ServiceModel, Version\=2.0.0.0"을 참조하는 모든 XML 노드를 찾아 해당 노드 및 모든 자식 노드를 삭제합니다.파일을 저장하고 ServiceModelReg.exe를 다시 실행하면 이 문제가 해결됩니다.  
  
## 예제  
 다음 예제에서는 ServiceModelReg.exe 도구의 가장 일반적인 옵션을 사용하는 방법을 보여 줍니다.  
  
```  
ServiceModelReg.exe -ia  
  Installs all components  
ServiceModelReg.exe -i -c:httpnamespace -c:etw  
  Installs HTTP namespace reservation and ETW manifests  
ServiceModelReg.exe -u -c:etw  
  Uninstalls ETW manifests  
ServiceModelReg.exe -r  
  Repairs an extended install  
```