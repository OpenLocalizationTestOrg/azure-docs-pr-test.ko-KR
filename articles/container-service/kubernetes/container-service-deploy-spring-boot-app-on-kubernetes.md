---
title: "Azure 컨테이너 서비스의 Kubernetes에서 스프링 부팅 앱 aaaDeploy | Microsoft Docs"
description: "이 자습서에서는 안내 합니다 하지만 hello 단계 toodeploy 스프링 부팅 응용 프로그램 Kubernetes 클러스터에서 Microsoft Azure에서."
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
ms.openlocfilehash: 2bf9df459f874a1f478f43cdd29992d86c370837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-hello-azure-container-service"></a>Hello Azure 컨테이너 서비스의에서 Kubernetes 클러스터에서 스프링 부팅 응용 프로그램 배포

hello  **[Spring Framework]**  는 인기 있는 오픈 소스 프레임 워크 Java 개발자가 웹, 모바일 및 API 응용 프로그램을 만들 수 있도록 합니다. 이 자습서를 사용 하 여 만든 샘플 응용 프로그램을 사용 하 여 [스프링 부팅], 스프링 tooget 사용 하기 위한 규칙 기반 접근 방식을 신속 하 게 시작 합니다.

**[Kubernetes]**  및  **[Docker]**  는 개발자가 하는 오픈 소스 솔루션 자동화 hello 배포, 배율 및를 실행 하는 응용 프로그램 관리 컨테이너입니다.

이 자습서에서는 경우에 이러한 두 인기 있는 오픈 소스 기술 toodevelop 결합 하 고 스프링 부팅 응용 프로그램 tooMicrosoft Azure를 배포 합니다. 사용 하는 보다 구체적으로,  *[스프링 부팅]*  응용 프로그램 개발에 대 한  *[Kubernetes]*  컨테이너 배포 및 hello에 대 한 [Azure 컨테이너 서비스 (ACS)] toohost 응용 프로그램입니다.

### <a name="prerequisites"></a>필수 조건

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

스프링 부팅 웹 응용 프로그램을 작성 하 고 로컬로 테스트 단계를 수행 하는 hello 설명 합니다.

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

1. 복제 hello [스프링 부팅 Docker 시작에] hello 디렉터리로 샘플 프로젝트입니다.
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. 완료 toohello 프로젝트 디렉터리를 변경 합니다.
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. Maven toobuild 및 실행된 hello 샘플 응용 프로그램을 사용 합니다.
   ```
   mvn package spring-boot:run
   ```

1. 테스트 hello 웹 앱 또는 hello 다음 toohttp://localhost:8080를 검색 하 여 `curl` 명령:
   ```
   curl http://localhost:8080
   ```

1. Hello 메시지 표시의 뒤에 표시 됩니다: **Docker는 Hello World**

   ![로컬로 샘플 앱 찾아보기][SB01]

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a>Azure 컨테이너 레지스트리 hello Azure CLI를 사용 하 여 만들기

1. 명령 프롬프트를 엽니다.

1. Azure 계정 tooyour에 로그인 합니다.
   ```azurecli
   az login
   ```

1. 이 자습서에 사용 된 Azure 리소스 hello에 대 한 리소스 그룹을 만듭니다.
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. Hello 리소스 그룹에서 사설 Azure 컨테이너 레지스트리를 만듭니다. hello 자습서 이후 단계에서 Docker 이미지 toothis 레지스트리로 hello 샘플 응용 프로그램을 푸시합니다. `wingtiptoysregistry`를 레지스트리의 고유한 이름으로 바꿉니다.
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-toohello-container-registry"></a>응용 프로그램 toohello 컨테이너 레지스트리 푸시

1. Maven 설치에 대 한 toohello 구성 디렉터리 탐색 (기본 ~/.m2/ 또는 C:\Users\username\.m2) 및 열기 hello *settings.xml* 파일 텍스트 편집기를 사용 합니다.

1. Hello Azure CLI에서에서 컨테이너 레지스트리에 대 한 hello 암호를 검색 합니다.
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
  "name": "password",
  "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. 추가 하면 Azure 컨테이너 레지스트리 id와 암호 tooa 새 `<server>` hello에 대 한 컬렉션 *settings.xml* 파일입니다.
hello `id` 및 `username` hello 레지스트리 hello 이름입니다. 사용 하 여 hello `password` hello 이전 명령 (따옴표 제외)의 값입니다.

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. 스프링 부팅 응용 프로그램에 대 한 완료 toohello 프로젝트 디렉터리를 이동 (예를 들어 "*C:\SpringBoot\gs-spring-boot-docker\complete*"또는"*/users/robert/SpringBoot/gs-spring-boot-docker / 전체*"), 및 열기 hello *pom.xml* 파일 텍스트 편집기를 사용 합니다.

1. 업데이트 hello `<properties>` hello에 대 한 컬렉션 *pom.xml* Azure 컨테이너 레지스트리에 대 한 hello 로그인 서버 값을 갖는 파일입니다.

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. 업데이트 hello `<plugins>` hello에 대 한 컬렉션 *pom.xml* 하는 hello 되므로 파일 `<plugin>` hello 로그인 서버 주소 및 레지스트리 이름 Azure 컨테이너 레지스트리에 대 한 포함 합니다.

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

1. 스프링 부팅 응용 프로그램에 대 한 완료 toohello 프로젝트 디렉터리를 이동 하 고 hello 명령 toobuild hello Docker 컨테이너 및 푸시 hello 이미지 toohello 레지스트리 다음 실행:

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  hello 다음의 유사한 tooone Maven 푸시 hello 이미지 tooAzure 하는 경우 오류 메시지가 나타날 수 있습니다.
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> 이 오류가 tooAzure hello Docker 명령줄에서 로그인 합니다.
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> 그런 다음 컨테이너를 푸시합니다.
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-acs-using-hello-azure-cli"></a>Hello Azure CLI를 사용 하는 ACS에서 Kubernetes 클러스터를 만듭니다

1. Azure Container Service에서 Kubernetes 클러스터를 만듭니다. hello 다음 명령은 만듭니다는 *kubernetes* hello에 대 한 클러스터 *wingtiptoys kubernetes* 리소스 그룹에 *wingtiptoys containerservice* hello 클러스터로 이름 및 *wingtiptoys kubernetes* hello DNS 접두사로:
   ```azurecli
   az acs create --orchestrator-type=kubernetes --resource-group=wingtiptoys-kubernetes \ 
    --name=wingtiptoys-containerservice --dns-prefix=wingtiptoys-kubernetes
   ```
   이 명령은 잠시 기다려 주십시오 toocomplete 합니다.

1. 설치 `kubectl` Azure CLI hello를 사용 하 여 합니다. Linux 사용자 tooprefix이이 명령에 있을 수 있습니다 `sudo` hello Kubernetes CLI 너무 배포 이후`/usr/local/bin`합니다.
   ```azurecli
   az acs kubernetes install-cli
   ```

1. Hello Kubernetes 웹 인터페이스에서 클러스터를 관리할 수 있도록 hello 클러스터 구성 정보를 다운로드 하 고 `kubectl`합니다. 
   ```azurecli
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes  \ 
    --name=wingtiptoys-containerservice
   ```

## <a name="deploy-hello-image-tooyour-kubernetes-cluster"></a>Hello 이미지 tooyour Kubernetes 클러스터 배포

이 자습서를 사용 하 여 hello 앱 배포 `kubectl`를 통해 있습니다 tooexplore hello 배포 hello Kubernetes 웹 인터페이스를 통해 합니다.

### <a name="deploy-with-hello-kubernetes-web-interface"></a>Hello Kubernetes 웹 인터페이스를 사용 하 여 배포

1. 명령 프롬프트를 엽니다.

1. 기본 브라우저에서 Kubernetes 클러스터에 대 한 hello 구성 웹 사이트를 엽니다.
   ```
   az acs kubernetes browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-containerservice
   ```

1. 브라우저에서 hello Kubernetes 구성 웹 사이트를 열면 hello 링크 클릭 너무**컨테이너 화 된 응용 프로그램 배포**:

   ![Kubernetes 구성 웹 사이트][KB01]

1. Hello 때 **컨테이너 화 된 응용 프로그램 배포** 페이지가 표시 되 면 hello 다음 옵션을 지정 합니다.

   a. **Specify app details below**를 선택합니다.

   b. Hello에 대 한 스프링 부팅 응용 프로그램 이름을 입력 **응용 프로그램 이름**; 예: "*스프링 부팅 docker gs*"입니다.

   c. Hello에 대 한 이전 버전에서 로그인 서버 및 컨테이너 이미지를 입력 **컨테이너 이미지**; 예: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"입니다.

   d. 선택 **외부** hello에 대 한 **서비스**합니다.

   e. Hello에서 외부 및 내부 포트를 지정 **포트** 및 **포트 대상** 텍스트 상자입니다.

   ![Kubernetes 구성 웹 사이트][KB02]


1. 클릭 **배포** toodeploy hello 컨테이너입니다.

   ![컨테이너 배포][KB05]

1. 응용 프로그램이 배포되면 **Services** 아래에 Spring Boot 응용 프로그램이 표시됩니다.

   ![Kubernetes 서비스][KB06]

1. 에 대 한 hello 링크를 클릭 하면 **외부 끝점**, 스프링 부팅 응용 프로그램을 Azure에서 실행을 확인할 수 있습니다.

   ![Kubernetes 서비스][KB07]

   ![Azure에서 샘플 앱 찾아보기][SB02]


### <a name="deploy-with-kubectl"></a>kubectl을 사용하여 배포

1. 명령 프롬프트를 엽니다.

1. Hello를 사용 하 여 hello Kubernetes 클러스터 컨테이너 실행 `kubectl run` 명령입니다. Kubernetes에서 응용 프로그램에 대 한 서비스 이름 및 hello 전체 이미지 이름을 지정 합니다. 예:
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   이 명령에서 다음이 적용됩니다.

   * hello 컨테이너 이름을 `gs-spring-boot-docker` hello 직후 지정 `run` 명령

   * hello `--image` hello 결합 된 서버 로그인 및 이미지 이름으로 매개 변수 지정`wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`

1. Hello를 사용 하 여 외부에서 Kubernetes 클러스터 노출 `kubectl expose` 명령입니다. Hello 공용 TCP 사용 되는 포트 tooaccess hello 앱 및 hello 내부 대상 포트에서 수신 대기 응용 프로그램, 서비스 이름을 지정 합니다. 예:
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   이 명령에서 다음이 적용됩니다.

   * hello 컨테이너 이름을 `gs-spring-boot-docker` hello 직후 지정 `expose deployment` 명령

   * hello `--type` 해당 hello 클러스터 부하 분산 장치를 사용 하 여 매개 변수 지정

   * hello `--port` 매개 변수는 hello 공용 TCP 포트 80 지정 합니다. 이 포트에서 hello 앱에 액세스합니다.

   * hello `--target-port` 매개 변수는 hello 내부 TCP 포트 8080 지정 합니다. hello 부하 분산 장치는이 포트에서 요청 tooyour 응용 프로그램을 전달합니다.

1. Hello 앱을 배포한 후 toohello 클러스터 hello 외부 IP 주소를 쿼리하고 웹 브라우저에서 엽니다.

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![Azure에서 샘플 앱 찾아보기][SB02]


## <a name="next-steps"></a>다음 단계

Azure에서 스프링 부팅을 사용 하는 방법에 대 한 자세한 내용은 다음 문서는 hello 참조:

* [스프링 부팅 응용 프로그램 toohello Azure 앱 서비스 배포](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [Hello 컨테이너 서비스를 Azure에서에서 Linux에서 스프링 부팅 응용 프로그램 배포](container-service-deploy-spring-boot-app-on-linux.md)

Java와 함께 Azure 사용에 대 한 자세한 내용은 참조 hello [Azure Java 개발자 센터] 및 hello [Visual Studio Team Services에 대 한 Java 도구]합니다.

Docker 예제 프로젝트에서 스프링 부팅 hello에 대 한 자세한 내용은 참조 [스프링 부팅 Docker 시작에]합니다.

링크를 따라 hello 스프링 부팅 응용 프로그램을 만드는 방법에 대 한 추가 정보가 표시 됩니다.

* 간단한 스프링 부팅 응용 프로그램을 만드는 방법에 대 한 자세한 내용은 https://start.spring.io/에서 스프링 Initializr hello를 참조 하십시오.

hello 다음 링크를 제공 Kubernetes Azure와 함께 사용 하는 방법에 대 한 추가 정보:

* [Container Service에서 Kubernetes 클러스터 시작](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-walkthrough)
* [Kubernetes 웹 hello를 사용 하 여 Azure 컨테이너 서비스와 UI](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-ui)

Kubernetes 명령줄 인터페이스를 사용 하는 방법에 대 한 자세한 정보는 hello에 **kubectl** 사용자 가이드에 <https://kubernetes.io/docs/user-guide/kubectl/>합니다.

hello Kubernetes 웹 사이트에 이미지를 사용 하 여 사설 레지스트리에서 설명 하는 몇 가지 문서:

* [Pod에 대한 서비스 계정 구성]
* [네임스페이스]
* [개인 레지스트리에서 이미지 끌어오기]

어떻게 toouse 사용자 지정 Docker 이미지를 azure에 대 한 추가 예제를 참조 하십시오. [Linux에서 Azure 웹 앱에 대 한 사용자 지정 Docker 이미지를 사용 하 여]합니다.

<!-- URL List -->

[Azure 명령줄 인터페이스 (CLI)]: /cli/azure/overview
[Azure 컨테이너 서비스 (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java 개발자 센터]: https://azure.microsoft.com/develop/java/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Linux에서 Azure 웹 앱에 대 한 사용자 지정 Docker 이미지를 사용 하 여]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[무료 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[JDK(Java Developer Kit)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Visual Studio Team Services에 대 한 Java 도구]: https://java.visualstudio.com/
[Kubernetes]: https://kubernetes.io/
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[Maven]: http://maven.apache.org/
[MSDN 구독자 혜택]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[스프링 부팅]: http://projects.spring.io/spring-boot/
[스프링 부팅 Docker 시작에]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Pod에 대한 서비스 계정 구성]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/
[네임스페이스]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
[개인 레지스트리에서 이미지 끌어오기]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/

<!-- IMG List -->

[SB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB01.png
[SB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB02.png

[AR01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR01.png
[AR02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR02.png
[AR03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR03.png
[AR04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR04.png

[KB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB01.png
[KB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB02.png
[KB03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB03.png
[KB04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB04.png
[KB05]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB05.png
[KB06]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB06.png
[KB07]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB07.png
