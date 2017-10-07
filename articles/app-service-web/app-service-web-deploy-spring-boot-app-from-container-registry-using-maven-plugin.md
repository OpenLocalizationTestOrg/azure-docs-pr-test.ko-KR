---
title: "Azure 웹 앱 toodeploy Azure 컨테이너 레지스트리 tooAzure 앱 서비스에서에서 스프링 부팅 앱에 대 한 aaaHow toouse hello Maven 플러그 인"
description: "이 자습서 들을 하지만 hello 단계 toodeploy 스프링 부팅 응용 프로그램에서 Azure 컨테이너 레지스트리 tooAzure tooAzure 앱 서비스 Maven 플러그 인을 사용 하 여 합니다."
services: 
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/07/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 55b95e310c9ee186a6d77d941c5a620c2e259d8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-in-azure-container-registry-tooazure-app-service"></a>어떻게 toouse hello Maven 플러그 인 toodeploy Azure 웹 앱에 대 한 Azure 컨테이너 레지스트리 tooAzure 앱 서비스에서에서 스프링 부팅 앱

hello  **[Spring Framework]**  는 인기 있는 오픈 소스 프레임 워크 Java 개발자가 웹, 모바일 및 API 응용 프로그램을 만들 수 있도록 합니다. 이 자습서를 사용 하 여 만든 샘플 응용 프로그램을 사용 하 여 [스프링 부팅], 스프링 tooget 사용 하기 위한 규칙 기반 접근 방식을 신속 하 게 시작 합니다.

이 문서에서는 방법을 toodeploy 샘플 스프링 부팅 응용 프로그램 tooAzure 컨테이너 레지스트리 및 사용 하 여 hello Maven 플러그 인 toodeploy Azure 웹 앱에 대 한 앱 서비스 프로그램 응용 프로그램 tooAzure 보여줍니다.

> [!NOTE]
>
> Azure 웹 앱에 대 한 Maven 플러그인 hello는 현재 미리 보기로 사용할 수 있습니다. 지금은 FTP 게시만 지원 되지만 이후 hello에 대 한 추가 기능이 계획 합니다.
>

## <a name="prerequisites"></a>필수 조건

이 자습서에서는 toocomplete hello 단계 순서를 필수 구성 요소를 다음 toohave hello가 필요 합니다.

* Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [무료 Azure 계정]에 등록할 수 있습니다.
* hello [Azure 명령줄 인터페이스 (CLI)]합니다.
* 최신 [JDK(Java Development Kit)], 버전 1.7 이상
* Apache의 [Maven] 빌드 도구(버전 3)
* [Git] 클라이언트
* [Docker] 클라이언트

> [!NOTE]
>
> 이 자습서의 toohello 가상화 요구 사항 때문; 가상 컴퓨터에이 문서의 hello 단계를 따를 수 없는 물리적 컴퓨터를 사용 하 여 가상화 기능을 사용 하도록 설정 해야 합니다.
>

## <a name="clone-hello-sample-spring-boot-on-docker-web-app"></a>Docker 웹 응용 프로그램에 복제 hello 샘플 스프링 부팅

이 섹션에서는 컨테이너화된 Spring Boot 응용 프로그램을 복제하고 로컬로 테스트합니다.

1. 명령 프롬프트 또는 터미널 윈도우를 열고 스프링 부팅 응용 프로그램 및 toothat 디렉터리를 변경 합니다; 로컬 디렉터리 toohold 만들기 예를 들어:
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   -- 또는 --
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. 복제 hello [스프링 부팅 Docker 시작에] 샘플 프로젝트를 만든; hello 디렉터리 예:
   ```shell
   git clone -b private-registry https://github.com/Microsoft/gs-spring-boot-docker
   ```

1. 디렉터리 toohello 완료 된 프로젝트를 변경 합니다. 예를 들어:
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. Maven;를 사용 하 여 hello JAR 파일 빌드 예를 들어:
   ```shell
   mvn clean package
   ```

1. Hello 웹 응용 프로그램을 만들면 Maven;를 사용 하 여 hello 웹 응용 프로그램을 시작 합니다. 예를 들어:
   ```shell
   mvn spring-boot:run
   ```

1. 웹 브라우저를 사용 하 여 로컬로 tooit 이동 하 여 hello 웹 앱을 테스트 합니다. 예를 들어 hello curl을 사용할 수 있는 경우 다음 명령을 사용할 수 있습니다.
   ```shell
   curl http://localhost:8080
   ```

1. Hello 메시지 표시의 뒤에 표시 됩니다: **Docker는 Hello World**

   ![로컬로 샘플 앱 찾아보기][SB01]

## <a name="create-an-azure-service-principal"></a>Azure 서비스 주체 만들기

이 섹션에서는 Azure 컨테이너 tooAzure를 배포할 때 Maven 플러그 인 사용 하 여 hello 서비스 사용자를 만듭니다.

1. 명령 프롬프트를 엽니다.

1. 사용 하 여 Azure 계정에 로그인 Azure CLI hello:
   ```azurecli
   az login
   ```
   Hello 지침 toocomplete hello 로그인 프로세스를 따릅니다.

1. Azure 서비스 주체 만들기
   ```azurecli
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   여기서 `uuuuuuuu` hello 사용자 이름 및 `pppppppp` hello 서비스 사용자에 대 한 hello 암호입니다.

1. Azure는 다음 예제는 hello 유사한 JSON로 응답 합니다.
   ```json
   {
      "appId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
      "displayName": "uuuuuuuu",
      "name": "http://uuuuuuuu",
      "password": "pppppppp",
      "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

   > [!NOTE]
   >
   > Hello Maven 플러그 인 toodeploy 컨테이너 tooAzure를 구성할 때 hello 값이 JSON 응답을 사용 합니다. hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, 및 `tttttttt` 되는 자리 표시자 값은 사용이 예제에서는 toomake에 보다 쉽게 toomap 이러한 값 tootheir 각 요소가 사용자 Maven을 구성할 때 `settings.xml` hello에 다음 파일 단원을 참조 하십시오입니다.
   >
   >

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a>Azure 컨테이너 레지스트리 hello Azure CLI를 사용 하 여 만들기

1. 명령 프롬프트를 엽니다.

1. Azure 계정 tooyour에 로그인 합니다.
   ```azurecli
   az login
   ```

1. 이 문서의 hello에 대 한 리소스 그룹 사용 하 여 Azure 리소스를 만듭니다.
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   이 예제에서 `wingtiptoysresources`를 리소스 그룹의 고유 이름으로 바꿉니다.

1. 스프링 부팅 앱에 대 한 hello 리소스 그룹에서 사설 Azure 컨테이너 레지스트리를 만듭니다. 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   이 예제에서 `wingtiptoysregistry`를 컨테이너 레지스트리의 고유 이름으로 바꿉니다.

1. 컨테이너 레지스트리에 대 한 hello 암호를 검색 합니다.
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   Azure는 암호로 응답합니다. 예:
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-tooyour-maven-settings"></a>Azure 컨테이너 레지스트리 및 Azure 서비스 주체 tooyour Maven 설정 추가

1. 프로그램 Maven 열고 `settings.xml` 텍스트 편집기에서 파일;이 파일은 다음 예제는 hello와 같은 경로에 있을 수 있습니다.
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. 이 문서 toohello의 hello 이전 섹션에서 Azure 컨테이너 레지스트리 액세스 설정을 추가 `<servers>` hello에 대 한 컬렉션 *settings.xml* 파일; 예:

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   여기서,
   요소 | 설명
   ---|---|---
   `<id>` | 개인 Azure 컨테이너 레지스트리 hello 이름을 포함합니다.
   `<username>` | 개인 Azure 컨테이너 레지스트리 hello 이름을 포함합니다.
   `<password>` | Hello이 문서의 이전 섹션에서 검색 하는 hello 암호가 포함 됩니다.

1. 이 문서 toohello의 이전 단원에서 Azure 서비스 보안 주체 설정 추가 `<servers>` hello에 대 한 컬렉션 *settings.xml* 파일; 예:

   ```xml
   <servers>
      <server>
        <id>azure-auth</id>
         <configuration>
            <client>aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa</client>
            <tenant>tttttttt-tttt-tttt-tttt-tttttttttttt</tenant>
            <key>pppppppp</key>
            <environment>AZURE</environment>
         </configuration>
      </server>
   </servers>
   ```
   여기서,
   요소 | 설명
   ---|---|---
   `<id>` | Maven 웹 응용 프로그램 tooAzure를 배포할 때 toolook 보안 설정을 사용 하는 고유한 이름을 지정 합니다.
   `<client>` | Hello 포함 `appId` 서비스 사용자의 값입니다.
   `<tenant>` | Hello 포함 `tenant` 서비스 사용자의 값입니다.
   `<key>` | Hello 포함 `password` 서비스 사용자의 값입니다.
   `<environment>` | hello 대상 Azure 클라우드 환경 정의 `AZURE` 이 예에서 합니다. (전체 환경 목록을 hello 영어로 [Azure 웹 앱에 대 한 Maven 플러그인] 설명서)

1. 저장 후 닫기 hello *settings.xml* 파일입니다.

## <a name="build-your-docker-container-image-and-push-it-tooyour-azure-container-registry"></a>프로그램 Docker 컨테이너 이미지를 빌드하고 tooyour Azure 컨테이너 레지스트리 푸시

1. 스프링 부팅 응용 프로그램에 대 한 완료 toohello 프로젝트 디렉터리 (예: 탐색 "*C:\SpringBoot\gs-spring-boot-docker\complete*"또는"*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), 및 열기 hello *pom.xml* 있는 파일을 텍스트 편집기입니다.

1. 업데이트 hello `<properties>` hello에 대 한 컬렉션 *pom.xml* hello;이 자습서의 이전 섹션에서 Azure 컨테이너 레지스트리에 대 한 hello 로그인 서버 값을 갖는 파일 예:

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   여기서,
   요소 | 설명
   ---|---|---
   `<azure.containerRegistry>` | 개인 Azure 컨테이너 레지스트리 hello 이름을 지정합니다.
   `<docker.image.prefix>` | 사용자 개인 Azure 컨테이너 레지스트리에 추가 하 여 파생의 hello URL을 지정 ". azurecr.io" 개인 컨테이너 레지스트리 toohello 이름입니다.

1. 되어 있는지 확인 `<plugin>` 있는 hello Docker 플러그 인에 대 한 프로그램 *pom.xml* 파일이이 자습서에서는 hello hello 로그인 주소와 레지스트리에서에서 서버 이름 hello 이전 단계에 대 한 올바른 속성을 포함 합니다. 예:

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <registryUrl>https://${docker.image.prefix}</registryUrl>
         <serverId>${azure.containerRegistry}</serverId>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```
   여기서,
   요소 | 설명
   ---|---|---
   `<serverId>` | 개인 Azure 컨테이너 레지스트리의 이름이 포함 되어 hello 속성을 지정 합니다.
   `<registryUrl>` | 개인 Azure 컨테이너 레지스트리 hello URL이 포함 된 hello 속성을 지정 합니다.

1. 스프링 부팅 응용 프로그램에 대 한 완료 toohello 프로젝트 디렉터리를 이동 하 고 hello 다음 명령 toorebuild hello 응용 프로그램을 실행 푸시 hello 컨테이너 tooyour Azure 컨테이너 레지스트리:

   ```
   mvn package docker:build -DpushImage 
   ```

1. 선택 사항: toohello 찾아보기 [Azure 포털] 라는 Docker 컨테이너 이미지 인지 확인 하 고 **스프링 부팅 docker gs** 컨테이너 레지스트리에 합니다.

   ![Azure Portal에서 컨테이너 확인][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-tooazure"></a>프로그램 pom.xml 사용자 지정 합니다 빌드 및 컨테이너 tooAzure 배포

열기 hello `pom.xml` 텍스트 편집기에서 스프링 부팅 응용 프로그램에 대 한 파일을 찾은 후 hello `<plugin>` 요소에 대 한 `azure-webapp-maven-plugin`합니다. 이 요소에는 다음 예제는 hello와 유사 합니다.

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>wingtiptoysresources</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
            <registryUrl>https://${docker.image.prefix}</registryUrl>
            <serverId>${azure.containerRegistry}</serverId>
         </containerSettings>
         <appSettings>
            <property>
               <name>PORT</name>
               <value>8080</value>
            </property>
         </appSettings>
      </configuration>
   </plugin>
   ```

Hello Maven 플러그 인에 대해 수정할 수 있는 값이 여러 개인 및 이러한 각 요소에 대 한 자세한 설명을 hello 영어로 [Azure 웹 앱에 대 한 Maven 플러그인] 설명서입니다. 즉, 이 문서에서 강조 표시된 값은 여러 개입니다.

요소 | 설명
---|---|---
`<version>` | Hello 버전의 hello 지정 [Azure 웹 앱에 대 한 Maven 플러그인]합니다. Hello에 나열 된 hello 버전을 검사 해야 하면 [Maven 중앙 리포지토리](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) 사용 중인 tooensure hello 최신 버전입니다.
`<authentication>` | 이 예제에 포함 된 Azure의 hello 인증 정보를 지정 된 `<serverId>` 포함 된 요소 `azure-auth`; Maven hello Azure 서비스 주체 값을 해당 값 toolook 프로그램 Maven에서 사용 하 여 *settings.xml* 이 문서의 이전 섹션에 정의 된 파일입니다.
`<resourceGroup>` | Hello 대상 리소스 그룹, 즉 지정 `wingtiptoysresources` 이 예에서 합니다. hello 리소스 그룹이 아직 없는 경우 배포 중 만들어질 수 있습니다.
`<appName>` | 웹 앱에 대 한 hello 대상 이름을 지정합니다. 이 예제에서는 hello 대상 이름은 `maven-linux-app-${maven.build.timestamp}`여기서 hello `${maven.build.timestamp}` 이 예제에서는 tooavoid 충돌의 접미사가 추가 됩니다. (hello 타임 스탬프는 선택 사항) hello 응용 프로그램 이름에 대 한 고유 문자열을 모두 지정할 수 있습니다.
`<region>` | 이 예제는 hello 대상 지역을 지정 `westus`합니다. (전체 목록은 hello에 [Azure 웹 앱에 대 한 Maven 플러그인] 설명서입니다.)
`<containerSettings>` | Hello 이름 및 컨테이너의 URL을 포함 하는 hello 속성을 지정 합니다.
`<appSettings>` | 웹 앱 tooAzure를 배포할 때 Maven toouse에 대 한 고유한 설정을 지정 합니다. 이 예제는 `<property>` 요소 앱에 대 한 hello 포트를 지정 하는 자식 요소의 이름/값 쌍을 포함 합니다.

> [!NOTE]
>
> 이 예에서 hello 설정을 toochange hello 포트 번호는 hello 기본값과에서 hello 포트를 변경 하는 경우에 필요 합니다.
>

1. Hello 명령 프롬프트 또는 이전에 사용 하 던 터미널 창에서 모든 변경 내용을 toohello을 만든 경우 Maven를 사용 하 여 hello JAR 파일을 다시 작성 *pom.xml* 파일; 예:
   ```shell
   mvn clean package
   ```

1. Maven;를 사용 하 여 웹 응용 프로그램 tooAzure 배포 예를 들어:
   ```shell
   mvn azure-webapp:deploy
   ```

Maven 프로그램 웹 응용 프로그램 tooAzure; 배포 웹 앱 hello가 아직 없는 경우 생성 됩니다.

> [!NOTE]
>
> 경우 hello에서 지정 하는 hello 지역 `<region>` 의 요소 프로그램 *pom.xml* 파일에 없는 사용할 수 있는 충분 한 서버 배포를 시작 하는 경우, 다음 예제에서는 오류 유사한 toohello 표시 될 수 있습니다.
>
> ```
> [INFO] Start deploying tooWeb App maven-linux-app-20170804...
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.059 s
> [INFO] Finished at: 2017-08-04T12:15:47-07:00
> [INFO] Final Memory: 51M/279M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed tooexecute goal com.microsoft.azure:azure-webapp-maven-plugin:0.1.3:deploy (default-cli) on project gs-spring-boot-docker: null: MojoExecutionException: CloudException: OnError while emitting onNext value: retrofit2.Response.class
> ```
>
> 이 경우 다른 영역을 다시 실행 Maven 명령 toodeploy 응용 프로그램를 hello를 지정할 수 있습니다.
>
>

웹 배포 된 수 toomanage 됩니다 hello를 사용 하 여 [Azure 포털]합니다.

* 웹앱은 **App Services**에 나열됩니다.

   ![Azure Portal App Services에 나열된 웹앱][AP01]

* 웹 앱 hello에 나열 됩니다에 대 한 URL을 hello 및 **개요** 웹 앱에 대 한:

   ![웹 앱에 대 한 hello URL 확인][AP02]

## <a name="next-steps"></a>다음 단계

Hello에 대 한 자세한 내용은이 문서에서 설명 하는 다양 한 기술 참조 문서 다음 hello:

* [Azure 웹 앱에 대 한 Maven 플러그인]

* [TooAzure hello Azure CLI에서 로그인](/azure/xplat-cli-connect)

* [Azure CLI 2.0을 사용하여 Azure 서비스 주체 만들기](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Maven 설정 참조](https://maven.apache.org/settings.html)

* [Maven의 Docker 플러그 인]

<!-- URL List -->

[Azure 명령줄 인터페이스 (CLI)]: /cli/azure/overview
[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Azure 포털]: https://portal.azure.com/
[Azure 웹 앱에 대 한 Maven 플러그인]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[Maven의 Docker 플러그 인]: https://github.com/spotify/docker-maven-plugin
[무료 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN 구독자 혜택]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[스프링 부팅]: http://projects.spring.io/spring-boot/
[스프링 부팅 Docker 시작에]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/SB01.png
[CR01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/CR01.png
[AP01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP02.png
