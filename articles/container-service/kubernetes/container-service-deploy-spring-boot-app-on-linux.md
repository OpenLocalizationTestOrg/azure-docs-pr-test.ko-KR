---
title: "Azure Container Service에서 Linux에 Spring Boot Web App 배포 | Microsoft Docs"
description: "이 자습서에서는 Microsoft Azure에서 Linux Web App으로 Spring Boot 응용 프로그램을 배포하는 단계를 설명합니다."
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
ms.openlocfilehash: 5f0b470bd46cfeaf00b3092dbe9db507ed50f622
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-spring-boot-application-on-linux-in-the-azure-container-service"></a><span data-ttu-id="c47eb-103">Azure Container Service에서 Linux에 Spring Boot 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="c47eb-103">Deploy a Spring Boot application on Linux in the Azure Container Service</span></span>

<span data-ttu-id="c47eb-104">**[Spring Framework]**는 Java 개발자가 엔터프라이즈 수준의 응용 프로그램을 만드는 데 도움이 되는 오픈 소스 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-104">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="c47eb-105">해당 플랫폼을 기반으로 하여 빌드되는 인기 있는 프로젝트 중 하나가 [Spring Boot]입니다. 이 프로젝트는 독립 실행형 Java 응용 프로그램을 만드는 간단한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-105">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span>

<span data-ttu-id="c47eb-106">**[Docker]**는 개발자가 컨테이너에서 실행되는 응용 프로그램의 배포, 크기 조정 및 관리를 자동화하는 데 도움이 되는 오픈 소스 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-106">**[Docker]** is open-source solutions that helps developers automate the deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="c47eb-107">이 자습서에서는 Docker를 사용하여 [ACS(Azure Container Service)]에서 Spring Boot 응용 프로그램을 개발하고 Linux 호스트에 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-107">This tutorial walks you through using Docker to develop and deploy a Spring Boot application to a Linux host in the [Azure Container Service (ACS)].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c47eb-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c47eb-108">Prerequisites</span></span>

<span data-ttu-id="c47eb-109">이 자습서의 단계를 완료하려면 다음 필수 구성 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-109">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="c47eb-110">Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [무료 Azure 계정]에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="c47eb-111">[Azure CLI(명령줄 인터페이스)]</span><span class="sxs-lookup"><span data-stu-id="c47eb-111">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="c47eb-112">최신 [JDK(Java Developer Kit)]</span><span class="sxs-lookup"><span data-stu-id="c47eb-112">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="c47eb-113">Apache의 [Maven] 빌드 도구(버전 3)</span><span class="sxs-lookup"><span data-stu-id="c47eb-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="c47eb-114">[Git] 클라이언트</span><span class="sxs-lookup"><span data-stu-id="c47eb-114">A [Git] client.</span></span>
* <span data-ttu-id="c47eb-115">[Docker] 클라이언트</span><span class="sxs-lookup"><span data-stu-id="c47eb-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="c47eb-116">이 자습서의 가상화 요구 사항으로 인해 가상 컴퓨터에는 이 문서의 단계를 따를 수 없습니다. 따라서 가상화 기능이 사용하도록 설정된 물리적 컴퓨터를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-116">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="c47eb-117">Spring Boot on Docker 시작 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="c47eb-117">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="c47eb-118">다음 단계에서는 간단한 Spring Boot 웹 응용 프로그램을 만들어 로컬로 테스트하는 데 필요한 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-118">The following steps walk you through the steps that are required to create a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="c47eb-119">명령 프롬프트를 열고 응용 프로그램을 저장할 로컬 디렉터리를 만들고 해당 디렉터리로 변경합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="c47eb-119">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="c47eb-120">-- 또는 --</span><span class="sxs-lookup"><span data-stu-id="c47eb-120">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="c47eb-121">[Spring Boot on Docker 시작하기] 샘플 프로젝트를 방금 만든 디렉터리에 복제합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="c47eb-121">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="c47eb-122">디렉터리를 완료된 프로젝트로 변경합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="c47eb-122">Change directory to the completed project; for example:</span></span>
   ```
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="c47eb-123">Maven을 사용하여 JAR 파일을 빌드합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="c47eb-123">Build the JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="c47eb-124">웹앱이 만들어지면 디렉터리를 JAR 파일이 위치한 `target` 디렉터리로 변경하고 웹앱을 시작합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="c47eb-124">Once the web app has been created, change directory to the `target` directory where the JAR file is located and start the web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. <span data-ttu-id="c47eb-125">웹 브라우저를 사용하여 로컬로 이동하여 웹앱을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-125">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="c47eb-126">예를 들어 curl을 사용할 수 있고 포트 80에서 실행하도록 Tomcat 서버를 한 경우:</span><span class="sxs-lookup"><span data-stu-id="c47eb-126">For example, if you have curl available and you configured the Tomcat server to run on port 80:</span></span>
   ```
   curl http://localhost
   ```

1. <span data-ttu-id="c47eb-127">**Hello Docker World!**라는 메시지가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-127">You should see the following message displayed: **Hello Docker World!**</span></span>

   ![로컬로 샘플 앱 찾아보기][SB01]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a><span data-ttu-id="c47eb-129">Azure Container Registry를 만들어서 개인 Docker 레지스트리로 사용</span><span class="sxs-lookup"><span data-stu-id="c47eb-129">Create an Azure Container Registry to use as a Private Docker Registry</span></span>

<span data-ttu-id="c47eb-130">다음 단계에서는 Azure Portal을 사용하여 Azure Container Registry를 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-130">The following steps walk you through using the Azure portal to create an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="c47eb-131">Azure Portal 대신 Azure CLI를 사용하려는 경우 [Azure CLI 2.0을 사용하여 개인 Docker 컨테이너 레지스트리 만들기](../../container-registry/container-registry-get-started-azure-cli.md)의 단계에 따르세요.</span><span class="sxs-lookup"><span data-stu-id="c47eb-131">If you want to use the Azure CLI instead of the Azure portal, follow the steps in [Create a private Docker container registry using the Azure CLI 2.0](../../container-registry/container-registry-get-started-azure-cli.md).</span></span>
>

1. <span data-ttu-id="c47eb-132">[Azure Portal]을 찾아 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-132">Browse to the [Azure portal] and sign in.</span></span>

   <span data-ttu-id="c47eb-133">Azure Portal에서 사용자의 계정에 로그인하면 [Azure Portal을 사용하여 개인 Docker 컨테이너 레지스트리 만들기] 문서의 단계를 수행할 수 있습니다. 편의상 다음 단계에서 다시 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-133">Once you have signed in to your account on the Azure portal, you can follow the steps in the [Create a private Docker container registry using the Azure portal] article, which are paraphrased in the following steps for the sake of expediency.</span></span>

1. <span data-ttu-id="c47eb-134">**+ 새로 만들기**의 메뉴 아이콘을 클릭하고 **컨테이너**를 클릭한 다음 **Azure Container Registry**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-134">Click the menu icon for **+ New**, then click **Containers**, and then click **Azure Container Registry**.</span></span>
   
   ![새로운 Azure Container Registry 만들기][AR01]

1. <span data-ttu-id="c47eb-136">Azure Container Registry 템플릿에 대한 정보 페이지가 표시되면 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-136">When the information page for the Azure Container Registry template is displayed, click **Create**.</span></span> 

   ![새로운 Azure Container Registry 만들기][AR02]

1. <span data-ttu-id="c47eb-138">**컨테이너 레지스트리 만들기** 페이지가 표시되면 **레지스트리 이름** 및 **리소스 그룹**을 입력하고 **관리 사용자**에 대해 **사용**을 선택한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-138">When the **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for the **Admin user**, and then click **Create**.</span></span>

   ![Azure Container Registry 설정 구성][AR03]

1. <span data-ttu-id="c47eb-140">컨테이너 레지스트리를 만들면 Azure Portal에서 컨테이너 레지스트리를 탐색한 다음 **선택키**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-140">Once your container registry has been created, navigate to your container registry in the Azure portal, and then click **Access Keys**.</span></span> <span data-ttu-id="c47eb-141">다음 단계에서 사용자 이름과 암호를 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-141">Take note of the username and password for the next steps.</span></span>

   ![Azure Container Registry 선택키][AR04]

## <a name="configure-maven-to-use-your-azure-container-registry-access-keys"></a><span data-ttu-id="c47eb-143">Azure Container Registry 선택키를 사용하도록 Maven 구성</span><span class="sxs-lookup"><span data-stu-id="c47eb-143">Configure Maven to use your Azure Container Registry access keys</span></span>

1. <span data-ttu-id="c47eb-144">Maven 설치에 대한 구성 디렉터리로 이동한 후 텍스트 편집기를 사용하여 *settings.xml* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-144">Navigate to the configuration directory for your Maven installation and open the *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="c47eb-145">이 자습서의 이전 섹션에서 *settings.xml* 파일의 `<servers>` 컬렉션에 Azure Container Registry 액세스 설정을 추가합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="c47eb-145">Add your Azure Container Registry access settings from the previous section of this tutorial to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="c47eb-146">Spring Boot 응용 프로그램에 대해 완료된 프로젝트 디렉터리로 이동하고(예: “*C:\SpringBoot\gs-spring-boot-docker\complete*” 또는 “*/users/robert/SpringBoot/gs-spring-boot-docker/complete*”) 텍스트 편집기를 사용하여 *pom.xml* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-146">Navigate to the completed project directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="c47eb-147">*pom.xml* 파일의 `<properties>` 컬렉션을 이 자습서의 이전 섹션에서 사용한 Azure Container Registry의 로그인 서버 값으로 업데이트합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="c47eb-147">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry from the previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="c47eb-148">*pom.xml* 파일의 `<plugins>` 컬렉션을 업데이트하여 `<plugin>`에 이 자습서의 이전 섹션에서 사용한 Azure Container Registry의 로그인 서버 주소 및 레지스트리 이름이 포함되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-148">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the login server address and registry name for your Azure Container Registry from the previous section of this tutorial.</span></span> <span data-ttu-id="c47eb-149">예:</span><span class="sxs-lookup"><span data-stu-id="c47eb-149">For example:</span></span>

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

1. <span data-ttu-id="c47eb-150">Spring Boot 응용 프로그램의 완성된 프로젝트 디렉터리로 이동하고 다음 명령을 실행하여 응용 프로그램을 다시 빌드하고 Azure Container Registry에 컨테이너를 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-150">Navigate to the completed project directory for your Spring Boot application and run the following command to rebuild the application and push the container to your Azure Container Registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

> [!NOTE]
>
> <span data-ttu-id="c47eb-151">Docker 컨테이너를 성공적으로 만들었더라도 Azure에 Docker 컨테이너를 푸시할 때 다음 중 하나와 비슷한 오류 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-151">When you are pushing your Docker container to Azure, you may receive an error message that is similar to one of the following even though your Docker container was created successfully:</span></span>
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="c47eb-152">이런 경우 Docker 명령줄에서 Azure 계정에 로그인해야 합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="c47eb-152">If this happens, you may need to sign in to your Azure account from the Docker command line; for example:</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="c47eb-153">그런 다음 명령줄에서 컨테이너를 푸시할 수 있습니다. 예:</span><span class="sxs-lookup"><span data-stu-id="c47eb-153">You can then push your container from the command line; for example:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a><span data-ttu-id="c47eb-154">컨테이너 이미지를 사용하여 Azure App Service에서 Linux에 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="c47eb-154">Create a web app on Linux on Azure App Service using your container image</span></span>

1. <span data-ttu-id="c47eb-155">[Azure Portal]을 찾아 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-155">Browse to the [Azure portal] and sign in.</span></span>

1. <span data-ttu-id="c47eb-156">**+ 새로 만들기**의 메뉴 아이콘을 클릭하고 **웹 + 모바일**을 클릭한 다음 **Linux의 웹앱**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-156">Click the menu icon for **+ New**, then click **Web + Mobile**, and then click **Web App on Linux**.</span></span>
   
   ![Azure Portal에서 새로운 웹앱 만들기][LX01]

1. <span data-ttu-id="c47eb-158">**Linux의 웹앱** 페이지가 표시되면 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-158">When the **Web App on Linux** page is displayed, enter the following information:</span></span>

   <span data-ttu-id="c47eb-159">a.</span><span class="sxs-lookup"><span data-stu-id="c47eb-159">a.</span></span> <span data-ttu-id="c47eb-160">**앱 이름**에 고유한 이름을 입력합니다. 예: "*wingtiptoyslinux*."</span><span class="sxs-lookup"><span data-stu-id="c47eb-160">Enter a unique name for the **App name**; for example: "*wingtiptoyslinux*."</span></span>

   <span data-ttu-id="c47eb-161">b.</span><span class="sxs-lookup"><span data-stu-id="c47eb-161">b.</span></span> <span data-ttu-id="c47eb-162">드롭다운 목록에서 **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-162">Choose your **Subscription** from the drop-down list.</span></span>

   <span data-ttu-id="c47eb-163">c.</span><span class="sxs-lookup"><span data-stu-id="c47eb-163">c.</span></span> <span data-ttu-id="c47eb-164">기존 **리소스 그룹**을 선택하거나 새 리소스 그룹을 만들기 위해 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-164">Choose an existing **Resource Group**, or specify a name to create a new resource group.</span></span>

   <span data-ttu-id="c47eb-165">d.</span><span class="sxs-lookup"><span data-stu-id="c47eb-165">d.</span></span> <span data-ttu-id="c47eb-166">**컨테이너 구성**을 클릭하고 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-166">Click **Configure container** and enter the following information:</span></span>

      * <span data-ttu-id="c47eb-167">**개인 레지스트리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-167">Choose **Private registry**.</span></span>

      * <span data-ttu-id="c47eb-168">**이미지 및 선택적 태그**: 이전에 사용한 컨테이너 이름을 지정합니다. 예: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"</span><span class="sxs-lookup"><span data-stu-id="c47eb-168">**Image and optional tag**: Specify your container name from earlier; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"</span></span>

      * <span data-ttu-id="c47eb-169">**서버 URL**: 이전에 사용한 레지스트리 URL을 지정합니다. 예: "*https://wingtiptoysregistry.azurecr.io*"</span><span class="sxs-lookup"><span data-stu-id="c47eb-169">**Server URL**: Specify your registry URL from earlier; for example: "*https://wingtiptoysregistry.azurecr.io*"</span></span>

      * <span data-ttu-id="c47eb-170">**로그인 사용자 이름** 및 **암호**: 이전 단계에서 사용한 **액세스 키**의 로그인 자격 증명을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-170">**Login username** and **Password**: Specify your login credentials from your **Access Keys** that you used in previous steps.</span></span>
   
   <span data-ttu-id="c47eb-171">e.</span><span class="sxs-lookup"><span data-stu-id="c47eb-171">e.</span></span> <span data-ttu-id="c47eb-172">위의 정보를 모두 입력하면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-172">Once you have entered all of the above information, click **OK**.</span></span>

   ![웹앱 설정 구성][LX02]

1. <span data-ttu-id="c47eb-174">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-174">Click **Create**.</span></span>

> [!NOTE]
>
> <span data-ttu-id="c47eb-175">Azure에서는 표준 포트 80 또는 8080에서 실행되는 포함된 Tomcat 서버에 인터넷 요청을 자동으로 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-175">Azure will automatically map Internet requests to embedded Tomcat server that is running on the standard ports of 80 or 8080.</span></span> <span data-ttu-id="c47eb-176">그러나 사용자 지정 포트에서 포함된 Tomcat 서버를 실행하도록 구성한 경우 포함된 Tomcat 서버에 포트를 정의하는 웹앱에 환경 변수를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-176">However, if you configured your embedded Tomcat server to run on a custom port, you need to add an environment variable to your web app that defines the port for your embedded Tomcat server.</span></span> <span data-ttu-id="c47eb-177">이렇게 하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-177">To do so, use the following steps:</span></span>
>
> 1. <span data-ttu-id="c47eb-178">[Azure Portal]을 찾아 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-178">Browse to the [Azure portal] and sign in.</span></span>
> 
> 2. <span data-ttu-id="c47eb-179">**App Services** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-179">Click the icon for **App Services**.</span></span> <span data-ttu-id="c47eb-180">(아래 이미지에서 항목 #1 참조)</span><span class="sxs-lookup"><span data-stu-id="c47eb-180">(See item #1 in the image below.)</span></span>
>
> 3. <span data-ttu-id="c47eb-181">목록에서 웹앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-181">Select your web app from the list.</span></span> <span data-ttu-id="c47eb-182">(아래 이미지에서 항목 #2)</span><span class="sxs-lookup"><span data-stu-id="c47eb-182">(Item #2 in the image below.)</span></span>
>
> 4. <span data-ttu-id="c47eb-183">**응용 프로그램 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-183">Click **Application Settings**.</span></span> <span data-ttu-id="c47eb-184">(아래 이미지에서 항목 #3)</span><span class="sxs-lookup"><span data-stu-id="c47eb-184">(Item #3 in the image below.)</span></span>
>
> 5. <span data-ttu-id="c47eb-185">**앱 설정** 섹션에서 **PORT**라는 새 환경 변수를 추가하고 값에 사용자 지정 포트 번호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-185">In the **App settings** section, add a new environment variable named **PORT** and enter your custom port number for the value.</span></span> <span data-ttu-id="c47eb-186">(아래 이미지에서 항목 #4)</span><span class="sxs-lookup"><span data-stu-id="c47eb-186">(Item #4 in the image below.)</span></span>
>
> 6. <span data-ttu-id="c47eb-187">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c47eb-187">Click **Save**.</span></span> <span data-ttu-id="c47eb-188">(아래 이미지에서 항목 #5)</span><span class="sxs-lookup"><span data-stu-id="c47eb-188">(Item #5 in the image below.)</span></span>
>
> ![Azure Portal에서 사용자 지정 포트 번호 저장][LX03]
>

<!--
##  OPTIONAL: Configure the embedded Tomcat server to run on a different port

The embedded Tomcat server in the sample Spring Boot application is configured to run on port 8080 by default. However, if you want to run the embedded Tomcat server to run on a different port, such as port 80 for local testing, you can configure the port by using the following steps.

1. Go to the *resources* directory (or create the directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open the *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify the **server** setting so that the server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close the *application.yml* file.
-->

## <a name="next-steps"></a><span data-ttu-id="c47eb-190">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c47eb-190">Next steps</span></span>

<span data-ttu-id="c47eb-191">Azure에서 Spring Boot 응용 프로그램을 사용 하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c47eb-191">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="c47eb-192">Azure App Service에 Spring Boot 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="c47eb-192">Deploy a Spring Boot Application to the Azure App Service</span></span>](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [<span data-ttu-id="c47eb-193">Azure Container Service의 Kubernetes 클러스터에 Spring Boot 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="c47eb-193">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="c47eb-194">Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Azure Java 개발자 센터] 및 [Visual Studio Team Services용 Java 도구]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c47eb-194">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="c47eb-195">Spring Boot on Docker 샘플 프로젝트에 대한 자세한 정보는 [Spring Boot on Docker 시작하기]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c47eb-195">For further details about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="c47eb-196">자체 Spring Boot 응용 프로그램을 시작하는 데 도움이 필요하면 https://start.spring.io/에서 **Spring Initializr**를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c47eb-196">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="c47eb-197">간단한 Spring Boot 응용 프로그램을 만들기 시작하는 방법에 대한 자세한 내용은 https://start.spring.io/에서 Spring Initializr를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c47eb-197">For more information about getting started with creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="c47eb-198">Azure와 함께 사용자 지정 Docker 이미지를 사용하는 방법에 대한 추가 예제를 보려면 [Linux에서 Azure Web App에 대한 사용자 지정 Docker 이미지 사용]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c47eb-198">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

<span data-ttu-id="c47eb-199">[Azure CLI(명령줄 인터페이스)]: /cli/azure/overview</span><span class="sxs-lookup"><span data-stu-id="c47eb-199">[Azure Command-Line Interface (CLI)]: /cli/azure/overview</span></span>
<span data-ttu-id="c47eb-200">[ACS(Azure Container Service)]: https://azure.microsoft.com/services/container-service/</span><span class="sxs-lookup"><span data-stu-id="c47eb-200">[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/</span></span>
<span data-ttu-id="c47eb-201">[Azure Java 개발자 센터]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="c47eb-201">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="c47eb-202">[Azure Portal]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="c47eb-202">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="c47eb-203">[Azure Portal을 사용하여 개인 Docker 컨테이너 레지스트리 만들기]: /azure/container-registry/container-registry-get-started-portal</span><span class="sxs-lookup"><span data-stu-id="c47eb-203">[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal</span></span>
<span data-ttu-id="c47eb-204">[Linux에서 Azure Web App에 대한 사용자 지정 Docker 이미지 사용]: /azure/app-service-web/app-service-linux-using-custom-docker-image</span><span class="sxs-lookup"><span data-stu-id="c47eb-204">[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image</span></span>
<span data-ttu-id="c47eb-205">[Docker]: https://www.docker.com/</span><span class="sxs-lookup"><span data-stu-id="c47eb-205">[Docker]: https://www.docker.com/</span></span>
<span data-ttu-id="c47eb-206">[무료 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="c47eb-206">[free Azure account]: https://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="c47eb-207">[Git]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="c47eb-207">[Git]: https://github.com/</span></span>
<span data-ttu-id="c47eb-208">[JDK(Java Developer Kit)]: http://www.oracle.com/technetwork/java/javase/downloads/</span><span class="sxs-lookup"><span data-stu-id="c47eb-208">[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/</span></span>
<span data-ttu-id="c47eb-209">[Visual Studio Team Services용 Java 도구]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="c47eb-209">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>
<span data-ttu-id="c47eb-210">[Maven]: http://maven.apache.org/</span><span class="sxs-lookup"><span data-stu-id="c47eb-210">[Maven]: http://maven.apache.org/</span></span>
<span data-ttu-id="c47eb-211">[MSDN 구독자 혜택]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span><span class="sxs-lookup"><span data-stu-id="c47eb-211">[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span></span>
<span data-ttu-id="c47eb-212">[Spring Boot]: http://projects.spring.io/spring-boot/</span><span class="sxs-lookup"><span data-stu-id="c47eb-212">[Spring Boot]: http://projects.spring.io/spring-boot/</span></span>
<span data-ttu-id="c47eb-213">[Spring Boot on Docker 시작하기]: https://github.com/spring-guides/gs-spring-boot-docker</span><span class="sxs-lookup"><span data-stu-id="c47eb-213">[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker</span></span>
<span data-ttu-id="c47eb-214">[Spring Framework]: https://spring.io/</span><span class="sxs-lookup"><span data-stu-id="c47eb-214">[Spring Framework]: https://spring.io/</span></span>

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
