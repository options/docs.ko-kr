---
title: "/nostdlib (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/nostdlib"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "nostdlib compiler option [C#]"
  - "-nostdlib compiler option [C#]"
  - "/nostdlib compiler option [C#]"
ms.assetid: ec197989-fa49-4725-a455-e06b551eb65f
caps.latest.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 18
---
# /nostdlib (C# Compiler Options)
**\/nostdlib**를 사용하면 전체 시스템 네임스페이스를 정의하는 mscorlib.dll을 가져올 수 없습니다.  
  
## 구문  
  
```  
/nostdlib[+ | -]  
```  
  
## 설명  
 고유한 시스템 네임스페이스와 개체를 정의하거나 만들려면 이 옵션을 사용합니다.  
  
 **\/nostdlib**를 지정하지 않으면 mscorlib.dll을 프로그램으로 가져옵니다\(**\/nostdlib\-** 지정과 동일함\).**\/nostdlib**를 지정하는 것은 **\/nostdlib\+**를 지정하는 것과 같습니다.  
  
### Visual Studio 개발 환경에서 이 컴파일러 옵션을 설정하려면  
  
1.  프로젝트의 **속성** 페이지를 엽니다.  
  
2.  **빌드** 속성 페이지를 클릭합니다.  
  
3.  **고급** 단추를 클릭합니다.  
  
4.  **mscorlib.dll을 참조하지 않음** 속성을 수정합니다.  
  
 이 컴파일러 옵션을 프로그래밍 방식으로 설정하는 방법에 대한 자세한 내용은 <xref:VSLangProj80.CSharpProjectConfigurationProperties3.NoStdLib%2A>을 참조하세요.  
  
## 참고 항목  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)