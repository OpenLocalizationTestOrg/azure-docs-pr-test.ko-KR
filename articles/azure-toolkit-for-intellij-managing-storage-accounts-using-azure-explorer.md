---
title: "사용 하 여 저장소 계정을 aaaManage IntelliJ에 대 한 Azure 탐색기 hello | Microsoft Docs"
description: "어떻게 toomanage Azure 저장소는 IntelliJ 용 hello Azure 탐색기를 사용 하 여을 계정에 대해 알아봅니다."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: b094bdcd2fa2782cb12b67c96ac406fbe4c1aa3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-storage-accounts-by-using-hello-azure-explorer-for-intellij"></a>IntelliJ 용 hello Azure 탐색기를 사용 하 여 저장소 계정 관리

hello hello IntelliJ 용 Azure 도구 키트의 일부인 Azure 탐색기에서 자신의 Azure 계정에 저장소 계정을 관리 하기 위한 사용 하기 쉬운 솔루션과 Java 개발자가 제공 hello IntelliJ 통합된 개발 환경 (IDE) 안에 있습니다.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-intellij"></a>IntelliJ에서 저장소 계정 만들기

toocreate hello Azure 탐색기를 사용 하 여 저장소 계정을 다음 hello지 않습니다.

1. Hello를 사용 하 여 Azure 계정 tooyour 로그인 [hello Eclipse 용 Azure 도구 키트에 대 한 로그인 지침]합니다. 

2. Hello에 **Azure 탐색기** 보기, hello 확장 **Azure** 노드를 마우스 오른쪽 단추로 클릭 **저장소 계정은**, 클릭 하 고 **저장소 계정 만들기**.

   ![저장소 계정 만들기 명령][CS01]

3. Hello에 **저장소 계정 만들기** 대화 상자를 hello 다음 옵션을 지정 합니다.

   ![새 저장소 계정 만들기 대화 상자][CS02]

   * **이름**: hello 새 저장소 계정에 대 한 hello 이름을 지정 합니다.

   * **Kind 계정**: 저장소 계정 toocreate (예: "Blob storage")의 hello 유형을 지정 합니다. 자세한 내용은 [Azure 저장소 계정 정보]를 참조하세요. 

   * **성능**: toouse (예: "프리미엄") hello 선택한 게시자에서 제공 하는 저장소 계정을 지정 합니다. 자세한 내용은 [Azure Storage 확장성 및 성능 목표]를 참조하세요. 

   * **복제**: hello 저장소 계정 (예를 들어 "영역 중복")에 대 한 hello 복제를 지정 합니다. 자세한 내용은 [Azure Storage 복제]를 참조하세요. 

   * **구독**: hello hello 새 저장소 계정에 대 한 toouse 되도록 Azure 구독을 지정 합니다.

   * **위치**: hello 위치 (예: "West US") 저장소 계정을 만들 위치를 지정 합니다.

   * **리소스 그룹**: 가상 컴퓨터에 대 한 hello 리소스 그룹을 지정 합니다. Hello 다음 옵션 중 하나를 선택 합니다.
      * **새로 만들기**: toocreate 새 리소스 그룹 한다고 지정 합니다.
      * **기존 그룹 사용**: Azure 계정에 연결된 리소스 그룹 목록에서 선택하도록 지정합니다.

4. Hello 앞에 옵션을 모두 지정한 경우 클릭 **확인**합니다.

## <a name="create-a-storage-container-in-intellij"></a>IntelliJ에서 저장소 컨테이너 만들기

hello Azure 탐색기를 사용 하 여 저장소 컨테이너 toocreate 다음 hello지 않습니다.

1. Azure 폴더 보기 hello toocreate 컨테이너를 선택 하 고 클릭 hello 저장소 계정을 마우스 오른쪽 단추로 클릭 **blob 컨테이너 만들기**합니다.

   ![Blob 컨테이너 만들기 명령][CC01]

2. Hello에 **blob 컨테이너 만들기** 대화 상자에서 사용자 컨테이너에 대 한 hello 이름을 지정 하 고 클릭 **확인**합니다. 저장소 컨테이너 이름 지정에 대한 자세한 내용은 [컨테이너, BLOB, 메타데이터 이름 지정 및 참조]를 참조하세요.

   ![저장소 컨테이너 만들기 대화 상자][CC02]

## <a name="delete-a-storage-container-in-intellij"></a>IntelliJ에서 저장소 컨테이너 삭제

hello Azure 탐색기를 사용 하 여 저장소 컨테이너 toodelete 다음 hello지 않습니다.

1. Hello Azure 탐색기 보기에서에서 hello 저장소 컨테이너를 마우스 오른쪽 단추로 클릭 하 고 클릭 **삭제**합니다.

   ![저장소 컨테이너 삭제 명령][DC01]

2. Hello 확인 창에서 클릭 **예**합니다.

   ![저장소 컨테이너 삭제 확인 창][DC02]

## <a name="delete-a-storage-account-in-intellij"></a>IntelliJ에서 저장소 계정 삭제

toodelete hello Azure 탐색기를 사용 하 여 저장소 계정을 다음 hello지 않습니다.

1. Hello에 **Azure 탐색기** 확인, hello 저장소 계정을 마우스 오른쪽 단추로 클릭 한 다음 선택 **삭제**합니다.

   ![저장소 계정 삭제 메뉴][DS01]

2. Hello 확인 창에서 클릭 **예**합니다.

   ![저장소 계정 삭제 확인 창][DS02]

## <a name="next-steps"></a>다음 단계
Azure 저장소 계정, 크기 및 가격에 대 한 자세한 내용은 다음 리소스는 hello 참조:

* [Azure 저장소 소개 tooMicrosoft]
* [Azure 저장소 계정 정보]
* Azure Storage 계정 크기
  * [Azure의 Windows 저장소 계정 크기]
  * [Azure의 Linux 저장소 계정 크기]
* Azure Storage 계정 가격 책정
  * [Windows 저장소 계정 가격 책정]
  * [Linux 저장소 계정 가격 책정]

Java Ide에 대 한 Azure 도구 키트에 대 한 자세한 내용은 hello 다음 리소스를 참조 하세요.

* [Eclipse용 Azure 도구 키트]
  * [Hello Eclipse 용 Azure 도구 키트의에서 새로운 기능]
  * [Hello Eclipse 용 Azure 도구 키트 설치]
  * [hello Eclipse 용 Azure 도구 키트에 대 한 로그인 지침]
  * [Eclipse에서 Azure용 Hello World 웹앱 만들기]
* [IntelliJ용 Azure 도구 키트]
  * [Hello IntelliJ 용 Azure 도구 키트의에서 새로운 기능]
  * [IntelliJ 용 hello Azure 도구 키트 설치]
  * [로그인에 대 한 지침 Azure 도구 키트 hello IntelliJ]
  * [IntelliJ에서 Azure용 Hello World 웹앱 만들기]

Java와 함께 Azure를 사용하는 것에 대한 자세한 내용은 [Azure Java 개발자 센터] 및 [Visual Studio Team Services용 Java 도구]를 참조하세요.

<!-- URL List -->

[Eclipse용 Azure 도구 키트]: ./azure-toolkit-for-eclipse.md
[IntelliJ용 Azure 도구 키트]: ./azure-toolkit-for-intellij.md
[Eclipse에서 Azure용 Hello World 웹앱 만들기]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[IntelliJ에서 Azure용 Hello World 웹앱 만들기]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Hello Eclipse 용 Azure 도구 키트 설치]: ./azure-toolkit-for-eclipse-installation.md
[IntelliJ 용 hello Azure 도구 키트 설치]: ./azure-toolkit-for-intellij-installation.md
[hello Eclipse 용 Azure 도구 키트에 대 한 로그인 지침]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[로그인에 대 한 지침 Azure 도구 키트 hello IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Hello Eclipse 용 Azure 도구 키트의에서 새로운 기능]: ./azure-toolkit-for-eclipse-whats-new.md
[Hello IntelliJ 용 Azure 도구 키트의에서 새로운 기능]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java 개발자 센터]: https://azure.microsoft.com/develop/java/
[Visual Studio Team Services용 Java 도구]: https://java.visualstudio.com/

[Azure 저장소 소개 tooMicrosoft]: /azure/storage/storage-introduction
[Azure 저장소 계정 정보]: /azure/storage/storage-create-storage-account
[Azure Storage 복제]: /azure/storage/storage-redundancy
[Azure Storage 확장성 및 성능 목표]: /azure/storage/storage-scalability-targets
[컨테이너, BLOB, 메타데이터 이름 지정 및 참조]: http://go.microsoft.com/fwlink/?LinkId=255555

[Azure의 Windows 저장소 계정 크기]: /azure/virtual-machines/virtual-machines-windows-sizes
[Azure의 Linux 저장소 계정 크기]: /azure/virtual-machines/virtual-machines-linux-sizes
[Windows 저장소 계정 가격 책정]: /pricing/details/virtual-machines/windows/
[Linux 저장소 계정 가격 책정]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[CS01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC02.png
