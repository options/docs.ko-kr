---
title: "데이터 집합 콘텐츠를 XML 데이터로 작성 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fd15f8a5-3b4c-46d0-a561-4559ab2a4705
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# 데이터 집합 콘텐츠를 XML 데이터로 작성
ADO.NET에서의 XML 표현을 작성할 수는 <xref:System.Data.DataSet>, 또는 스키마 없이 합니다. 스키마 정보가 XML과 함께 인라인에 포함된 경우에는 XSD(XML 스키마 정의 언어)를 사용하여 작성됩니다. 테이블 정의 포함 하는 스키마는 <xref:System.Data.DataSet> 관계 및 제약 조건 정의가 있습니다.  
  
 때는 <xref:System.Data.DataSet> 행에 XML 데이터로 작성 되는 <xref:System.Data.DataSet> 은 자신의 현재 버전으로 작성 합니다. 그러나는 <xref:System.Data.DataSet> 하 현재 및 행의 원래 값을 모두 포함 됩니다 DiffGram로 작성할 수도 있습니다.  
  
 XML 표현을 <xref:System.Data.DataSet> 스트림, 파일에 쓸 수는 **XmlWriter**, 또는 문자열입니다. 이러한 선택 항목의 XML 표현을 전송 하는 방법은 매우 유연는 <xref:System.Data.DataSet>합니다. XML 표현을 <xref:System.Data.DataSet> 문자열로 사용 하 여는 **GetXml** 메서드는 다음 예와에서 같이 합니다.  
  
```vb  
Dim xmlDS As String = custDS.GetXml()  
```  
  
```csharp  
string xmlDS = custDS.GetXml();  
```  
  
 **GetXml** 의 XML 표현을 반환 된 <xref:System.Data.DataSet> 스키마 정보 없이 합니다. 스키마 정보를 작성 하는 <xref:System.Data.DataSet> (XML 스키마)로 사용 하 여 문자열로 **GetXmlSchema**합니다.  
  
 작성 하는 <xref:System.Data.DataSet> 파일 스트림 또는 **XmlWriter**를 사용 하 여는 **WriteXml** 메서드. 에 전달 하는 첫 번째 매개 변수 **WriteXml** XML 출력의 대상입니다. 예를 들어 파일 이름을 포함 하는 문자열을 전달는 **System.IO.TextWriter** 개체 크며 등등 합니다. 두 번째 선택적 매개 변수를 전달할 수는 **XmlWriteMode** XML 출력이 작성 방법을 지정할 수 있습니다.  
  
 다음 표에서에 대 한 옵션을 보여 줍니다. **XmlWriteMode**합니다.  
  
|XmlWriteMode 옵션|설명|  
|-------------------------|-----------------|  
|**IgnoreSchema**|현재 내용을 씁니다는 <xref:System.Data.DataSet> XML 스키마 없이 XML 데이터로 합니다. 이 값이 기본값입니다.|  
|**쓰려면**|현재 내용을 씁니다는 <xref:System.Data.DataSet> 인라인 XML 스키마와 동일한 관계형 구조를 가진 XML 데이터로 합니다.|  
|**DiffGram**|전체 씁니다 <xref:System.Data.DataSet> DiffGram으로 원래 및 현재 값을 포함 합니다. 자세한 내용은 참조 [Diffgram](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/diffgrams.md)합니다.|  
  
 XML 표현을 작성 하는 경우는 <xref:System.Data.DataSet> 포함 된 **DataRelation** 개체를 가장 합니다는 관련된 된 부모 요소 내에 중첩 된 각 관계의 자식 행을 결과 XML입니다. 이를 위해 설정는 **중첩** 의 속성은 **DataRelation** 를 **true** 추가 하는 경우는 **DataRelation** 에 <xref:System.Data.DataSet>. 자세한 내용은 참조 [중첩 Datarelation](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/nesting-datarelations.md)합니다.  
  
 XML 표현을 작성 하는 방법의 두 가지 예는 <xref:System.Data.DataSet> 파일에 있습니다. 첫 번째 예제에 대 한 문자열로 결과 XML에 대 한 파일 이름을 전달 **WriteXml**합니다. 두 번째 예에서는 전달 하는 **System.IO.StreamWriter** 개체입니다.  
  
```vb  
custDS.WriteXml("Customers.xml", XmlWriteMode.WriteSchema)  
  
```  
  
```csharp  
custDS.WriteXml("Customers.xml", XmlWriteMode.WriteSchema);  
  
```  
  
```vb  
Dim xmlSW As System.IO.StreamWriter = New System.IO.StreamWriter("Customers.xml")  
custDS.WriteXml(xmlSW, XmlWriteMode.WriteSchema)  
xmlSW.Close()  
  
```  
  
```csharp  
System.IO.StreamWriter xmlSW = new System.IO.StreamWriter("Customers.xml");  
custDS.WriteXml(xmlSW, XmlWriteMode.WriteSchema);  
xmlSW.Close();  
```  
  
## <a name="mapping-columns-to-xml-elements-attributes-and-text"></a>열을 XML 요소, 특성 및 텍스트에 매핑  
 XML에서 테이블의 열을 표현 하는 방법을 지정할 수 있습니다를 사용 하 여는 **ColumnMapping** 의 속성은 **DataColumn** 개체입니다. 다음 표에서 서로 다른 **MappingType** 에 대 한 값은 **ColumnMapping** 테이블 열 및 결과 XML의 속성입니다.  
  
|MappingType 값|설명|  
|-----------------------|-----------------|  
|**요소**|이 값이 기본값입니다. 열이 XML 요소로 작성되며, 이 때 ColumnName이 요소의 이름이 되고 열의 내용은 요소의 텍스트로 작성됩니다. 예를 들면 다음과 같습니다.<br /><br /> `<ColumnName>Column Contents</ColumnName>`|  
|**특성**|열이 현재 행에 대한 XML 요소의 XML 특성으로 작성되며, 이 때 특성의 이름은 ColumnName이며 열의 내용은 특성의 값으로 작성됩니다. 예:<br /><br /> `<RowElement ColumnName="Column Contents" />`|  
|**SimpleContent**|열의 내용이 현재 행에 대한 XML 요소의 텍스트로 작성됩니다. 예:<br /><br /> `<RowElement>Column Contents</RowElement>`<br /><br /> **SimpleContent** 가 있는 테이블의 열에 대해 설정할 수 없습니다 **요소** 열 이나 중첩 된 관계입니다.|  
|**숨김**|열이 XML 출력으로 작성되지 않습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [데이터 집합에서 XML 사용](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)   
 [Diffgram](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/diffgrams.md)   
 [Datarelation 중첩](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/nesting-datarelations.md)   
 [데이터 집합 스키마 정보를 XSD로 작성](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/writing-dataset-schema-information-as-xsd.md)   
 [Dataset, Datatable 및 Dataview](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [ADO.NET 관리 되는 공급자 및 데이터 집합 개발자 센터](http://go.microsoft.com/fwlink/?LinkId=217917)