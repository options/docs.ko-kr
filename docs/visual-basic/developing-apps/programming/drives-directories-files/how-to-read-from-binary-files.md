---
title: "How to: Read From Binary Files in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "binary files, reading from"
  - "I/O [Visual Basic], reading from binary files"
  - "ReadAllBytes method, reading from binary files"
  - "My.Computer.FileSystem object, reading from binary files"
ms.assetid: d2b1269e-24b6-42e0-9414-ae708db282d8
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# How to: Read From Binary Files in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

`My.Computer.FileSystem` 개체는 이진 파일을 읽기 위한 `ReadAllBytes` 메서드를 제공합니다.  
  
### 이진 파일을 읽으려면  
  
-   파일의 내용을 바이트 배열로 반환하는 `ReadAllBytes` 메서드를 사용합니다.  이 예제에서는 `C:/Documents and Settings/selfportrait.jpg` 파일을 읽습니다.  
  
     [!code-vb[VbVbcnMyFileSystem#78](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-binary-files_1.vb)]  
  
-   큰 이진 파일의 경우 <xref:System.IO.FileStream> 개체의 <xref:System.IO.FileStream.Read%2A> 메서드를 사용하여 한 번에 지정된 양만큼만 파일을 읽을 수 있습니다.  각 읽기 작업에 대해 메모리에 로드되는 파일의 양을 제한할 수 있습니다.  다음 코드 예제에서는 파일을 복사하고 호출자가 읽기 작업당 메모리로 읽어오는 파일의 양을 지정할 수 있도록 합니다.  
  
     [!code-vb[VbVbcnMyFileSystem#91](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-binary-files_2.vb)]  
  
## 강력한 프로그래밍  
 다음 조건에서 예외가 throw될 수 있습니다.  
  
-   길이가 0인 문자열이거나, 공백만 포함하거나, 잘못된 문자를 포함하거나, 경로가 장치 경로인 경우와 같은 여러 가지 이유 중 하나로 경로가 올바르지 않은 경우\(<xref:System.ArgumentException>\)  
  
-   경로가 `Nothing`이기 때문에 올바르지 않은 경우\(<xref:System.ArgumentNullException>\)  
  
-   파일이 없는 경우\(<xref:System.IO.FileNotFoundException>\)  
  
-   다른 프로세스에서 파일을 사용 중이거나 I\/O 오류가 발생한 경우\(<xref:System.IO.IOException>\)  
  
-   경로가 시스템 정의 최대 길이를 초과하는 경우\(<xref:System.IO.PathTooLongException>\)  
  
-   경로의 파일 이름이나 디렉터리 이름에 콜론\(:\)이 있거나 이름의 형식이 잘못된 경우\(<xref:System.NotSupportedException>\)  
  
-   문자열을 버퍼에 쓰기 위한 메모리가 부족한 경우\(<xref:System.OutOfMemoryException>\)  
  
-   경로를 보는 데 필요한 권한이 사용자에게 없는 경우\(<xref:System.Security.SecurityException>\)  
  
 파일 이름을 바탕으로 파일 내용을 판단하면 안 됩니다.  예를 들어, Form1.vb 파일이 Visual Basic 소스 파일이 아닐 수도 있습니다.  
  
 응용 프로그램에서 데이터를 사용하기 전에 모든 입력을 확인해야 합니다.  파일의 내용이 예상한 내용과 다를 수 있으며 파일을 읽는 메서드가 실패할 수도 있습니다.  
  
## 참고 항목  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.ReadAllBytes%2A>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllBytes%2A>   
 [Reading from Files](../../../../visual-basic/developing-apps/programming/drives-directories-files/reading-from-files.md)   
 [How to: Read From Text Files with Multiple Formats](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-text-files-with-multiple-formats.md)   
 [Storing Data to and Reading from the Clipboard](../../../../visual-basic/developing-apps/programming/computer-resources/storing-data-to-and-reading-from-the-clipboard.md)