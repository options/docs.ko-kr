---
title: "방법: Windows Forms RichTextBox 컨트롤에서 끌어서 놓기 작업 사용 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
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
  - "예제[Windows Forms], 텍스트 상자"
  - "끌어서 놓기, RichTextBox 컨트롤"
  - "텍스트 상자, 끌어서 놓기 작업"
  - "RichTextBox 컨트롤[Windows Forms], 끌어서 놓기 작업"
ms.assetid: ca167d1c-2014-4cf0-96a0-20598470be3b
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 방법: Windows Forms RichTextBox 컨트롤에서 끌어서 놓기 작업 사용
Windows Forms <xref:System.Windows.Forms.RichTextBox> 컨트롤을 사용한 끌어서 놓기 작업은 <xref:System.Windows.Forms.RichTextBox.DragEnter> 및 <xref:System.Windows.Forms.RichTextBox.DragDrop> 이벤트를 처리하여 수행됩니다. 따라서 <xref:System.Windows.Forms.RichTextBox> 컨트롤을 사용하면 끌어서 놓기 작업이 매우 간단합니다.  
  
### RichTextBox 컨트롤에서 끌기 작업을 사용하도록 설정하려면  
  
1.  <xref:System.Windows.Forms.RichTextBox> 컨트롤의 <xref:System.Windows.Forms.RichTextBox.AllowDrop%2A> 속성을 `true`로 설정합니다.  
  
2.  <xref:System.Windows.Forms.RichTextBox.DragEnter> 이벤트의 이벤트 처리기에서 코드를 작성합니다.`if` 문을 사용하여 끌고 있는 데이터가 허용되는 형식\(이 경우 텍스트\)인지 확인합니다.<xref:System.Windows.Forms.DragEventArgs.Effect%2A?displayProperty=fullName> 속성은 <xref:System.Windows.Forms.DragDropEffects> 열거형의 값 중 하나로 설정할 수 있습니다.  
  
    ```vb  
    Private Sub RichTextBox1_DragEnter(ByVal sender As Object, _   
       ByVal e As System.Windows.Forms.DragEventArgs) _   
       Handles RichTextBox1.DragEnter  
       If (e.Data.GetDataPresent(DataFormats.Text)) Then  
          e.Effect = DragDropEffects.Copy  
       Else  
          e.Effect = DragDropEffects.None  
       End If  
    End Sub  
  
    ```  
  
    ```csharp  
    private void richTextBox1_DragEnter(object sender,   
    System.Windows.Forms.DragEventArgs e)  
    {  
       if (e.Data.GetDataPresent(DataFormats.Text))   
          e.Effect = DragDropEffects.Copy;  
       else  
          e.Effect = DragDropEffects.None;  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void richTextBox1_DragEnter(System::Object ^  sender,  
          System::Windows::Forms::DragEventArgs ^  e)  
       {  
          if (e->Data->GetDataPresent(DataFormats::Text))  
             e->Effect = DragDropEffects::Copy;  
          else  
             e->Effect = DragDropEffects::None;  
       }  
    ```  
  
     \([!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 및 [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]\) 폼 생성자에 다음 코드를 추가하여 이벤트 처리기를 등록합니다.  
  
    ```csharp  
    this.richTextBox1.DragEnter += new  
        System.Windows.Forms.DragEventHandler  
        (this.richTextBox1_DragEnter);  
    ```  
  
    ```cpp  
    this->richTextBox1->DragEnter += gcnew  
       System::Windows::Forms::DragEventHandler  
       (this, &Form1::richTextBox1_DragEnter);  
    ```  
  
3.  <xref:System.Windows.Forms.RichTextBox.DragDrop> 이벤트를 처리할 코드를 작성합니다.<xref:System.Windows.Forms.DataObject.GetData%2A?displayProperty=fullName> 메서드를 사용하여 끌고 있는 데이터를 검색합니다.  
  
     아래 예제에서 코드는 <xref:System.Windows.Forms.RichTextBox> 컨트롤의 <xref:System.Windows.Forms.RichTextBox.Text%2A> 속성을 끌고 있는 데이터와 같도록 설정합니다.<xref:System.Windows.Forms.RichTextBox> 컨트롤에 이미 텍스트가 있는 경우에는 끌어온 텍스트가 삽입 지점에 삽입됩니다.  
  
    ```vb  
    Private Sub RichTextBox1_DragDrop(ByVal sender As Object, _   
       ByVal e As System.Windows.Forms.DragEventArgs) _   
       Handles RichTextBox1.DragDrop  
       Dim i As Int16   
       Dim s As String  
  
       ' Get start position to drop the text.  
       i = RichTextBox1.SelectionStart  
       s = RichTextBox1.Text.Substring(i)  
       RichTextBox1.Text = RichTextBox1.Text.Substring(0, i)  
  
       ' Drop the text on to the RichTextBox.  
       RichTextBox1.Text = RichTextBox1.Text + _  
          e.Data.GetData(DataFormats.Text).ToString()  
       RichTextBox1.Text = RichTextBox1.Text + s  
    End Sub  
  
    ```  
  
    ```csharp  
    private void richTextBox1_DragDrop(object sender,   
    System.Windows.Forms.DragEventArgs e)  
    {  
       int i;  
       String s;  
  
       // Get start position to drop the text.  
       i = richTextBox1.SelectionStart;  
       s = richTextBox1.Text.Substring(i);  
       richTextBox1.Text = richTextBox1.Text.Substring(0,i);  
  
       // Drop the text on to the RichTextBox.  
       richTextBox1.Text = richTextBox1.Text +   
          e.Data.GetData(DataFormats.Text).ToString();  
       richTextBox1.Text = richTextBox1.Text + s;  
    }  
  
    ```  
  
    ```cpp  
    private:  
       System::Void richTextBox1_DragDrop(System::Object ^  sender,  
          System::Windows::Forms::DragEventArgs ^  e)  
       {  
          int i;  
          String ^s;  
  
       // Get start position to drop the text.  
       i = richTextBox1->SelectionStart;  
       s = richTextBox1->Text->Substring(i);  
       richTextBox1->Text = richTextBox1->Text->Substring(0,i);  
  
       // Drop the text on to the RichTextBox.  
       String ^str = String::Concat(richTextBox1->Text, e->Data  
       ->GetData(DataFormats->Text)->ToString());   
       richTextBox1->Text = String::Concat(str, s);  
       }  
    ```  
  
     \([!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 및 [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]\) 폼 생성자에 다음 코드를 추가하여 이벤트 처리기를 등록합니다.  
  
    ```csharp  
    this.richTextBox1.DragDrop += new  
        System.Windows.Forms.DragEventHandler  
        (this.richTextBox1_DragDrop);  
  
    ```  
  
    ```cpp  
    this->richTextBox1->DragDrop += gcnew   
       System::Windows::Forms::DragEventHandler  
       (this, &Form1::richTextBox1_DragDrop);  
    ```  
  
### 응용 프로그램에서 끌어서 놓기 기능을 테스트하려면  
  
1.  응용 프로그램을 저장하고 빌드합니다. 응용 프로그램이 실행되는 동안 워드패드를 실행합니다.  
  
     워드패드는 끌어서 놓기 작업을 허용하는 Windows에 설치된 텍스트 편집기입니다.**시작** 단추를 클릭하고 **실행**을 선택한 다음 **실행** 대화 상자의 텍스트 상자에 `WordPad`를 입력하고 **확인**을 클릭하면 액세스할 수 있습니다.  
  
2.  워드패드가 열리면 텍스트 문자열을 입력합니다. 마우스를 사용하여 텍스트를 선택한 다음 Windows 응용 프로그램의 <xref:System.Windows.Forms.RichTextBox> 컨트롤 위로 선택한 텍스트를 끕니다.  
  
     <xref:System.Windows.Forms.RichTextBox> 컨트롤을 마우스로 가리키면\(결과적으로 <xref:System.Windows.Forms.RichTextBox.DragEnter> 이벤트 발생\) 마우스 포인터가 바뀌고 선택한 텍스트를 <xref:System.Windows.Forms.RichTextBox> 컨트롤로 끌 수 있습니다.  
  
     마우스 단추를 놓으면 선택한 텍스트가 놓이고\(즉, <xref:System.Windows.Forms.RichTextBox.DragDrop> 이벤트 발생\) <xref:System.Windows.Forms.RichTextBox> 컨트롤 내에 삽입됩니다.  
  
## 참고 항목  
 <xref:System.Windows.Forms.RichTextBox>   
 [방법: 응용 프로그램 간에 끌어서 놓기 작업 수행](../../../../docs/framework/winforms/advanced/how-to-perform-drag-and-drop-operations-between-applications.md)   
 [RichTextBox 컨트롤](../../../../docs/framework/winforms/controls/richtextbox-control-windows-forms.md)   
 [Windows Forms에 사용할 수 있는 컨트롤](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)