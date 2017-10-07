---
title: "사용 하 여 Docker 컨테이너 스프링 부팅 앱 aaaPublish hello Azure Toolkit for Eclipse | Microsoft Docs"
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
ms.date: 06/21/2017
ms.author: robmcm
ms.openlocfilehash: 29390c49c339a1ebb87cb3951b21cea01c0da15f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a>Eclipse 용 Azure 도구 키트 hello를 사용 하 여 Docker 컨테이너 스프링 부팅 앱 게시

hello [Spring Framework] 은 오픈 소스 솔루션으로 Java 개발자가 엔터프라이즈 수준의 응용 프로그램을 만들 수 있도록 합니다. 중 만들어지는 hello 더 이상 인기 있는 프로젝트의 플랫폼은 [스프링 부팅], 독립 실행형 Java 응용 프로그램을 만들기 위한 있는 간단한 접근 방법을 제공 합니다.

[Docker] hello 배포, 배율 및 컨테이너에서 실행 되는 응용 프로그램의 관리 하는데 도움이 되는 오픈 소스 솔루션 자동화 됩니다.

이 자습서에서는 hello 단계 toodeploy 스프링 부팅 응용 프로그램으로 Docker 컨테이너 tooMicrosoft Azure Eclipse 용 Azure 도구 키트 hello를 사용 하 여 합니다.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repository"></a>Hello 기본 스프링 부팅 Docker 리포지토리 복제

### <a name="import-hello-public-repository"></a>Hello 공개 저장소 가져오기

hello 다음 단계에 관한 IntelliJ를 사용 하 여 hello 스프링 부팅 Docker 리포지토리 tooyour 로컬 컴퓨터를 복제 합니다. Toouse 명령줄 참조 [컨테이너 서비스를 Azure에서 Linux에서 스프링 부팅 응용 프로그램 배포][Deploy Spring Boot on Linux in ACS]합니다.

1. Eclipse를 엽니다.

1. **File** > **Import**를 차례로 클릭합니다.

   ![File Import 메뉴][CL01]

1. Hello 때 **가져오기** 대화 상자가 열립니다.

   a. **Git**를 확장합니다.

   b. **Projects from Git**를 선택합니다.
   
   c. **다음**을 누릅니다.

   ![Import 대화 상자][CL02]

1. Hello에 **리포지토리 원본 선택** 페이지:

   a. **Clone URI**를 선택합니다.
   
   b. **다음**을 누릅니다.

   ![Select Repository Source 페이지][CL03]

1. Hello에 **소스 Git 리포지토리에** 페이지:

   a. **URI**에 대해 `https://github.com/spring-guides/gs-spring-boot-docker.git`를 입력합니다. 이 단계는 자동으로 hello 채워야 **호스트** 및 **리포지토리 경로** hello로 필드 값을 수정 합니다.
   
   b. Git 사용자 이름 및 암호 tooenter 있어서는 안 되므로 hello 스프링 부팅 저장소는 public입니다.
   
   c. **다음**을 누릅니다.

   ![Source Git Repository 페이지][CL04]

1. Hello에 **분기 선택** 페이지 **다음**합니다.

   ![Branch Selection 페이지][CL05]

1. Hello에 **로컬 대상** 페이지:

   a. 사용자의 로컬 리포지토리를 넣을 hello 로컬 폴더를 지정 합니다.
   
   b. **다음**을 누릅니다.

   ![Local Destination 페이지][CL06]

1. Hello에 **프로젝트 가져오기 마법사 toouse 선택** 페이지:

   a. **Import as a general project**를 선택합니다.
   
   b. **다음**을 누릅니다.

   !["프로젝트 가져오기 마법사 toouse 선택" 페이지][CL07]

1. Hello에 **가져오기 프로젝트** 페이지:

   a. 프로젝트 이름을 지정합니다.
   
   b. **마침**을 클릭합니다.

   ![Import Projects 페이지][CL08]

1. Hello 리포지토리 복제 했습니다. Eclipse에서 나와 hello 파일 중 일부만 표시 됩니다.

   ![로컬 리포지토리][CL09]

### <a name="create-a-maven-project-from-your-local-repository"></a>로컬 리포지토리에서 Maven 프로젝트 만들기

hello 스프링 부팅 Docker 리포지토리가이 자습서에 사용 하 여 완료 된 Maven 프로젝트가 포함 되어 있습니다. 

1. **File** > **Import**를 차례로 클릭합니다.

   ![가져오기 hello 파일 메뉴 명령][CL01]

1. Hello 때 **가져오기** 대화 상자가 열립니다.

   a. **Maven**을 확장합니다.
   
   b. **Existing Maven Projects**를 선택합니다.
   
   c. **다음**을 누릅니다.

   ![Import 대화 상자][MV01]

1. Hello에 **Maven 프로젝트** 페이지:

   a. 에 대 한 **루트 디렉터리**, hello 지정 **완료** 로컬 리포지토리 폴더입니다.
   
   b. Hello 확장 **고급** 섹션을 사용자 지정 이름을 입력 **이름 템플릿**합니다.
   
   c. Hello에 대 한 선택 hello 상자 **pom.xml** hello 프로젝트 파일에에서 있습니다.
   
   d. **마침**을 클릭합니다.

   ![Maven Projects 페이지][MV02]

1. Hello Maven 프로젝트를 성공적으로 열면 Eclipse에 나열 된 두 번째 프로젝트를 확인할 수 있습니다.

   ![로컬 Maven 프로젝트][MV03]

## <a name="build-your-spring-boot-app-by-using-maven"></a>Maven을 사용하여 Spring Boot 앱 빌드

1. Hello Eclipse 프로젝트 탐색기에서에서 hello Maven 프로젝트를 선택 합니다.

1. **Run** > **Run As** > **Maven build**를 차례로 클릭합니다.

   ![Maven 빌드 명령 toorun][BU01]

1. 응용 프로그램을 성공적으로 빌드되면 hello 상태가 hello 콘솔 창에 표시 됩니다.

   ![성공적인 Maven 빌드][BU02]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Docker 컨테이너를 사용 하 여 웹 응용 프로그램 tooAzure 게시

1. Hello Eclipse 프로젝트 탐색기에서에서 hello Maven 프로젝트를 선택 합니다.

1. Azure hello 클릭 **게시** 메뉴를 차례로 클릭 **Docker 컨테이너로 게시**합니다.

   ![Docker 컨테이너로 게시 명령][PU01]

1. Hello 때 **Azure에서 Docker 컨테이너 배포** 대화 상자가 나타납니다.

   a. 사용자 지정 Docker 이미지 이름을 입력합니다.
   
   b. 에 대 한 **아티팩트 toodeploy**, hello 경로 toohello 지정 **gs-스프링-부팅-docker-0.1.0.jar** 방금 빌드한 파일입니다.

   ![Docker 옵션 지정][PU02]

   기존의 모든 Docker 호스트가 표시됩니다. 

1. Toodeploy tooan 기존 호스트를 선택 하면 toostep 5를 건너뛸 수 있습니다. 그렇지 않으면 다음 단계 toocreate 호스트 hello를 사용 합니다.

   a. **추가**를 클릭합니다.

      ![새 Docker 호스트 추가][PU03]

   b. Hello 때 **Docker 호스트 만들기** 대화 상자가 표시 됩니다, tooaccept hello 기본값을 선택 하거나 새 Docker 호스트에 대 한 사용자 지정 설정을 지정할 수 있습니다. (다양 한 설정, 참조에 대 한 자세한 설명은 hello [IntelliJ 용 Azure 도구 키트 hello를 사용 하 여 Docker 컨테이너와 웹 응용 프로그램을 게시할][Publish Container with Azure Toolkit].) 클릭 **다음** 어떤 설정 toouse 지정 했으면 합니다.

      ![Docker 호스트 옵션 지정][PU04]

   c. Azure 키 자격 증명 모음에서 toouse 기존 로그인 자격 증명을 선택할 수 있습니다 또는 새 Docker에 대 한 로그인 자격 증명 tooenter를 선택할 수 있습니다. 옵션을 지정하면 **마침**을 클릭합니다.

      ![Docker 호스트 자격 증명 지정][PU05]

1. Docker 호스트를 선택하고 **다음**을 클릭합니다.

   ![Docker 호스트 toouse 선택][PU06]

1. Hello hello의 마지막 페이지에 **Azure에서 Docker 컨테이너 배포** 대화 상자 hello 다음 옵션을 지정 합니다.

   a. Docker 컨테이너를 호스팅할 hello 컨테이너에 대 한 사용자 지정 이름을 toospecify를 선택할 수 있습니다 또는 hello 기본값을 그대로 사용할 수 있습니다.

   b. 구문 다음 hello를 사용 하 여 docker 호스트에 대 한 hello TCP 포트를 입력: *[외부 포트]*:*[내부 포트]*합니다. 예를 들어 **80:8080** 외부 포트 80 및 hello 기본 내부 스프링 부팅 포트 8080 지정 합니다.
   
      내부 포트 (예를 들어 파일 편집 하 여 hello application.yml) 사용자 지정을 Azure의 hello 올바른 라우팅 toooccur toospecify hello 포트 번호가 필요 합니다.

   c. 이러한 옵션을 구성했으면 **Finish**를 클릭합니다.

   ![Azure에 Docker 컨테이너 배포][PU07]

1. Azure 도구 키트 hello 게시 완료 되 면 hello Azure 활동 로그 표시 **게시 됨** hello 상태에 대 한 합니다.

   ![Docker 호스트를 성공적으로 배포][PU08]

## <a name="next-steps"></a>다음 단계

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL01.png
[CL02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL02.png
[CL03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL09.png

[MV01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV01.png
[MV02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV02.png
[MV03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV03.png

[BU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU02.png

[PU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU02.png
[PU03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU03.png
[PU04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU06.png
[PU07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU07.png
[PU08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU08.png
