---
title: "Message Security 샘플 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 82444166-6288-493a-85d4-85f43f134d19
caps.latest.revision: 33
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 33
---
# Message Security 샘플
이 샘플에서는 `basicHttpBinding` 및 메시지 보안을 사용하는 응용 프로그램을 구현하는 방법을 보여 줍니다.이 샘플은 계산기 서비스를 구현하는 [시작](../../../../docs/framework/wcf/samples/getting-started-sample.md)을 기반으로 합니다.  
  
> [!NOTE]
>  이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.  
  
 `basicHttpBinding`의 보안 모드는 `Message`, `Transport`, `TransportWithMessageCredential`, `TransportCredentialOnly` 및 `None` 등의 값으로 설정할 수 있습니다.다음 샘플 서비스 App.config 파일에서 끝점 정의는 `basicHttpBinding`을 지정하며, 다음 샘플 구성에서 보여 주는 것처럼 `Binding1`이라는 바인딩 구성을 참조합니다.  
  
```  
<system.serviceModel>  
  <services>  
    <service name="Microsoft.ServiceModel.Samples.CalculatorService"  
             behaviorConfiguration="CalculatorServiceBehavior">  
     <!-- This endpoint is exposed at the base address provided by -->  
     <!-- host: http://localhost:8000/ServiceModelSamples/service.-->  
     <endpoint address=""  
               binding="basicHttpBinding"  
               bindingConfiguration="Binding1"   
               contract="Microsoft.ServiceModel.Samples.ICalculator" />  
    </service>  
  </services>   …  
</system.serviceModel>  
```  
  
 다음 샘플 구성에서 보여 주는 것처럼 바인딩 구성에서는 [\<security\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-basichttpbinding.md)의 `mode` 특성을 `Message`로 설정하고 [\<message\>](../../../../docs/framework/configure-apps/file-schema/wcf/message-of-basichttpbinding.md)의 `clientCredentialType` 특성을 `Certificate`로 설정합니다.  
  
```  
<bindings>  
  <basicHttpBinding>  
    <!--   
        This configuration defines the SecurityMode as Message and   
        the clientCredentialType as Certificate.  
        -->  
    <binding name="Binding1" >  
      <security mode = "Message">  
        <message clientCredentialType="Certificate"/>  
      </security>  
    </binding>  
  </basicHttpBinding>  
</bindings>  
```  
  
 서비스가 클라이언트에게 자신을 인증하는 데 사용하는 인증서는 구성 파일의 behaviors 섹션에 있는 `serviceCredentials` 요소 아래에 설정됩니다.클라이언트가 서비스에 자신을 인증하는 데 사용하는 인증서에 적용되는 유효성 검사 모드 또한 behaviors 섹션에서 `clientCertificate` 요소 아래에 설정됩니다.  
  
```  
<!--For debugging purposes, set the includeExceptionDetailInFaults attribute to true.-->  
<behaviors>  
  <serviceBehaviors>  
    <behavior name="CalculatorServiceBehavior">  
      <serviceMetadata httpGetEnabled="True"/>  
      <serviceDebug includeExceptionDetailInFaults="False" />  
      <!--The serviceCredentials behavior allows one to define a -->  
      <!--service certificate. A service certificate is used by a -->  
      <!--client to authenticate the service and provide message -->  
      <!-- protection. This configuration references the "localhost"-->  
      <!--certificate installed during the setup instructions. -->  
      <serviceCredentials>  
        <serviceCertificate findValue="localhost"  
               storeLocation="LocalMachine"   
               storeName="My" x509FindType="FindBySubjectName" />  
        <clientCertificate>  
          <!-- Setting the certificateValidationMode to -->  
          <!-- PeerOrChainTrust means that if the certificate -->  
          <!--is in the user's Trusted People store, then it is -->  
          <!-- trusted without performing a validation of the -->  
          <!-- certificate's issuer chain. This setting is used -->  
          <!-- here for convenience so that the sample can be run -->  
          <!-- without having to have certificates issued by a -->  
          <!-- certification authority (CA). -->  
          <!-- This setting is less secure than the default, -->  
          <!-- ChainTrust. The security implications of this -->  
          <!-- setting should be carefully considered before using -->  
          <!-- PeerOrChainTrust in production code. -->  
          <authentication   
                       certificateValidationMode="PeerOrChainTrust" />  
        </clientCertificate>  
      </serviceCredentials>  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
 동일한 바인딩 및 보안 세부 정보가 클라이언트 구성 파일에 지정됩니다.  
  
 호출자의 ID는 다음 코드를 사용하여 서비스 콘솔 창에 표시됩니다.  
  
```  
Console.WriteLine("Called by {0}", ServiceSecurityContext.Current.PrimaryIdentity.Name);  
```  
  
 샘플을 실행하면 작업 요청 및 응답이 클라이언트 콘솔 창에 표시됩니다.클라이언트를 종료하려면 클라이언트 창에서 Enter 키를 누릅니다.  
  
```  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
Press <ENTER> to terminate client.  
```  
  
### 샘플을 설치하고 빌드하려면  
  
1.  [Windows Communication Foundation 샘플의 일회 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행했는지 확인합니다.  
  
2.  C\# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Windows Communication Foundation 샘플 빌드](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.  
  
### 단일 컴퓨터 구성에서 샘플을 실행하려면  
  
1.  샘플 설치 폴더에서 Setup.bat를 실행하여샘플 실행에 필요한 모든 인증서를 설치합니다.  
  
    > [!NOTE]
    >  Setup.bat 배치 파일은 Windows SDK 명령 프롬프트에서 실행되도록 디자인되었습니다.MSSDK 환경 변수는 SDK가 설치되는 디렉터리를 가리켜야 합니다.이 환경 변수는 Windows SDK 명령 프롬프트 내에서 자동으로 설정됩니다.  
  
2.  \\service\\bin에서 서비스 응용 프로그램을 실행합니다.  
  
3.  \\client\\bin에서 클라이언트 응용 프로그램을 실행합니다.클라이언트 콘솔 응용 프로그램에 클라이언트 동작이 표시됩니다.  
  
4.  클라이언트와 서비스가 통신할 수 없는 경우 [Troubleshooting Tips](http://msdn.microsoft.com/ko-kr/8787c877-5e96-42da-8214-fa737a38f10b)을 참조하십시오.  
  
5.  샘플 사용을 마치면 Cleanup.bat를 실행하여 인증서를 제거합니다.다른 보안 샘플에도 동일한 인증서가 사용됩니다.  
  
### 다중 컴퓨터 구성에서 샘플을 실행하려면  
  
1.  서비스 컴퓨터에 서비스 이진 파일용 디렉터리를 만듭니다.  
  
2.  서비스 프로그램 파일을 서버의 서비스 디렉터리에 복사합니다.Setup.bat, Cleanup.bat 및 ImportClientCert.bat 파일도 서버에 복사합니다.  
  
3.  클라이언트 컴퓨터에 클라이언트 이진 파일용 디렉터리를 만듭니다.  
  
4.  클라이언트 프로그램 파일을 클라이언트 컴퓨터의 클라이언트 디렉터리로 복사합니다.Setup.bat, Cleanup.bat 및 ImportServiceCert.bat 파일도 클라이언트로 복사합니다.  
  
5.  서버에서 `setup.bat service`를 실행합니다.`service` 인수를 사용하여 `setup.bat`를 실행하면 컴퓨터의 정규화된 도메인 이름이 지정된 서비스 인증서가 생성되어 Service.cer이라는 파일로 내보내집니다.  
  
6.  컴퓨터의 정규화된 도메인 이름과 같은 새 인증서 이름\([\<serviceCertificate\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md) 요소의 `findValue` 특성에 있음\)이 반영되도록 Service.exe.config를 편집합니다.또한 기본 주소 값을 변경하여 localhost 대신 정규화된 컴퓨터 이름을 지정합니다.`.`  
  
7.  서비스 디렉터리에서 클라이언트 컴퓨터의 클라이언트 디렉터리로 Service.cer 파일을 복사합니다.  
  
8.  클라이언트에서 `setup.bat client`를 실행합니다.`client` 인수를 사용하여 `setup.bat`를 실행하면 client.com이라는 클라이언트 인증서가 만들어져 Client.cer이라는 파일로 내보내집니다.  
  
9. 클라이언트 컴퓨터의 Client.exe.config 파일에서 끝점의 주소 값을 서비스의 새 주소와 일치하도록 변경합니다.이 작업을 수행하려면 localhost를 서버의 정규화된 도메인 이름으로 바꿉니다.또한 [\<defaultCertificate\>](../../../../docs/framework/configure-apps/file-schema/wcf/defaultcertificate-element.md)의 `findValue` 특성을 서버의 정규화된 도메인 이름인 새 서비스 인증서 이름으로 변경합니다.  
  
10. 클라이언트 디렉터리에서 서버의 서비스 디렉터리로 Client.cer 파일을 복사합니다.  
  
11. 클라이언트에서 ImportServiceCert.bat를 실행합니다.이 작업은 Service.cer 파일의 서비스 인증서를 CurrentUser \- TrustedPeople 저장소로 가져옵니다.  
  
12. 서버에서 ImportClientCert.bat를 실행하여 Client.cer 파일에서 LocalMachine \- TrustedPeople 저장소로 클라이언트 인증서를 가져옵니다.  
  
13. 서비스 컴퓨터의 명령 프롬프트에서 Service.exe를 실행합니다.  
  
14. 클라이언트 컴퓨터의 명령 프롬프트 창에서 Client.exe를 실행합니다.  
  
    1.  클라이언트와 서비스가 통신할 수 없는 경우 [Troubleshooting Tips](http://msdn.microsoft.com/ko-kr/8787c877-5e96-42da-8214-fa737a38f10b)을 참조하십시오.  
  
### 샘플 실행 후 정리를 수행하려면  
  
-   샘플 실행을 완료했으면 샘플 폴더에서 Cleanup.bat를 실행합니다.  
  
    > [!NOTE]
    >  다중 컴퓨터 구성에서 이 샘플을 실행할 경우에는 이 스크립트로 서비스 인증서를 제거할 수 없습니다.다중 컴퓨터 구성의 인증서를 사용하는 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 샘플을 실행한 경우 CurrentUser \- TrustedPeople 저장소에 설치된 서비스 인증서를 지워야 합니다.이를 수행하려면 `certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>` 명령을 사용합니다\(예: `certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`\).  
  
> [!IMPORTANT]
>  컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다.계속하기 전에 다음\(기본\) 디렉터리를 확인하십시오.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  이 디렉터리가 없으면 [Windows Communication Foundation \(WCF\) and Windows Workflow Foundation \(WF\) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780)로 이동하여 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 모두 다운로드하십시오.이 샘플은 다음 디렉터리에 있습니다.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\Basic\MessageSecurity`  
  
## 참고 항목