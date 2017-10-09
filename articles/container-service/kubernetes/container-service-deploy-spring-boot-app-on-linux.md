---
title: "컨테이너 서비스를 Azure에서 Linux에서 스프링 부팅 웹 응용 프로그램 aaaDeploy | Microsoft Docs"
description: "이 자습서에서는 하지만 hello 단계 toodeploy 스프링 부팅 응용 프로그램에서 Linux 웹 앱으로 Microsoft Azure에서."
services: container-service
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: container-service
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/04/2017
ms.author: asirveda;robmcm
ms.custom: mvc
ms.openlocfilehash: 2c44be1c7f66a38f48239001f0be9e90c7e6edef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-on-linux-in-hello-azure-container-service"></a>Hello 컨테이너 서비스를 Azure에서에서 Linux에서 스프링 부팅 응용 프로그램 배포

hello  **[Spring Framework]**  은 오픈 소스 솔루션으로 Java 개발자가 엔터프라이즈 수준의 응용 프로그램을 만들 수 있도록 합니다. 만들어지는 hello 더 이상 인기 있는 프로젝트 중 하나의 플랫폼은 [스프링 부팅], 독립 실행형 Java 응용 프로그램을 만들기 위한 간단한 방법을 제공 하는 합니다.

**[Docker]**  hello 배포, 배율 및 컨테이너에서 실행 되는 응용 프로그램의 관리 하는데 도움이 되는 오픈 소스 솔루션 자동화 됩니다.

이 자습서 안내 하 toodevelop Docker를 사용 하 고 hello에 스프링 부팅 응용 프로그램 tooa Linux 호스트를 배포할 [Azure 컨테이너 서비스 (ACS)]합니다.

## <a name="prerequisites"></a>필수 조건

이 자습서에서는 toocomplete hello 단계 순서를 필수 구성 요소를 다음 toohave hello가 필요 합니다.

* Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [무료 Azure 계정]에 등록할 수 있습니다.
* hello [Azure 명령줄 인터페이스 (CLI)]합니다.
* 최신 [JDK(Java Developer Kit)]
* Apache의 [Maven] 빌드 도구(버전 3)
* [Git] 클라이언트
* [Docker] 클라이언트

> [!NOTE]
>
> 이 자습서의 toohello 가상화 요구 사항 때문; 가상 컴퓨터에이 문서의 hello 단계를 따를 수 없는 물리적 컴퓨터를 사용 하 여 가상화 기능을 사용 하도록 설정 해야 합니다.
>

## <a name="create-hello-spring-boot-on-docker-getting-started-web-app"></a>Hello 스프링 부팅 Docker 시작 웹 응용 프로그램 만들기

hello 다음 단계에 관한 필요한 toocreate 간단한 스프링 부팅 웹 응용 프로그램 로컬 테스트 된 hello 단계입니다.

1. 명령 프롬프트를 열고 응용 프로그램 및 toothat 디렉터리를 변경 합니다; 로컬 디렉터리 toohold 만들 예를 들어:
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   -- 또는 --
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. 복제 hello [스프링 부팅 Docker 시작에] 샘플 프로젝트를 만든; hello 디렉터리 예:
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. 디렉터리 toohello 완료 된 프로젝트를 변경 합니다. 예를 들어:
   ```
   cd gs-spring-boot-docker/complete
   ```

1. Maven;를 사용 하 여 hello JAR 파일 빌드 예를 들어:
   ```
   mvn package
   ```

1. Hello 웹 응용 프로그램을 만든 후 변경 디렉터리 toohello `target` hello JAR 파일의 위치를 hello 웹 응용 프로그램을 시작 하는 디렉터리 예:
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. 웹 브라우저를 사용 하 여 로컬로 tooit 이동 하 여 hello 웹 앱을 테스트 합니다. 예를 들어 있는 경우 사용 가능한 curl 하 고 hello Tomcat 서버 toorun 포트 80에 구성:
   ```
   curl http://localhost
   ```

1. Hello 메시지 표시의 뒤에 표시 됩니다: **Docker는 Hello World!**

   ![로컬로 샘플 앱 찾아보기][SB01]

## <a name="create-an-azure-container-registry-toouse-as-a-private-docker-registry"></a>Azure 컨테이너 레지스트리 toouse 개인 Docker 레지스트리로 만들기

hello 다음 단계에 관한 hello Azure 포털 toocreate Azure 컨테이너 레지스트리를 사용 하 여입니다.

> [!NOTE]
>
> Azure 포털 hello 대신 toouse hello Azure CLI 원한다 면 hello 단계에 따라 [hello Azure CLI 2.0을 사용 하 여 개인 Docker 컨테이너 등록 만들기](../../container-registry/container-registry-get-started-azure-cli.md)합니다.
>

1. Toohello 찾아보기 [Azure 포털] 에 로그인 합니다.

   Hello에 hello 단계를 수행 tooyour hello Azure 포털에는 계정에 로그인 하면 [hello Azure 포털을 사용 하 여 개인 Docker 컨테이너 등록 만들기] hello에 대 한 단계를 수행 하는 hello에 paraphrased 문서 expediency의 찾았을 합니다.

1. Hello 메뉴 아이콘을 클릭 하 여 **+ 새로 만들기**, 클릭 **컨테이너**, 클릭 하 고 **Azure 컨테이너 레지스트리**합니다.
   
   ![새로운 Azure Container Registry 만들기][AR01]

1. Hello Azure 컨테이너 레지스트리 서식 파일에 대 한 hello 정보 페이지 표시 되 면 클릭 **만들기**합니다. 

   ![새로운 Azure Container Registry 만들기][AR02]

1. Hello 때 **만들기 컨테이너 레지스트리** 페이지가 표시 되 면 입력 프로그램 **레지스트리 이름** 및 **리소스 그룹**, 선택 **사용** 에 대 한 hello **Admin 사용자**, 클릭 하 고 **만들기**합니다.

   ![Azure Container Registry 설정 구성][AR03]

1. 컨테이너 레지스트리를 만든 후 hello Azure 포털에서에서 tooyour 컨테이너 레지스트리 키를 찾은 다음 클릭 **선택 키**합니다. Hello 사용자 이름 및 암호 hello 다음 단계를 기록해 둡니다.

   ![Azure Container Registry 선택키][AR04]

## <a name="configure-maven-toouse-your-azure-container-registry-access-keys"></a>Maven toouse Azure 컨테이너 레지스트리 액세스 키 구성

1. Maven 설치에 대 한 toohello 구성 디렉터리를 이동 하 고 hello 열고 *settings.xml* 파일 텍스트 편집기를 사용 합니다.

1. 이 자습서 toohello의 hello 이전 섹션에서 Azure 컨테이너 레지스트리 액세스 설정을 추가 `<servers>` hello에 대 한 컬렉션 *settings.xml* 파일; 예:

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. 스프링 부팅 응용 프로그램에 대 한 완료 toohello 프로젝트 디렉터리를 이동 (예: "*C:\SpringBoot\gs-spring-boot-docker\complete*"또는"*/users/robert/SpringBoot/gs-spring-boot-docker / 전체*"), 및 열기 hello *pom.xml* 파일 텍스트 편집기를 사용 합니다.

1. 업데이트 hello `<properties>` hello에 대 한 컬렉션 *pom.xml* hello;이 자습서의 이전 섹션에서 Azure 컨테이너 레지스트리에 대 한 hello 로그인 서버 값을 갖는 파일 예:

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. 업데이트 hello `<plugins>` hello에 대 한 컬렉션 *pom.xml* 하는 hello 되므로 파일 `<plugin>` hello 로그인 서버 주소 및 레지스트리 이름 hello이이 자습서의 이전 섹션에서 Azure 컨테이너 레지스트리에 대 한 포함 합니다. 예:

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
         <serverId>wingtiptoysregistry</serverId>
         <registryUrl>https://wingtiptoysregistry.azurecr.io</registryUrl>
      </configuration>
   </plugin>
   ```

1. 스프링 부팅 응용 프로그램에 대 한 완료 toohello 프로젝트 디렉터리를 이동 하 고 hello 다음 명령 toorebuild hello 응용 프로그램을 실행 푸시 hello 컨테이너 tooyour Azure 컨테이너 레지스트리:

   ```
   mvn package docker:build -DpushImage 
   ```

> [!NOTE]
>
> Docker 컨테이너 tooAzure 강제로 hello 뒤에 Docker 컨테이너를 성공적으로 만들어진 경우에 비슷한 tooone 오류 메시지가 나타날 수 있습니다.
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> 이 경우 toosign tooyour hello Docker 명령줄;에서 Azure 계정에서에서 할 수 있습니다. 예를 들어:
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> 컨테이너에서 hello 명령줄; 밀어 넣을 수 있으며 예를 들어:
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a>컨테이너 이미지를 사용하여 Azure App Service에서 Linux에 웹앱 만들기

1. Toohello 찾아보기 [Azure 포털] 에 로그인 합니다.

1. Hello 메뉴 아이콘을 클릭 하 여 **+ 새로 만들기**, 클릭 **웹 + 모바일**, 클릭 하 고 **Linux에서 웹 앱**합니다.
   
   ![Hello Azure 포털에서에서 새 웹 앱 만들기][LX01]

1. Hello 때 **Linux에서 웹 앱** 페이지가 표시 되 면 hello 다음 정보를 입력 합니다.

   a. Hello에 대 한 고유한 이름을 입력 **응용 프로그램 이름**; 예: "*wingtiptoyslinux*."

   b. 선택 하면 **구독** hello 드롭 다운 목록에서 합니다.

   c. 기존 선택 **리소스 그룹**, 하거나 이름 toocreate 새 리소스 그룹을 지정 합니다.

   d. 클릭 **구성 컨테이너** hello 다음 정보를 입력 합니다.

      * **개인 레지스트리**를 선택합니다.

      * **이미지 및 선택적 태그**: 이전에 사용한 컨테이너 이름을 지정합니다. 예: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"

      * **서버 URL**: 이전에 사용한 레지스트리 URL을 지정합니다. 예: "*https://wingtiptoysregistry.azurecr.io*"

      * **로그인 사용자 이름** 및 **암호**: 이전 단계에서 사용한 **액세스 키**의 로그인 자격 증명을 지정합니다.
   
   e. 클릭 하 여 모든 hello 정보를 입력 하 고 나면 **확인**합니다.

   ![웹앱 설정 구성][LX02]

1. **만들기**를 클릭합니다.

> [!NOTE]
>
> Azure가 인터넷 요청 tooembedded Tomcat 서버를 hello 표준 포트 80 또는 8080에서 실행 되는 자동으로 매핑합니다. 그러나 사용자 지정 포트에 포함 된 프로그램 Tomcat 서버 toorun를 구성한 경우 tooadd 포함된 Tomcat 서버에 대 한 hello 포트를 정의 하는 환경 변수 tooyour 웹 앱 필요 합니다. 따라서 toodo 단계를 수행 하는 hello를 사용 합니다.
>
> 1. Toohello 찾아보기 [Azure 포털] 에 로그인 합니다.
> 
> 2. Hello 아이콘을 클릭 **응용 프로그램 서비스**합니다. (아래의 hello 이미지의 항목 #1 참조).
>
> 3. Hello 목록에서 웹 앱을 선택 합니다. (항목 #2 hello 이미지 아래에 있습니다.)
>
> 4. **응용 프로그램 설정**을 클릭합니다. (# 3의에서 항목 아래의 hello 이미지입니다.)
>
> 5. Hello에 **앱 설정** 섹션에서 명명 된 새 환경 변수를 추가 **포트** hello 값에 대 한 사용자 지정 포트 번호를 입력 합니다. (항목 #4 hello 이미지 아래에 있습니다.)
>
> 6. **Save**를 클릭합니다. (항목 #5 hello 이미지 아래에 있습니다.)
>
> ![Hello Azure 포털에서에서 사용자 지정 포트 번호를 저장합니다.][LX03]
>

<!--
##  OPTIONAL: Configure hello embedded Tomcat server toorun on a different port

hello embedded Tomcat server in hello sample Spring Boot application is configured toorun on port 8080 by default. However, if you want toorun hello embedded Tomcat server toorun on a different port, such as port 80 for local testing, you can configure hello port by using hello following steps.

1. Go toohello *resources* directory (or create hello directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open hello *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify hello **server** setting so that hello server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close hello *application.yml* file.
-->

## <a name="next-steps"></a>다음 단계

Azure에서 스프링 부팅 응용 프로그램을 사용 하는 방법에 대 한 자세한 내용은 다음 문서는 hello 참조:

* [스프링 부팅 응용 프로그램 toohello Azure 앱 서비스 배포](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [Hello Azure 컨테이너 서비스의에서 Kubernetes 클러스터에서 스프링 부팅 응용 프로그램 배포](container-service-deploy-spring-boot-app-on-kubernetes.md)

Java와 함께 Azure 사용에 대 한 자세한 내용은 참조 hello [Azure Java 개발자 센터] 및 hello [Visual Studio Team Services에 대 한 Java 도구]합니다.

Docker 예제 프로젝트에서 스프링 부팅 hello에 대 한 자세한 내용은 참조 하십시오. [스프링 부팅 Docker 시작에]합니다.

스프링 부팅 응용 프로그램 시작 하기 도움말을 참조 hello **스프링 Initializr** https://start.spring.io/에 있습니다.

간단한 스프링 부팅 응용 프로그램을 만드는 것부터 시작 하는 방법에 대 한 자세한 내용은 https://start.spring.io/에서 스프링 Initializr hello를 참조 하십시오.

어떻게 toouse 사용자 지정 Docker 이미지를 azure에 대 한 추가 예제를 참조 하십시오. [Linux에서 Azure 웹 앱에 대 한 사용자 지정 Docker 이미지를 사용 하 여]합니다.

<!-- URL List -->

[Azure 명령줄 인터페이스 (CLI)]: /cli/azure/overview
[Azure 컨테이너 서비스 (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java 개발자 센터]: https://azure.microsoft.com/develop/java/
[Azure 포털]: https://portal.azure.com/
[hello Azure 포털을 사용 하 여 개인 Docker 컨테이너 등록 만들기]: /azure/container-registry/container-registry-get-started-portal
[Linux에서 Azure 웹 앱에 대 한 사용자 지정 Docker 이미지를 사용 하 여]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[무료 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[JDK(Java Developer Kit)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Visual Studio Team Services에 대 한 Java 도구]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN 구독자 혜택]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[스프링 부팅]: http://projects.spring.io/spring-boot/
[스프링 부팅 Docker 시작에]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/container-service-deploy-spring-boot-app-on-linux/SB01.png
[SB02]: ./media/container-service-deploy-spring-boot-app-on-linux/SB02.png

[AR01]: ./media/container-service-deploy-spring-boot-app-on-linux/AR01.png
[AR02]: ./media/container-service-deploy-spring-boot-app-on-linux/AR02.png
[AR03]: ./media/container-service-deploy-spring-boot-app-on-linux/AR03.png
[AR04]: ./media/container-service-deploy-spring-boot-app-on-linux/AR04.png

[LX01]: ./media/container-service-deploy-spring-boot-app-on-linux/LX01.png
[LX02]: ./media/container-service-deploy-spring-boot-app-on-linux/LX02.png
[LX03]: ./media/container-service-deploy-spring-boot-app-on-linux/LX03.png
