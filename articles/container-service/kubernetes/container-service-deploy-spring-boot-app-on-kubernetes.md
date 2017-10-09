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
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-hello-azure-container-service"></a><span data-ttu-id="985b1-103">Hello Azure 컨테이너 서비스의에서 Kubernetes 클러스터에서 스프링 부팅 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="985b1-103">Deploy a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>

<span data-ttu-id="985b1-104">hello  **[Spring Framework]**  는 인기 있는 오픈 소스 프레임 워크 Java 개발자가 웹, 모바일 및 API 응용 프로그램을 만들 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-104">hello **[Spring Framework]** is a popular open-source framework that helps Java developers create web, mobile, and API applications.</span></span> <span data-ttu-id="985b1-105">이 자습서를 사용 하 여 만든 샘플 응용 프로그램을 사용 하 여 [스프링 부팅], 스프링 tooget 사용 하기 위한 규칙 기반 접근 방식을 신속 하 게 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-105">This tutorial uses a sample app created using [Spring Boot], a convention-driven approach for using Spring tooget started quickly.</span></span>

<span data-ttu-id="985b1-106">**[Kubernetes]**  및  **[Docker]**  는 개발자가 하는 오픈 소스 솔루션 자동화 hello 배포, 배율 및를 실행 하는 응용 프로그램 관리 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-106">**[Kubernetes]** and **[Docker]** are open-source solutions that help developers automate hello deployment, scaling, and management of their applications  running in containers.</span></span>

<span data-ttu-id="985b1-107">이 자습서에서는 경우에 이러한 두 인기 있는 오픈 소스 기술 toodevelop 결합 하 고 스프링 부팅 응용 프로그램 tooMicrosoft Azure를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-107">This tutorial walks you though combining these two popular, open-source technologies toodevelop and deploy a Spring Boot application tooMicrosoft Azure.</span></span> <span data-ttu-id="985b1-108">사용 하는 보다 구체적으로,  *[스프링 부팅]*  응용 프로그램 개발에 대 한  *[Kubernetes]*  컨테이너 배포 및 hello에 대 한 [Azure 컨테이너 서비스 (ACS)] toohost 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-108">More specifically, you use *[Spring Boot]* for application development, *[Kubernetes]* for container deployment, and hello [Azure Container Service (ACS)] toohost your application.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="985b1-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="985b1-109">Prerequisites</span></span>

* <span data-ttu-id="985b1-110">Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [무료 Azure 계정]에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="985b1-111">hello [Azure 명령줄 인터페이스 (CLI)]합니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="985b1-112">최신 [JDK(Java Developer Kit)]</span><span class="sxs-lookup"><span data-stu-id="985b1-112">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="985b1-113">Apache의 [Maven] 빌드 도구(버전 3)</span><span class="sxs-lookup"><span data-stu-id="985b1-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="985b1-114">[Git] 클라이언트</span><span class="sxs-lookup"><span data-stu-id="985b1-114">A [Git] client.</span></span>
* <span data-ttu-id="985b1-115">[Docker] 클라이언트</span><span class="sxs-lookup"><span data-stu-id="985b1-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="985b1-116">이 자습서의 toohello 가상화 요구 사항 때문; 가상 컴퓨터에이 문서의 hello 단계를 따를 수 없는 물리적 컴퓨터를 사용 하 여 가상화 기능을 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-116">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-hello-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="985b1-117">Hello 스프링 부팅 Docker 시작 웹 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="985b1-117">Create hello Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="985b1-118">스프링 부팅 웹 응용 프로그램을 작성 하 고 로컬로 테스트 단계를 수행 하는 hello 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-118">hello following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="985b1-119">명령 프롬프트를 열고 응용 프로그램 및 toothat 디렉터리를 변경 합니다; 로컬 디렉터리 toohold 만들 예를 들어:</span><span class="sxs-lookup"><span data-stu-id="985b1-119">Open a command-prompt and create a local directory toohold your application, and change toothat directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="985b1-120">-- 또는 --</span><span class="sxs-lookup"><span data-stu-id="985b1-120">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="985b1-121">복제 hello [스프링 부팅 Docker 시작에] hello 디렉터리로 샘플 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-121">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory.</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="985b1-122">완료 toohello 프로젝트 디렉터리를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-122">Change directory toohello completed project.</span></span>
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. <span data-ttu-id="985b1-123">Maven toobuild 및 실행된 hello 샘플 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-123">Use Maven toobuild and run hello sample app.</span></span>
   ```
   mvn package spring-boot:run
   ```

1. <span data-ttu-id="985b1-124">테스트 hello 웹 앱 또는 hello 다음 toohttp://localhost:8080를 검색 하 여 `curl` 명령:</span><span class="sxs-lookup"><span data-stu-id="985b1-124">Test hello web app by browsing toohttp://localhost:8080, or with hello following `curl` command:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="985b1-125">Hello 메시지 표시의 뒤에 표시 됩니다: **Docker는 Hello World**</span><span class="sxs-lookup"><span data-stu-id="985b1-125">You should see hello following message displayed: **Hello Docker World**</span></span>

   ![로컬로 샘플 앱 찾아보기][SB01]

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a><span data-ttu-id="985b1-127">Azure 컨테이너 레지스트리 hello Azure CLI를 사용 하 여 만들기</span><span class="sxs-lookup"><span data-stu-id="985b1-127">Create an Azure Container Registry using hello Azure CLI</span></span>

1. <span data-ttu-id="985b1-128">명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-128">Open a command prompt.</span></span>

1. <span data-ttu-id="985b1-129">Azure 계정 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-129">Log in tooyour Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="985b1-130">이 자습서에 사용 된 Azure 리소스 hello에 대 한 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-130">Create a resource group for hello Azure resources used in this tutorial.</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. <span data-ttu-id="985b1-131">Hello 리소스 그룹에서 사설 Azure 컨테이너 레지스트리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-131">Create a private Azure container registry in hello resource group.</span></span> <span data-ttu-id="985b1-132">hello 자습서 이후 단계에서 Docker 이미지 toothis 레지스트리로 hello 샘플 응용 프로그램을 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-132">hello tutorial pushes hello sample app as a Docker image toothis registry in later steps.</span></span> <span data-ttu-id="985b1-133">`wingtiptoysregistry`를 레지스트리의 고유한 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-133">Replace `wingtiptoysregistry` with a unique name for your registry.</span></span>
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-toohello-container-registry"></a><span data-ttu-id="985b1-134">응용 프로그램 toohello 컨테이너 레지스트리 푸시</span><span class="sxs-lookup"><span data-stu-id="985b1-134">Push your app toohello container registry</span></span>

1. <span data-ttu-id="985b1-135">Maven 설치에 대 한 toohello 구성 디렉터리 탐색 (기본 ~/.m2/ 또는 C:\Users\username\.m2) 및 열기 hello *settings.xml* 파일 텍스트 편집기를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-135">Navigate toohello configuration directory for your Maven installation (default ~/.m2/ or C:\Users\username\.m2) and open hello *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="985b1-136">Hello Azure CLI에서에서 컨테이너 레지스트리에 대 한 hello 암호를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-136">Retrieve hello password for your container registry from hello Azure CLI.</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
  "name": "password",
  "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. <span data-ttu-id="985b1-137">추가 하면 Azure 컨테이너 레지스트리 id와 암호 tooa 새 `<server>` hello에 대 한 컬렉션 *settings.xml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-137">Add your Azure Container Registry id and password tooa new `<server>` collection in hello *settings.xml* file.</span></span>
<span data-ttu-id="985b1-138">hello `id` 및 `username` hello 레지스트리 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-138">hello `id` and `username` are hello name of hello registry.</span></span> <span data-ttu-id="985b1-139">사용 하 여 hello `password` hello 이전 명령 (따옴표 제외)의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-139">Use hello `password` value from hello previous command (without quotes).</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="985b1-140">스프링 부팅 응용 프로그램에 대 한 완료 toohello 프로젝트 디렉터리를 이동 (예를 들어 "*C:\SpringBoot\gs-spring-boot-docker\complete*"또는"*/users/robert/SpringBoot/gs-spring-boot-docker / 전체*"), 및 열기 hello *pom.xml* 파일 텍스트 편집기를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-140">Navigate toohello completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open hello *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="985b1-141">업데이트 hello `<properties>` hello에 대 한 컬렉션 *pom.xml* Azure 컨테이너 레지스트리에 대 한 hello 로그인 서버 값을 갖는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-141">Update hello `<properties>` collection in hello *pom.xml* file with hello login server value for your Azure Container Registry.</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="985b1-142">업데이트 hello `<plugins>` hello에 대 한 컬렉션 *pom.xml* 하는 hello 되므로 파일 `<plugin>` hello 로그인 서버 주소 및 레지스트리 이름 Azure 컨테이너 레지스트리에 대 한 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-142">Update hello `<plugins>` collection in hello *pom.xml* file so that hello `<plugin>` contains hello login server address and registry name for your Azure Container Registry.</span></span>

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

1. <span data-ttu-id="985b1-143">스프링 부팅 응용 프로그램에 대 한 완료 toohello 프로젝트 디렉터리를 이동 하 고 hello 명령 toobuild hello Docker 컨테이너 및 푸시 hello 이미지 toohello 레지스트리 다음 실행:</span><span class="sxs-lookup"><span data-stu-id="985b1-143">Navigate toohello completed project directory for your Spring Boot application and run hello following command toobuild hello Docker container and push hello image toohello registry:</span></span>

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  <span data-ttu-id="985b1-144">hello 다음의 유사한 tooone Maven 푸시 hello 이미지 tooAzure 하는 경우 오류 메시지가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-144">You may receive an error message that is similar tooone of hello following when Maven pushes hello image tooAzure:</span></span>
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="985b1-145">이 오류가 tooAzure hello Docker 명령줄에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-145">If you get this error, log in tooAzure from hello Docker command line.</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="985b1-146">그런 다음 컨테이너를 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-146">Then push your container:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-acs-using-hello-azure-cli"></a><span data-ttu-id="985b1-147">Hello Azure CLI를 사용 하는 ACS에서 Kubernetes 클러스터를 만듭니다</span><span class="sxs-lookup"><span data-stu-id="985b1-147">Create a Kubernetes Cluster on ACS using hello Azure CLI</span></span>

1. <span data-ttu-id="985b1-148">Azure Container Service에서 Kubernetes 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-148">Create a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="985b1-149">hello 다음 명령은 만듭니다는 *kubernetes* hello에 대 한 클러스터 *wingtiptoys kubernetes* 리소스 그룹에 *wingtiptoys containerservice* hello 클러스터로 이름 및 *wingtiptoys kubernetes* hello DNS 접두사로:</span><span class="sxs-lookup"><span data-stu-id="985b1-149">hello following command creates a *kubernetes* cluster in hello *wingtiptoys-kubernetes* resource group, with *wingtiptoys-containerservice* as hello cluster name, and *wingtiptoys-kubernetes* as hello DNS prefix:</span></span>
   ```azurecli
   az acs create --orchestrator-type=kubernetes --resource-group=wingtiptoys-kubernetes \ 
    --name=wingtiptoys-containerservice --dns-prefix=wingtiptoys-kubernetes
   ```
   <span data-ttu-id="985b1-150">이 명령은 잠시 기다려 주십시오 toocomplete 합니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-150">This command may take a while toocomplete.</span></span>

1. <span data-ttu-id="985b1-151">설치 `kubectl` Azure CLI hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-151">Install `kubectl` using hello Azure CLI.</span></span> <span data-ttu-id="985b1-152">Linux 사용자 tooprefix이이 명령에 있을 수 있습니다 `sudo` hello Kubernetes CLI 너무 배포 이후`/usr/local/bin`합니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-152">Linux users may have tooprefix this command with `sudo` since it deploys hello Kubernetes CLI too`/usr/local/bin`.</span></span>
   ```azurecli
   az acs kubernetes install-cli
   ```

1. <span data-ttu-id="985b1-153">Hello Kubernetes 웹 인터페이스에서 클러스터를 관리할 수 있도록 hello 클러스터 구성 정보를 다운로드 하 고 `kubectl`합니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-153">Download hello cluster configuration information so you can manage your cluster from hello Kubernetes web interface and `kubectl`.</span></span> 
   ```azurecli
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes  \ 
    --name=wingtiptoys-containerservice
   ```

## <a name="deploy-hello-image-tooyour-kubernetes-cluster"></a><span data-ttu-id="985b1-154">Hello 이미지 tooyour Kubernetes 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="985b1-154">Deploy hello image tooyour Kubernetes cluster</span></span>

<span data-ttu-id="985b1-155">이 자습서를 사용 하 여 hello 앱 배포 `kubectl`를 통해 있습니다 tooexplore hello 배포 hello Kubernetes 웹 인터페이스를 통해 합니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-155">This tutorial deploys hello app using `kubectl`, then allow you tooexplore hello deployment through hello Kubernetes web interface.</span></span>

### <a name="deploy-with-hello-kubernetes-web-interface"></a><span data-ttu-id="985b1-156">Hello Kubernetes 웹 인터페이스를 사용 하 여 배포</span><span class="sxs-lookup"><span data-stu-id="985b1-156">Deploy with hello Kubernetes web interface</span></span>

1. <span data-ttu-id="985b1-157">명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-157">Open a command prompt.</span></span>

1. <span data-ttu-id="985b1-158">기본 브라우저에서 Kubernetes 클러스터에 대 한 hello 구성 웹 사이트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-158">Open hello configuration website for your Kubernetes cluster in your default browser:</span></span>
   ```
   az acs kubernetes browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-containerservice
   ```

1. <span data-ttu-id="985b1-159">브라우저에서 hello Kubernetes 구성 웹 사이트를 열면 hello 링크 클릭 너무**컨테이너 화 된 응용 프로그램 배포**:</span><span class="sxs-lookup"><span data-stu-id="985b1-159">When hello Kubernetes configuration website opens in your browser, click hello link too**deploy a containerized app**:</span></span>

   ![Kubernetes 구성 웹 사이트][KB01]

1. <span data-ttu-id="985b1-161">Hello 때 **컨테이너 화 된 응용 프로그램 배포** 페이지가 표시 되 면 hello 다음 옵션을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-161">When hello **Deploy a containerized app** page is displayed, specify hello following options:</span></span>

   <span data-ttu-id="985b1-162">a.</span><span class="sxs-lookup"><span data-stu-id="985b1-162">a.</span></span> <span data-ttu-id="985b1-163">**Specify app details below**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-163">Select **Specify app details below**.</span></span>

   <span data-ttu-id="985b1-164">b.</span><span class="sxs-lookup"><span data-stu-id="985b1-164">b.</span></span> <span data-ttu-id="985b1-165">Hello에 대 한 스프링 부팅 응용 프로그램 이름을 입력 **응용 프로그램 이름**; 예: "*스프링 부팅 docker gs*"입니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-165">Enter your Spring Boot application name for hello **App name**; for example: "*gs-spring-boot-docker*".</span></span>

   <span data-ttu-id="985b1-166">c.</span><span class="sxs-lookup"><span data-stu-id="985b1-166">c.</span></span> <span data-ttu-id="985b1-167">Hello에 대 한 이전 버전에서 로그인 서버 및 컨테이너 이미지를 입력 **컨테이너 이미지**; 예: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"입니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-167">Enter your login server and container image from earlier for hello **Container image**; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span></span>

   <span data-ttu-id="985b1-168">d.</span><span class="sxs-lookup"><span data-stu-id="985b1-168">d.</span></span> <span data-ttu-id="985b1-169">선택 **외부** hello에 대 한 **서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-169">Choose **External** for hello **Service**.</span></span>

   <span data-ttu-id="985b1-170">e.</span><span class="sxs-lookup"><span data-stu-id="985b1-170">e.</span></span> <span data-ttu-id="985b1-171">Hello에서 외부 및 내부 포트를 지정 **포트** 및 **포트 대상** 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-171">Specify your external and internal ports in hello **Port** and **Target port** text boxes.</span></span>

   ![Kubernetes 구성 웹 사이트][KB02]


1. <span data-ttu-id="985b1-173">클릭 **배포** toodeploy hello 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-173">Click **Deploy** toodeploy hello container.</span></span>

   ![컨테이너 배포][KB05]

1. <span data-ttu-id="985b1-175">응용 프로그램이 배포되면 **Services** 아래에 Spring Boot 응용 프로그램이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-175">Once your application has been deployed, you will see your Spring Boot application listed under **Services**.</span></span>

   ![Kubernetes 서비스][KB06]

1. <span data-ttu-id="985b1-177">에 대 한 hello 링크를 클릭 하면 **외부 끝점**, 스프링 부팅 응용 프로그램을 Azure에서 실행을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-177">If you click hello link for **External endpoints**, you can see your Spring Boot application running on Azure.</span></span>

   ![Kubernetes 서비스][KB07]

   ![Azure에서 샘플 앱 찾아보기][SB02]


### <a name="deploy-with-kubectl"></a><span data-ttu-id="985b1-180">kubectl을 사용하여 배포</span><span class="sxs-lookup"><span data-stu-id="985b1-180">Deploy with kubectl</span></span>

1. <span data-ttu-id="985b1-181">명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-181">Open a command prompt.</span></span>

1. <span data-ttu-id="985b1-182">Hello를 사용 하 여 hello Kubernetes 클러스터 컨테이너 실행 `kubectl run` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-182">Run your container in hello Kubernetes cluster by using hello `kubectl run` command.</span></span> <span data-ttu-id="985b1-183">Kubernetes에서 응용 프로그램에 대 한 서비스 이름 및 hello 전체 이미지 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-183">Give a service name for your app in Kubernetes and hello full image name.</span></span> <span data-ttu-id="985b1-184">예:</span><span class="sxs-lookup"><span data-stu-id="985b1-184">For example:</span></span>
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   <span data-ttu-id="985b1-185">이 명령에서 다음이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-185">In this command:</span></span>

   * <span data-ttu-id="985b1-186">hello 컨테이너 이름을 `gs-spring-boot-docker` hello 직후 지정 `run` 명령</span><span class="sxs-lookup"><span data-stu-id="985b1-186">hello container name `gs-spring-boot-docker` is specified immediately after hello `run` command</span></span>

   * <span data-ttu-id="985b1-187">hello `--image` hello 결합 된 서버 로그인 및 이미지 이름으로 매개 변수 지정`wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span><span class="sxs-lookup"><span data-stu-id="985b1-187">hello `--image` parameter specifies hello combined login server and image name as `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span></span>

1. <span data-ttu-id="985b1-188">Hello를 사용 하 여 외부에서 Kubernetes 클러스터 노출 `kubectl expose` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-188">Expose your Kubernetes cluster externally by using hello `kubectl expose` command.</span></span> <span data-ttu-id="985b1-189">Hello 공용 TCP 사용 되는 포트 tooaccess hello 앱 및 hello 내부 대상 포트에서 수신 대기 응용 프로그램, 서비스 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-189">Specify your service name, hello public-facing TCP port used tooaccess hello app, and hello internal target port your app listens on.</span></span> <span data-ttu-id="985b1-190">예:</span><span class="sxs-lookup"><span data-stu-id="985b1-190">For example:</span></span>
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   <span data-ttu-id="985b1-191">이 명령에서 다음이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-191">In this command:</span></span>

   * <span data-ttu-id="985b1-192">hello 컨테이너 이름을 `gs-spring-boot-docker` hello 직후 지정 `expose deployment` 명령</span><span class="sxs-lookup"><span data-stu-id="985b1-192">hello container name `gs-spring-boot-docker` is specified immediately after hello `expose deployment` command</span></span>

   * <span data-ttu-id="985b1-193">hello `--type` 해당 hello 클러스터 부하 분산 장치를 사용 하 여 매개 변수 지정</span><span class="sxs-lookup"><span data-stu-id="985b1-193">hello `--type` parameter specifies that hello cluster uses load balancer</span></span>

   * <span data-ttu-id="985b1-194">hello `--port` 매개 변수는 hello 공용 TCP 포트 80 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-194">hello `--port` parameter specifies hello public-facing TCP port of 80.</span></span> <span data-ttu-id="985b1-195">이 포트에서 hello 앱에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-195">You access hello app on this port.</span></span>

   * <span data-ttu-id="985b1-196">hello `--target-port` 매개 변수는 hello 내부 TCP 포트 8080 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-196">hello `--target-port` parameter specifies hello internal TCP port of 8080.</span></span> <span data-ttu-id="985b1-197">hello 부하 분산 장치는이 포트에서 요청 tooyour 응용 프로그램을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-197">hello load balancer forwards requests tooyour app on this port.</span></span>

1. <span data-ttu-id="985b1-198">Hello 앱을 배포한 후 toohello 클러스터 hello 외부 IP 주소를 쿼리하고 웹 브라우저에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-198">Once hello app is deployed toohello cluster, query hello external IP address and open it in your web browser:</span></span>

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![Azure에서 샘플 앱 찾아보기][SB02]


## <a name="next-steps"></a><span data-ttu-id="985b1-200">다음 단계</span><span class="sxs-lookup"><span data-stu-id="985b1-200">Next steps</span></span>

<span data-ttu-id="985b1-201">Azure에서 스프링 부팅을 사용 하는 방법에 대 한 자세한 내용은 다음 문서는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="985b1-201">For more information about using Spring Boot on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="985b1-202">스프링 부팅 응용 프로그램 toohello Azure 앱 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="985b1-202">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [<span data-ttu-id="985b1-203">Hello 컨테이너 서비스를 Azure에서에서 Linux에서 스프링 부팅 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="985b1-203">Deploy a Spring Boot application on Linux in hello Azure Container Service</span></span>](container-service-deploy-spring-boot-app-on-linux.md)

<span data-ttu-id="985b1-204">Java와 함께 Azure 사용에 대 한 자세한 내용은 참조 hello [Azure Java 개발자 센터] 및 hello [Visual Studio Team Services에 대 한 Java 도구]합니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-204">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="985b1-205">Docker 예제 프로젝트에서 스프링 부팅 hello에 대 한 자세한 내용은 참조 [스프링 부팅 Docker 시작에]합니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-205">For more information about hello Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="985b1-206">링크를 따라 hello 스프링 부팅 응용 프로그램을 만드는 방법에 대 한 추가 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-206">hello following links provide additional information about creating Spring Boot applications:</span></span>

* <span data-ttu-id="985b1-207">간단한 스프링 부팅 응용 프로그램을 만드는 방법에 대 한 자세한 내용은 https://start.spring.io/에서 스프링 Initializr hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="985b1-207">For more information about creating a simple Spring Boot application, see hello Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="985b1-208">hello 다음 링크를 제공 Kubernetes Azure와 함께 사용 하는 방법에 대 한 추가 정보:</span><span class="sxs-lookup"><span data-stu-id="985b1-208">hello following links provide additional information about using Kubernetes with Azure:</span></span>

* [<span data-ttu-id="985b1-209">Container Service에서 Kubernetes 클러스터 시작</span><span class="sxs-lookup"><span data-stu-id="985b1-209">Get started with a Kubernetes cluster in Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-walkthrough)
* [<span data-ttu-id="985b1-210">Kubernetes 웹 hello를 사용 하 여 Azure 컨테이너 서비스와 UI</span><span class="sxs-lookup"><span data-stu-id="985b1-210">Using hello Kubernetes web UI with Azure Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-ui)

<span data-ttu-id="985b1-211">Kubernetes 명령줄 인터페이스를 사용 하는 방법에 대 한 자세한 정보는 hello에 **kubectl** 사용자 가이드에 <https://kubernetes.io/docs/user-guide/kubectl/>합니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-211">More information about using Kubernetes command-line interface is available in hello **kubectl** user guide at <https://kubernetes.io/docs/user-guide/kubectl/>.</span></span>

<span data-ttu-id="985b1-212">hello Kubernetes 웹 사이트에 이미지를 사용 하 여 사설 레지스트리에서 설명 하는 몇 가지 문서:</span><span class="sxs-lookup"><span data-stu-id="985b1-212">hello Kubernetes website has several articles that discuss using images in private registries:</span></span>

* <span data-ttu-id="985b1-213">[Pod에 대한 서비스 계정 구성]</span><span class="sxs-lookup"><span data-stu-id="985b1-213">[Configuring Service Accounts for Pods]</span></span>
* <span data-ttu-id="985b1-214">[네임스페이스]</span><span class="sxs-lookup"><span data-stu-id="985b1-214">[Namespaces]</span></span>
* <span data-ttu-id="985b1-215">[개인 레지스트리에서 이미지 끌어오기]</span><span class="sxs-lookup"><span data-stu-id="985b1-215">[Pulling an Image from a Private Registry]</span></span>

<span data-ttu-id="985b1-216">어떻게 toouse 사용자 지정 Docker 이미지를 azure에 대 한 추가 예제를 참조 하십시오. [Linux에서 Azure 웹 앱에 대 한 사용자 지정 Docker 이미지를 사용 하 여]합니다.</span><span class="sxs-lookup"><span data-stu-id="985b1-216">For additional examples for how toouse custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

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
