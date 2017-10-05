---
title: "IntelliJ용 Azure Explorer를 사용하여 Virtual Machines 관리 | Microsoft Docs"
description: "IntelliJ용 Azure 탐색기를 사용하여 Azure Virtual Machines를 관리하는 방법을 알아봅니다."
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
ms.openlocfilehash: 9197580407b3509fbf9a842e1fee1e6348478c34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-virtual-machines-by-using-the-azure-explorer-for-intellij"></a>IntelliJ용 Azure Explorer를 사용하여 Virtual Machines 관리

IntelliJ용 Azure 도구 키트의 일부인 Azure Explorer는 IntelliJ IDE(통합 개발 환경) 내에서 Azure 계정의 Virtual Machines를 관리하기 위한 사용하기 쉬운 솔루션을 Java 개발자에게 제공합니다.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-intellij"></a>IntelliJ에서 가상 컴퓨터 만들기

Azure Explorer를 사용하여 가상 컴퓨터를 만들려면 다음을 수행합니다. 

1. [IntelliJ용 Azure 도구 키트에 대한 로그인 지침] 문서의 단계를 사용하여 Azure 계정에 로그인합니다.

2. **Azure Explorer** 보기에서 **Azure** 노드를 확장하고 **Virtual Machines**를 마우스 오른쪽 단추로 클릭한 후 **VM 만들기**를 클릭합니다. 

   ![VM 만들기 명령][CR01]  
    **새 가상 컴퓨터 만들기** 마법사가 열립니다.

3. **구독 선택** 창에서 구독을 선택하고 **다음**을 클릭합니다. 

   ![구독 선택 창][CR02]

4. **가상 컴퓨터 이미지 선택** 창에서 다음 정보를 입력합니다.

   * **위치**: 가상 컴퓨터를 만들 위치(예: *미국 서부*)를 지정합니다. 

   * **권장 이미지**: 일반적으로 사용되는 이미지의 요약 목록에서 이미지를 선택하도록 지정합니다.

   * **사용자 지정 이미지**: 다음 정보를 제공하여 사용자 지정 이미지를 선택하도록 지정합니다.

      * **게시자**: 가상 컴퓨터에 사용할 이미지를 만든 게시자를 지정합니다(예: *Microsoft*).

      * **제품**: 선택한 게시자에서 사용할 가상 컴퓨터 제품을 지정합니다(예: *JDK*).

      * **SKU**: 선택한 제품에서 사용할 SKU(Stockkeeping Unit)를 지정합니다(예: *JDK_8*).

      * **버전 번호**: 선택한 SKU에서 사용할 버전을 지정합니다.

   ![가상 컴퓨터 이미지 선택 창][CR03]

5. **다음**을 누릅니다. 

6. **가상 컴퓨터 기본 설정** 창에서 다음 정보를 입력합니다.

   * **가상 컴퓨터 이름**: 새 가상 컴퓨터의 이름을 지정합니다. 이름은 문자로 시작하고 문자, 숫자 및 하이픈만 포함해야 합니다.

   * **크기**: 가상 컴퓨터용으로 할당할 코어 수 및 메모리를 지정합니다.

   * **사용자 이름**: 가상 컴퓨터를 관리하기 위해 만들 관리자 계정을 지정합니다.

   * **암호** 및 **확인**: 관리자 계정의 암호를 지정합니다.

   ![가상 컴퓨터 기본 설정 창][CR04]

7. **다음**을 누릅니다. 

8. **연결된 리소스** 창에서 다음 정보를 입력합니다.

   * **리소스 그룹**: 가상 컴퓨터에 사용할 리소스 그룹을 지정합니다. 다음 옵션 중 하나를 선택합니다.
      * **새로 만들기**: 새 리소스 그룹을 만들도록 지정합니다.
      * **기존 그룹 사용**: Azure 계정에 연결된 리소스 그룹 목록에서 선택하도록 지정합니다.

       ![연결된 리소스 창][CR07]

   * **저장소 계정**: 가상 컴퓨터를 저장하는 데 사용할 저장소 계정을 지정합니다. 기존 저장소 계정을 사용하거나 새 저장소 계정을 만들 수 있습니다. **새로 만들기**를 선택하면 다음 대화 상자가 표시됩니다.

      ![저장소 계정 만들기 대화 상자][CR05]

   * **가상 네트워크** 및 **서브넷**: 가상 컴퓨터가 연결될 가상 네트워크 및 서브넷을 지정합니다. 기존 네트워크 및 서브넷을 사용하거나 새 네트워크 및 서브넷을 만들 수 있습니다. **새로 만들기**를 선택하는 경우 다음과 같은 대화 상자가 나타납니다.

      ![가상 네트워크 만들기 대화 상자][CR06]

   * **공용 IP 주소**: 가상 컴퓨터에 대한 외부 연결 IP 주소를 지정합니다. 새 IP 주소를 만들도록 선택하거나, 가상 컴퓨터에 공용 IP 주소가 없는 경우 **(없음)**을 선택할 수 있습니다. 

   * **네트워크 보안 그룹**: 가상 컴퓨터에 대한 선택적 네트워킹 방화벽을 지정합니다. 기존 방화벽을 선택하거나, 가상 컴퓨터에서 네트워크 방화벽을 사용하지 않을 경우 **(없음)**을 선택할 수 있습니다. 

   * **가용성 집합**: 가상 컴퓨터가 속할 선택적 가용성 집합을 지정합니다. 기존 가용성 집합을 선택하거나, 새 가용성 집합을 만들거나, 가상 컴퓨터가 가용성 집합에 속하지 않을 경우 **(없음)**을 선택할 수 있습니다.

9. **Finish**를 클릭합니다.  
    새 가상 컴퓨터가 Azure Explorer 도구 창에 나타납니다. 

   ![Azure Explorer 보기의 새 가상 컴퓨터][CR08]

## <a name="restart-a-virtual-machine-in-intellij"></a>IntelliJ에서 가상 컴퓨터 다시 시작

IntelliJ에서 Azure Explorer를 사용하여 가상 컴퓨터를 다시 시작하려면 다음을 수행합니다.

1. **Azure Explorer** 보기에서 가상 컴퓨터를 마우스 오른쪽 단추로 클릭하고 **다시 시작**을 선택합니다.

   ![가상 컴퓨터 다시 시작 명령][RE01]

2. 확인 창에서 **예**를 클릭합니다. 

   ![가상 컴퓨터 다시 시작 확인 창][RE02]

## <a name="shut-down-a-virtual-machine-in-intellij"></a>IntelliJ에서 가상 컴퓨터 종료

IntelliJ에서 Azure Explorer를 사용하여 가상 컴퓨터를 종료하려면 다음을 수행합니다.

1. **Azure Explorer** 보기에서 가상 컴퓨터를 마우스 오른쪽 단추로 클릭하고 **종료**를 선택합니다.

   ![가상 컴퓨터 종료 명령][SH01]

2. 확인 창에서 **예**를 클릭합니다. 

   ![가상 컴퓨터 종료 확인 창][SH02]

## <a name="delete-a-virtual-machine-in-intellij"></a>IntelliJ에서 가상 컴퓨터 삭제

IntelliJ에서 Azure Explorer를 사용하여 가상 컴퓨터를 삭제하려면 다음을 수행합니다.

1. **Azure Explorer** 보기에서 가상 컴퓨터를 마우스 오른쪽 단추로 클릭하고 **삭제**를 선택합니다.

   ![가상 컴퓨터 삭제 명령][DE01]

2. 확인 창에서 **예**를 클릭합니다. 

   ![가상 컴퓨터 삭제 확인 창][DE02]

## <a name="next-steps"></a>다음 단계
Azure 가상 컴퓨터 크기 및 가격 책정에 대한 자세한 내용은 다음 리소스를 참조하세요.

* Azure Virtual Machines 크기
  * [Azure에서 Windows 가상 컴퓨터에 대한 크기]
  * [Azure에서 Linux 가상 컴퓨터에 대한 크기]
* Azure Virtual Machines 가격 책정
  * [Windows 가상 컴퓨터 가격 책정]
  * [Linux 가상 컴퓨터 가격 책정]

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

[Azure에서 Windows 가상 컴퓨터에 대한 크기]: /azure/virtual-machines/virtual-machines-windows-sizes
[Azure에서 Linux 가상 컴퓨터에 대한 크기]: /azure/virtual-machines/virtual-machines-linux-sizes
[Windows 가상 컴퓨터 가격 책정]: /pricing/details/virtual-machines/windows/
[Linux 가상 컴퓨터 가격 책정]: /pricing/details/virtual-machines/linux/


<!-- IMG List -->

[RE01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR08.png
