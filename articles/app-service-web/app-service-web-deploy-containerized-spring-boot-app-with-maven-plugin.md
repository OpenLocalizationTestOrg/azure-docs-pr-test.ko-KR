---
title: "Azure 웹 앱 toodeploy 색인화 스프링 부팅 앱 tooAzure에 대 한 aaaHow toouse hello Maven 플러그 인"
description: "어떻게 toouse hello Maven 플러그 인 toodeploy Azure 웹 앱에 대 한 스프링 부팅 앱 tooAzure에 알아봅니다."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 08/07/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: e7e760d4ef5bd4c92a4126a50a2b12e5c8f2b4a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-containerized-spring-boot-app-tooazure"></a>어떻게 toouse hello Maven 플러그 인 toodeploy Azure 웹 앱에 대 한 컨테이너 화 된 스프링 부팅 앱 tooAzure

hello [Azure 웹 앱에 대 한 Maven 플러그인](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) 에 대 한 [Apache Maven](http://maven.apache.org/) Maven 프로젝트에 Azure 앱 서비스의 원활한 통합을 제공 하며 개발자 toodeploy 웹 앱에 대 한 hello 프로세스를 간소화 합니다. 앱 서비스 tooAzure 합니다.

이 문서에서는 Azure 웹 앱 toodeploy 용 hello Maven 플러그 인을 사용 하 여 Docker 컨테이너 tooAzure 응용 프로그램 서비스의에서 샘플 스프링 부팅 응용 프로그램입니다.

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
   git clone https://github.com/microsoft/gs-spring-boot-docker
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

## <a name="create-an-azure-service-principal"></a>Azure 서비스 주체 만들기

이 섹션에서는 Azure 컨테이너 tooAzure를 배포할 때 Maven 플러그 인 사용 하 여 hello 서비스 사용자를 만듭니다.

1. 명령 프롬프트를 엽니다.

1. 사용 하 여 Azure 계정에 로그인 Azure CLI hello:
   ```shell
   az login
   ```
   Hello 지침 toocomplete hello 로그인 프로세스를 따릅니다.

1. Azure 서비스 주체 만들기
   ```shell
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

## <a name="configure-maven-toouse-your-azure-service-principal"></a>Maven toouse Azure 서비스 사용자 구성

이 섹션에서는 컨테이너 tooAzure를 배포할 때 Maven에서 사용 하 여 Azure 서비스 주 tooconfigure hello 인증에서 hello 값을 사용 합니다.

1. 프로그램 Maven 열고 `settings.xml` 텍스트 편집기에서 파일;이 파일은 다음 예제는 hello와 같은 경로에 있을 수 있습니다.
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. 이 자습서 toohello의 hello 이전 섹션에서 Azure 서비스 보안 주체 설정 추가 `<servers>` hello에 대 한 컬렉션 *settings.xml* 파일; 예:

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

## <a name="optional-deploy-your-local-docker-file-toodocker-hub"></a>선택 사항: 배포에 로컬 Docker 파일 tooDocker 허브

Docker 계정이 있는 경우에 프로그램 Docker 컨테이너 이미지를 로컬에서 작성 하 고 tooDocker 허브를 푸시할 수 있습니다. 따라서, toodo 단계를 수행 하는 hello를 사용 합니다.

1. 열기 hello `pom.xml` 텍스트 편집기에서 스프링 부팅 응용 프로그램에 대 한 파일입니다.

1. Hello 찾을 `<imageName>` hello의 자식 요소 `<containerSettings>` 요소입니다.

1. 업데이트 hello `${docker.image.prefix}` 값을 Docker 계정 이름:
   ```xml
   <containerSettings>
      <imageName>mydockeraccountname/${project.artifactId}</imageName>
   </containerSettings>
   ```

1. Hello 다음 배포 방법 중 하나를 선택 합니다.

   * Maven에서로 로컬로 컨테이너 이미지를 구축 하 고 Docker toopush 사용 하 여 컨테이너 tooDocker 허브 여 키를 누릅니다.
      ```shell
      mvn clean package docker:build
      docker push
      ```
   
   * Hello 있으면 [Maven 용 Docker 플러그인] 설치를 자동으로 작성할 수 있으며, 사용자 컨테이너 이미지 tooDocker 허브를 사용 하 여 hello `-DpushImage` 매개 변수:
      ```shell
      mvn clean package docker:build -DpushImage
      ```

## <a name="optional-customize-your-pomxml-before-deploying-your-container-tooazure"></a>선택 사항: 사용자 지정 프로그램 pom.xml 컨테이너 tooAzure를 배포 하기 전에

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
         <resourceGroup>maven-plugin</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
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
`<resourceGroup>` | Hello 대상 리소스 그룹, 즉 지정 `maven-plugin` 이 예에서 합니다. hello 리소스 그룹이 아직 없는 경우 배포 중 만들어질 수 있습니다.
`<appName>` | 웹 앱에 대 한 hello 대상 이름을 지정합니다. 이 예제에서는 hello 대상 이름은 `maven-linux-app-${maven.build.timestamp}`여기서 hello `${maven.build.timestamp}` 이 예제에서는 tooavoid 충돌의 접미사가 추가 됩니다. (hello 타임 스탬프는 선택 사항) hello 응용 프로그램 이름에 대 한 고유 문자열을 모두 지정할 수 있습니다.
`<region>` | 이 예제는 hello 대상 지역을 지정 `westus`합니다. (전체 목록은 hello에 [Azure 웹 앱에 대 한 Maven 플러그인] 설명서입니다.)
`<appSettings>` | 웹 앱 tooAzure를 배포할 때 Maven toouse에 대 한 고유한 설정을 지정 합니다. 이 예제는 `<property>` 요소 앱에 대 한 hello 포트를 지정 하는 자식 요소의 이름/값 쌍을 포함 합니다.

> [!NOTE]
>
> 이 예에서 hello 설정을 toochange hello 포트 번호는 hello 기본값과에서 hello 포트를 변경 하는 경우에 필요 합니다.
>

## <a name="build-and-deploy-your-container-tooazure"></a>빌드 및 배포 컨테이너 tooAzure

준비 toodeploy는 hello 이전이 문서의 섹션에서에서 hello 설정을 모두 구성 했으면, 컨테이너 tooAzure 합니다. 따라서 toodo 단계를 수행 하는 hello를 사용 합니다.

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

Hello에 대 한 자세한 내용은이 문서에서 설명 하는 다양 한 기술 참조 문서 다음 hello:

* [Azure 웹 앱에 대 한 Maven 플러그인]

* [TooAzure hello Azure CLI에서 로그인](/azure/xplat-cli-connect)

* [어떻게 toouse hello Maven 플러그 인에 대 한 Azure 웹 앱 toodeploy 스프링 부팅 앱 tooAzure 앱 서비스](app-service-web-deploy-spring-boot-app-with-maven-plugin.md)

* [Azure CLI 2.0을 사용하여 Azure 서비스 주체 만들기](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Maven 설정 참조](https://maven.apache.org/settings.html)

* [Maven 용 Docker 플러그인]

<!-- URL List -->

[Azure 명령줄 인터페이스 (CLI)]: /cli/azure/overview
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Azure 포털]: https://portal.azure.com/
[Docker]: https://www.docker.com/
[Maven 용 Docker 플러그인]: https://github.com/spotify/docker-maven-plugin
[무료 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN 구독자 혜택]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[스프링 부팅 Docker 시작에]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Azure 웹 앱에 대 한 Maven 플러그인]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin/AP02.png
