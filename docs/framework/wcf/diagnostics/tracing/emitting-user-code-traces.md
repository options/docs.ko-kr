---
title: "사용자 코드 추적 내보내기 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fa54186a-8ffa-4332-b0e7-63867126fd49
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# 사용자 코드 추적 내보내기
구성에서 추적을 활성화하여 [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)]에서 생성되는 계측 데이터를 수집하는 외에도 사용자 코드에서 프로그래밍 방식으로 추적할 수도 있습니다.  이런 방식으로 계측 데이터를 사전에 작성하여 나중에 진단을 위해 확인할 수 있습니다.  이 항목에서는 이 작업을 수행하는 방법에 대해 설명합니다.  
  
 또한 [추적 확장](../../../../../docs/framework/wcf/samples/extending-tracing.md) 샘플에는 다음 단원에서 설명하는 모든 코드가 포함되어 있습니다.  
  
## 추적 소스 만들기  
 다음 코드를 사용하여 사용자 추적 소스를 만들 수 있습니다.  
  
```  
TraceSource ts = new TraceSource("myUserTraceSource");  
```  
  
## 동작 만들기  
 동작은 처리의 논리 단위입니다.  추적을 그룹화할 주 처리 단위별로 하나의 동작을 만들 수 있습니다.  예를 들어, 서비스 요청별로 하나의 동작을 만들 수 있습니다.  그렇게 하려면 다음 단계를 수행합니다.  
  
1.  범위 내의 동작 ID를 저장합니다.  
  
2.  새 동작 ID를 만듭니다.  
  
3.  범위 내의 동작을 새 동작으로 전송하고, 범위 내의 새 동작을 설정한 다음 해당 동작에 대한 Start 추적을 내보냅니다.  
  
 다음 코드에서는 이 작업을 수행하는 방법에 대해 설명합니다.  
  
```  
Guid oldID = Trace.CorrelationManager.ActivityId;  
Guid traceID = Guid.NewGuid();  
ts.TraceTransfer(0, "transfer", traceID);  
Trace.CorrelationManager.ActivityId = traceID; // Trace is static  
ts.TraceEvent(TraceEventType.Start, 0, "Add request");  
```  
  
## 사용자 동작에서 추적 내보내기  
 다음 코드는 사용자 동작에서 추적을 내보냅니다.  
  
```  
double value1 = 100.00D;  
double value2 = 15.99D;  
ts.TraceInformation("Client sends message to Add " + value1 + ", " + value2);  
double result = client.Add(value1, value2);  
ts.TraceInformation("Client receives Add response '" + result + "'");  
```  
  
## 동작 중지  
 동작을 중지하려면 이전 동작으로 다시 전송하고, 현재 동작 ID를 중지한 다음 범위 내의 이전 동작 ID를 다시 설정합니다.  
  
 다음 코드에서는 이 작업을 수행하는 방법에 대해 설명합니다.  
  
```  
ts.TraceTransfer(0, "transfer", oldID);  
ts.TraceEvent(TraceEventType.Stop, 0, "Add request");  
Trace.CorrelationManager.ActivityId = oldID;  
```  
  
## 서비스에 동작 ID 전파  
 클라이언트와 서비스 구성 파일 모두에서 `System.ServiceModel` 추적 소스에 대해 `propagateActivity` 특성을 `true`로 설정하면 클라이언트에 정의된 것과 동일한 동작에서 추가 요청에 대한 서비스 처리가 발생합니다.  서비스에서 자체 동작과 전송을 정의하는 경우 클라이언트가 전파한 동작에는 서비스 추적이 표시되지 않습니다.  대신 클라이언트가 해당 ID를 전파한 동작의 Transfer 추적에 의해 연결된 동작에 서비스 추적이 표시됩니다.  
  
> [!NOTE]
>  클라이언트와 서비스 모두에서 `propagateActivity` 특성이 `true`로 설정되어 있는 경우 서비스 작업 범위 내의 앰비언트 동작이 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)]에 의해 설정됩니다.  
  
 다음 코드를 사용하여 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)]에 의해 범위 내의 동작이 설정되었는지 여부를 확인할 수 있습니다.  
  
```  
// Check if an activity was set in scope by WCF, if it was   
// propagated from the client. If not, ( ambient activity is   
// equal to Guid.Empty), create a new one.  
if(Trace.CorrelationManager.ActivityId == Guid.Empty)  
{  
    Guid newGuid = Guid.NewGuid();  
    Trace.CorrelationManager.ActivityId = newGuid;  
}  
// Emit your Start trace.  
ts.TraceEvent(TraceEventType.Start, 0, "Add Activity");  
  
// Emit the processing traces for that request.  
serviceTs.TraceInformation("Service receives Add "   
                            + n1 + ", " + n2);  
// double result = n1 + n2;  
serviceTs.TraceInformation("Service sends Add result" + result);  
  
// Emit the Stop trace and exit the method scope.  
ts.TraceEvent(TraceEventType.Stop, 0, "Add Activity");  
// return result;  
```  
  
## 코드에서 Throw된 예외 추적  
 코드에서 예외를 throw한 경우 다음 코드를 사용하여 경고 수준 이상으로 예외를 추적할 수도 있습니다.  
  
```  
ts.TraceEvent(TraceEventType.Warning, 0, “Throwing exception “ + “exceptionMessage”);  
```  
  
## 서비스 추적 뷰어 도구에서 사용자 추적 보기  
 이 단원에는 [Service Trace Viewer 도구\(SvcTraceViewer.exe\)](../../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md)를 사용하여 볼 때 [추적 확장](../../../../../docs/framework/wcf/samples/extending-tracing.md) 샘플을 실행하여 생성된 추적에 대한 스크린 샷이 있습니다.  
  
 다음 다이어그램에서는 이전에 만든 “추가 요청” 동작을 왼쪽 패널에서 선택합니다.  응용 프로그램 클라이언트 프로그램을 구성하는 세 개의 수학 연산 동작\(나누기, 빼기, 곱하기\)으로 나열됩니다.  다른 요청에서 발생할 수 있는 잠재적 오류를 격리시키기 위해 사용자 코드에서 작업별로 하나의 새로운 동작을 정의했습니다.  
  
 [추적 확장](../../../../../docs/framework/wcf/samples/extending-tracing.md) 샘플에서 전송 사용에 대해 설명하려고 네 작업 요청을 캡슐화하는 계산기 동작을 만들었습니다.  각 요청에는 계산기 동작과 요청 동작 사이에 주고 받는 전송이 있습니다. 추적은 그림의 오른쪽 위 패널에 강조 표시되어 있습니다.  
  
 왼쪽 패널에서 동작을 선택하면 이 동작에 포함된 추적이 오른쪽 위 패널에 표시됩니다.  요청 경로의 모든 끝점에서 `propagateActivity`가 `true`이면 요청에 참여한 모든 프로세스에서 요청 동작을 추적합니다.  이 예제에서는 패널의 네 번째 열에서 클라이언트와 서비스 모두의 추적을 확인할 수 있습니다.  
  
 이 동작의 처리 순서는 다음과 같습니다.  
  
1.  클라이언트가 추가할 메시지를 보냅니다.  
  
2.  서비스가 추가 요청 메시지를 받습니다.  
  
3.  서비스가 추가 응답을 보냅니다.  
  
4.  클라이언트가 추가 응답을 받습니다.  
  
 이러한 모든 추적을 정보 수준에서 내보냅니다.  오른쪽 위 패널에서 추적을 클릭하면 해당 추적에 대한 자세한 내용이 오른쪽 아래 패널에 표시됩니다.  
  
 다음 다이어그램에서는 계산기 동작에서 보내거나 받은 Transfer 추적을 표시하고 요청 동작별로 두 개의 Start 및 Stop 추적 쌍을 표시합니다. 이 추적 쌍은 클라이언트와 서비스별로 각각 하나씩\(추적 소스별로 하나\) 표시됩니다.  
  
 ![추적 뷰어: 사용자 코드 추적 내보내기](../../../../../docs/framework/wcf/diagnostics/tracing/media/242c9358-475a-4baf-83f3-4227aa942fcd.gif "242c9358\-475a\-4baf\-83f3\-4227aa942fcd")  
생성 시간별 동작 목록\(왼쪽 패널\) 및 중첩된 동작 목록\(오른쪽 위 패널\)  
  
 서비스 코드가 예외를 throw하여 클라이언트에서도 예외가 throw되면\(예: 클라이언트가 요청에 대한 응답을 가져오지 않은 경우\), 서비스 및 클라이언트 경고 또는 오류 메시지가 직접 상관 관계에 대해 동일한 동작에서 표시됩니다.  다음 다이어그램에서 서비스는 "서비스가 사용자 코드에서 이 요청의 처리를 거부했습니다."라는 예외를 throw합니다. 클라이언트에서도 "내부 오류로 인해 서버에서 요청을 처리할 수 없습니다."라는 예외를 throw합니다.  
  
 ![추적 뷰어를 사용하여 사용자 코드 추적 내보내기](../../../../../docs/framework/wcf/diagnostics/tracing/media/e2etrace2.gif "e2eTrace2")  
지정된 요청에 대한 끝점에서의 오류는 요청 동작 ID가 전파된 경우와 동일한 동작에 표시됩니다.  
  
 왼쪽 패널에서 곱하기 동작을 두 번 클릭하면 다음과 같은 그래프가 표시되고 포함된 프로세스별로 곱하기 동작에 대한 추적 사항이 나타납니다.  서비스에서 처음 발생한 경고\(throw된 예외\)와 요청을 처리하지 못하여 클라이언트에서 발생한 경고 및 오류가 표시됩니다.  따라서 끝점 사이의 오류의 인과 관계를 유추하여 오류의 근본 원인을 파악할 수 있습니다.  
  
 ![추적 뷰어를 사용하여 사용자 코드 추적 내보내기](../../../../../docs/framework/wcf/diagnostics/tracing/media/e2etrace3.gif "e2eTrace3")  
오류 상관 관계 그래프 보기  
  
 이전 추적을 가져오려면 사용자 추적 소스에 대해 `ActivityTracing`을 설정하고 `System.ServiceModel` 추적 소스에 대해 `propagateActivity=true`로 설정합니다.  사용자 코드 동작 전파에 사용자 코드를 활성화하기 위해 `System.ServiceModel` 추적 소스에 대해서는 `ActivityTracing`을 설정하지 않았습니다.  ServiceModel 동작 추적이 설정되어 있으면 클라이언트에 정의된 동작 ID가 서비스 사용자 코드에 끝까지 전파되지 않지만, 전송은 클라이언트 및 서비스 사용자 코드 동작을 중간 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 동작에 연결합니다.  
  
 동작을 정의하고 동작 ID를 전파하면 끝점을 통해 오류 상관 관계를 직접 수행할 수 있습니다.  그러면 오류에 대한 근본적인 원인을 신속하게 찾을 수 있습니다.  
  
## 참고 항목  
 [추적 확장](../../../../../docs/framework/wcf/samples/extending-tracing.md)