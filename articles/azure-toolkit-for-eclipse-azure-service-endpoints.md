---
title: "aaaAzure 서비스 끝점"
description: "Hello Azure 서비스 끝점 설정 hello Eclipse 용 Azure 도구 키트에에서 설명 합니다."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9c6125ec-7278-461e-b69c-ed56e844f742
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 357aa56409a894719077f2c8f302575c8ebb6883
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-endpoints"></a>Azure 서비스 끝점
Azure 서비스 끝점 응용 프로그램이 hello 전역 Azure 플랫폼에서 관리 하는 배포 된 tooand 인지 Azure 21Vianet에서 운영 중국 또는 개인 Azure 플랫폼을 결정 합니다. hello **서비스 끝점** 대화 상자에서는 toospecify 서비스 toouse 원하는 끝점입니다. tooopen hello **서비스 끝점** Eclipse 내에서 대화 상자에서 클릭 **창**, 클릭 **기본 설정**, 확장 **Azure**, 클릭 하 고 **서비스 끝점**합니다. 설정 hello **활성 집합** 필드 현재 작업 영역에 있는 Azure 서비스 끝점 hello에 사용할 Azure 프로젝트를 확인 합니다.

hello 다음 표시 되어 hello **서비스 끝점** 대화 상자.

![][ic719493]

## <a name="tooset-hello-service-endpoints"></a>tooset hello 서비스 끝점
Hello에 **서비스 끝점** 대화 상자에서 hello 다음 동작 중 하나를 수행 합니다.

* Toouse hello 전역 Azure 플랫폼을 hello에서 원하는 **활성 집합** 드롭다운 목록에서 선택 **windowsazure.com** 클릭 **확인**합니다.

* Azure hello에서 중국의 21vianet이 운영 toouse 원하면 **활성 집합** 드롭다운 목록에서 선택 **windowsazure.cn (중국)** 클릭 **확인**합니다.

* 개인 Azure 플랫폼 toouse 하려는 경우:

  1. **편집**을 클릭합니다.

  2. 대화 상자가 열리고 해당 hello 알리는 **서비스 끝점** hello 기본 설정 집합 파일을 열 및 대화 상자가 닫힙니다. **확인**을 클릭합니다.

  3. Hello preferencesets.xml 파일에서 만들 새 `preferenceset` 요소입니다. 이 새 요소에 대 한 만들기 `name`, `blob`, `management`, `portalURL` 및 `publishsettings` 특성 및 tooyour 개인 Azure 플랫폼에 해당 하는 값을 추가 합니다. Hello 기존 제공 hello 값을 사용 하려면 `preferenceset` 템플릿으로 요소입니다. **참고**: hello에 사용 되는 값을 hello `blob` 특성 hello 텍스트 "blob" hello URL에 포함 되어야 합니다.

  4. preferencesets.xml을 저장하고 닫습니다.

  5. Hello를 다시 열고 **서비스 끝점** 대화 상자.

  6. Hello에서 **활성 집합** 드롭다운 목록에서 선택 hello 활성 집합 생성 하 고 클릭 **확인**합니다.

  7. 개인 Azure 플랫폼을 만든 후 `preferenceset` 요소인 hello 할당 된 값 tooit hello를 클릭 하 여 변경할 수 있습니다 **편집** hello 단추 **서비스 끝점** 대화 상자. 또한 원하는 경우 여러 개인 Azure 플랫폼 `preferenceset` 요소를 만들 수 있습니다.

## <a name="see-also"></a>참고 항목
[Eclipse용 Azure 도구 키트][Azure Toolkit for Eclipse]

[Hello Eclipse 용 Azure 도구 키트 설치][Installing hello Azure Toolkit for Eclipse] 

[Eclipse에서 Azure용 Hello World 응용 프로그램 만들기][Creating a Hello World Application for Azure in Eclipse]

Java와 함께 Azure 사용에 대 한 자세한 내용은 참조 hello [Azure Java 개발자 센터][Azure Java Developer Center]합니다.

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719493]: ./media/azure-toolkit-for-eclipse-azure-service-endpoints/ic719493.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268600.aspx -->
