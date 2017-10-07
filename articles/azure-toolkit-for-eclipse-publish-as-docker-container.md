---
title: "사용 하 여 Docker 컨테이너 aaaPublish hello Azure Toolkit for Eclipse | Microsoft Docs"
description: "자세한 방법을 사용 하 여 Docker 컨테이너도 Azure는 웹 응용 프로그램 tooMicrosoft toopublish hello Azure Toolkit for Eclipse."
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
ms.openlocfilehash: 53ec3a7f7a171691024e03622fd48d6f1e257b50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a>Eclipse 용 Azure 도구 키트 hello를 사용 하 여 Docker 컨테이너와 웹 응용 프로그램 게시

Docker 컨테이너는 웹 응용 프로그램을 배포하는 데 널리 사용되는 방법입니다. Docker 컨테이너를 사용 하 여 개발자는 모든 프로젝트 파일 및 종속성을 배포 tooa 서버에 대 한 단일 패키지를 통합할 수 있습니다. Azure Toolkit for Eclipse hello를 추가 하 여 Java 개발자를 위한이 프로세스를 간소화 *Docker 컨테이너로 게시* 배포 tooMicrosoft Azure에 대 한 기능입니다. 이 문서 안내 hello 단계 필요한 toopublish 응용 프로그램 tooAzure Docker 컨테이너.

> [!NOTE]
> Docker에 대 한 자세한 정보는 hello [Docker 웹 사이트]합니다.
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Docker 컨테이너를 사용 하 여 웹 응용 프로그램 tooAzure 게시

1. Eclipse의 웹앱 프로젝트를 엽니다.

2. toostart hello **Docker 컨테이너로 게시** 마법사 hello 다음 중 하나를 수행 합니다.

   * Hello에 **탐색기** 볼 프로젝트를 마우스 오른쪽 단추로 클릭 하 여 **Azure**, 클릭 하 고 **Docker 컨테이너로 게시**합니다.

      ![탐색기 보기 Docker 컨테이너 명령으로 게시][PUB01]

   * Hello Eclipse 도구 모음에서 hello **게시** 단추를 선택한 다음 클릭 **Docker 컨테이너로 게시**합니다.

      ![Eclipse 도구 모음 Docker 컨테이너 명령으로 게시][PUB02]
      
    hello **Azure에서 Docker 컨테이너 배포** 마법사가 열립니다.

    ![hello Azure 마법사에서 Docker 컨테이너 배포][PUB03]

3. Hello에 **이미지 이름을 입력 hello 아티팩트 경로 선택 하 고 사용 되는 Docker 호스트 toobe 확인** 창에서 다음 hello지 않습니다:

    a. Hello에 **Docker 이미지 이름** 상자 Docker 호스트에 대 한 고유 이름을 입력 합니다. (hello를 이름으로 자동으로 만듭니다 있지만 수정할 수 있습니다.)

    b. hello **호스트** Docker 호스트를 이미 만든 영역에 표시 됩니다. Hello 다음 중 하나를 수행 합니다.

    * 기존 Docker 호스트를 사용 하도록 설정한 경우 웹 앱 tooit을 배포할 수 있습니다.
    * 새 Docker 호스트 toocreate 클릭 **추가**합니다.  
      
    hello **Docker 호스트 만들기** 대화 상자가 열립니다.

    ![Azure에 Docker 컨테이너 배포 마법사][PUB04a]

4. Hello에 **hello 새 가상 컴퓨터 구성** 창의 hello 다음 Docker 호스트에 대 한 옵션을 지정 합니다. (hello 마법사, hello 옵션의 대부분을 자동으로 생성 하지만 그 중 하나를 수정할 수 있습니다.)

   a. **이름**: hello Docker 호스트에 대 한 고유한 이름을 입력 합니다. (이 하지 hello hello Docker 이미지 이름을 이전에 지정한 것과 동일 합니다.)

   b. **구독**: hello 호스트에 사용 하는 Azure 구독을 입력 합니다.

   c. **지역**: 호스트에 위치한 hello 지리적 지역을 입력 합니다.

   d. Hello에 **호스트 OS 및 크기** 탭:
     * **호스트 OS**: 호스트에 포함 된 hello 가상 컴퓨터에 대 한 hello 운영 체제를 입력 합니다.
     * **크기**: 호스트에 대 한 hello 가상 컴퓨터 크기를 입력 합니다.

   e. Hello에 **리소스 그룹** 탭:
     * **새 리소스 그룹**: 호스트에 사용할 새 리소스 그룹을 만듭니다.
     * **기존 리소스 그룹**: Azure 계정에서 기존 리소스 그룹을 입력합니다.

   f. Hello에 **네트워크** 탭:
     * **새 가상 네트워크**: 호스트에 사용할 새 가상 네트워크를 만듭니다.
     * **기존 가상 네트워크**: Azure 계정에서 기존 가상 네트워크를 입력합니다.

   g. Hello에 **저장소** 탭:
     * **새 저장소 계정**: 호스트에 사용할 새 저장소 계정을 만듭니다.
     * **기존 저장소 계정**: Azure 계정에서 기존 저장소 계정을 입력합니다.

5. **다음**을 누릅니다.

6. Hello에 **자격 증명에 로그를 구성 및 포트 설정이** 창의 hello 다음 옵션 중 하나를 선택 합니다.

    * **Azure Key Vault에서 자격 증명 가져오기**: Azure 구독에 저장되어 있는 이전에 저장한 자격 증명 집합을 지정합니다.

      >[!NOTE]
      >Azure 키 자격 증명 모음 특정 계정 또는 서비스 사용자를 사용 하 여 만든 다른 계정 또는 서비스 hello 구독을 공유 하는 사용자가 자동으로 액세스할 수 없는 합니다. tooallow 다른 계정 또는 서비스 보안 주체 toouse 주요 자격 증명 모음 hello hello Azure 포털 tooadd hello 계정 또는 서비스 사용자를 사용 해야 합니다.

    * **새 로그인 자격 증명**: 새 로그인 자격 증명 집합을 만듭니다. 이 옵션을 선택 하는 경우 다음 hello지 않습니다.
    
      * Hello에 **VM 자격 증명** 탭에서 Docker 호스트의 가상 컴퓨터 로그인 자격 증명을 hello에 대 한 옵션 hello 다음 중 하나를 선택 합니다.

          * **사용자 이름**: 가상 컴퓨터 로그인 자격 증명에 대 한 hello 사용자 이름을 입력 합니다.
          * **암호** 및 **Confirm**: 가상 컴퓨터 로그인 자격 증명에 대 한 hello 암호를 입력 합니다.
          * **SSH**: Docker 호스트에 대 한 hello SSH (보안 셸) 설정을 입력 합니다. Hello 다음 옵션에서에서 선택할 수 있습니다.
            * **없음**: 가상 컴퓨터에서 SSH 연결을 허용하지 않게 지정합니다.
            * **자동 생성**: SSH를 통해 연결 하기 위한 hello 필수 설정을 자동으로 만듭니다.
            * **디렉터리에서 가져오기**: 이전에 저장된 SSH 설정 집합을 포함하는 디렉터리를 지정합니다. hello 디렉터리 hello 다음 두 개의 파일이 포함 되어야 합니다.
                * *id_rsa*: 사용자에 대 한 hello RSA id를 포함 합니다.
                * *id_rsa.pub*: 인증에 사용 되는 hello RSA 공개 키를 포함 합니다.
        
        ![Docker 호스트 만들기][PUB05]

      * Hello에 **Docker 디먼 자격 증명** 탭 hello 다음 옵션을 지정 합니다.

          * **Docker 데몬 포트**: Docker 호스트에 대 한 hello 고유 TCP 포트를 입력 합니다.
          * **TLS 보안**: Docker 호스트에 대 한 hello 전송 계층 보안 설정을 입력 합니다. Hello 다음 옵션에서에서 선택할 수 있습니다.
            * **없음**: 가상 컴퓨터에서 TLS 연결을 허용하지 않게 지정합니다.
            * **자동 생성**: TLS를 통해 연결에 대 한 hello 필수 설정을 자동으로 만듭니다.
            * **디렉터리에서 가져오기**: 이전에 저장된 TLS 설정 집합을 포함하는 디렉터리를 지정합니다. 보다 구체적으로, hello 디렉터리 hello 다음 6 개 파일이 포함 되어야 합니다.
                * *ca.pem* 및 *ca key.pem*: hello 인증서 및 TLS 인증 기관 hello에 대 한 공개 키를 포함 합니다.
                * *cert.pem* 및 *key.pem*: hello 클라이언트 인증서 및 TLS 인증에 사용 되는 공개 키를 포함 합니다.
                * *server.pem* 및 *서버 key.pem*: hello 서버 인증서와 hello 호스트에 대 한 공개 키를 포함 합니다.

        ![Docker 호스트 만들기][PUB06]

7. 모든 hello 앞에 정보를 입력 한 후 클릭 **마침**합니다.

8. Hello에 **Azure에서 Docker 컨테이너 배포** 마법사를 클릭 하 여 **다음**합니다.

   ![hello Azure 마법사에서 Docker 컨테이너 배포][PUB07]

9. Hello에 **hello Docker 컨테이너 toobe 만든 구성** 창에서 다음 hello지 않습니다:

   a. Hello에 **Docker 컨테이너 이름을** 상자 Docker 컨테이너에 대 한 고유 이름을 입력 합니다.

   b. Hello Docker 이미지를 다음 중 하나를 선택 합니다.
     * **미리 정의된 Docker 이미지**: Azure에서 기존 Docker 이미지를 지정합니다.

       >[!NOTE]
       >이 상자에서 Docker 이미지 hello 목록은 여러 그림으로 구성 된 Azure 도구 키트는 hello 구성 toopatch 프로그램 아티팩트가 자동으로 배포 됩니다.

     * **사용자 지정 Dockerfile**: 로컬 컴퓨터에서 이전에 저장된 Dockerfile을 지정합니다.

       >[!NOTE]
       >이 기능은 toodeploy 자신의 Dockerfile 알아보려는 개발자를 위한 보다 고급입니다. 그러나 toodevelopers 자신의 Dockerfile 제대로 빌드는이 옵션 tooensure를 사용 하는 중일으로 설명 합니다. hello Azure 도구 키트 하므로 hello Dockerfile에 문제가 hello 배포가 실패할 수 있습니다 hello 콘텐츠 사용자 지정 Dockerfile의 유효성을 검사 하지 않습니다. 또한 Azure 도구 키트 hello hello 사용자 지정 Dockerfile toocontain 웹 응용 프로그램 아티팩트를 요구 하 고 tooopen HTTP 연결을 시도 합니다. 개발자가 다른 아티팩트 형식을 게시하는 경우 배포 후에 무해한 오류가 표시될 수도 있습니다.

   c. **포트 설정을**: hello 고유 TCP 포트 바인딩을 Docker 컨테이너에 대 한 입력 합니다.

     ![hello 구성 hello Docker 컨테이너 toobe 만든 창][PUB08]

10. 모든 hello 이전 단계를 완료 한 후 클릭 **마침**합니다.

hello Azure 도구 키트는 Docker 컨테이너에 웹 앱 tooAzure 프로그램 배포를 시작 합니다. 

## <a name="next-steps"></a>다음 단계
Java Ide에 대 한 hello Azure 도구 키트에 대 한 자세한 내용은 hello 다음 리소스를 참조 하세요.

* [Eclipse용 Azure 도구 키트]
  * [Hello Eclipse 용 Azure 도구 키트의에서 새로운 기능]
  * [Hello Eclipse 용 Azure 도구 키트 설치]
  * [Eclipse 용 Azure 도구 키트 hello에 대 한 로그인 지침]
  * [Eclipse에서 Azure용 Hello World 웹앱 만들기]
* [IntelliJ용 Azure 도구 키트]
  * [Hello IntelliJ 용 Azure 도구 키트의에서 새로운 기능]
  * [IntelliJ 용 hello Azure 도구 키트 설치]
  * [로그인에 대 한 지침 Azure 도구 키트 hello IntelliJ]
  * [IntelliJ에서 Azure용 Hello World 웹앱 만들기]

Java와 함께 Azure를 사용하는 것에 대한 자세한 내용은 [Azure Java 개발자 센터] 및 [Visual Studio Team Services용 Java 도구]를 참조하세요.

Docker에 대 한 추가 리소스에 대 한 참조 hello 공식 [Docker 웹 사이트]합니다.

<!-- URL List -->

[Eclipse용 Azure 도구 키트]: ./azure-toolkit-for-eclipse.md
[IntelliJ용 Azure 도구 키트]: ./azure-toolkit-for-intellij.md
[Eclipse에서 Azure용 Hello World 웹앱 만들기]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[IntelliJ에서 Azure용 Hello World 웹앱 만들기]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Hello Eclipse 용 Azure 도구 키트 설치]: ./azure-toolkit-for-eclipse-installation.md
[IntelliJ 용 hello Azure 도구 키트 설치]: ./azure-toolkit-for-intellij-installation.md
[Eclipse 용 Azure 도구 키트 hello에 대 한 로그인 지침]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[로그인에 대 한 지침 Azure 도구 키트 hello IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Hello Eclipse 용 Azure 도구 키트의에서 새로운 기능]: ./azure-toolkit-for-eclipse-whats-new.md
[Hello IntelliJ 용 Azure 도구 키트의에서 새로운 기능]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java 개발자 센터]: https://azure.microsoft.com/develop/java/
[Visual Studio Team Services용 Java 도구]: https://java.visualstudio.com/

[Docker 웹 사이트]: https://www.docker.com/

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB08.png