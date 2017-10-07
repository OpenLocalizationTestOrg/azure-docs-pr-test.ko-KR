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
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-in-azure-container-registry-tooazure-app-service"></a><span data-ttu-id="48c61-103">어떻게 toouse hello Maven 플러그 인 toodeploy Azure 웹 앱에 대 한 Azure 컨테이너 레지스트리 tooAzure 앱 서비스에서에서 스프링 부팅 앱</span><span class="sxs-lookup"><span data-stu-id="48c61-103">How toouse hello Maven Plugin for Azure Web Apps toodeploy a Spring Boot app in Azure Container Registry tooAzure App Service</span></span>

<span data-ttu-id="48c61-104">hello  **[Spring Framework]**  는 인기 있는 오픈 소스 프레임 워크 Java 개발자가 웹, 모바일 및 API 응용 프로그램을 만들 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-104">hello **[Spring Framework]** is a popular open-source framework that helps Java developers create web, mobile, and API applications.</span></span> <span data-ttu-id="48c61-105">이 자습서를 사용 하 여 만든 샘플 응용 프로그램을 사용 하 여 [스프링 부팅], 스프링 tooget 사용 하기 위한 규칙 기반 접근 방식을 신속 하 게 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-105">This tutorial uses a sample app created using [Spring Boot], a convention-driven approach for using Spring tooget started quickly.</span></span>

<span data-ttu-id="48c61-106">이 문서에서는 방법을 toodeploy 샘플 스프링 부팅 응용 프로그램 tooAzure 컨테이너 레지스트리 및 사용 하 여 hello Maven 플러그 인 toodeploy Azure 웹 앱에 대 한 앱 서비스 프로그램 응용 프로그램 tooAzure 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-106">This article demonstrates how toodeploy a sample Spring Boot application tooAzure Container Registry, and then use hello Maven Plugin for Azure Web Apps toodeploy your application tooAzure App Service.</span></span>

> [!NOTE]
>
> <span data-ttu-id="48c61-107">Azure 웹 앱에 대 한 Maven 플러그인 hello는 현재 미리 보기로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-107">hello Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="48c61-108">지금은 FTP 게시만 지원 되지만 이후 hello에 대 한 추가 기능이 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-108">For now, only FTP publishing is supported, although additional features are planned for hello future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="48c61-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="48c61-109">Prerequisites</span></span>

<span data-ttu-id="48c61-110">이 자습서에서는 toocomplete hello 단계 순서를 필수 구성 요소를 다음 toohave hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-110">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="48c61-111">Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [무료 Azure 계정]에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-111">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="48c61-112">hello [Azure 명령줄 인터페이스 (CLI)]합니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-112">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="48c61-113">최신 [JDK(Java Development Kit)], 버전 1.7 이상</span><span class="sxs-lookup"><span data-stu-id="48c61-113">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="48c61-114">Apache의 [Maven] 빌드 도구(버전 3)</span><span class="sxs-lookup"><span data-stu-id="48c61-114">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="48c61-115">[Git] 클라이언트</span><span class="sxs-lookup"><span data-stu-id="48c61-115">A [Git] client.</span></span>
* <span data-ttu-id="48c61-116">[Docker] 클라이언트</span><span class="sxs-lookup"><span data-stu-id="48c61-116">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="48c61-117">이 자습서의 toohello 가상화 요구 사항 때문; 가상 컴퓨터에이 문서의 hello 단계를 따를 수 없는 물리적 컴퓨터를 사용 하 여 가상화 기능을 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-117">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-hello-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="48c61-118">Docker 웹 응용 프로그램에 복제 hello 샘플 스프링 부팅</span><span class="sxs-lookup"><span data-stu-id="48c61-118">Clone hello sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="48c61-119">이 섹션에서는 컨테이너화된 Spring Boot 응용 프로그램을 복제하고 로컬로 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-119">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="48c61-120">명령 프롬프트 또는 터미널 윈도우를 열고 스프링 부팅 응용 프로그램 및 toothat 디렉터리를 변경 합니다; 로컬 디렉터리 toohold 만들기 예를 들어:</span><span class="sxs-lookup"><span data-stu-id="48c61-120">Open a command prompt or terminal window and create a local directory toohold your Spring Boot application, and change toothat directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="48c61-121">-- 또는 --</span><span class="sxs-lookup"><span data-stu-id="48c61-121">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="48c61-122">복제 hello [스프링 부팅 Docker 시작에] 샘플 프로젝트를 만든; hello 디렉터리 예:</span><span class="sxs-lookup"><span data-stu-id="48c61-122">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory you created; for example:</span></span>
   ```shell
   git clone -b private-registry https://github.com/Microsoft/gs-spring-boot-docker
   ```

1. <span data-ttu-id="48c61-123">디렉터리 toohello 완료 된 프로젝트를 변경 합니다. 예를 들어:</span><span class="sxs-lookup"><span data-stu-id="48c61-123">Change directory toohello completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="48c61-124">Maven;를 사용 하 여 hello JAR 파일 빌드 예를 들어:</span><span class="sxs-lookup"><span data-stu-id="48c61-124">Build hello JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="48c61-125">Hello 웹 응용 프로그램을 만들면 Maven;를 사용 하 여 hello 웹 응용 프로그램을 시작 합니다. 예를 들어:</span><span class="sxs-lookup"><span data-stu-id="48c61-125">When hello web app has been created, start hello web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="48c61-126">웹 브라우저를 사용 하 여 로컬로 tooit 이동 하 여 hello 웹 앱을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-126">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="48c61-127">예를 들어 hello curl을 사용할 수 있는 경우 다음 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-127">For example, you could use hello following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="48c61-128">Hello 메시지 표시의 뒤에 표시 됩니다: **Docker는 Hello World**</span><span class="sxs-lookup"><span data-stu-id="48c61-128">You should see hello following message displayed: **Hello Docker World**</span></span>

   ![로컬로 샘플 앱 찾아보기][SB01]

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="48c61-130">Azure 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="48c61-130">Create an Azure service principal</span></span>

<span data-ttu-id="48c61-131">이 섹션에서는 Azure 컨테이너 tooAzure를 배포할 때 Maven 플러그 인 사용 하 여 hello 서비스 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-131">In this section, you create an Azure service principal that hello Maven plugin uses when deploying your container tooAzure.</span></span>

1. <span data-ttu-id="48c61-132">명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-132">Open a command prompt.</span></span>

1. <span data-ttu-id="48c61-133">사용 하 여 Azure 계정에 로그인 Azure CLI hello:</span><span class="sxs-lookup"><span data-stu-id="48c61-133">Sign into your Azure account by using hello Azure CLI:</span></span>
   ```azurecli
   az login
   ```
   <span data-ttu-id="48c61-134">Hello 지침 toocomplete hello 로그인 프로세스를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-134">Follow hello instructions toocomplete hello sign-in process.</span></span>

1. <span data-ttu-id="48c61-135">Azure 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="48c61-135">Create an Azure service principal:</span></span>
   ```azurecli
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="48c61-136">여기서 `uuuuuuuu` hello 사용자 이름 및 `pppppppp` hello 서비스 사용자에 대 한 hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-136">Where `uuuuuuuu` is hello user name and `pppppppp` is hello password for hello service principal.</span></span>

1. <span data-ttu-id="48c61-137">Azure는 다음 예제는 hello 유사한 JSON로 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-137">Azure responds with JSON that resembles hello following example:</span></span>
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
   > <span data-ttu-id="48c61-138">Hello Maven 플러그 인 toodeploy 컨테이너 tooAzure를 구성할 때 hello 값이 JSON 응답을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-138">You will use hello values from this JSON response when you configure hello Maven plugin toodeploy your container tooAzure.</span></span> <span data-ttu-id="48c61-139">hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, 및 `tttttttt` 되는 자리 표시자 값은 사용이 예제에서는 toomake에 보다 쉽게 toomap 이러한 값 tootheir 각 요소가 사용자 Maven을 구성할 때 `settings.xml` hello에 다음 파일 단원을 참조 하십시오입니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-139">hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example toomake it easier toomap these values tootheir respective elements when you configure your Maven `settings.xml` file in hello next section.</span></span>
   >
   >

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a><span data-ttu-id="48c61-140">Azure 컨테이너 레지스트리 hello Azure CLI를 사용 하 여 만들기</span><span class="sxs-lookup"><span data-stu-id="48c61-140">Create an Azure Container Registry using hello Azure CLI</span></span>

1. <span data-ttu-id="48c61-141">명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-141">Open a command prompt.</span></span>

1. <span data-ttu-id="48c61-142">Azure 계정 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-142">Log in tooyour Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="48c61-143">이 문서의 hello에 대 한 리소스 그룹 사용 하 여 Azure 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-143">Create a resource group for hello Azure resources you will use in this article:</span></span>
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   <span data-ttu-id="48c61-144">이 예제에서 `wingtiptoysresources`를 리소스 그룹의 고유 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-144">Replace `wingtiptoysresources` in this example with a unique name for your resource group.</span></span>

1. <span data-ttu-id="48c61-145">스프링 부팅 앱에 대 한 hello 리소스 그룹에서 사설 Azure 컨테이너 레지스트리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-145">Create a private Azure container registry in hello resource group for your Spring Boot app:</span></span> 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   <span data-ttu-id="48c61-146">이 예제에서 `wingtiptoysregistry`를 컨테이너 레지스트리의 고유 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-146">Replace `wingtiptoysregistry` in this example with a unique name for your container registry.</span></span>

1. <span data-ttu-id="48c61-147">컨테이너 레지스트리에 대 한 hello 암호를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-147">Retrieve hello password for your container registry:</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   <span data-ttu-id="48c61-148">Azure는 암호로 응답합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="48c61-148">Azure will respond with your password; for example:</span></span>
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-tooyour-maven-settings"></a><span data-ttu-id="48c61-149">Azure 컨테이너 레지스트리 및 Azure 서비스 주체 tooyour Maven 설정 추가</span><span class="sxs-lookup"><span data-stu-id="48c61-149">Add your Azure container registry and Azure service principal tooyour Maven settings</span></span>

1. <span data-ttu-id="48c61-150">프로그램 Maven 열고 `settings.xml` 텍스트 편집기에서 파일;이 파일은 다음 예제는 hello와 같은 경로에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-150">Open your Maven `settings.xml` file in a text editor; this file might be in a path like hello following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="48c61-151">이 문서 toohello의 hello 이전 섹션에서 Azure 컨테이너 레지스트리 액세스 설정을 추가 `<servers>` hello에 대 한 컬렉션 *settings.xml* 파일; 예:</span><span class="sxs-lookup"><span data-stu-id="48c61-151">Add your Azure Container Registry access settings from hello previous section of this article toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   <span data-ttu-id="48c61-152">여기서,</span><span class="sxs-lookup"><span data-stu-id="48c61-152">Where:</span></span>
   <span data-ttu-id="48c61-153">요소</span><span class="sxs-lookup"><span data-stu-id="48c61-153">Element</span></span> | <span data-ttu-id="48c61-154">설명</span><span class="sxs-lookup"><span data-stu-id="48c61-154">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="48c61-155">개인 Azure 컨테이너 레지스트리 hello 이름을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-155">Contains hello name of your private Azure container registry.</span></span>
   `<username>` | <span data-ttu-id="48c61-156">개인 Azure 컨테이너 레지스트리 hello 이름을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-156">Contains hello name of your private Azure container registry.</span></span>
   `<password>` | <span data-ttu-id="48c61-157">Hello이 문서의 이전 섹션에서 검색 하는 hello 암호가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-157">Contains hello password you retrieved in hello previous section of this article.</span></span>

1. <span data-ttu-id="48c61-158">이 문서 toohello의 이전 단원에서 Azure 서비스 보안 주체 설정 추가 `<servers>` hello에 대 한 컬렉션 *settings.xml* 파일; 예:</span><span class="sxs-lookup"><span data-stu-id="48c61-158">Add your Azure service principal settings from an earlier section of this article toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="48c61-159">여기서,</span><span class="sxs-lookup"><span data-stu-id="48c61-159">Where:</span></span>
   <span data-ttu-id="48c61-160">요소</span><span class="sxs-lookup"><span data-stu-id="48c61-160">Element</span></span> | <span data-ttu-id="48c61-161">설명</span><span class="sxs-lookup"><span data-stu-id="48c61-161">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="48c61-162">Maven 웹 응용 프로그램 tooAzure를 배포할 때 toolook 보안 설정을 사용 하는 고유한 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-162">Specifies a unique name which Maven uses toolook up your security settings when you deploy your web app tooAzure.</span></span>
   `<client>` | <span data-ttu-id="48c61-163">Hello 포함 `appId` 서비스 사용자의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-163">Contains hello `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="48c61-164">Hello 포함 `tenant` 서비스 사용자의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-164">Contains hello `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="48c61-165">Hello 포함 `password` 서비스 사용자의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-165">Contains hello `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="48c61-166">hello 대상 Azure 클라우드 환경 정의 `AZURE` 이 예에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-166">Defines hello target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="48c61-167">(전체 환경 목록을 hello 영어로 [Azure 웹 앱에 대 한 Maven 플러그인] 설명서)</span><span class="sxs-lookup"><span data-stu-id="48c61-167">(A full list of environments is available in hello [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="48c61-168">저장 후 닫기 hello *settings.xml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-168">Save and close hello *settings.xml* file.</span></span>

## <a name="build-your-docker-container-image-and-push-it-tooyour-azure-container-registry"></a><span data-ttu-id="48c61-169">프로그램 Docker 컨테이너 이미지를 빌드하고 tooyour Azure 컨테이너 레지스트리 푸시</span><span class="sxs-lookup"><span data-stu-id="48c61-169">Build your Docker container image and push it tooyour Azure container registry</span></span>

1. <span data-ttu-id="48c61-170">스프링 부팅 응용 프로그램에 대 한 완료 toohello 프로젝트 디렉터리 (예: 탐색 "*C:\SpringBoot\gs-spring-boot-docker\complete*"또는"*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), 및 열기 hello *pom.xml* 있는 파일을 텍스트 편집기입니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-170">Navigate toohello completed project directory for your Spring Boot application, (e.g. "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open hello *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="48c61-171">업데이트 hello `<properties>` hello에 대 한 컬렉션 *pom.xml* hello;이 자습서의 이전 섹션에서 Azure 컨테이너 레지스트리에 대 한 hello 로그인 서버 값을 갖는 파일 예:</span><span class="sxs-lookup"><span data-stu-id="48c61-171">Update hello `<properties>` collection in hello *pom.xml* file with hello login server value for your Azure Container Registry from hello previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   <span data-ttu-id="48c61-172">여기서,</span><span class="sxs-lookup"><span data-stu-id="48c61-172">Where:</span></span>
   <span data-ttu-id="48c61-173">요소</span><span class="sxs-lookup"><span data-stu-id="48c61-173">Element</span></span> | <span data-ttu-id="48c61-174">설명</span><span class="sxs-lookup"><span data-stu-id="48c61-174">Description</span></span>
   ---|---|---
   `<azure.containerRegistry>` | <span data-ttu-id="48c61-175">개인 Azure 컨테이너 레지스트리 hello 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-175">Specifies hello name of your private Azure container registry.</span></span>
   `<docker.image.prefix>` | <span data-ttu-id="48c61-176">사용자 개인 Azure 컨테이너 레지스트리에 추가 하 여 파생의 hello URL을 지정 ". azurecr.io" 개인 컨테이너 레지스트리 toohello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-176">Specifies hello URL of your private Azure container registry, which is derived by appending ".azurecr.io" toohello name of your private container registry.</span></span>

1. <span data-ttu-id="48c61-177">되어 있는지 확인 `<plugin>` 있는 hello Docker 플러그 인에 대 한 프로그램 *pom.xml* 파일이이 자습서에서는 hello hello 로그인 주소와 레지스트리에서에서 서버 이름 hello 이전 단계에 대 한 올바른 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-177">Verify that `<plugin>` for hello Docker plugin in your *pom.xml* file contains hello correct properties for hello login server address and registry name from hello previous step in this tutorial.</span></span> <span data-ttu-id="48c61-178">예:</span><span class="sxs-lookup"><span data-stu-id="48c61-178">For example:</span></span>

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
   <span data-ttu-id="48c61-179">여기서,</span><span class="sxs-lookup"><span data-stu-id="48c61-179">Where:</span></span>
   <span data-ttu-id="48c61-180">요소</span><span class="sxs-lookup"><span data-stu-id="48c61-180">Element</span></span> | <span data-ttu-id="48c61-181">설명</span><span class="sxs-lookup"><span data-stu-id="48c61-181">Description</span></span>
   ---|---|---
   `<serverId>` | <span data-ttu-id="48c61-182">개인 Azure 컨테이너 레지스트리의 이름이 포함 되어 hello 속성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-182">Specifies hello property which contains name of your private Azure container registry.</span></span>
   `<registryUrl>` | <span data-ttu-id="48c61-183">개인 Azure 컨테이너 레지스트리 hello URL이 포함 된 hello 속성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-183">Specifies hello property which contains hello URL of your private Azure container registry.</span></span>

1. <span data-ttu-id="48c61-184">스프링 부팅 응용 프로그램에 대 한 완료 toohello 프로젝트 디렉터리를 이동 하 고 hello 다음 명령 toorebuild hello 응용 프로그램을 실행 푸시 hello 컨테이너 tooyour Azure 컨테이너 레지스트리:</span><span class="sxs-lookup"><span data-stu-id="48c61-184">Navigate toohello completed project directory for your Spring Boot application and run hello following command toorebuild hello application and push hello container tooyour Azure container registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

1. <span data-ttu-id="48c61-185">선택 사항: toohello 찾아보기 [Azure 포털] 라는 Docker 컨테이너 이미지 인지 확인 하 고 **스프링 부팅 docker gs** 컨테이너 레지스트리에 합니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-185">OPTIONAL: Browse toohello [Azure portal] and verify that there is Docker container image named **gs-spring-boot-docker** in your container registry.</span></span>

   ![Azure Portal에서 컨테이너 확인][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-tooazure"></a><span data-ttu-id="48c61-187">프로그램 pom.xml 사용자 지정 합니다 빌드 및 컨테이너 tooAzure 배포</span><span class="sxs-lookup"><span data-stu-id="48c61-187">Customize your pom.xml, then build and deploy your container tooAzure</span></span>

<span data-ttu-id="48c61-188">열기 hello `pom.xml` 텍스트 편집기에서 스프링 부팅 응용 프로그램에 대 한 파일을 찾은 후 hello `<plugin>` 요소에 대 한 `azure-webapp-maven-plugin`합니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-188">Open hello `pom.xml` file for your Spring Boot application in a text editor, and then locate hello `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="48c61-189">이 요소에는 다음 예제는 hello와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-189">This element should resemble hello following example:</span></span>

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

<span data-ttu-id="48c61-190">Hello Maven 플러그 인에 대해 수정할 수 있는 값이 여러 개인 및 이러한 각 요소에 대 한 자세한 설명을 hello 영어로 [Azure 웹 앱에 대 한 Maven 플러그인] 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-190">There are several values that you can modify for hello Maven plugin, and a detailed description for each of these elements is available in hello [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="48c61-191">즉, 이 문서에서 강조 표시된 값은 여러 개입니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-191">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="48c61-192">요소</span><span class="sxs-lookup"><span data-stu-id="48c61-192">Element</span></span> | <span data-ttu-id="48c61-193">설명</span><span class="sxs-lookup"><span data-stu-id="48c61-193">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="48c61-194">Hello 버전의 hello 지정 [Azure 웹 앱에 대 한 Maven 플러그인]합니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-194">Specifies hello version of hello [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="48c61-195">Hello에 나열 된 hello 버전을 검사 해야 하면 [Maven 중앙 리포지토리](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) 사용 중인 tooensure hello 최신 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-195">You should check hello version listed in hello [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure that you are using hello latest version.</span></span>
`<authentication>` | <span data-ttu-id="48c61-196">이 예제에 포함 된 Azure의 hello 인증 정보를 지정 된 `<serverId>` 포함 된 요소 `azure-auth`; Maven hello Azure 서비스 주체 값을 해당 값 toolook 프로그램 Maven에서 사용 하 여 *settings.xml* 이 문서의 이전 섹션에 정의 된 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-196">Specifies hello authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value toolook up hello Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="48c61-197">Hello 대상 리소스 그룹, 즉 지정 `wingtiptoysresources` 이 예에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-197">Specifies hello target resource group, which is `wingtiptoysresources` in this example.</span></span> <span data-ttu-id="48c61-198">hello 리소스 그룹이 아직 없는 경우 배포 중 만들어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-198">hello resource group will be created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="48c61-199">웹 앱에 대 한 hello 대상 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-199">Specifies hello target name for your web app.</span></span> <span data-ttu-id="48c61-200">이 예제에서는 hello 대상 이름은 `maven-linux-app-${maven.build.timestamp}`여기서 hello `${maven.build.timestamp}` 이 예제에서는 tooavoid 충돌의 접미사가 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-200">In this example, hello target name is `maven-linux-app-${maven.build.timestamp}`, where hello `${maven.build.timestamp}` suffix is appended in this example tooavoid conflict.</span></span> <span data-ttu-id="48c61-201">(hello 타임 스탬프는 선택 사항) hello 응용 프로그램 이름에 대 한 고유 문자열을 모두 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-201">(hello timestamp is optional; you can specify any unique string for hello app name.)</span></span>
`<region>` | <span data-ttu-id="48c61-202">이 예제는 hello 대상 지역을 지정 `westus`합니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-202">Specifies hello target region, which in this example is `westus`.</span></span> <span data-ttu-id="48c61-203">(전체 목록은 hello에 [Azure 웹 앱에 대 한 Maven 플러그인] 설명서입니다.)</span><span class="sxs-lookup"><span data-stu-id="48c61-203">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<containerSettings>` | <span data-ttu-id="48c61-204">Hello 이름 및 컨테이너의 URL을 포함 하는 hello 속성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-204">Specifies hello properties which contain hello name and URL of your container.</span></span>
`<appSettings>` | <span data-ttu-id="48c61-205">웹 앱 tooAzure를 배포할 때 Maven toouse에 대 한 고유한 설정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-205">Specifies any unique settings for Maven toouse when deploying your web app tooAzure.</span></span> <span data-ttu-id="48c61-206">이 예제는 `<property>` 요소 앱에 대 한 hello 포트를 지정 하는 자식 요소의 이름/값 쌍을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-206">In this example, a `<property>` element contains a name/value pair of child elements that specify hello port for your app.</span></span>

> [!NOTE]
>
> <span data-ttu-id="48c61-207">이 예에서 hello 설정을 toochange hello 포트 번호는 hello 기본값과에서 hello 포트를 변경 하는 경우에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-207">hello settings toochange hello port number in this example are only necessary when you are changing hello port from hello default.</span></span>
>

1. <span data-ttu-id="48c61-208">Hello 명령 프롬프트 또는 이전에 사용 하 던 터미널 창에서 모든 변경 내용을 toohello을 만든 경우 Maven를 사용 하 여 hello JAR 파일을 다시 작성 *pom.xml* 파일; 예:</span><span class="sxs-lookup"><span data-stu-id="48c61-208">From hello command prompt or terminal window that you were using earlier, rebuild hello JAR file using Maven if you made any changes toohello *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="48c61-209">Maven;를 사용 하 여 웹 응용 프로그램 tooAzure 배포 예를 들어:</span><span class="sxs-lookup"><span data-stu-id="48c61-209">Deploy your web app tooAzure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="48c61-210">Maven 프로그램 웹 응용 프로그램 tooAzure; 배포 웹 앱 hello가 아직 없는 경우 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-210">Maven will deploy your web app tooAzure; if hello web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="48c61-211">경우 hello에서 지정 하는 hello 지역 `<region>` 의 요소 프로그램 *pom.xml* 파일에 없는 사용할 수 있는 충분 한 서버 배포를 시작 하는 경우, 다음 예제에서는 오류 유사한 toohello 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-211">If hello region which you specify in hello `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar toohello following example:</span></span>
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
> <span data-ttu-id="48c61-212">이 경우 다른 영역을 다시 실행 Maven 명령 toodeploy 응용 프로그램를 hello를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-212">If this happens, you can specify another region and re-run hello Maven command toodeploy your application.</span></span>
>
>

<span data-ttu-id="48c61-213">웹 배포 된 수 toomanage 됩니다 hello를 사용 하 여 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-213">When your web has been deployed, you will be able toomanage it by using hello [Azure portal].</span></span>

* <span data-ttu-id="48c61-214">웹앱은 **App Services**에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="48c61-214">Your web app will be listed in **App Services**:</span></span>

   ![Azure Portal App Services에 나열된 웹앱][AP01]

* <span data-ttu-id="48c61-216">웹 앱 hello에 나열 됩니다에 대 한 URL을 hello 및 **개요** 웹 앱에 대 한:</span><span class="sxs-lookup"><span data-stu-id="48c61-216">And hello URL for your web app will be listed in hello **Overview** for your web app:</span></span>

   ![웹 앱에 대 한 hello URL 확인][AP02]

## <a name="next-steps"></a><span data-ttu-id="48c61-218">다음 단계</span><span class="sxs-lookup"><span data-stu-id="48c61-218">Next steps</span></span>

<span data-ttu-id="48c61-219">Hello에 대 한 자세한 내용은이 문서에서 설명 하는 다양 한 기술 참조 문서 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="48c61-219">For more information about hello various technologies discussed in this article, see hello following articles:</span></span>

* <span data-ttu-id="48c61-220">[Azure 웹 앱에 대 한 Maven 플러그인]</span><span class="sxs-lookup"><span data-stu-id="48c61-220">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="48c61-221">TooAzure hello Azure CLI에서 로그인</span><span class="sxs-lookup"><span data-stu-id="48c61-221">Log in tooAzure from hello Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="48c61-222">Azure CLI 2.0을 사용하여 Azure 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="48c61-222">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="48c61-223">Maven 설정 참조</span><span class="sxs-lookup"><span data-stu-id="48c61-223">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="48c61-224">[Maven의 Docker 플러그 인]</span><span class="sxs-lookup"><span data-stu-id="48c61-224">[Docker plugin for Maven]</span></span>

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
