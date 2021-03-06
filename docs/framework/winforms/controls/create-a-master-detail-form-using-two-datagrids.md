---
title: "방법: 두 개의 Windows Forms DataGridView 컨트롤을 사용하여 마스터/세부 폼 만들기 | Microsoft Docs"
ms.custom: ""
ms.date: "02/15/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "DataGridView 컨트롤[Windows Forms], 마스터/세부 폼"
  - "마스터-세부 목록, 만들기"
  - "부모-자식 표, Windows Forms에 표시"
ms.assetid: 99f6e876-3f7f-4139-9063-e36587c95b02
caps.latest.revision: 23
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 방법: 두 개의 Windows Forms DataGridView 컨트롤을 사용하여 마스터/세부 폼 만들기
다음 코드 예제에서는 두 개의 <xref:System.Windows.Forms.BindingSource> 구성 요소에 바인딩된 두 개의 <xref:System.Windows.Forms.DataGridView> 컨트롤을 사용하여 마스터\/세부 폼을 만듭니다.  데이터 소스는 SQL Server Northwind 샘플 데이터베이스의 `Customers` 및 `Orders` 테이블과 `CustomerID` 열을 통해 두 테이블을 연결하는 <xref:System.Data.DataRelation>을 포함하는 <xref:System.Data.DataSet>니다.  
  
 하나의 <xref:System.Windows.Forms.BindingSource>가 데이터 집합의 부모 `Customers` 테이블에 바인딩됩니다.  이 데이터는 마스터 <xref:System.Windows.Forms.DataGridView> 컨트롤에 표시됩니다.  다른 <xref:System.Windows.Forms.BindingSource>는 첫 번째 데이터 커넥터에 바인딩됩니다.  두 번째 <xref:System.Windows.Forms.BindingSource>의 <xref:System.Windows.Forms.BindingSource.DataMember%2A> 속성은 <xref:System.Data.DataRelation> 이름으로 설정됩니다.  이렇게 하면 연결된 세부 <xref:System.Windows.Forms.DataGridView> 컨트롤에 마스터 <xref:System.Windows.Forms.DataGridView> 컨트롤의 현재 행에 해당하는 자식 `Orders` 테이블의 행이 표시됩니다.  
  
 이 코드 예제에 대한 자세한 설명은 [연습: 두 개의 Windows Forms DataGridView 컨트롤을 사용하여 마스터\/세부 폼 만들기](../../../../docs/framework/winforms/controls/creating-a-master-detail-form-using-two-datagrids.md)를 참조하세요.  
  
## 예제  
 [!code-csharp[System.Windows.Forms.DataGridViewMasterDetails#00](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMasterDetails/CS/masterdetails.cs#00)]
 [!code-vb[System.Windows.Forms.DataGridViewMasterDetails#00](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMasterDetails/VB/masterdetails.vb#00)]  
  
## 코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
-   System, System.Data, System.Windows.Forms 및 System.XML 어셈블리에 대한 참조  
  
 명령줄에서 [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] 또는 [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)]용으로 이 예제를 빌드하는 방법에 대한 자세한 내용은 [명령줄에서 빌드](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) 또는 [csc.exe를 사용한 명령줄 빌드](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)를 참조하세요.  [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)]에서 코드를 새 프로젝트에 붙여넣어 이 예제를 빌드할 수도 있습니다.  [방법: Visual Studio를 사용하여 전체 Windows Forms 코드 예제 컴파일 및 실행](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\))을 참조하세요.  
  
## .NET Framework 보안  
 암호와 같은 중요한 정보를 연결 문자열 내에 저장하면 응용 프로그램 보안 문제가 발생할 수 있습니다.  데이터베이스 액세스를 제어할 경우에는 통합 보안이라고도 하는 Windows 인증을 사용하는 방법이 더 안전합니다.  자세한 내용은 [연결 정보 보호](../../../../docs/framework/data/adonet/protecting-connection-information.md)을 참조하세요.  
  
## 참고 항목  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.BindingSource>   
 [연습: 두 개의 Windows Forms DataGridView 컨트롤을 사용하여 마스터\/세부 폼 만들기](../../../../docs/framework/winforms/controls/creating-a-master-detail-form-using-two-datagrids.md)   
 [Windows Forms DataGridView 컨트롤에서 데이터 표시](../../../../docs/framework/winforms/controls/displaying-data-in-the-windows-forms-datagridview-control.md)   
 [연결 정보 보호](../../../../docs/framework/data/adonet/protecting-connection-information.md)