---
title: "&lt;remarks&gt;(C# 프로그래밍 가이드) | Microsoft 문서"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- remarks
- <remarks>
dev_langs:
- CSharp
helpviewer_keywords:
- remarks C# XML tag
- <remarks> C# XML tag
ms.assetid: f8641391-31f3-4735-af7a-c502a5b6a251
caps.latest.revision: 15
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
ms.openlocfilehash: 4d830e5df5af7d2c50cbf1501cbed67d1a0ffdad
ms.lasthandoff: 03/13/2017

---
# <a name="ltremarksgt-c-programming-guide"></a>&lt;remarks&gt;(C# 프로그래밍 가이드)
## <a name="syntax"></a>구문  
  
```  
<remarks>description</remarks>  
```  
  
#### <a name="parameters"></a>매개 변수  
 `Description`  
 멤버에 대한 설명입니다.  
  
## <a name="remarks"></a>주의  
 \<remarks> 태그는 형식에 대한 정보를 추가하여 [\<summary>](../../../csharp/programming-guide/xmldoc/summary.md)로 지정된 정보를 보완하기 위해 사용됩니다. 이 정보는 개체 브라우저 창에 표시됩니다.  
  
 [/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md)로 컴파일하여 문서 주석을 파일로 처리합니다.  
  
## <a name="example"></a>예제  
 [!code-cs[csProgGuideDocComments#9](../../../csharp/programming-guide/xmldoc/codesnippet/CSharp/remarks_1.cs)]  
  
## <a name="see-also"></a>참고 항목  
 [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)   
 [문서 주석에 대한 권장 태그](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)
