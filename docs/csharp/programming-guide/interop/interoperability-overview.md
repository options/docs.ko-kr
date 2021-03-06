---
title: "상호 운용성 개요(C# 프로그래밍 가이드) | Microsoft 문서"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- COM interop
- C# language, interoperability
- C++ Interop
- interoperability, about interoperability
- platform invoke
ms.assetid: c025b2e0-2357-4c27-8461-118f0090aeff
caps.latest.revision: 43
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: b1b6d5bf9943c5826685b9cc72c79187c7f51364
ms.lasthandoff: 03/13/2017

---
# <a name="interoperability-overview-c-programming-guide"></a>상호 운용성 개요(C# 프로그래밍 가이드)
이 항목에서는 C# 관리 코드와 비관리 코드 간의 상호 운용성을 사용하도록 설정하는 방법을 설명합니다.  
  
## <a name="platform-invoke"></a>플랫폼 호출  
 *플랫폼 호출*은 Microsoft Win32 API의 함수와 같이 DLL(동적 연결 라이브러리)에서 구현된 관리되지 않는 함수를 관리 코드가 호출할 수 있도록 하는 서비스입니다. 이 서비스는 내보낸 함수를 찾아서 호출하고 필요에 따라 상호 운용 경계를 가로질러 인수(정수, 문자열, 배열, 구조체 등)를 마샬링합니다.  
  
 자세한 내용은 [관리되지 않는 DLL 함수 사용](http://msdn.microsoft.com/library/eca7606e-ebfb-4f47-b8d9-289903fdc045) 및 [방법: 플랫폼 호출을 사용하여 웨이브 파일 재생](../../../csharp/programming-guide/interop/how-to-use-platform-invoke-to-play-a-wave-file.md)을 참조하세요.  
  
> [!NOTE]
>  CLR([공용 언어 런타임](http://msdn.microsoft.com/library/059a624e-f7db-4134-ba9f-08b676050482))은 시스템 리소스에 대한 액세스를 관리합니다. CLR 외부에 있는 비관리 코드를 호출하면 이 보안 메커니즘을 우회하므로 보안 위험이 제기됩니다. 예를 들어 비관리 코드는 CLR 보안 메커니즘을 우회하여 비관리 코드의 리소스를 직접 호출할 수 있습니다. 자세한 내용은 [.NET Framework 보안](http://go.microsoft.com/fwlink/?LinkId=37122)을 참조하세요.  
  
## <a name="c-interop"></a>C++ Interop  
 C# 또는 다른 .NET Framework 언어로 작성된 코드에서 사용할 수 있도록 IJW(It Just Works)라고도 하는 C++ interop를 사용하여 네이티브 C++ 클래스를 래핑할 수 있습니다. 이렇게 하려면 C++ 코드를 작성하여 네이티브 DLL 또는 COM 구성 요소를 래핑합니다. 다른 .NET Framework 언어와 달리 [!INCLUDE[vcprvc](../../../csharp/programming-guide/interop/includes/vcprvc_md.md)]에는 관리 코드와 비관리 코드가 동일한 응용 프로그램 및 동일한 파일에 있을 수 있도록 하는 상호 운용성 지원이 있습니다. 그런 다음 **/clr** 컴파일러 스위치로 관리되는 어셈블리를 생성하여 C++ 코드를 빌드합니다. 마지막으로, C# 프로젝트의 어셈블리에 대한 참조를 추가하고 다른 관리되는 클래스를 사용하는 것처럼 래핑된 개체를 사용합니다.  
  
## <a name="exposing-com-components-to-c"></a>C에 COM 구성 요소 노출#  
 C# 프로젝트에서 COM 구성 요소를 사용할 수 있습니다. 일반적인 단계는 다음과 같습니다.  
  
1.  COM 구성 요소를 찾아서 사용하고 등록합니다. regsvr32.exe를 사용하여 COM DLL을 등록하거나 등록을 취소합니다.  
  
2.  COM 구성 요소 또는 형식 라이브러리에 대한 참조를 프로젝트에 추가합니다.  
  
     참조를 추가하면 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]에서 형식 라이브러리를 입력으로 사용하는 [Tlbimp.exe(형식 라이브러리 가져오기)](http://msdn.microsoft.com/library/ec0a8d63-11b3-4acd-b398-da1e37e97382)를 통해 .NET Framework interop 어셈블리를 출력합니다. RCW(런타임 호출 가능 래퍼)라고도 하는 어셈블리는 형식 라이브러리에 있는 인터페이스 및 COM 클래스를 래핑하는 인터페이스 및 관리되는 클래스를 포함합니다. [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]에서 생성된 어셈블리에 대한 참조를 프로젝트에 추가합니다.  
  
3.  RCW에서 정의된 클래스의 인스턴스를 만듭니다. 그러면 COM 개체의 인스턴스가 생성됩니다.  
  
4.  다른 관리되는 개체와 동일한 방식으로 개체를 사용합니다. 개체가 가비지 수집에 의해 회수되면 COM 개체 인스턴스도 메모리에서 해제됩니다.  
  
 자세한 내용은 [.NET Framework에 COM 구성 요소 노출](http://msdn.microsoft.com/library/e78b14f1-e487-43cd-9c6d-1a07483f1730)을 참조하세요.  
  
## <a name="exposing-c-to-com"></a>COM에 C# 노출  
 COM 클라이언트는 올바르게 노출된 C# 형식을 사용할 수 있습니다. C# 형식을 노출하는 기본 단계는 다음과 같습니다.  
  
1.  C# 프로젝트에서 Interop 특성을 추가합니다.  
  
     [!INCLUDE[csprcs](../../../csharp/includes/csprcs_md.md)] 프로젝트 속성을 수정하여 어셈블리 COM이 표시되도록 설정할 수 있습니다. 자세한 내용은 [어셈블리 정보 대화 상자](https://docs.microsoft.com/visualstudio/ide/reference/assembly-information-dialog-box)를 참조하세요.  
  
2.  COM 형식 라이브러리를 생성하고 COM 사용을 위해 등록합니다.  
  
     COM interop에 대해 C# 어셈블리를 자동으로 등록하도록 [!INCLUDE[csprcs](../../../csharp/includes/csprcs_md.md)] 프로젝트 속성을 수정할 수 있습니다. [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]에서는 [Regasm.exe(어셈블리 등록 도구)](http://msdn.microsoft.com/library/e190e342-36ef-4651-a0b4-0e8c2c0281cb)를 사용하며, 관리되는 어셈블리를 입력으로 사용하는 `/tlb` 명령줄 스위치를 통해 형식 라이브러리를 생성합니다. 이 형식 라이브러리는 어셈블리의 `public` 형식을 설명하고, COM 클라이언트가 관리되는 클래스를 만들 수 있도록 레지스트리 항목을 추가합니다.  
  
 자세한 내용은 [.NET Framework 구성 요소를 COM에 노출](http://msdn.microsoft.com/library/e42a65f7-1e61-411f-b09a-aca1bbce24c6) 및 [예제 COM 클래스](../../../csharp/programming-guide/interop/example-com-class.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Interop 성능 향상](http://go.microsoft.com/fwlink/?LinkId=99564)   
 [COM Interop 소개](http://go.microsoft.com/fwlink/?LinkId=112406)   
 [관리 코드와 비관리 코드 간의 마샬링](http://go.microsoft.com/fwlink/?LinkId=112398)   
 [비관리 코드와의 상호 운용](https://msdn.microsoft.com/library/sd10k43k)   
 [고급 COM 상호 운용성](http://msdn.microsoft.com/en-us/3ada36e5-2390-4d70-b490-6ad8de92f2fb)   
 [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)
