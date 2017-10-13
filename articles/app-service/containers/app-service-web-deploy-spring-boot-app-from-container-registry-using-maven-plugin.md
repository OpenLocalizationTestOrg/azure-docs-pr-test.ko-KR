---
title: "Azure Web Apps의 Maven 플러그 인을 사용하여 Azure Container Registry의 Spring Boot 앱을 Azure App Service에 배포하는 방법"
description: "이 자습서는 Maven 플러그 인을 사용하여 Azure App Service에 Azure Container Registry의 Spring Boot 응용 프로그램을 배포하는 단계를 설명합니다."
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
ms.openlocfilehash: b087003b3a1e236e4a306678904107b8bf99395e
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2017
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-spring-boot-app-in-azure-container-registry-to-azure-app-service"></a>Azure Web Apps의 Maven 플러그 인을 사용하여 Azure Container Registry의 Spring Boot 앱을 Azure App Service에 배포하는 방법

**[Spring Framework]**는 Java 개발자가 웹, 모바일 및 API 응용 프로그램을 만들 수 있는 인기 있는 오픈 소스 프레임워크입니다. 이 자습서에서는 Spring을 사용하여 빠르게 시작하기 위한 규칙 기반 접근법인 [Spring Boot]를 사용하여 만든 샘플 앱을 사용합니다.

이 문서에서는 Azure Container Registry에 샘플 Spring Boot 응용 프로그램을 배포하고 Azure Web Apps의 Maven 플러그 인을 사용하여 Azure App Service에 응용 프로그램을 배포하는 방법을 보여줍니다.

> [!NOTE]
>
> Azure Web Apps의 Maven 플러그 인은 현재 미리 보기로 사용할 수 있습니다. 지금은 FTP 게시만 지원되지만 향후에 기능이 추가될 계획입니다.
>

## <a name="prerequisites"></a>필수 조건

이 자습서의 단계를 완료하려면 다음 필수 구성 요소가 필요합니다.

* Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [무료 Azure 계정]에 등록할 수 있습니다.
* [Azure CLI(명령줄 인터페이스)]
* 최신 [JDK(Java Development Kit)], 버전 1.7 이상
* Apache의 [Maven] 빌드 도구(버전 3)
* [Git] 클라이언트
* [Docker] 클라이언트

> [!NOTE]
>
> 이 자습서의 가상화 요구 사항으로 인해 가상 컴퓨터에는 이 문서의 단계를 따를 수 없습니다. 따라서 가상화 기능이 사용하도록 설정된 물리적 컴퓨터를 사용해야 합니다.
>

## <a name="clone-the-sample-spring-boot-on-docker-web-app"></a>Docker 웹앱에 샘플 Spring Boot 복제

이 섹션에서는 컨테이너화된 Spring Boot 응용 프로그램을 복제하고 로컬로 테스트합니다.

1. 명령 프롬프트 또는 터미널 창을 열고 Spring Boot 응용 프로그램을 저장할 로컬 디렉터리를 만들고 해당 디렉터리로 변경합니다. 예:
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   -- 또는 --
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. [Spring Boot on Docker 시작하기] 샘플 프로젝트를 방금 만든 디렉터리에 복제합니다. 예:
   ```shell
   git clone -b private-registry https://github.com/Microsoft/gs-spring-boot-docker
   ```

1. 디렉터리를 완료된 프로젝트로 변경합니다. 예:
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. Maven을 사용하여 JAR 파일을 빌드합니다. 예:
   ```shell
   mvn clean package
   ```

1. 웹앱을 만들면 Maven을 사용하여 웹앱을 시작합니다. 예:
   ```shell
   mvn spring-boot:run
   ```

1. 웹 브라우저를 사용하여 로컬로 이동하여 웹앱을 테스트합니다. 예를 들어, curl을 사용할 수 있는 경우 다음 명령을 사용할 수 있습니다.
   ```shell
   curl http://localhost:8080
   ```

1. **Hello Docker World** 메시지가 표시됩니다.

   ![로컬로 샘플 앱 찾아보기][SB01]

## <a name="create-an-azure-service-principal"></a>Azure 서비스 주체 만들기

이 섹션에서는 컨테이너를 Azure에 배포할 때 Maven 플러그 인에서 사용하는 Azure 서비스 주체를 만듭니다.

1. 명령 프롬프트를 엽니다.

1. Azure CLI를 사용하여 Azure 계정에 로그인합니다.
   ```azurecli
   az login
   ```
   지시에 따라 로그인 프로세스를 완료합니다.

1. Azure 서비스 주체 만들기
   ```azurecli
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   여기서 `uuuuuuuu`는 사용자 이름이고 `pppppppp`는 서비스 사용자에 대한 암호입니다.

1. Azure는 다음 예제와 유사한 JSON로 응답합니다.
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
   > 컨테이너를 Azure에 배포하도록 Maven 플러그 인을 구성하는 경우 이 JSON 응답의 값을 사용합니다. `aaaaaaaa`, `uuuuuuuu`, `pppppppp` 및 `tttttttt`는 다음 섹션에서 Maven `settings.xml` 파일을 구성할 때 이러한 값을 해당 요소에 쉽게 매핑할 수 있도록 이 예제에서 사용되는 자리 표시자 값입니다.
   >
   >

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a>Azure CLI를 사용하여 Azure Container Registry 만들기

1. 명령 프롬프트를 엽니다.

1. Azure 계정에 로그인합니다.
   ```azurecli
   az login
   ```

1. 이 문서에서 사용할 Azure 리소스에 대한 리소스 그룹을 만듭니다.
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   이 예제에서 `wingtiptoysresources`를 리소스 그룹의 고유 이름으로 바꿉니다.

1. Spring Boot 앱의 리소스 그룹에서 개인 Azure Container Registry를 만듭니다. 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   이 예제에서 `wingtiptoysregistry`를 컨테이너 레지스트리의 고유 이름으로 바꿉니다.

1. 컨테이너 레지스트리에 대한 암호를 검색합니다.
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

## <a name="add-your-azure-container-registry-and-azure-service-principal-to-your-maven-settings"></a>Maven 설정에 Azure Container Registry 및 Azure 서비스 주체 추가

1. 텍스트 편집기에서 Maven `settings.xml` 파일을 엽니다. 이 파일은 다음 예제와 같은 경로에 있을 수 있습니다.
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. 이 문서의 이전 섹션에서 *settings.xml* 파일의 `<servers>` 컬렉션에 Azure Container Registry 액세스 설정을 추가합니다. 예:

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
   `<id>` | 개인 Azure Container Registry 이름을 포함합니다.
   `<username>` | 개인 Azure Container Registry 이름을 포함합니다.
   `<password>` | 이 문서의 이전 섹션에서 검색된 암호를 포함합니다.

1. *settings.xml* 파일의 `<servers>` 컬렉션에 이 문서의 이전 섹션에 있는 Azure 서비스 주체 설정을 추가합니다. 예:

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
   `<id>` | Azure에 웹앱을 배포할 때 Maven을 사용하여 보안 설정을 조회하는 고유한 이름을 지정합니다.
   `<client>` | 서비스 사용자의 `appId` 값을 포함합니다.
   `<tenant>` | 서비스 사용자의 `tenant` 값을 포함합니다.
   `<key>` | 서비스 사용자의 `password` 값을 포함합니다.
   `<environment>` | 대상 Azure 클라우드 환경을 정의합니다. 이 예에서는 `AZURE`입니다. (환경의 전체 목록은 [Azure Web Apps의 Maven 플러그 인] 설명서에서 제공됩니다.)

1. *settings.xml* 파일을 저장하고 닫습니다.

## <a name="build-your-docker-container-image-and-push-it-to-your-azure-container-registry"></a>Docker 컨테이너 이미지 빌드 및 Azure Container Registry에 푸시

1. Spring Boot 응용 프로그램의 완료된 프로젝트 디렉터리로 이동합니다. (예: "*C:\SpringBoot\gs-spring-boot-docker\complete*" 또는 "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*") 텍스트 편집기를 사용하여 *pom.xml* 파일을 엽니다.

1. *pom.xml* 파일의 `<properties>` 컬렉션을 이 자습서의 이전 섹션에서 사용한 Azure Container Registry의 로그인 서버 값으로 업데이트합니다. 예:

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
   `<azure.containerRegistry>` | 개인 Azure Container Registry의 이름을 지정합니다.
   `<docker.image.prefix>` | 개인 컨테이너 레지스트리의 이름에 ".azurecr.io"를 추가하여 파생되는 개인 Azure Container Registry의 URL을 추가합니다.

1. *pom.xml* 파일에서 Docker 플러그 인의 `<plugin>`이 이 자습서의 이전 단계에서 로그인 서버 주소 및 레지스트리 이름에 대한 올바른 속성을 포함하는지 확인합니다. 예:

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
   `<serverId>` | 개인 Azure Container Registry의 이름을 포함하는 속성을 지정합니다.
   `<registryUrl>` | 개인 Azure Container Registry의 URL을 포함하는 속성을 지정합니다.

1. Spring Boot 응용 프로그램의 완성된 프로젝트 디렉터리로 이동하고 다음 명령을 실행하여 응용 프로그램을 다시 빌드하고 Azure Container Registry에 컨테이너를 푸시합니다.

   ```
   mvn package docker:build -DpushImage 
   ```

1. 선택 사항: [Azure Portal]로 이동하고 컨테이너 레지스트리에서 **gs-spring-boot-docker**라는 Docker 컨테이너 이미지가 있는지 확인합니다.

   ![Azure Portal에서 컨테이너 확인][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-to-azure"></a>pom.xml을 사용자 지정하고 컨테이너를 Azure에 빌드하고 배포합니다.

텍스트 편집기에서 Spring Boot 응용 프로그램에 대한 `pom.xml` 파일을 열고 `azure-webapp-maven-plugin`에 대한 `<plugin>` 요소를 찾습니다. 이 요소는 다음 예제와 유사합니다.

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

Maven 플러그 인에 대해 수정할 수 있는 여러 값이 있으며 이러한 각 요소에 대한 자세한 설명을 [Azure Web Apps의 Maven 플러그 인] 설명서에서 사용할 수 있습니다. 즉, 이 문서에서 강조 표시된 값은 여러 개입니다.

요소 | 설명
---|---|---
`<version>` | [Azure Web Apps의 Maven 플러그 인] 버전을 지정합니다. [Maven 중앙 리포지토리](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22)에 나열된 버전을 검사하여 최신 버전을 사용하고 있는지 확인해야 합니다.
`<authentication>` | Azure에 대한 인증 정보를 지정합니다. 이 예제에서는 `azure-auth`이 포함된 `<serverId>` 요소를 포함합니다. Maven에서는 해당 값을 사용하여 이 문서의 이전 섹션에 정의된 Maven *settings.xml* 파일에서 Azure 서비스 주체 값을 조회합니다.
`<resourceGroup>` | 대상 리소스 그룹, 즉, 이 예에서 `wingtiptoysresources`을 지정합니다. 리소스 그룹이 아직 존재하지 않는 경우 배포 중에 만들어집니다.
`<appName>` | 웹앱에 대한 대상 이름을 지정합니다. 이 예제에서는 대상 이름은 `maven-linux-app-${maven.build.timestamp}`이며 이 예제에서 충돌을 피하기 위해 여기에 `${maven.build.timestamp}` 접미사가 추가됩니다. (타임스탬프는 선택 사항입니다. 앱 이름에 대한 고유한 문자열을 지정할 수 있습니다.)
`<region>` | 대상 지역을 지정합니다. 이 예제에서는 `westus`입니다. (전체 목록은 [Azure Web Apps의 Maven 플러그 인] 설명서에서 제공됩니다.)
`<containerSettings>` | 컨테이너의 이름 및 URL을 포함하는 속성을 지정합니다.
`<appSettings>` | Maven에 대한 고유한 설정을 지정하여 Azure에 웹앱을 배포할 때 사용합니다. 이 예제에서 `<property>` 요소는 앱에 대한 포트를 지정하는 자식 요소의 이름/값 쌍을 포함합니다.

> [!NOTE]
>
> 이 예제에서 기본값의 포트를 변경하는 경우 포트 번호를 변경하도록 설정해야 합니다.
>

1. *pom.xml* 파일을 변경한 경우 이전에 사용하던 명령 프롬프트 또는 터미널 창에서 Maven를 사용하여 JAR 파일을 다시 작성합니다. 예:
   ```shell
   mvn clean package
   ```

1. Maven을 사용하여 Azure에 웹앱을 배포합니다. 예:
   ```shell
   mvn azure-webapp:deploy
   ```

Maven은 Azure에 웹앱을 배포합니다. 웹앱이 아직 없는 경우 생성됩니다.

> [!NOTE]
>
> *pom.xml* 파일의 `<region>` 요소에서 지정한 지역이 배포를 시작할 때 서버를 충분히 사용할 수 없는 경우 다음 예제와 비슷한 오류가 표시될 수 있습니다.
>
> ```
> [INFO] Start deploying to Web App maven-linux-app-20170804...
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.059 s
> [INFO] Finished at: 2017-08-04T12:15:47-07:00
> [INFO] Final Memory: 51M/279M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed to execute goal com.microsoft.azure:azure-webapp-maven-plugin:0.1.3:deploy (default-cli) on project gs-spring-boot-docker: null: MojoExecutionException: CloudException: OnError while emitting onNext value: retrofit2.Response.class
> ```
>
> 이 경우에 다른 지역을 지정하고 Maven 명령을 다시 실행하여 응용 프로그램을 배포할 수 있습니다.
>
>

웹을 배포하면 [Azure Portal]을 사용하여 작업을 관리할 수 있습니다.

* 웹앱은 **App Services**에 나열됩니다.

   ![Azure Portal App Services에 나열된 웹앱][AP01]

* 웹앱의 URL은 웹앱의 **개요**에 나열됩니다.

   ![웹앱의 URL 확인][AP02]

## <a name="next-steps"></a>다음 단계

이 문서에서 설명하는 다양한 기술에 대한 자세한 내용은 다음 문서를 참조하세요.

* [Azure Web Apps의 Maven 플러그 인]

* [Azure CLI에서 Azure에 로그인](/azure/xplat-cli-connect)

* [Azure CLI 2.0을 사용하여 Azure 서비스 주체 만들기](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Maven 설정 참조](https://maven.apache.org/settings.html)

* [Maven의 Docker 플러그 인]

<!-- URL List -->

[Azure CLI(명령줄 인터페이스)]: /cli/azure/overview
[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Azure Portal]: https://portal.azure.com/
[Azure Web Apps의 Maven 플러그 인]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Using a custom Docker image for Azure Web App on Linux]: tutorial-custom-docker-image.md
[Docker]: https://www.docker.com/
[Maven의 Docker 플러그 인]: https://github.com/spotify/docker-maven-plugin
[무료 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN 구독자 혜택]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker 시작하기]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/SB01.png
[CR01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/CR01.png
[AP01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP02.png
