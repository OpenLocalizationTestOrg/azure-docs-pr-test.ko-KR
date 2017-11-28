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
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-containerized-spring-boot-app-tooazure"></a><span data-ttu-id="25ead-103">어떻게 toouse hello Maven 플러그 인 toodeploy Azure 웹 앱에 대 한 컨테이너 화 된 스프링 부팅 앱 tooAzure</span><span class="sxs-lookup"><span data-stu-id="25ead-103">How toouse hello Maven Plugin for Azure Web Apps toodeploy a containerized Spring Boot app tooAzure</span></span>

<span data-ttu-id="25ead-104">hello [Azure 웹 앱에 대 한 Maven 플러그인](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) 에 대 한 [Apache Maven](http://maven.apache.org/) Maven 프로젝트에 Azure 앱 서비스의 원활한 통합을 제공 하며 개발자 toodeploy 웹 앱에 대 한 hello 프로세스를 간소화 합니다. 앱 서비스 tooAzure 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-104">hello [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service  into Maven projects, and streamlines hello process for developers toodeploy web apps tooAzure App Service .</span></span>

<span data-ttu-id="25ead-105">이 문서에서는 Azure 웹 앱 toodeploy 용 hello Maven 플러그 인을 사용 하 여 Docker 컨테이너 tooAzure 응용 프로그램 서비스의에서 샘플 스프링 부팅 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-105">This article demonstrates using hello Maven Plugin for Azure Web Apps toodeploy a sample Spring Boot application in a Docker container tooAzure App Services.</span></span>

> [!NOTE]
>
> <span data-ttu-id="25ead-106">Azure 웹 앱에 대 한 Maven 플러그인 hello는 현재 미리 보기로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-106">hello Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="25ead-107">지금은 FTP 게시만 지원 되지만 이후 hello에 대 한 추가 기능이 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-107">For now, only FTP publishing is supported, although additional features are planned for hello future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="25ead-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="25ead-108">Prerequisites</span></span>

<span data-ttu-id="25ead-109">이 자습서에서는 toocomplete hello 단계 순서를 필수 구성 요소를 다음 toohave hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-109">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="25ead-110">Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [무료 Azure 계정]에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="25ead-111">hello [Azure 명령줄 인터페이스 (CLI)]합니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="25ead-112">최신 [JDK(Java Development Kit)], 버전 1.7 이상</span><span class="sxs-lookup"><span data-stu-id="25ead-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="25ead-113">Apache의 [Maven] 빌드 도구(버전 3)</span><span class="sxs-lookup"><span data-stu-id="25ead-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="25ead-114">[Git] 클라이언트</span><span class="sxs-lookup"><span data-stu-id="25ead-114">A [Git] client.</span></span>
* <span data-ttu-id="25ead-115">[Docker] 클라이언트</span><span class="sxs-lookup"><span data-stu-id="25ead-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="25ead-116">이 자습서의 toohello 가상화 요구 사항 때문; 가상 컴퓨터에이 문서의 hello 단계를 따를 수 없는 물리적 컴퓨터를 사용 하 여 가상화 기능을 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-116">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-hello-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="25ead-117">Docker 웹 응용 프로그램에 복제 hello 샘플 스프링 부팅</span><span class="sxs-lookup"><span data-stu-id="25ead-117">Clone hello sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="25ead-118">이 섹션에서는 컨테이너화된 Spring Boot 응용 프로그램을 복제하고 로컬로 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-118">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="25ead-119">명령 프롬프트 또는 터미널 윈도우를 열고 스프링 부팅 응용 프로그램 및 toothat 디렉터리를 변경 합니다; 로컬 디렉터리 toohold 만들기 예를 들어:</span><span class="sxs-lookup"><span data-stu-id="25ead-119">Open a command prompt or terminal window and create a local directory toohold your Spring Boot application, and change toothat directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="25ead-120">-- 또는 --</span><span class="sxs-lookup"><span data-stu-id="25ead-120">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="25ead-121">복제 hello [스프링 부팅 Docker 시작에] 샘플 프로젝트를 만든; hello 디렉터리 예:</span><span class="sxs-lookup"><span data-stu-id="25ead-121">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot-docker
   ```

1. <span data-ttu-id="25ead-122">디렉터리 toohello 완료 된 프로젝트를 변경 합니다. 예를 들어:</span><span class="sxs-lookup"><span data-stu-id="25ead-122">Change directory toohello completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="25ead-123">Maven;를 사용 하 여 hello JAR 파일 빌드 예를 들어:</span><span class="sxs-lookup"><span data-stu-id="25ead-123">Build hello JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="25ead-124">Hello 웹 응용 프로그램을 만들면 Maven;를 사용 하 여 hello 웹 응용 프로그램을 시작 합니다. 예를 들어:</span><span class="sxs-lookup"><span data-stu-id="25ead-124">When hello web app has been created, start hello web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="25ead-125">웹 브라우저를 사용 하 여 로컬로 tooit 이동 하 여 hello 웹 앱을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-125">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="25ead-126">예를 들어 hello curl을 사용할 수 있는 경우 다음 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-126">For example, you could use hello following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="25ead-127">Hello 메시지 표시의 뒤에 표시 됩니다: **Docker는 Hello World**</span><span class="sxs-lookup"><span data-stu-id="25ead-127">You should see hello following message displayed: **Hello Docker World**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="25ead-128">Azure 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="25ead-128">Create an Azure service principal</span></span>

<span data-ttu-id="25ead-129">이 섹션에서는 Azure 컨테이너 tooAzure를 배포할 때 Maven 플러그 인 사용 하 여 hello 서비스 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-129">In this section, you create an Azure service principal that hello Maven plugin uses when deploying your container tooAzure.</span></span>

1. <span data-ttu-id="25ead-130">명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-130">Open a command prompt.</span></span>

1. <span data-ttu-id="25ead-131">사용 하 여 Azure 계정에 로그인 Azure CLI hello:</span><span class="sxs-lookup"><span data-stu-id="25ead-131">Sign into your Azure account by using hello Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="25ead-132">Hello 지침 toocomplete hello 로그인 프로세스를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-132">Follow hello instructions toocomplete hello sign-in process.</span></span>

1. <span data-ttu-id="25ead-133">Azure 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="25ead-133">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="25ead-134">여기서 `uuuuuuuu` hello 사용자 이름 및 `pppppppp` hello 서비스 사용자에 대 한 hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-134">Where `uuuuuuuu` is hello user name and `pppppppp` is hello password for hello service principal.</span></span>

1. <span data-ttu-id="25ead-135">Azure는 다음 예제는 hello 유사한 JSON로 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-135">Azure responds with JSON that resembles hello following example:</span></span>
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
   > <span data-ttu-id="25ead-136">Hello Maven 플러그 인 toodeploy 컨테이너 tooAzure를 구성할 때 hello 값이 JSON 응답을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-136">You will use hello values from this JSON response when you configure hello Maven plugin toodeploy your container tooAzure.</span></span> <span data-ttu-id="25ead-137">hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, 및 `tttttttt` 되는 자리 표시자 값은 사용이 예제에서는 toomake에 보다 쉽게 toomap 이러한 값 tootheir 각 요소가 사용자 Maven을 구성할 때 `settings.xml` hello에 다음 파일 단원을 참조 하십시오입니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-137">hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example toomake it easier toomap these values tootheir respective elements when you configure your Maven `settings.xml` file in hello next section.</span></span>
   >
   >

## <a name="configure-maven-toouse-your-azure-service-principal"></a><span data-ttu-id="25ead-138">Maven toouse Azure 서비스 사용자 구성</span><span class="sxs-lookup"><span data-stu-id="25ead-138">Configure Maven toouse your Azure service principal</span></span>

<span data-ttu-id="25ead-139">이 섹션에서는 컨테이너 tooAzure를 배포할 때 Maven에서 사용 하 여 Azure 서비스 주 tooconfigure hello 인증에서 hello 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-139">In this section, you use hello values from your Azure service principal tooconfigure hello authentication that Maven will use when deploying your container tooAzure.</span></span>

1. <span data-ttu-id="25ead-140">프로그램 Maven 열고 `settings.xml` 텍스트 편집기에서 파일;이 파일은 다음 예제는 hello와 같은 경로에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-140">Open your Maven `settings.xml` file in a text editor; this file might be in a path like hello following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="25ead-141">이 자습서 toohello의 hello 이전 섹션에서 Azure 서비스 보안 주체 설정 추가 `<servers>` hello에 대 한 컬렉션 *settings.xml* 파일; 예:</span><span class="sxs-lookup"><span data-stu-id="25ead-141">Add your Azure service principal settings from hello previous section of this tutorial toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="25ead-142">여기서,</span><span class="sxs-lookup"><span data-stu-id="25ead-142">Where:</span></span>
   <span data-ttu-id="25ead-143">요소</span><span class="sxs-lookup"><span data-stu-id="25ead-143">Element</span></span> | <span data-ttu-id="25ead-144">설명</span><span class="sxs-lookup"><span data-stu-id="25ead-144">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="25ead-145">Maven 웹 응용 프로그램 tooAzure를 배포할 때 toolook 보안 설정을 사용 하는 고유한 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-145">Specifies a unique name which Maven uses toolook up your security settings when you deploy your web app tooAzure.</span></span>
   `<client>` | <span data-ttu-id="25ead-146">Hello 포함 `appId` 서비스 사용자의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-146">Contains hello `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="25ead-147">Hello 포함 `tenant` 서비스 사용자의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-147">Contains hello `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="25ead-148">Hello 포함 `password` 서비스 사용자의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-148">Contains hello `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="25ead-149">hello 대상 Azure 클라우드 환경 정의 `AZURE` 이 예에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-149">Defines hello target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="25ead-150">(전체 환경 목록을 hello 영어로 [Azure 웹 앱에 대 한 Maven 플러그인] 설명서)</span><span class="sxs-lookup"><span data-stu-id="25ead-150">(A full list of environments is available in hello [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="25ead-151">저장 후 닫기 hello *settings.xml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-151">Save and close hello *settings.xml* file.</span></span>

## <a name="optional-deploy-your-local-docker-file-toodocker-hub"></a><span data-ttu-id="25ead-152">선택 사항: 배포에 로컬 Docker 파일 tooDocker 허브</span><span class="sxs-lookup"><span data-stu-id="25ead-152">OPTIONAL: Deploy your local Docker file tooDocker Hub</span></span>

<span data-ttu-id="25ead-153">Docker 계정이 있는 경우에 프로그램 Docker 컨테이너 이미지를 로컬에서 작성 하 고 tooDocker 허브를 푸시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-153">If you have a Docker account, you can build your Docker container image locally and push it tooDocker Hub.</span></span> <span data-ttu-id="25ead-154">따라서, toodo 단계를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-154">toodo so, use hello following steps.</span></span>

1. <span data-ttu-id="25ead-155">열기 hello `pom.xml` 텍스트 편집기에서 스프링 부팅 응용 프로그램에 대 한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-155">Open hello `pom.xml` file for your Spring Boot application in a text editor.</span></span>

1. <span data-ttu-id="25ead-156">Hello 찾을 `<imageName>` hello의 자식 요소 `<containerSettings>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-156">Locate hello `<imageName>` child element of hello `<containerSettings>` element.</span></span>

1. <span data-ttu-id="25ead-157">업데이트 hello `${docker.image.prefix}` 값을 Docker 계정 이름:</span><span class="sxs-lookup"><span data-stu-id="25ead-157">Update hello `${docker.image.prefix}` value with your Docker account name:</span></span>
   ```xml
   <containerSettings>
      <imageName>mydockeraccountname/${project.artifactId}</imageName>
   </containerSettings>
   ```

1. <span data-ttu-id="25ead-158">Hello 다음 배포 방법 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-158">Choose one of hello following deployment methods:</span></span>

   * <span data-ttu-id="25ead-159">Maven에서로 로컬로 컨테이너 이미지를 구축 하 고 Docker toopush 사용 하 여 컨테이너 tooDocker 허브 여 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-159">Build your container image locally with Maven, and then use Docker toopush your container tooDocker Hub:</span></span>
      ```shell
      mvn clean package docker:build
      docker push
      ```
   
   * <span data-ttu-id="25ead-160">Hello 있으면 [Maven 용 Docker 플러그인] 설치를 자동으로 작성할 수 있으며, 사용자 컨테이너 이미지 tooDocker 허브를 사용 하 여 hello `-DpushImage` 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="25ead-160">If you have hello [Docker plugin for Maven] installed, you can automatically build and your container image tooDocker Hub by using hello `-DpushImage` parameter:</span></span>
      ```shell
      mvn clean package docker:build -DpushImage
      ```

## <a name="optional-customize-your-pomxml-before-deploying-your-container-tooazure"></a><span data-ttu-id="25ead-161">선택 사항: 사용자 지정 프로그램 pom.xml 컨테이너 tooAzure를 배포 하기 전에</span><span class="sxs-lookup"><span data-stu-id="25ead-161">OPTIONAL: Customize your pom.xml before deploying your container tooAzure</span></span>

<span data-ttu-id="25ead-162">열기 hello `pom.xml` 텍스트 편집기에서 스프링 부팅 응용 프로그램에 대 한 파일을 찾은 후 hello `<plugin>` 요소에 대 한 `azure-webapp-maven-plugin`합니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-162">Open hello `pom.xml` file for your Spring Boot application in a text editor, and then locate hello `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="25ead-163">이 요소에는 다음 예제는 hello와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-163">This element should resemble hello following example:</span></span>

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

<span data-ttu-id="25ead-164">Hello Maven 플러그 인에 대해 수정할 수 있는 값이 여러 개인 및 이러한 각 요소에 대 한 자세한 설명을 hello 영어로 [Azure 웹 앱에 대 한 Maven 플러그인] 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-164">There are several values that you can modify for hello Maven plugin, and a detailed description for each of these elements is available in hello [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="25ead-165">즉, 이 문서에서 강조 표시된 값은 여러 개입니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-165">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="25ead-166">요소</span><span class="sxs-lookup"><span data-stu-id="25ead-166">Element</span></span> | <span data-ttu-id="25ead-167">설명</span><span class="sxs-lookup"><span data-stu-id="25ead-167">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="25ead-168">Hello 버전의 hello 지정 [Azure 웹 앱에 대 한 Maven 플러그인]합니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-168">Specifies hello version of hello [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="25ead-169">Hello에 나열 된 hello 버전을 검사 해야 하면 [Maven 중앙 리포지토리](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) 사용 중인 tooensure hello 최신 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-169">You should check hello version listed in hello [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure that you are using hello latest version.</span></span>
`<authentication>` | <span data-ttu-id="25ead-170">이 예제에 포함 된 Azure의 hello 인증 정보를 지정 된 `<serverId>` 포함 된 요소 `azure-auth`; Maven hello Azure 서비스 주체 값을 해당 값 toolook 프로그램 Maven에서 사용 하 여 *settings.xml* 이 문서의 이전 섹션에 정의 된 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-170">Specifies hello authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value toolook up hello Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="25ead-171">Hello 대상 리소스 그룹, 즉 지정 `maven-plugin` 이 예에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-171">Specifies hello target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="25ead-172">hello 리소스 그룹이 아직 없는 경우 배포 중 만들어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-172">hello resource group will be created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="25ead-173">웹 앱에 대 한 hello 대상 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-173">Specifies hello target name for your web app.</span></span> <span data-ttu-id="25ead-174">이 예제에서는 hello 대상 이름은 `maven-linux-app-${maven.build.timestamp}`여기서 hello `${maven.build.timestamp}` 이 예제에서는 tooavoid 충돌의 접미사가 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-174">In this example, hello target name is `maven-linux-app-${maven.build.timestamp}`, where hello `${maven.build.timestamp}` suffix is appended in this example tooavoid conflict.</span></span> <span data-ttu-id="25ead-175">(hello 타임 스탬프는 선택 사항) hello 응용 프로그램 이름에 대 한 고유 문자열을 모두 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-175">(hello timestamp is optional; you can specify any unique string for hello app name.)</span></span>
`<region>` | <span data-ttu-id="25ead-176">이 예제는 hello 대상 지역을 지정 `westus`합니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-176">Specifies hello target region, which in this example is `westus`.</span></span> <span data-ttu-id="25ead-177">(전체 목록은 hello에 [Azure 웹 앱에 대 한 Maven 플러그인] 설명서입니다.)</span><span class="sxs-lookup"><span data-stu-id="25ead-177">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<appSettings>` | <span data-ttu-id="25ead-178">웹 앱 tooAzure를 배포할 때 Maven toouse에 대 한 고유한 설정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-178">Specifies any unique settings for Maven toouse when deploying your web app tooAzure.</span></span> <span data-ttu-id="25ead-179">이 예제는 `<property>` 요소 앱에 대 한 hello 포트를 지정 하는 자식 요소의 이름/값 쌍을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-179">In this example, a `<property>` element contains a name/value pair of child elements that specify hello port for your app.</span></span>

> [!NOTE]
>
> <span data-ttu-id="25ead-180">이 예에서 hello 설정을 toochange hello 포트 번호는 hello 기본값과에서 hello 포트를 변경 하는 경우에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-180">hello settings toochange hello port number in this example are only necessary when you are changing hello port from hello default.</span></span>
>

## <a name="build-and-deploy-your-container-tooazure"></a><span data-ttu-id="25ead-181">빌드 및 배포 컨테이너 tooAzure</span><span class="sxs-lookup"><span data-stu-id="25ead-181">Build and deploy your container tooAzure</span></span>

<span data-ttu-id="25ead-182">준비 toodeploy는 hello 이전이 문서의 섹션에서에서 hello 설정을 모두 구성 했으면, 컨테이너 tooAzure 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-182">Once you have configured all of hello settings in hello preceding sections of this article, you are ready toodeploy your container tooAzure.</span></span> <span data-ttu-id="25ead-183">따라서 toodo 단계를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-183">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="25ead-184">Hello 명령 프롬프트 또는 이전에 사용 하 던 터미널 창에서 모든 변경 내용을 toohello을 만든 경우 Maven를 사용 하 여 hello JAR 파일을 다시 작성 *pom.xml* 파일; 예:</span><span class="sxs-lookup"><span data-stu-id="25ead-184">From hello command prompt or terminal window that you were using earlier, rebuild hello JAR file using Maven if you made any changes toohello *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="25ead-185">Maven;를 사용 하 여 웹 응용 프로그램 tooAzure 배포 예를 들어:</span><span class="sxs-lookup"><span data-stu-id="25ead-185">Deploy your web app tooAzure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="25ead-186">Maven 프로그램 웹 응용 프로그램 tooAzure; 배포 웹 앱 hello가 아직 없는 경우 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-186">Maven will deploy your web app tooAzure; if hello web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="25ead-187">경우 hello에서 지정 하는 hello 지역 `<region>` 의 요소 프로그램 *pom.xml* 파일에 없는 사용할 수 있는 충분 한 서버 배포를 시작 하는 경우, 다음 예제에서는 오류 유사한 toohello 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-187">If hello region which you specify in hello `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar toohello following example:</span></span>
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
> <span data-ttu-id="25ead-188">이 경우 다른 영역을 다시 실행 Maven 명령 toodeploy 응용 프로그램를 hello를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-188">If this happens, you can specify another region and re-run hello Maven command toodeploy your application.</span></span>
>
>

<span data-ttu-id="25ead-189">웹 배포 된 수 toomanage 됩니다 hello를 사용 하 여 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-189">When your web has been deployed, you will be able toomanage it by using hello [Azure portal].</span></span>

* <span data-ttu-id="25ead-190">웹앱은 **App Services**에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="25ead-190">Your web app will be listed in **App Services**:</span></span>

   ![Azure Portal App Services에 나열된 웹앱][AP01]

* <span data-ttu-id="25ead-192">웹 앱 hello에 나열 됩니다에 대 한 URL을 hello 및 **개요** 웹 앱에 대 한:</span><span class="sxs-lookup"><span data-stu-id="25ead-192">And hello URL for your web app will be listed in hello **Overview** for your web app:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="25ead-194">다음 단계</span><span class="sxs-lookup"><span data-stu-id="25ead-194">Next steps</span></span>

<span data-ttu-id="25ead-195">Hello에 대 한 자세한 내용은이 문서에서 설명 하는 다양 한 기술 참조 문서 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="25ead-195">For more information about hello various technologies discussed in this article, see hello following articles:</span></span>

* <span data-ttu-id="25ead-196">[Azure 웹 앱에 대 한 Maven 플러그인]</span><span class="sxs-lookup"><span data-stu-id="25ead-196">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="25ead-197">TooAzure hello Azure CLI에서 로그인</span><span class="sxs-lookup"><span data-stu-id="25ead-197">Log in tooAzure from hello Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="25ead-198">어떻게 toouse hello Maven 플러그 인에 대 한 Azure 웹 앱 toodeploy 스프링 부팅 앱 tooAzure 앱 서비스</span><span class="sxs-lookup"><span data-stu-id="25ead-198">How toouse hello Maven Plugin for Azure Web Apps toodeploy a Spring Boot app tooAzure App Service </span></span>](app-service-web-deploy-spring-boot-app-with-maven-plugin.md)

* [<span data-ttu-id="25ead-199">Azure CLI 2.0을 사용하여 Azure 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="25ead-199">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="25ead-200">Maven 설정 참조</span><span class="sxs-lookup"><span data-stu-id="25ead-200">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="25ead-201">[Maven 용 Docker 플러그인]</span><span class="sxs-lookup"><span data-stu-id="25ead-201">[Docker plugin for Maven]</span></span>

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
