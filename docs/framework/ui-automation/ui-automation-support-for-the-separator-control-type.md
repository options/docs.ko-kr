---
title: "UI Automation Support for the Separator Control Type | Microsoft Docs"
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
  - "UI Automation, Separator control type"
  - "Separator control type"
  - "control types, Separator"
ms.assetid: 89f42247-c699-4afa-91e1-2baaf0d86c9d
caps.latest.revision: 20
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 20
---
# UI Automation Support for the Separator Control Type
> [!NOTE]
>  이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다.[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]에 대한 최신 정보는 [Windows 자동화 API: UI 자동화](http://go.microsoft.com/fwlink/?LinkID=156746)를 참조하세요.  
  
 이 항목에서는 Separator 컨트롤 형식에 대한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 지원 정보를 제공합니다.[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]에서, 컨트롤 형식은 <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty> 속성을 사용하기 위해 컨트롤이 충족해야 하는 조건 집합입니다. 이 조건에는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리 구조, [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 속성 값, 컨트롤 패턴에 대한 특정 지침이 포함됩니다.  
  
 구분 기호 컨트롤은 시각적으로 공간을 두 영역으로 나누는 데 사용됩니다. 예를 들어, 구분 기호 컨트롤은 하나의 창에 두 개의 창을 정의하는 막대일 수 있습니다. 구분 기호를 이동할 수 있는 경우, 이 컨트롤은 Thumb 컨트롤 형식으로 노출되어야 합니다.  
  
 다음 섹션에서는 Separator 컨트롤 형식에 필요한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리 구조, 속성, 컨트롤 패턴, 이벤트를 정의합니다.[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 요구 사항은 [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)], [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)] 또는 [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)]의 모든 목록 컨트롤에 적용됩니다.  
  
<a name="Required_UI_Automation_Tree_Structure"></a>   
## 필요한 UI 자동화 트리 구조  
 다음 표는 구분 기호 컨트롤과 관련된 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리의 컨트롤 뷰 및 콘텐츠 뷰를 보여주고 각 뷰에 포함될 수 있는 내용에 대해 설명합니다.[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리에 대한 자세한 내용은 [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)를 참조하세요.  
  
|컨트롤 뷰|콘텐츠 뷰|  
|-----------|-----------|  
|구분 기호|-   Separator 컨트롤에는 콘텐츠가 없습니다.|  
  
<a name="Required_UI_Automation_Properties"></a>   
## 필요한 UI 자동화 속성  
 다음 표에서는 값 또는 정의가 구분 기호 컨트롤과 특별히 관련된 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 속성을 나열하여 보여줍니다.[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 속성에 대한 자세한 내용은 [UI Automation Properties for Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md)를 참조하세요.  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 속성|값|노트|  
|------------------------------------------------------------------------------|-------|--------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|메모를 참조하세요.|이 속성의 값은 응용 프로그램의 모든 컨트롤에서 고유해야 합니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|메모를 참조하세요.|전체 컨트롤이 포함된 가장 바깥쪽 사각형입니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|메모를 참조하세요.|경계 사각형이 없는 경우 지원됩니다. 경계 사각형 내의 일부 지점이 클릭 가능하지 않으며 특수화된 적중 테스트를 수행하는 경우 클릭 가능한 지점을 재정의하고 제공하세요.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|메모를 참조하세요.|컨트롤이 키보드 포커스를 받을 수 있으면 해당 컨트롤은 이 속성을 지원해야 합니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|""|구분 기호 컨트롤에는 NameProperty가 필요하지 않습니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|`null`|구분 기호 컨트롤에는 정적 레이블이 없습니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|구분 기호|이 값은 모든 UI 프레임워크에 대해 동일합니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|"Separator"|Separator 컨트롤 형식에 해당하는 지역화된 문자열입니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|False|구분 기호 컨트롤은 콘텐츠가 아닙니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|구분 기호 컨트롤이 항상 컨트롤이어야 합니다.|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>   
## 필요한 UI 자동화 컨트롤 패턴  
 구분 기호 컨트롤은 컨트롤 패턴을 지원하는 데 필요하지 않습니다.  
  
<a name="Required_UI_Automation_Events"></a>   
## 필요한 UI 자동화 이벤트  
 다음 표에서는 모든 구분 기호 컨트롤에서 지원되는 데 필요한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 이벤트를 나열하여 보여줍니다. 이벤트에 대한 자세한 내용은 [UI Automation Events Overview](../../../docs/framework/ui-automation/ui-automation-events-overview.md)를 참조하세요.  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 이벤트|지원|노트|  
|-------------------------------------------------------------------------------|--------|--------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> 속성 변경 이벤트|필수|없음|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty> 속성 변경 이벤트|필수|없음|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 속성 변경 이벤트|필수|없음|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|필수|없음|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|필수|없음|  
  
## 참고 항목  
 <xref:System.Windows.Automation.ControlType.Separator>   
 [UI Automation Control Types Overview](../../../docs/framework/ui-automation/ui-automation-control-types-overview.md)   
 [UI Automation Overview](../../../docs/framework/ui-automation/ui-automation-overview.md)