---
title: "숫자 데이터 형식 (Visual Basic) | Microsoft 문서"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- integral types, Visual Basic
- Short data type, numeric data types
- Double data type, numeric data types
- Long data type, Visual Basic numeric data types
- numbers, whole
- fractions
- numbers
- whole numbers
- integer numbers
- numbers, integer
- fractional data types
- mantissas, of fractional numbers
- mantissas
- data types [Visual Basic], numeric
- Integer data type, numeric data types
- exponent, of fractional numbers
- integers
- numeric data types, Visual Basic
- Single data type, numeric types
- Decimal data type, numeric data types
ms.assetid: a27bd4d0-7e14-43eb-9cc4-b42eaab323c9
caps.latest.revision: 25
author: dotnet-bot
ms.author: dotnetcontent
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 3c3098370b8d9dcb6aafcb06dcfb8f4e144b899a
ms.lasthandoff: 03/13/2017

---
# <a name="numeric-data-types-visual-basic"></a>숫자 데이터 형식(Visual Basic)
[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]몇 가지 제공 *숫자 데이터 형식* 다양 한 표현에서 숫자 처리할 수 있도록 합니다. *정수 계열* 형식은 나타냅니다 정수만 (양수, 음수 및&0;) 및 *비정 수 계열* 형식은 정수 부분과 소수 부분을 모두 있는 숫자를 나타냅니다.  
  
 나란히 비교를 보여 주는 표는 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 데이터 형식 참조 [데이터 형식](../../../../visual-basic/language-reference/data-types/data-type-summary.md)합니다.  
  
## <a name="integral-numeric-types"></a>정수 계열 숫자 형식  
 *정수 계열 데이터 형식* 는 소수 부분 없이 유일한 숫자를 나타냅니다.  
  
 *서명* 정수 데이터 형식이 [SByte 데이터 형식](../../../../visual-basic/language-reference/data-types/sbyte-data-type.md) (8 비트), [Short 데이터 형식](../../../../visual-basic/language-reference/data-types/short-data-type.md) (16 비트), [정수 데이터 형식](../../../../visual-basic/language-reference/data-types/integer-data-type.md) (32 비트) 및 [Long 데이터 형식](../../../../visual-basic/language-reference/data-types/long-data-type.md) (64 비트)입니다. 변수는 항상 소수 자릿수 숫자 대신 정수를 저장, 경우에 이러한 형식 중 하나로 선언 합니다.  
  
 *서명 되지 않은* 정수 계열 형식은 [Byte 데이터 형식](../../../../visual-basic/language-reference/data-types/byte-data-type.md) (8 비트), [UShort 데이터 형식](../../../../visual-basic/language-reference/data-types/ushort-data-type.md) (16 비트), [UInteger 데이터 형식](../../../../visual-basic/language-reference/data-types/uinteger-data-type.md) (32 비트) 및 [ULong 데이터 형식](../../../../visual-basic/language-reference/data-types/ulong-data-type.md) (64 비트)입니다. 이진 데이터 또는 알 수 없는 특성의 데이터를 포함 하는 변수, 경우에 이러한 형식 중 하나로 선언 합니다.  
  
### <a name="performance"></a>성능  
 산술 연산에는 다른 데이터 형식과 정수 계열 형식 보다 빠릅니다. 이들은와 가장 빠른는 `Integer` 및 `UInteger` 의 형식은 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]합니다.  
  
### <a name="large-integers"></a>큰 정수  
 보다 큰 정수를 저장 해야 하는 경우는 `Integer` 데이터 형식을 저장할 수 있는, 사용할 수는 `Long` 데이터 형식을 대신 합니다. `Long`변수는-9223372036854775808에서 9223372036854775807 까지의 숫자를 보유할 수 있습니다. 작업과 `Long` 와 보다 약간 더 느려집니다 `Integer`합니다.  
  
 이보다 훨씬 더 큰 값을 해야 하는 경우 사용할 수 있습니다는 [Decimal 데이터 형식](../../../../visual-basic/language-reference/data-types/decimal-data-type.md)합니다. 79228162514264337593543950335 79228162514264337593543950335 ~ 까지의 숫자를 보유할 수는 `Decimal` 소수 자릿수를 사용 하지 않는 경우에 변수입니다. 그러나 작업과 `Decimal` 번호는 다른 숫자 데이터 형식 보다 상당히 느립니다.  
  
### <a name="small-integers"></a>작은 정수  
 전체 범위를 필요 하지 않은 경우는 `Integer` 사용할 수 있는 데이터 형식는 `Short` -32, 768 32, 767 까지의 정수를 포함할 수 있는 데이터 형식입니다. 가장 작은 정수 범위는 `SByte` -128에서 127 까지의 정수를 저장 하는 데이터 형식입니다. 공용 언어 런타임 저장할 수 있습니다 작은 정수를 포함 하는 변수가 매우 많은 경우 프로그램 `Short` 및 `SByte` 변수 보다 효율적이 고 메모리 사용을 저장 합니다. 그러나 작업과 `Short` 및 `SByte` 는와 보다 다소 느립니다 `Integer`합니다.  
  
### <a name="unsigned-integers"></a>부호 없는 정수  
 변수는 음수를 포함할 필요가 사용할 수 있습니다 알고 있는 경우는 *부호 없는 형식*`Byte`, `UShort`, `UInteger`, 및 `ULong`합니다. 양의 정수를 크기의 두 배 해당 부호 있는 형식으로 저장할 수 있는 이러한 각 유형의 데이터 (`SByte`, `Short`, `Integer`, 및 `Long`). 성능의 측면에서 서명 되지 않은 각 유형은 해당 부호 있는 형식으로 정확 하 게 효율적입니다. 특히, `UInteger` 와 공유 `Integer` 구별할 모든 기본 숫자 데이터 형식 중에서 가장 효율적입니다.  
  
## <a name="nonintegral-numeric-types"></a>비정 수 숫자 형식  
 *비정 수 데이터 형식* 은 정수와 소수 부분을 사용 하 여 숫자를 나타냅니다.  
  
 비정 수 숫자 데이터 형식은 `Decimal` (128 비트 고정된 소수점) [단일 데이터 형식](../../../../visual-basic/language-reference/data-types/single-data-type.md) (32 비트 부동 소수점) 및 [Double 데이터 형식](../../../../visual-basic/language-reference/data-types/double-data-type.md) (64 비트 부동 소수점). 서명 된 전체 유형이 있습니다. 변수 분수를 포함할 수 있으면 이러한 형식 중 하나로 선언 합니다.  
  
 `Decimal`부동 소수점 데이터 형식이 아닙니다. `Decimal`숫자에는 이진 정수 값 있고 소수 값의 부분을 지정 하는 정수 배율 인수입니다.  
  
 사용할 수 있습니다 `Decimal` money 값에 대 한 변수입니다. 장점은 값의 정밀도입니다. `Double` 데이터 형식은 빠릅니다 메모리를 적게 사용 하지만 반올림 오류 영향을 받습니다. `Decimal` 데이터 형식에 소수 자릿수가 28 정확성을 유지 합니다.  
  
 부동 소수점 (`Single` 및 `Double`) 보다 더 큰 범위를 포함 하는 숫자 `Decimal` 숫자 이지만 반올림 오류가 발생할 수 있습니다. 부동 소수점 형식 지원 보다 적은 유효 자릿수 `Decimal` 하지만 더 큰 값을 나타낼 수 있습니다.  
  
 비정 수 숫자 값으로 표현 될 수 mmmEeee에서 mmm 인는 *가 수* (유효 자릿수가)은 여 *지 수* (10의 거듭제곱). 비정 수 형식의 가장 큰 양수 값은 7.9228162514264337593543950335 e + 28 `Decimal`, 3.4028235 e + 38 `Single`, 및에 대 한 1.79769313486231570 e + 308 `Double`합니다.  
  
### <a name="performance"></a>성능  
 `Double`소수 데이터 형식 중 가장 효율적인 이므로 현재 플랫폼의 프로세서 배정밀도의 부동 소수점 연산을 수행 합니다. 그러나 작업과 `Double` 과 같은 정수 계열 형식에서와 마찬가지로 빠르지 않습니다 `Integer`합니다.  
  
### <a name="small-magnitudes"></a>작은 크기  
 (0에 가장 가까운), 가능한 가장 작은 크기를 사용 하 여 숫자에 대 한 `Double` 변수-4.94065645841246544E로 작은 숫자를 보유할 수 있습니다-음수 값과 4.94065645841246544E 324-324 양수 값입니다.  
  
### <a name="small-fractional-numbers"></a>작은 소수  
 전체 범위를 필요 하지 않은 경우는 `Double` 사용할 수 있는 데이터 형식는 `Single` -3.4028235 e + 38에서 3.4028235 e + 38 까지의 부동 소수점 숫자를 사용할 수 있는 데이터 형식입니다. 사용할 수 있는 가장 작은 크기 `Single` 변수는-1.401298 e-45 음수 값 및 1.401298 e-45 양수 값입니다. 공용 언어 런타임 저장할 수 있습니다 작은 부동 소수점 숫자를 포함 하는 변수가 매우 많은 경우 프로그램 `Single` 변수 보다 효율적이 고 메모리 사용을 저장 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [기본 데이터 형식](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)   
 [문자 데이터 형식](../../../../visual-basic/programming-guide/language-features/data-types/character-data-types.md)   
 [기타 데이터 형식](../../../../visual-basic/programming-guide/language-features/data-types/miscellaneous-data-types.md)   
 [데이터 형식 문제 해결](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [방법: 부호 없는 형식을 사용하는 Windows 함수 호출](../../../../visual-basic/programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)
