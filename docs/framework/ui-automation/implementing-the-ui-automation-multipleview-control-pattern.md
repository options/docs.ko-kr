---
title: "Implementing the UI Automation MultipleView Control Pattern | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "UI Automation, MultipleView control pattern"
  - "MultipleView control pattern"
  - "control patterns, MultipleView"
ms.assetid: 5bf1b248-ffee-48c8-9613-0b134bbe9f6a
caps.latest.revision: 15
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 15
---
# Implementing the UI Automation MultipleView Control Pattern
> [!NOTE]
>  이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다.[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]에 대한 최신 정보는 [Windows 자동화 API: UI 자동화](http://go.microsoft.com/fwlink/?LinkID=156746)를 참조하세요.  
  
 이 항목에서는 이벤트 및 속성에 대한 정보를 포함하여 <xref:System.Windows.Automation.Provider.IMultipleViewProvider>를 구현하기 위한 지침 및 규칙을 제공합니다. 추가 참조에 대한 링크는 항목 끝에 나열되어 있습니다.  
  
 <xref:System.Windows.Automation.MultipleViewPattern> 컨트롤 패턴은 동일한 정보 또는 자식 컨트롤 집합의 여러 표현 간을 전환할 수 있는 컨트롤을 지원하는 데 사용됩니다.  
  
 여러 뷰를 제공할 수 있는 컨트롤의 예로는 목록 뷰\(축소판, 타일, 아이콘 또는 세부 정보로 내용을 표시할 수 있는 뷰\), [!INCLUDE[TLA#tla_xl](../../../includes/tlasharptla-xl-md.md)] 차트\(원형, 꺾은선형, 막대형, 수식이 있는 셀 값\), [!INCLUDE[TLA#tla_word](../../../includes/tlasharptla-word-md.md)] 문서\(보통, 웹 레이아웃, 인쇄 레이아웃, 읽기 레이아웃, 개요\), [!INCLUDE[TLA#tla_outlook](../../../includes/tlasharptla-outlook-md.md)] 달력\(연도, 월, 주, 일\) 및 [!INCLUDE[TLA#tla_wmp](../../../includes/tlasharptla-wmp-md.md)] 스킨이 있습니다. 지원되는 뷰는 컨트롤 개발자가 결정하며 컨트롤마다 다릅니다.  
  
<a name="Implementation_Guidelines_and_Conventions"></a>   
## 구현 지침 및 규칙  
 Multiple View 컨트롤 패턴을 구현할 때는 다음 지침 및 규칙에 유의하세요.  
  
-   <xref:System.Windows.Automation.Provider.IMultipleViewProvider>가 현재 보기를 제공하는 컨트롤과 다를 경우 현재 보기를 관리하는 컨테이너에도 구현해야 합니다. 예를 들어, 컨트롤의 뷰가 Windows 탐색기 응용 프로그램에서 관리되는 동안 Windows 탐색기에는 현재 폴더 내용에 대한 목록 컨트롤이 포함됩니다.  
  
-   콘텐츠를 정렬할 수 있는 컨트롤은 여러 뷰를 지원한다고 간주되지 않습니다.  
  
-   뷰 컬렉션은 인스턴스 간에 동일해야 합니다.  
  
-   뷰 이름은 텍스트 읽어주기, 브라유 점자 및 기타 사람이 읽을 수 있는 응용 프로그램에서 사용하기 적합해야 합니다.  
  
<a name="Required_Members_for_IMultipleViewProvider"></a>   
## IMultipleViewProvider에 필요한 멤버  
 IMultipleViewProvider를 구현하려면 다음과 같은 속성 및 메서드가 필요합니다.  
  
|필요한 멤버|멤버 형식|노트|  
|------------|-----------|--------|  
|<xref:System.Windows.Automation.Provider.IMultipleViewProvider.CurrentView%2A>|속성|없음|  
|<xref:System.Windows.Automation.Provider.IMultipleViewProvider.GetSupportedViews%2A>|메서드|없음|  
|<xref:System.Windows.Automation.Provider.IMultipleViewProvider.GetViewName%2A>|메서드|없음|  
|<xref:System.Windows.Automation.Provider.IMultipleViewProvider.SetCurrentView%2A>|메서드|없음|  
  
 이 컨트롤 패턴과 관련된 이벤트가 없습니다.  
  
<a name="Exceptions"></a>   
## 예외  
 공급자는 다음과 같은 예외를 발생해야 합니다.  
  
|예외 형식|조건|  
|-----------|--------|  
|<xref:System.ArgumentException>|지원되는 뷰 컬렉션 멤버가 아닌 매개 변수로 <xref:System.Windows.Automation.Provider.IMultipleViewProvider.SetCurrentView%2A> 또는 <xref:System.Windows.Automation.Provider.IMultipleViewProvider.GetViewName%2A>이 호출되는 경우.|  
  
## 참고 항목  
 [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)   
 [Support Control Patterns in a UI Automation Provider](../../../docs/framework/ui-automation/support-control-patterns-in-a-ui-automation-provider.md)   
 [UI Automation Control Patterns for Clients](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)   
 [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)   
 [Use Caching in UI Automation](../../../docs/framework/ui-automation/use-caching-in-ui-automation.md)