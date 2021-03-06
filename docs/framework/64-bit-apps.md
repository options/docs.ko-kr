---
title: "64비트 응용 프로그램 | Microsoft Docs"
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
  - "64비트 응용 프로그램[C++]"
  - "64비트 프로그래밍[C++]"
  - "응용 프로그램[C++], 64비트"
ms.assetid: fd4026bc-2c3d-4b27-86dc-ec5e96018181
caps.latest.revision: 53
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 53
---
# 64비트 응용 프로그램
응용 프로그램을 컴파일할 때 Windows 64비트 운영 체제에서 네이티브 응용 프로그램으로 실행되거나 WOW64\(Windows 64비트 기반 Windows 32비트\)를 통해 실행되도록 지정할 수 있습니다.  WOW64는 32비트 응용 프로그램이 64비트 시스템에서 실행되도록 하는 호환성 환경입니다.  WOW64는 Windows 운영 체제의 모든 64비트 버전에 포함됩니다.  
  
## Windows에서 32비트 응용 프로그램과 64비트 응용 프로그램의 실행 비교  
 .NET Framework 1.0 또는 1.1에서 빌드된 모든 응용 프로그램은 64비트 운영 체제에서 32비트 응용 프로그램으로 처리되고 항상 WOW64 및 32비트 CLR\(공용 언어 런타임\)을 통해 실행됩니다.  [!INCLUDE[net_v40_long](../../includes/net-v40-long-md.md)] 이상 버전에서 빌드된 32비트 응용 프로그램은 64비트 시스템에서 WOW64를 통해 실행됩니다.  
  
 Visual Studio에서는 32비트 버전의 CLR을 x86 컴퓨터에 설치하고 32비트 버전 및 해당하는 64비트 버전의 CLR을 64비트 Windows 컴퓨터에 설치합니다.  Visual Studio는 32비트 응용 프로그램이므로 64비트 시스템에 설치될 때 WOW64를 통해 실행됩니다.  
  
> [!NOTE]
>  Itanium 프로세서 제품군용 x86 에뮬레이션 및 WOW64 하위 시스템의 설계 때문에 응용 프로그램은 한 프로세서에서 실행되도록 제한됩니다.  이들 요소 때문에 Itanium 기반 시스템에서 실행되는 32비트 .NET Framework 응용 프로그램의 성능과 확장성이 감소합니다.  성능과 확장성을 높이려면 Itanium 기반 시스템에 대한 네이티브 64비트 지원이 포함된 [!INCLUDE[net_v40_long](../../includes/net-v40-long-md.md)]을\(를\) 사용하는 것이 좋습니다.  
  
 기본적으로 64비트 관리되는 응용 프로그램을 64비트 Windows 운영 체제에서 실행할 때 2GB 이하 개체를 만들 수 있습니다.  그러나 [!INCLUDE[net_v45](../../includes/net-v45-md.md)]에서는 이 제한을 늘릴 수 있습니다.  자세한 내용은 [\<gcAllowVeryLargeObjects\> 요소](../../docs/framework/configure-apps/file-schema/runtime/gcallowverylargeobjects-element.md)를 참조하세요.  
  
 대부분 어셈블리는 32비트 CLR 및 64비트 CLR에서 둘 다 똑같이 실행됩니다.  그러나 일부 응용 프로그램은 다음의 하나 이상을 포함할 경우 CLR에 따라 다르게 동작할 수 있습니다.  
  
-   포인터 형식과 같이 플랫폼에 따라 크기가 달라지는 멤버를 포함하는 구조체.  
  
-   상수 크기를 포함하는 포인터 산술 연산  
  
-   핸들에 대해 `Int32` 대신 `IntPtr`를 사용하는 잘못된 플랫폼 호출 또는 COM 선언  
  
-   `IntPtr`을 `Int32`로 캐스팅하는 코드.  
  
 64비트 CLR에서 실행되도록 32비트 응용 프로그램을 이식하는 방법에 대한 자세한 내용은 MSDN Library에서 [32비트 관리 코드를 64비트로 마이그레이션\(영문\)](http://go.microsoft.com/fwlink/?LinkId=150542)을 참조하세요.  
  
## 일반 64비트 프로그래밍 정보  
 64비트 프로그래밍에 대한 일반적인 정보는 다음 문서를 참조하세요.  
  
-   64비트 Windows 컴퓨터의 64비트 버전 CLR에 대한 자세한 내용은 MSDN 웹 사이트에서 [.NET Framework 개발자 센터](http://go.microsoft.com/fwlink/?LinkId=37079)를 참조하세요.  
  
-   [!INCLUDE[winsdkshort](../../includes/winsdkshort-md.md)] 설명서에서 [64비트 Windows 프로그래밍 가이드\(영문\)](http://go.microsoft.com/fwlink/p/?LinkId=253512)를 참조하세요.  
  
-   64비트 버전 CLR을 다운로드하는 방법에 대한 자세한 내용은 MSDN 웹 사이트에서 [.NET Framework 개발자 센터](http://go.microsoft.com/fwlink/?LinkId=50953)를 참조하세요.  
  
-   64비트 응용 프로그램을 만들기 위한 Visual Studio 지원에 대한 자세한 내용은 [Visual Studio IDE 64비트 지원](../Topic/Visual%20Studio%20IDE%2064-Bit%20Support.md)을 참조하세요.  
  
## 64비트 응용 프로그램을 만들기 위한 컴파일러 지원  
 기본적으로 .NET Framework를 사용하여 32비트 또는 64비트 컴퓨터에서 응용 프로그램을 빌드할 때 응용 프로그램은 64비트 컴퓨터에서 WOW64를 통해서가 아니라 네이티브 응용 프로그램으로 실행됩니다.  다음 표에는 Visual Studio 컴파일러를 사용하여 네이티브로 실행되거나, WOW64를 통해 실행되거나, 실행에 두 방법을 모두 사용하는 64비트 응용 프로그램을 만드는 방법을 설명하는 문서가 나와 있습니다.  
  
|컴파일러|컴파일러 옵션|  
|----------|-------------|  
|Visual Basic|[\/platform](../Topic/-platform%20\(Visual%20Basic\).md)|  
|Visual C\#|[\/platform \(Specify Output Platform\)](../Topic/-platform%20\(C%23%20Compiler%20Options\).md)|  
|Visual C\+\+|**\/clr:safe**를 사용하여 플랫폼 제약 없는 MSIL\(Microsoft intermediate language\) 응용 프로그램을 만들 수 있습니다.  자세한 내용은 [\/clr\(공용 언어 런타임 컴파일\)](../Topic/-clr%20\(Common%20Language%20Runtime%20Compilation\).md)을 참조하세요.<br /><br /> Visual C\+\+에는 각 64비트 운영 체제에 대한 별도의 컴파일러가 포함됩니다.  Visual C\+\+를 사용하여 64비트 Windows 운영 체제에서 실행되는 네이티브 응용 프로그램을 만드는 방법에 대한 자세한 내용은 [64비트 프로그래밍](http://msdn.microsoft.com/library/h2k70f3s\(v=vs.80\))을 참조하세요.|  
  
## .exe 파일 또는 .dll 파일 상태 확인  
 .exe 파일이나 .dll 파일을 특정 플랫폼 또는 WOW64에서만 실행해야 하는지를 확인하려면 [CorFlags.exe\(CorFlags 변환 도구\)](../../docs/framework/tools/corflags-exe-corflags-conversion-tool.md)를 옵션 없이 사용합니다.  CorFlags.exe를 사용하여 .exe 파일이나 .dll 파일의 플랫폼 상태를 변경할 수도 있습니다.  Visual Studio 어셈블리의 CLR 헤더에서 주 런타임 버전은 2로 설정되고 부 런타임 버전 번호는 5로 설정됩니다.  부 런타임 버전이 0으로 설정된 응용 프로그램은 레거시 응용 프로그램으로 처리되고 항상 WOW64를 통해 실행됩니다.  
  
 .exe 또는 .dll을 프로그래밍 방식으로 쿼리하여 특정 플랫폼 또는 WOW64에서만 실행해야 하는지를 확인하려면 <xref:System.Reflection.Module.GetPEKind%2A?displayProperty=fullName> 메서드를 사용합니다.