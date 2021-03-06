---
title: "컨트롤 | Microsoft Docs"
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
  - "컨트롤[WPF], WPF 컨트롤 정보"
ms.assetid: 3f255a8a-35a8-4712-9065-472ff7d75599
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 컨트롤
<a name="introduction"></a> [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]에서는 <xref:System.Windows.Controls.Button>, <xref:System.Windows.Controls.Label>, <xref:System.Windows.Controls.TextBox>, <xref:System.Windows.Controls.Menu> 및 <xref:System.Windows.Controls.ListBox>와 같이 거의 모든 Windows 응용 프로그램에서 사용되는 대부분의 일반 UI 구성 요소가 제공됩니다.  지금까지는 이러한 개체를 컨트롤이라고 했습니다.  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] SDK에서는 응용 프로그램의 시각적 개체를 나타내는 모든 클래스를 대략적으로 의미하기 위해 "컨트롤"이라는 용어를 계속 사용하지만 클래스가 시각적 존재가 되기 위해 <xref:System.Windows.Controls.Control> 클래스에서 상속될 필요가 없다는 점이 중요합니다.  <xref:System.Windows.Controls.Control> 클래스에서 상속되는 클래스에는 <xref:System.Windows.Controls.ControlTemplate>가 포함되어 있으므로 컨트롤 소비자는 새 서브클래스를 만들 필요 없이 컨트롤 모양을 완전히 변경할 수 있습니다.  이 항목에서는 컨트롤\(<xref:System.Windows.Controls.Control> 클래스에서 상속되는 경우와 상속되지 않는 경우 모두\)이 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서 일반적으로 사용되는 방법에 대해 설명합니다.  
  
 [!INCLUDE[autoOutline](../Token/autoOutline_md.md)]  
  
<a name="creating_an_instance_of_a_control"></a>   
## 컨트롤의 인스턴스 만들기  
 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 또는 코드를 사용하여 응용 프로그램에 컨트롤을 추가할 수 있습니다.  다음 예제에서는 사용자에게 이름과 성을 묻는 간단한 응용 프로그램을 만드는 방법을 보여 줍니다.  이 예제에서는 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]에서 6개의 컨트롤\(2개의 레이블, 2개의 텍스트 상자 및 두 개의 단추\)을 만듭니다.  모든 컨트롤을 비슷하게 만들 수 있습니다.  
  
 [!code-xml[ControlsOverview#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/Window1.xaml#1)]  
  
 다음 예제에서는 코드에서 동일한 응용 프로그램을 만듭니다.  간단한 설명을 위해 <xref:System.Windows.Controls.Grid>, `grid1` 생성은 샘플에서 제외되었습니다.  `grid1`에는 이전 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 예제와 동일한 열 및 행 정의가 있습니다.  
  
 [!code-csharp[ControlsOverview#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml.cs#2)]
 [!code-vb[ControlsOverview#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ControlsOverview/VisualBasic/AppInCode.xaml.vb#2)]  
  
<a name="changing_the_appearance_of_a_control"></a>   
## 컨트롤 모양 변경  
 응용 프로그램의 모양 및 느낌에 맞도록 컨트롤의 모양을 변경하는 것이 일반적입니다.  원하는 결과에 따라 다음 중 하나를 수행하여 컨트롤의 모양을 변경할 수 있습니다.  
  
-   컨트롤의 속성 값을 변경합니다.  
  
-   컨트롤의 <xref:System.Windows.Style>을 만듭니다.  
  
-   컨트롤의 새 <xref:System.Windows.Controls.ControlTemplate>을 만듭니다.  
  
### 컨트롤의 속성 값 변경  
 대부분의 컨트롤에는 <xref:System.Windows.Controls.Button>의 <xref:System.Windows.Controls.Control.Background%2A>와 같이 컨트롤 모양을 변경할 수 있게 하는 속성이 있습니다.  [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 및 코드에서 값 속성을 설정할 수 있습니다.  다음 예제에서는 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]에서 <xref:System.Windows.Controls.Button>의 <xref:System.Windows.Controls.Control.Background%2A>, <xref:System.Windows.Controls.Control.FontSize%2A> 및 <xref:System.Windows.Controls.Control.FontWeight%2A> 속성을 설정합니다.  
  
 [!code-xml[ControlsOverview#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml#3)]  
  
 다음 예제에서는 코드에서 동일한 속성을 설정합니다.  
  
 [!code-csharp[ControlsOverview#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml.cs#4)]
 [!code-vb[ControlsOverview#4](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ControlsOverview/VisualBasic/AppInCode.xaml.vb#4)]  
  
### 컨트롤의 스타일 만들기  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서는 응용 프로그램의 각 인스턴스에서 속성을 설정하는 대신에 <xref:System.Windows.Style>을 만들어 컨트롤 모양을 전체적으로 지정할 수 있는 기능이 제공됩니다.  다음 예제에서는 응용 프로그램의 각 <xref:System.Windows.Controls.Button>에 적용되는 <xref:System.Windows.Style>을 만듭니다. <xref:System.Windows.Style> 정의는 일반적으로 <xref:System.Windows.FrameworkElement>의 <xref:System.Windows.FrameworkElement.Resources%2A> 속성과 같은 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]의 <xref:System.Windows.ResourceDictionary>에서 정의됩니다.  
  
 [!code-xml[ControlsOverview#5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml#5)]  
  
 또한 스타일에 키를 할당하고 컨트롤의 `Style` 속성에서 해당 키를 지정하여 특정 형식의 특정 컨트롤에만 스타일을 적용할 수 있습니다.  스타일에 대한 자세한 내용은 [스타일 지정 및 템플릿](../../../../docs/framework/wpf/controls/styling-and-templating.md)을 참조하십시오.  
  
### ControlTemplate 만들기  
 <xref:System.Windows.Style>을 사용하면 여러 컨트롤에서 속성을 동시에 설정할 수 있지만 경우에 따라서는 <xref:System.Windows.Style>을 만들어 수행할 수 있는 범위를 넘어서 <xref:System.Windows.Controls.Control>의 모양을 사용자 지정하고 싶을 때가 있습니다.  <xref:System.Windows.Controls.Control> 클래스에서 상속되는 클래스에는 <xref:System.Windows.Controls.Control>의 구조와 모양을 정의하는 <xref:System.Windows.Controls.ControlTemplate>이 있습니다.  <xref:System.Windows.Controls.Control>의 <xref:System.Windows.Controls.Control.Template%2A> 속성은 공용이므로 기본값과 다른 <xref:System.Windows.Controls.ControlTemplate>을 <xref:System.Windows.Controls.Control>에 제공할 수 있습니다.  일반적으로 <xref:System.Windows.Controls.Control>의 모양을 사용자 지정하기 위해 컨트롤에서 상속하는 대신에 <xref:System.Windows.Controls.Control>에 대한 새로운 <xref:System.Windows.Controls.ControlTemplate>을 지정할 수 있습니다.  
  
 매우 일반적인 컨트롤인 <xref:System.Windows.Controls.Button>의 경우를 살펴봅니다.  <xref:System.Windows.Controls.Button>의 기본 동작은 사용자가 클릭했을 때 응용 프로그램에서 일정한 작업을 수행할 수 있게 하는 것입니다.  기본적으로 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서 <xref:System.Windows.Controls.Button>은 볼록한 사각형으로 표시됩니다.  응용 프로그램을 개발하면서 단추의 클릭 이벤트를 처리하여 <xref:System.Windows.Controls.Button>의 동작을 활용하려고 하지만 단추 속성 변경으로 수행할 수 없는 단추 모양 변경이 필요할 수도 있습니다.  이러한 경우 <xref:System.Windows.Controls.ControlTemplate>을 새로 만들 수 있습니다.  
  
 다음 예제에서는 <xref:System.Windows.Controls.Button>에 대한 <xref:System.Windows.Controls.ControlTemplate>을 만듭니다.  <xref:System.Windows.Controls.ControlTemplate>은 둥근 모서리와 그라데이션 배경이 있는 <xref:System.Windows.Controls.Button>을 만듭니다.  <xref:System.Windows.Controls.ControlTemplate>에는 <xref:System.Windows.Controls.Border>가 포함되어 있으며 이 개체의 <xref:System.Windows.Controls.Border.Background%2A>는 두 개의 <xref:System.Windows.Media.GradientStop> 개체가 있는 <xref:System.Windows.Media.LinearGradientBrush>입니다.  첫 번째 <xref:System.Windows.Media.GradientStop>은 데이터 바인딩을 사용하여 <xref:System.Windows.Media.GradientStop>의 <xref:System.Windows.Media.GradientStop.Color%2A> 속성을 단추의 배경색에 바인딩합니다.  <xref:System.Windows.Controls.Button>의 <xref:System.Windows.Controls.Control.Background%2A> 속성을 설정할 경우 해당 값의 색이 첫 번째 <xref:System.Windows.Media.GradientStop>으로 사용됩니다.  데이터 바인딩에 대한 자세한 내용은 [데이터 바인딩 개요](../../../../docs/framework/wpf/data/data-binding-overview.md)를 참조하십시오.  또한 이 예제에서는 <xref:System.Windows.Controls.Primitives.ButtonBase.IsPressed%2A>가 `true`일 경우 <xref:System.Windows.Controls.Button>의 모양을 변경하는 <xref:System.Windows.Trigger>를 만듭니다.  
  
 [!code-xml[ControlsOverview#6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/Window1.xaml#6)]  
[!code-xml[ControlsOverview#7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml#7)]  
  
> [!NOTE]
>  예제가 제대로 작동하려면 <xref:System.Windows.Controls.Button>의 <xref:System.Windows.Controls.Control.Background%2A> 속성은 <xref:System.Windows.Media.SolidColorBrush>로 설정되어야 합니다.  
  
<a name="subscribing_to_events"></a>   
## 이벤트에 등록  
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 또는 코드를 사용하여 컨트롤의 이벤트를 구독해야 하지만 코드에서만 이벤트를 처리할 수 있습니다.  다음 예제에서는 <xref:System.Windows.Controls.Button>의 `Click` 이벤트를 구독하는 방법을 보여 줍니다.  
  
 [!code-xml[ControlsOverview#10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/Window1.xaml#10)]  
  
 [!code-csharp[ControlsOverview#8](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml.cs#8)]
 [!code-vb[ControlsOverview#8](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ControlsOverview/VisualBasic/AppInCode.xaml.vb#8)]  
  
 다음 예제에서는 <xref:System.Windows.Controls.Button>의 `Click` 이벤트를 처리합니다.  
  
 [!code-csharp[ControlsOverview#9](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml.cs#9)]
 [!code-vb[ControlsOverview#9](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ControlsOverview/VisualBasic/AppInCode.xaml.vb#9)]  
  
<a name="rich_content_in_controls"></a>   
## 컨트롤의 풍부한 콘텐츠  
 <xref:System.Windows.Controls.Control> 클래스에서 상속되는 대부분의 클래스는 풍부한 콘텐츠를 포함할 수 있습니다.  예를 들어 <xref:System.Windows.Controls.Label>은 문자열, <xref:System.Windows.Controls.Image> 또는 <xref:System.Windows.Controls.Panel>과 같은 모든 개체를 포함할 수 있습니다.  다음 클래스는 풍부한 콘텐츠에 대한 지원을 제공하며 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]의 대부분의 컨트롤에 대한 기본 클래스로 작동합니다.  
  
-   <xref:System.Windows.Controls.ContentControl>\-\- 이 클래스에서 상속되는 클래스의 몇 가지 예로는 <xref:System.Windows.Controls.Label>, <xref:System.Windows.Controls.Button> 및 <xref:System.Windows.Controls.ToolTip>이 있습니다.  
  
-   <xref:System.Windows.Controls.ItemsControl>\-\- 이 클래스에서 상속되는 클래스의 몇 가지 예로는 <xref:System.Windows.Controls.ListBox>, <xref:System.Windows.Controls.Menu> 및 <xref:System.Windows.Controls.Primitives.StatusBar>가 있습니다.  
  
-   <xref:System.Windows.Controls.HeaderedContentControl>\-\- 이 클래스에서 상속되는 클래스의 몇 가지 예로는 <xref:System.Windows.Controls.TabItem>, <xref:System.Windows.Controls.GroupBox> 및 <xref:System.Windows.Controls.Expander>가 있습니다.  
  
-   <xref:System.Windows.Controls.HeaderedItemsControl>\-\-이 클래스에서 상속되는 클래스의 몇 가지 예로는 <xref:System.Windows.Controls.MenuItem>, <xref:System.Windows.Controls.TreeViewItem> 및 <xref:System.Windows.Controls.ToolBar>가 있습니다.  
  
 이러한 기본 클래스에 대한 자세한 내용은 [WPF 콘텐츠 모델](../../../../docs/framework/wpf/controls/wpf-content-model.md)을 참조하십시오.  
  
## 참고 항목  
 [스타일 지정 및 템플릿](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [컨트롤 범주](../../../../docs/framework/wpf/controls/controls-by-category.md)   
 [컨트롤 라이브러리](../../../../docs/framework/wpf/controls/control-library.md)   
 [데이터 템플릿 개요](../../../../docs/framework/wpf/data/data-templating-overview.md)   
 [데이터 바인딩 개요](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [입력](../../../../docs/framework/wpf/advanced/input-wpf.md)   
 [명령 사용](../../../../docs/framework/wpf/advanced/how-to-enable-a-command.md)   
 [연습: 사용자 지정 애니메이션 단추 만들기](../../../../docs/framework/wpf/controls/walkthroughs-create-a-custom-animated-button.md)   
 [컨트롤 사용자 지정](../../../../docs/framework/wpf/controls/control-customization.md)