---
title: "IntelliJ용 Azure Explorer를 사용하여 저장소 계정 관리 | Microsoft Docs"
description: "IntelliJ용 Azure 탐색기를 사용하여 Azure Storage 계정을 관리하는 방법을 알아봅니다."
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
ms.openlocfilehash: a1b56cc2751fc43a1ad6917eca77eec460f26694
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-storage-accounts-by-using-the-azure-explorer-for-intellij"></a>IntelliJ용 Azure Explorer를 사용하여 저장소 계정 관리

IntelliJ용 Azure 도구 키트의 일부인 Azure Explorer는 IntelliJ IDE(통합 개발 환경) 내에서 Azure 계정의 저장소 계정을 관리하기 위한 사용하기 쉬운 솔루션을 Java 개발자에게 제공합니다.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-intellij"></a>IntelliJ에서 저장소 계정 만들기

Azure Explorer를 사용하여 저장소 계정을 만들려면 다음을 수행합니다.

1. [Eclipse용 Azure 도구 키트에 대한 로그인 지침]을 사용하여 Azure 계정에 로그인합니다. 

2. **Azure Explorer** 보기에서 **Azure** 노드를 확장하고 **저장소 계정**을 마우스 오른쪽 단추로 클릭한 후 **저장소 계정 만들기**를 클릭합니다.

   ![저장소 계정 만들기 명령][CS01]

3. **저장소 계정 만들기** 대화 상자에서 다음 옵션을 지정합니다.

   ![새 저장소 계정 만들기 대화 상자][CS02]

   * **이름**: 새 저장소 계정의 이름을 지정합니다.

   * **계정 종류**: 만들려는 저장소 계정의 형식을 지정합니다(예: “Blob Storage”). 자세한 내용은 [Azure 저장소 계정 정보]를 참조하세요. 

   * **성능**: 선택한 게시자에서 사용할 저장소 계정 제품을 지정합니다(예: “프리미엄”). 자세한 내용은 [Azure Storage 확장성 및 성능 목표]를 참조하세요. 

   * **복제**: 저장소 계정에 대한 복제를 지정합니다(예: “영역 중복”). 자세한 내용은 [Azure Storage 복제]를 참조하세요. 

   * **구독**: 새 저장소 계정에 사용할 Azure 구독을 지정합니다.

   * **위치**: 저장소 계정을 만들 위치를 지정합니다(예: “미국 서부”).

   * **리소스 그룹**: 가상 컴퓨터에 사용할 리소스 그룹을 지정합니다. 다음 옵션 중 하나를 선택합니다.
      * **새로 만들기**: 새 리소스 그룹을 만들도록 지정합니다.
      * **기존 그룹 사용**: Azure 계정에 연결된 리소스 그룹 목록에서 선택하도록 지정합니다.

4. 위의 옵션을 모두 지정했으면 **확인**을 클릭합니다.

## <a name="create-a-storage-container-in-intellij"></a>IntelliJ에서 저장소 컨테이너 만들기

Azure Explorer를 사용하여 저장소 컨테이너를 만들려면 다음을 수행합니다.

1. Azure Explorer에서 컨테이너를 만들 저장소 계정을 마우스 오른쪽 단추로 클릭하고 **Blob 컨테이너 만들기**를 클릭합니다.

   ![Blob 컨테이너 만들기 명령][CC01]

2. **Blob 컨테이너 만들기** 대화 상자에서 컨테이너의 이름을 지정하고 **확인**을 클릭합니다. 저장소 컨테이너 이름 지정에 대한 자세한 내용은 [컨테이너, BLOB 및 메타데이터 이름 지정 및 참조]를 참조하세요.

   ![저장소 컨테이너 만들기 대화 상자][CC02]

## <a name="delete-a-storage-container-in-intellij"></a>IntelliJ에서 저장소 컨테이너 삭제

Azure Explorer를 사용하여 저장소 컨테이너를 삭제하려면 다음을 수행합니다.

1. Azure Explorer 보기에서 저장소 컨테이너를 마우스 오른쪽 단추로 클릭하고 **삭제**를 클릭합니다.

   ![저장소 컨테이너 삭제 명령][DC01]

2. 확인 창에서 **예**를 클릭합니다.

   ![저장소 컨테이너 삭제 확인 창][DC02]

## <a name="delete-a-storage-account-in-intellij"></a>IntelliJ에서 저장소 계정 삭제

Azure Explorer를 사용하여 저장소 계정을 삭제하려면 다음을 수행합니다.

1. **Azure Explorer** 보기에서 저장소 계정을 마우스 오른쪽 단추로 클릭하고 **삭제**를 선택합니다.

   ![저장소 계정 삭제 메뉴][DS01]

2. 확인 창에서 **예**를 클릭합니다.

   ![저장소 계정 삭제 확인 창][DS02]

## <a name="next-steps"></a>다음 단계
Azure Storage 계정, 크기 및 가격 책정에 대한 자세한 내용은 다음 리소스를 참조하세요.

* [Microsoft Azure 저장소 소개]
* [Azure 저장소 계정 정보]
* Azure Storage 계정 크기
  * [Azure의 Windows 저장소 계정 크기]
  * [Azure의 Linux 저장소 계정 크기]
* Azure Storage 계정 가격 책정
  * [Windows 저장소 계정 가격 책정]
  * [Linux 저장소 계정 가격 책정]

Java IDE용 Azure 도구 키트에 대한 자세한 내용은 다음 리소스를 참조하세요.

* [Eclipse용 Azure 도구 키트]
  * [Eclipse용 Azure 도구 키트의 새로운 기능]
  * [Eclipse용 Azure 도구 키트 설치]
  * [Eclipse용 Azure 도구 키트에 대한 로그인 지침]
  * [Eclipse에서 Azure용 Hello World 웹앱 만들기]
* [IntelliJ용 Azure 도구 키트]
  * [IntelliJ용 Azure 도구 키트의 새로운 기능]
  * [IntelliJ용 Azure 도구 키트 설치]
  * [IntelliJ용 Azure 도구 키트에 대한 로그인 지침]
  * [IntelliJ에서 Azure용 Hello World 웹앱 만들기]

Java와 함께 Azure를 사용하는 것에 대한 자세한 내용은 [Azure Java 개발자 센터] 및 [Visual Studio Team Services용 Java 도구]를 참조하세요.

<!-- URL List -->

[Eclipse용 Azure 도구 키트]: ./azure-toolkit-for-eclipse.md
[IntelliJ용 Azure 도구 키트]: ./azure-toolkit-for-intellij.md
[Eclipse에서 Azure용 Hello World 웹앱 만들기]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[IntelliJ에서 Azure용 Hello World 웹앱 만들기]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Eclipse용 Azure 도구 키트 설치]: ./azure-toolkit-for-eclipse-installation.md
[IntelliJ용 Azure 도구 키트 설치]: ./azure-toolkit-for-intellij-installation.md
[Eclipse용 Azure 도구 키트에 대한 로그인 지침]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[IntelliJ용 Azure 도구 키트에 대한 로그인 지침]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Eclipse용 Azure 도구 키트의 새로운 기능]: ./azure-toolkit-for-eclipse-whats-new.md
[IntelliJ용 Azure 도구 키트의 새로운 기능]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java 개발자 센터]: https://azure.microsoft.com/develop/java/
[Visual Studio Team Services용 Java 도구]: https://java.visualstudio.com/

[Microsoft Azure 저장소 소개]: /azure/storage/storage-introduction
[Azure 저장소 계정 정보]: /azure/storage/storage-create-storage-account
[Azure Storage 복제]: /azure/storage/storage-redundancy
[Azure Storage 확장성 및 성능 목표]: /azure/storage/storage-scalability-targets
[컨테이너, BLOB 및 메타데이터 이름 지정 및 참조]: http://go.microsoft.com/fwlink/?LinkId=255555

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
