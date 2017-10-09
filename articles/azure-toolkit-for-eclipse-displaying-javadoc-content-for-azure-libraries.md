---
title: "Eclipse에서 Javadoc 콘텐츠 aaaDisplaying hello Java 용 Azure 라이브러리 패키지에 대 한"
description: "어떻게 toodisplay Javadoc 콘텐츠를 Eclipse에서 Azure 라이브러리 hello에 대 한 hello 합니다."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 30f8b6a1-1d76-4d1c-861b-1db478c46e6b
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 8070023a24dc07eca8df906db5b8b662ceed6ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="displaying-javadoc-content-in-eclipse-for-hello-azure-libraries-package-for-java"></a>Hello Java 용 Azure 라이브러리 패키지에 대 한 Eclipse에서 Javadoc 콘텐츠 표시
hello Javadoc 콘텐츠 toohello Java 용 Azure 라이브러리를 연결 하 여 hello hello Java 용 Azure 라이브러리에 Javadoc 콘텐츠를 Eclipse 환경 내에서 볼 수 있습니다. hello 다음 단계 방법을 보여 줍니다 toouse Eclipse 내에서이 기능입니다.

이 절차에서는 Java tooyour 빌드 경로 대 한 Azure 라이브러리 hello 이미 추가 했다고 가정 합니다.

## <a name="toodisplay-javadoc-content-in-eclipse-for-hello-azure-libraries-for-java"></a>toodisplay hello Java 용 Azure 라이브러리에 대 한 Eclipse에서 Javadoc 콘텐츠
* Hello에 Eclipse의 프로젝트 탐색기 내에서 **참조 되는 라이브러리** 프로젝트의 섹션을 Java JAR 용 Azure 라이브러리 hello에 대 한 상황에 맞는 메뉴를 열고 hello 합니다. 예를 들어 **windowsazure api 0.1.0.jar microsoft** (hello 버전 번호는 설치한 버전에 따라 다를 수 수 있습니다).

* **속성**을 클릭합니다.

* Hello 내 **속성** hello 왼쪽 창에서 대화 상자에서 클릭 **Javadoc 위치**합니다. hello **Javadoc 위치** 대화 상자가 표시 됩니다.

* **Javadoc URL** 또는 **보관 중인 Javadoc**을 지정할 수 있습니다.

   * Toospecify를 선택 하는 경우는 **Javadoc URL**와 같은 hello Url을 사용 하 여 **http://dl.windowsazure.com/javadoc** 또는 **http://dl.windowsazure.com/storage/javadoc**합니다.

   * Toouse를 선택 하면 **보관 파일의 Javadoc**, 외부 파일 또는 작업 영역 파일을 지정할 수 있습니다.

   필요에 따라 선택하여 찾거나 유효성을 검사합니다. hello 다음 예제에서는 Java 용 Azure 라이브러리 hello와 연결 해당 Javadoc JAR 된 라는 tooa 폴더 로컬로 다운로드 hello **c:\MyAzureJARs**합니다.

   ![][ic553487]

* *옵션 단계*: **유효성 검사**를 클릭합니다. 잠재적인 문제 hello Javadoc JAR에 여기에 표시할 수 없습니다.

* **확인**을 클릭합니다.

Hello 라이브러리와 연결 된, 일단 hello Javadoc 콘텐츠가 Eclipse IDE 내에서 표시 되어야 합니다. 예를 들어 경우 `blob` 형식의 정의 `CloudBlockBlob` hello 다음은의 Javadoc 콘텐츠를 입력할 때 표시 되는 예, 코드 내 `blob.acquireLease` 코드에서:

![][ic553488]

## <a name="see-also"></a>참고 항목
[Eclipse용 Azure 도구 키트][Azure Toolkit for Eclipse]

[Eclipse에서 Azure용 Hello World 응용 프로그램 만들기][Creating a Hello World Application for Azure in Eclipse]

[Hello Eclipse 용 Azure 도구 키트 설치][Installing hello Azure Toolkit for Eclipse] 

Java와 함께 Azure 사용에 대 한 자세한 내용은 참조 hello [Azure Java 개발자 센터][Azure Java Developer Center]합니다.

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic553487]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553487.png
[ic553488]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553488.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh698319.aspx -->
