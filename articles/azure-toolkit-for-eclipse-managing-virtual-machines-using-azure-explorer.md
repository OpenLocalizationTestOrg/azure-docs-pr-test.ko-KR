---
title: "사용 하 여 가상 컴퓨터 aaaManage hello Eclipse 용 Azure 탐색기 | Microsoft Docs"
description: "어떻게 toomanage Azure 가상 컴퓨터를 사용 하 여 hello Azure 탐색기에 대 한 자세한 내용은 Eclipse."
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
ms.openlocfilehash: aa83ec7546a0a8514842723b51ce8a5af81f98f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-by-using-hello-azure-explorer-for-eclipse"></a>Eclipse 용 Azure 탐색기 hello를 사용 하 여 가상 컴퓨터를 관리 합니다.

hello hello Eclipse 용 Azure 도구 키트의 일부인 Azure 탐색기의 Azure 계정과에서에서 가상 컴퓨터를 관리 하기 위한 사용 하기 쉬운 솔루션과 Java 개발자가 제공 hello Eclipse 통합된 개발 환경 (IDE) 안에 있습니다.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-eclipse"></a>Eclipse에서 가상 컴퓨터 만들기

toocreate hello Azure 탐색기를 사용 하 여 가상 컴퓨터는 다음 hello지 않습니다.

1. Hello를 사용 하 여 Azure 계정 tooyour 로그인 [hello Eclipse 용 Azure 도구 키트에 대 한 로그인 지침]합니다.

2. Hello에 **Azure 탐색기** 보기, 확장 hello **Azure** 노드를 마우스 오른쪽 단추로 클릭 **가상 컴퓨터**, 클릭 하 고 **VM 만들기**합니다.

   ![hello VM 만들기 명령][CR01]  
   hello **새 가상 컴퓨터 만들기** 마법사가 열립니다.

3. Hello에 **구독 선택** 창에서 구독을 선택한 다음 클릭 **다음**합니다.

   ![hello 선택 구독 창][CR02]

4. Hello에 **가상 컴퓨터 이미지 선택** 창의 hello 다음 정보를 입력 합니다.

   * **위치**: 가상 컴퓨터를 만들 위치(예: *미국 서부*)를 지정합니다.

   * **게시자**: toocreate 가상 컴퓨터가 사용 하는 hello 이미지를 만든 hello 게시자를 지정 합니다 (예를 들어 *Microsoft*).

   * **제공**: toouse hello 선택한 게시자에서 제공 하는 hello 가상 컴퓨터를 지정 합니다 (예를 들어 *JDK*).

   * **Sku**: hello stockkeeping 단위 (SKU) toouse hello 선택한를 지정 합니다 (예를 들어 *JDK_8*).

   * **버전 #**: 버전을 선택 하는 hello 지정 SKU toouse 합니다.

    ![가상 컴퓨터 이미지 기간을 선택 하는 hello][CR03]

5. **다음**을 누릅니다.

6. Hello에 **가상 컴퓨터 기본 설정** 창의 hello 다음 정보를 입력 합니다.

   * **가상 컴퓨터 이름**: 문자로 시작 하 고 문자, 숫자 및 하이픈만 포함 해야 하는 새 가상 컴퓨터에 대 한 hello 이름을 지정 합니다.

   * **크기**: 코어와 메모리 tooallocate 가상 컴퓨터에 대 한 hello 수를 지정 합니다.

   * **사용자 이름**: 가상 컴퓨터를 관리 하기 위한 관리자 계정 toocreate hello를 지정 합니다.

   * **암호** 및 **Confirm**: hello 프로그램 관리자 계정의 암호를 지정 합니다.

    ![hello 가상 컴퓨터 기본 설정 창][CR04]

7. **다음**을 누릅니다.

8. Hello에 **새 저장소 계정 만들기** 창의 hello 다음 정보를 입력 합니다.

   * **리소스 그룹**: 가상 컴퓨터에 대 한 hello 리소스 그룹을 지정 합니다. Hello 다음 옵션 중 하나를 선택 합니다.
      * **새로 만들기**: toocreate 새 리소스 그룹 한다고 지정 합니다.
      * **기존 항목 사용**: tooselect 이미 Azure 계정과 연결 되어 있는 리소스 그룹 한다고 지정 합니다.

      ![hello 새 저장소 계정 만들기 대화 상자][CR05]

   * **저장소 계정**: 가상 컴퓨터를 저장 하기 위한 저장소 계정 toouse hello를 지정 합니다. 기존 저장소 계정을 사용하거나 새 저장소 계정을 만들 수 있습니다.

   * **가상 네트워크** 및 **서브넷**: hello 가상 네트워크 및 가상 컴퓨터에 연결 하는 서브넷을 지정 합니다. 기존 네트워크 및 서브넷을 사용하거나 새 네트워크 및 서브넷을 만들 수 있습니다. 선택 하는 경우 **새로 만들기**, hello 다음 대화 상자가 표시 됩니다.

      ![hello 새 가상 네트워크 만들기 대화 상자][CR06]

9. Hello에 **연결 된 리소스** 창 hello 다음 정보를 입력 합니다.

   * **공용 IP 주소**: 가상 컴퓨터에 대한 외부 연결 IP 주소를 지정합니다. Toocreate 새 IP 주소를 선택할 수 있습니다 또는 선택할 수 가상 컴퓨터에는 공용 IP 주소를 없으면 **(없음)**합니다.

   * **네트워크 보안 그룹**: 가상 컴퓨터에 대한 선택적 네트워킹 방화벽을 지정합니다. 기존 방화벽을 선택하거나, 가상 컴퓨터에서 네트워크 방화벽을 사용하지 않을 경우 **(없음)**을 선택할 수 있습니다.

   * **가용성 집합**: 가상 컴퓨터가 속할 선택적 가용성 집합을 지정합니다. 기존 가용성 집합을 선택 하거나 새 가용성 집합을 만들 수 있습니다 하거나, 가상 컴퓨터가 tooan 가용성 집합에 속하지 것입니다, 선택할 수 있습니다 **(없음)**합니다.

   ![hello 연결 된 리소스 창][CR07]

9. **마침**을 클릭합니다.  
  새 가상 컴퓨터에는 hello Azure 탐색기 도구 창에 표시 됩니다.

   ![새 가상 컴퓨터][CR08]

## <a name="restart-a-virtual-machine-in-eclipse"></a>Eclipse에서 가상 컴퓨터 다시 시작

toorestart Eclipse에서 Azure 탐색기 hello를 사용 하 여 가상 컴퓨터는 다음 hello지 않습니다.

1. Hello에 **Azure 탐색기** 확인, hello 가상 컴퓨터를 마우스 오른쪽 단추로 클릭 한 다음 선택 **다시 시작**합니다.

   ![가상 컴퓨터 다시 시작 명령을 hello합니다][RE01]

2. Hello 확인 창에서 클릭 **예**합니다.

   ![hello 다시 시작 확인 창][RE02]

## <a name="shut-down-a-virtual-machine-in-eclipse"></a>Eclipse에서 가상 컴퓨터 종료

Eclipse에서 Azure 탐색기 hello를 사용 하 여 실행 중인 가상 컴퓨터를 tooshut 다음 hello지 않습니다.

1. Hello에 **Azure 탐색기** 확인, hello 가상 컴퓨터를 마우스 오른쪽 단추로 클릭 한 다음 선택 **종료**합니다.

   ![가상 컴퓨터 종료 명령은 hello][SH01]

2. Hello 확인 창에서 클릭 **예**합니다.

   ![hello 가상 컴퓨터 종료 확인 창][SH02]

## <a name="delete-a-virtual-machine-in-eclipse"></a>Eclipse에서 가상 컴퓨터 삭제

toodelete Eclipse에서 Azure 탐색기 hello를 사용 하 여 가상 컴퓨터는 다음 hello지 않습니다.

1. Hello에 **Azure 탐색기** 확인, hello 가상 컴퓨터를 마우스 오른쪽 단추로 클릭 한 다음 선택 **삭제**합니다.

   ![hello 가상 컴퓨터 삭제 명령][DE01]

2. Hello 확인 창에서 클릭 **예**합니다.

   ![hello 가상 컴퓨터 삭제 확인 창][DE02]

## <a name="next-steps"></a>다음 단계
Azure 가상 컴퓨터 크기 및 가격에 대 한 자세한 내용은 다음 리소스는 hello 참조:

* Azure Virtual Machines 크기
  * [Azure에서 Windows 가상 컴퓨터에 대한 크기]
  * [Azure에서 Linux 가상 컴퓨터에 대한 크기]
* Azure Virtual Machines 가격 책정
  * [Windows 가상 컴퓨터 가격 책정]
  * [Linux 가상 컴퓨터 가격 책정]

Java Ide에 대 한 hello Azure 도구 키트에 대 한 자세한 내용은 hello 다음 리소스를 참조 하세요.

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

[Azure에서 Windows 가상 컴퓨터에 대한 크기]: /azure/virtual-machines/virtual-machines-windows-sizes
[Azure에서 Linux 가상 컴퓨터에 대한 크기]: /azure/virtual-machines/virtual-machines-linux-sizes
[Windows 가상 컴퓨터 가격 책정]: /pricing/details/virtual-machines/windows/
[Linux 가상 컴퓨터 가격 책정]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[RE01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR08.png
