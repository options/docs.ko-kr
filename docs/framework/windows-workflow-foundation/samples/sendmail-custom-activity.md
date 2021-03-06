---
title: "SendMail 사용자 지정 활동 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 947a9ae6-379c-43a3-9cd5-87f573a5739f
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# SendMail 사용자 지정 활동
이 샘플에서는 워크플로 응용 프로그램 내에서 사용하기 위해 <xref:System.Activities.AsyncCodeActivity>로부터 파생되는 사용자 지정 활동을 만들어 SMTP를 사용하여 메일을 보내는 방법을 보여 줍니다.사용자 지정 활동은 <xref:System.Net.Mail.SmtpClient>의 기능을 사용하여 전자 메일을 비동기적으로 보내고 인증된 메일을 보냅니다.또한 테스트 모드, 토큰 바꾸기, 파일 템플릿 및 테스트 드롭 경로와 같은 몇 가지 최종 사용자 기능도 제공합니다.  
  
 다음 표에서는 `SendMail` 활동의 인수에 대해 자세히 설명합니다.  
  
||||  
|-|-|-|  
|이름|형식|설명|  
|Host|String|SMTP 서버 호스트의 주소입니다.|  
|Port|String|호스트에 있는 SMTP 서비스의 포트입니다.|  
|EnableSsl|bool|<xref:System.Net.Mail.SmtpClient>에서 SSL\(Secure Sockets Layer\)을 사용하여 연결을 암호화할지 여부를 지정합니다.|  
|UserName|String|보낸 사람의 <xref:System.Net.Mail.SmtpClient.Credentials%2A> 속성을 인증하는 자격 증명을 설정할 사용자 이름입니다.|  
|Password|String|보낸 사람의 <xref:System.Net.Mail.SmtpClient.Credentials%2A> 속성을 인증하는 자격 증명을 설정할 암호입니다.|  
|Subject|<xref:System.Activities.InArgument%601>\<string\>|메시지 제목입니다.|  
|Body|<xref:System.Activities.InArgument%601>\<string\>|메시지 본문입니다.|  
|Attachments|<xref:System.Activities.InArgument%601>\<string\>|이 전자 메일 메시지에 첨부된 데이터를 저장하는 데 사용되는 첨부 파일 컬렉션입니다.|  
|From|<xref:System.Net.Mail.MailAddress>|이 전자 메일 메시지의 보낸 사람 주소입니다.|  
|To|<xref:System.Activities.InArgument%601>\<<xref:System.Net.Mail.MailAddressCollection>\>|이 전자 메일 메시지의 받는 사람이 들어 있는 주소 컬렉션입니다.|  
|CC|<xref:System.Activities.InArgument%601>\<<xref:System.Net.Mail.MailAddressCollection>\>|이 전자 메일 메시지의 CC\(참조\)를 받는 사람이 들어 있는 주소 컬렉션입니다.|  
|BCC|<xref:System.Activities.InArgument%601>\<<xref:System.Net.Mail.MailAddressCollection>\>|이 전자 메일 메시지의 BCC\(숨은 참조\)를 받는 사람이 들어 있는 주소 컬렉션입니다.|  
|Tokens|<xref:System.Activities.InArgument%601>\<IDictionary\<string, string\>\>|본문에서 바꿀 토큰입니다.사용자는 이 기능을 통해 나중에 이 속성을 사용하여 제공된 토큰으로 바꿀 수 있는 일부 값을 본문에 지정할 수 있습니다.|  
|BodyTemplateFilePath|String|본문에 대한 템플릿의 경로입니다.`SendMail` 활동은 이 파일의 내용을 본문 속성에 복사합니다.<br /><br /> 템플릿에는 토큰 속성의 내용으로 바뀌는 토큰이 포함될 수 있습니다.|  
|TestMailTo|<xref:System.Net.Mail.MailAddress>|이 속성이 설정되면 모든 전자 메일은 속성에 지정된 주소로 보내집니다.<br /><br /> 이 속성은 워크플로를 테스트할 때 사용할 수 있습니다.예를 들어 받는 사람에게 실제로 보내지는 않고 모든 전자 메일이 보내지는지 확인하려는 경우 사용할 수 있습니다.|  
|TestDropPath|String|이 속성이 설정되면 모든 전자 메일은 지정된 파일에도 저장됩니다.<br /><br /> 이 속성은 보내는 전자 메일의 형식과 내용이 적합하지 확인하기 위해 워크플로를 테스트할 때나 디버그할 때 사용할 수 있습니다.|  
  
## 솔루션 개념  
 솔루션에는 두 개의 프로젝트가 포함되어 있습니다.  
  
|프로젝트|설명|중요한 파일|  
|----------|--------|------------|  
|SendMail|SendMail 활동|1.  SendMail.cs: 기본 활동에 대한 구현<br />2.  SendMailDesigner.xaml 및 SendMailDesigner.xaml.cs: SendMail 활동에 대한 디자이너<br />3.  MailTemplateBody.htm: 보낼 전자 메일에 대한 템플릿|  
|SendMailTestClient|SendMail 활동을 테스트할 클라이언트입니다.이 프로젝트에서는 SendMail 활동을 호출하는 두 가지 방식, 즉 선언 방식과 프로그래밍 방식을 보여 줍니다.|1.  Sequence1.xaml: SendMail 활동을 호출하는 워크플로입니다.<br />2.  Program.cs: Sequence1을 호출하고 SendMail을 사용하는 워크플로를 프로그래밍 방식으로 만듭니다.|  
  
## SendMail 활동의 추가 구성  
 샘플에는 표시되지 않지만 사용자는 SendMail 활동의 구성을 추가할 수 있습니다.다음 세 개의 섹션에서는 이를 수행하는 방법을 보여 줍니다.  
  
### 본문에 지정된 토큰을 사용하여 전자 메일 보내기  
 이 코드 조각에서는 본문에 토큰이 포함된 전자 메일을 보낼 수 있는 방법을 보여 줍니다.토큰이 본문 속성에 어떻게 제공되는지 확인합니다.해당 토큰 값은 토큰 속성에 제공됩니다.  
  
```html  
IDictionary<string, string> tokens = new Dictionary<string, string>();  
tokens.Add("@name", "John Doe");  
tokens.Add("@date", DateTime.Now.ToString());  
tokens.Add("@server", "localhost");  
  
new SendMail  
{  
    From = new LambdaValue<MailAddress>(ctx => new MailAddress("john.doe@contoso.com")),  
    To = new LambdaValue<MailAddressCollection>(  
                    ctx => new MailAddressCollection() { new MailAddress("someone@microsoft.com") }),  
    Subject = "Test email",  
    Body = "Hello @name. This is a test email sent from @server. Current date is @date",  
    Host = "localhost",  
    Port = 25,  
    Tokens = new LambdaValue<IDictionary<string, string>>(ctx => tokens)  
};  
  
```  
  
### 템플릿을 사용하여 전자 메일 보내기  
 이 조각에서는 본문의 템플릿 토큰을 사용하여 전자 메일을 보내는 방법을 보여 줍니다.`BodyTemplateFilePath` 속성을 설정할 때 Body 속성 값을 제공할 필요가 없습니다. 템플릿 파일의 내용이 본문에 복사되기 때문입니다.  
  
```  
new SendMail  
{    
    From = new LambdaValue<MailAddress>(ctx => new MailAddress("john.doe@contoso.com")),  
    To = new LambdaValue<MailAddressCollection>(  
                    ctx => new MailAddressCollection() { new MailAddress("someone@microsoft.com") }),  
    Subject = "Test email",  
    Host = "localhost",  
    Port = 25,  
    Tokens = new LambdaValue<IDictionary<string, string>>(ctx => tokens),  
    BodyTemplateFilePath = @"..\..\..\SendMail\Templates\MailTemplateBody.htm",   
};  
  
```  
  
### 테스트 모드에서 메일 보내기  
 이 코드 조각에서는 두 개의 테스트 속성을 설정하는 방법을 보여 줍니다. `TestMailTo`를 설정하면 To, Cc, Bcc 값과 관계없이 모든 메시지가 john.doe@contoso.con에게 전송되고TestDropPath를 설정하면 나가는 모든 전자 메일이 제공된 경로에도 기록됩니다.이러한 속성은 서로 관련되어 있지 않으므로 독립적으로 설정할 수 있습니다.  
  
```  
new SendMail  
{    
   From = new LambdaValue<MailAddress>(ctx => new MailAddress("john.doe@contoso.com")),  
   To = new LambdaValue<MailAddressCollection>(  
                    ctx => new MailAddressCollection() { new MailAddress("someone@microsoft.com") }),  
   Subject = "Test email",  
   Host = "localhost",  
   Port = 25,  
   Tokens = new LambdaValue<IDictionary<string, string>>(ctx => tokens),  
   BodyTemplateFilePath = @"..\..\..\SendMail\Templates\MailTemplateBody.htm",  
   TestMailTo= new LambdaValue<MailAddress>(ctx => new MailAddress("john.doe@contoso.com")),  
   TestDropPath = @"c:\Samples\SendMail\TestDropPath\",  
};  
  
```  
  
## 설치 지침  
 이 샘플을 실행하려면 SMTP 서버에 액세스해야 합니다.  
  
 SMTP 서버 설치[!INCLUDE[crabout](../../../../includes/crabout-md.md)] 다음 링크를 참조하십시오.  
  
-   [Microsoft Technet](http://go.microsoft.com/fwlink/?LinkId=166060)  
  
-   [Configuring the SMTP Service \(IIS 6.0\)](http://go.microsoft.com/fwlink/?LinkId=150456)  
  
-   [IIS 7.0: SMTP 전자 메일 구성](http://go.microsoft.com/fwlink/?LinkId=150457)  
  
-   [SMTP 서비스를 설치하는 방법](http://go.microsoft.com/fwlink/?LinkId=150458)  
  
 타사에서 제공하는 SMTP 에뮬레이터를 다운로드할 수 있습니다.  
  
##### 이 샘플을 실행하려면  
  
1.  [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)]에서 SendMail.sln 솔루션 파일을 엽니다.  
  
2.  올바른 SMTP 서버에 액세스할 수 있는 권한이 있는지 확인합니다.설치 지침을 참조하십시오.  
  
3.  서버 주소와 보낸 사람 및 받는 사람 전자 메일 주소를 사용하여 프로그램을 구성합니다.  
  
     이 샘플을 올바르게 실행하려면 Program.cs 및 Sequence.xaml에서 보낸 사람 및 받는 사람 주소와 SMTP 서버 주소를 구성해야 할 수 있습니다.프로그램은 메일을 두 가지 다른 방식으로 보내므로 두 위치에서 모두 주소를 변경해야 합니다.  
  
4.  Ctrl\+Shift\+B를 눌러 솔루션을 빌드합니다.  
  
5.  Ctrl\+F5를 눌러 솔루션을 실행합니다.  
  
> [!IMPORTANT]
>  컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다.계속하기 전에 다음\(기본\) 디렉터리를 확인하십시오.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  이 디렉터리가 없으면 [Windows Communication Foundation \(WCF\) and Windows Workflow Foundation \(WF\) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780)로 이동하여 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 모두 다운로드하십시오.이 샘플은 다음 디렉터리에 있습니다.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\SendMail`  
  
## 참고 항목