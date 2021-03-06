---
title: "방법: 요소의 높이 속성 설정 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "높이 속성"
  - "Panel 컨트롤, 요소의 높이 속성"
ms.assetid: 5ab9e781-dbb8-469a-a3c8-cf38ce312647
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 방법: 요소의 높이 속성 설정
## 예제  
 이 예제에서는 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]의 높이와 관련된 네 가지 속성이 지닌 렌더링 동작의 차이점을 보여 줍니다.  
  
 <xref:System.Windows.FrameworkElement> 클래스는 요소의 높이 특성을 정의하는 네 가지 속성을 노출합니다.  이 네 가지 속성은 서로 충돌할 수 있으며 충돌하는 경우 <xref:System.Windows.FrameworkElement.MinHeight%2A> 값, <xref:System.Windows.FrameworkElement.MaxHeight%2A> 값 및 <xref:System.Windows.FrameworkElement.Height%2A> 값의 순으로 우선 순위가 결정됩니다.  네 번째 속성인 <xref:System.Windows.FrameworkElement.ActualHeight%2A>는 읽기 전용이며, 레이아웃 프로세스와의 상호 작용을 통해 확인된 실제 높이를 보고합니다.  
  
 다음 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 예제에서는 <xref:System.Windows.Controls.Canvas>의 자식으로 <xref:System.Windows.Shapes.Rectangle> 요소\(`rect1`\)를 그립니다.  <xref:System.Windows.FrameworkElement.MinHeight%2A>, <xref:System.Windows.FrameworkElement.MaxHeight%2A> 및 <xref:System.Windows.FrameworkElement.Height%2A>의 속성 값을 나타내는 일련의 <xref:System.Windows.Controls.ListBox> 요소를 사용하여 <xref:System.Windows.Shapes.Rectangle>의 높이 속성을 변경할 수 있습니다.  이런 식으로 각 속성의 우선 순위가 시각적으로 표시됩니다.  
  
 [!code-xml[HeightMinHeightMaxHeight#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HeightMinHeightMaxHeight/CSharp/Window1.xaml#1)]  
[!code-xml[HeightMinHeightMaxHeight#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HeightMinHeightMaxHeight/CSharp/Window1.xaml#2)]  
  
 다음 코드 숨김 예제에서는 <xref:System.Windows.Controls.Primitives.Selector.SelectionChanged> 이벤트가 발생시키는 이벤트를 처리합니다.  각 처리기는 <xref:System.Windows.Controls.ListBox>에서 입력을 가져와 <xref:System.Double>로 값을 구문 분석한 다음 지정된 높이 관련 속성에 적용합니다.  높이 값도 문자열로 변환되어 여러 <xref:System.Windows.Controls.TextBlock> 요소에 기록됩니다. 이러한 요소의 정의는 선택한 XAML에 표시되어 있지 않습니다.  
  
 [!code-csharp[HeightMinHeightMaxHeight#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HeightMinHeightMaxHeight/CSharp/Window1.xaml.cs#3)]
 [!code-vb[HeightMinHeightMaxHeight#3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HeightMinHeightMaxHeight/VisualBasic/Window1.xaml.vb#3)]  
  
 전체 샘플을 보려면 [Height Properties 샘플](http://go.microsoft.com/fwlink/?LinkID=159993)을 참조하십시오.  
  
## 참고 항목  
 <xref:System.Windows.FrameworkElement>   
 <xref:System.Windows.Controls.ListBox>   
 <xref:System.Windows.FrameworkElement.ActualHeight%2A>   
 <xref:System.Windows.FrameworkElement.MaxHeight%2A>   
 <xref:System.Windows.FrameworkElement.MinHeight%2A>   
 <xref:System.Windows.FrameworkElement.Height%2A>   
 [요소의 너비 속성 설정](../../../../docs/framework/wpf/controls/how-to-set-the-width-properties-of-an-element.md)   
 [Panel 개요](../../../../docs/framework/wpf/controls/panels-overview.md)   
 [Height Properties 샘플](http://go.microsoft.com/fwlink/?LinkID=159993)