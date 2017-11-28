---
title: "사용 하 여 Docker 컨테이너 스프링 부팅 앱 aaaPublish IntelliJ에 대 한 Azure 도구 키트 hello | Microsoft Docs"
description: "자세한 내용은 toopublish 웹 앱 tooMicrosoft Docker 컨테이너를 사용 하 여 Azure IntelliJ에 대 한 Azure 도구 키트를 hello 하는 방법입니다."
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
ms.openlocfilehash: 8964cb33fd8f61a39f091633ae9074d9658232fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a><span data-ttu-id="56cdb-103">IntelliJ 용 Azure 도구 키트 hello를 사용 하 여 Docker 컨테이너 스프링 부팅 앱 게시</span><span class="sxs-lookup"><span data-stu-id="56cdb-103">Publish a Spring Boot app as a Docker container by using hello Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="56cdb-104">hello [Spring Framework] 은 오픈 소스 솔루션으로 Java 개발자가 엔터프라이즈 수준의 응용 프로그램을 만들 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-104">hello [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="56cdb-105">중 만들어지는 hello 더 이상 인기 있는 프로젝트의 플랫폼은 [스프링 부팅], 독립 실행형 Java 응용 프로그램을 만들기 위한 있는 간단한 접근 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-105">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="56cdb-106">[Docker] hello 배포, 배율 및 컨테이너에서 실행 되는 응용 프로그램의 관리 하는데 도움이 되는 오픈 소스 솔루션 자동화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-106">[Docker] is an open-source solution that helps developers automate hello deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="56cdb-107">이 자습서에서는 hello 단계 toodeploy 스프링 부팅 응용 프로그램으로 Docker 컨테이너 tooMicrosoft Azure IntelliJ 용 Azure 도구 키트 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-107">This tutorial walks you through hello steps toodeploy a Spring Boot application as a Docker container tooMicrosoft Azure by using hello Azure Toolkit for IntelliJ.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repo"></a><span data-ttu-id="56cdb-108">Hello 기본 스프링 부팅 Docker 리포지토리 복제</span><span class="sxs-lookup"><span data-stu-id="56cdb-108">Clone hello default Spring Boot Docker repo</span></span>

<span data-ttu-id="56cdb-109">hello 다음 단계에 관한 IntelliJ를 사용 하 여 hello 스프링 부팅 Docker 리포지토리를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-109">hello following steps walk you through cloning hello Spring Boot Docker repo by using IntelliJ.</span></span> <span data-ttu-id="56cdb-110">Toouse 명령줄 참조 [컨테이너 서비스를 Azure에서 Linux에서 스프링 부팅 응용 프로그램 배포][Deploy Spring Boot on Linux in ACS]합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-110">If you want toouse a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].</span></span>

1. <span data-ttu-id="56cdb-111">IntelliJ를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-111">Open IntelliJ.</span></span>

1. <span data-ttu-id="56cdb-112">Hello 시작 화면에 선택 hello **GitHub** hello에 대 한 옵션 **버전 제어에서 체크 아웃** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-112">On hello welcome screen, select hello **GitHub** option in hello **Check out from Version Control** list.</span></span>

   ![버전 제어에 대한 GitHub 옵션][CL01]

1. <span data-ttu-id="56cdb-114">증명된 toolog 경우 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-114">Enter your credentials if you are prompted toolog in.</span></span>

   * <span data-ttu-id="56cdb-115">사용자 이름/암호 toolog tooGitHub 사용 중인 경우:</span><span class="sxs-lookup"><span data-stu-id="56cdb-115">If you are using a username/password toolog in tooGitHub:</span></span>

      ![GitHub 사용자 이름 및 암호를 입력하는 대화 상자][CL02a]

   * <span data-ttu-id="56cdb-117">토큰 toolog tooGitHub 사용 중인 경우:</span><span class="sxs-lookup"><span data-stu-id="56cdb-117">If you are using a token toolog in tooGitHub:</span></span>

      ![GitHub 토큰을 입력하는 대화 상자][CL02b]

1. <span data-ttu-id="56cdb-119">입력 **https://github.com/spring-guides/gs-spring-boot-docker.git** hello 리포지토리의 URL에 대 한 로컬 경로 및 폴더 정보를 지정 하 고 클릭 **복제**합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-119">Enter **https://github.com/spring-guides/gs-spring-boot-docker.git** for hello repo URL, specify your local path and folder information, and then click **Clone**.</span></span>

   ![리포지토리 복제 대화 상자][CL03]

1. <span data-ttu-id="56cdb-121">프롬프트 메시지가 나타날 때 선택 IntelliJ 프로젝트 toocreate **아니요**합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-121">When you're prompted toocreate an IntelliJ project, select **No**.</span></span>

   ![IntelliJ 프로젝트 toocreate 감소 하 고][CL04]

1. <span data-ttu-id="56cdb-123">Hello 시작 페이지에서 클릭 **가져오기 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-123">On hello welcome page, click **Import Project**.</span></span>

   ![프로젝트 가져오기 선택 영역][CL05]

1. <span data-ttu-id="56cdb-125">Hello 스프링 부팅 리포지토리를 복제 하는 hello 경로 확인, hello 선택 **완료** hello 루트 및 클릭 한 다음 아래에 폴더 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-125">Locate hello path where you cloned hello Spring Boot repo, select hello **complete** folder under hello root, and then click **OK**.</span></span>

   ![가져올 폴더 선택][CL06]

1. <span data-ttu-id="56cdb-127">메시지가 표시되면 **기존 원본에서 프로젝트 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-127">When you're prompted, select **Create project from existing sources**.</span></span>

   ![옵션 toocreate 기존 소스에서 프로젝트][CL07]

1. <span data-ttu-id="56cdb-129">프로젝트 이름을 지정 하거나 hello 기본값을 그대로, 올바른 경로 toohello hello 확인 **완료** 폴더를 마우스 클릭 한 다음 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-129">Specify your project name or accept hello default, verify hello correct path toohello **complete** folder, and then click **Next**.</span></span>

   ![Hello 프로젝트 이름 지정][CL08]

1. <span data-ttu-id="56cdb-131">가져오기에 대한 모든 디렉터리를 사용자 지정한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-131">Customize any directories for importing, and then click **Next**.</span></span>

   ![디렉터리 선택][CL09]

1. <span data-ttu-id="56cdb-133">Hello 라이브러리 tooimport 검토 한 다음 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-133">Review hello libraries tooimport, and then click **Next**.</span></span>

   ![프로젝트 라이브러리 검토][CL10]

1. <span data-ttu-id="56cdb-135">Hello 모듈 구조를 검토 한 다음 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-135">Review hello module structure, and then click **Next**.</span></span>

   ![모듈 구조 검토][CL11]

1. <span data-ttu-id="56cdb-137">JDK를 지정한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-137">Specify your JDK, and then click **Next**.</span></span>

   ![JDK 지정][CL12]

1. <span data-ttu-id="56cdb-139">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-139">Click **Finish**.</span></span>

   ![마침 단추][CL13]

<span data-ttu-id="56cdb-141">IntelliJ는 hello 스프링 부팅 앱 프로젝트로 가져오고 hello 가져오기 완료 되 면 hello 구조를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-141">IntelliJ imports hello Spring Boot app as a project and displays hello structure when hello import has finished.</span></span>

![IntelliJ에서 Spring Boot 앱][CL14]

## <a name="build-your-spring-boot-app"></a><span data-ttu-id="56cdb-143">Spring Boot 앱 빌드</span><span class="sxs-lookup"><span data-stu-id="56cdb-143">Build your Spring Boot app</span></span>

### <a name="build-hello-app-by-using-hello-maven-pom"></a><span data-ttu-id="56cdb-144">Maven POM hello를 사용 하 여 hello 앱 빌드</span><span class="sxs-lookup"><span data-stu-id="56cdb-144">Build hello app by using hello Maven POM</span></span>

1. <span data-ttu-id="56cdb-145">아직 열려 있지 않은 경우 hello Maven 도구 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-145">Open hello Maven tool window if it is not already opened.</span></span> <span data-ttu-id="56cdb-146">**보기** > **도구 창** > **Maven 프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-146">Click **View** > **Tool Windows** > **Maven Projects**.</span></span>

   ![도구 창과 Maven 프로젝트 명령][BU01]

1. <span data-ttu-id="56cdb-148">Hello Maven 도구 창에서 마우스 오른쪽 단추로 클릭 **패키지** 선택 **Maven 빌드 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-148">In hello Maven tool window, right-click **package** and select **Run Maven Build**.</span></span> <span data-ttu-id="56cdb-149">(Maven 프로젝트 자동으로 표시 되지 않으면를 클릭 하 여 hello **다시 가져오는** hello Maven 도구 모음의 아이콘을 합니다.)</span><span class="sxs-lookup"><span data-stu-id="56cdb-149">(If your Maven project does not show up automatically, click hello **Reimport** icon on hello Maven toolbar.)</span></span>

   ![Maven 빌드 실행 명령][BU02]

1. <span data-ttu-id="56cdb-151">IntelliJ는 Spring Boot 앱이 성공적으로 생성되면 **빌드 성공** 메시지를 표시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-151">IntelliJ should display a **BUILD SUCCESS** message when your Spring Boot app is successfully created.</span></span>

   ![빌드 성공 메시지][BU03]

### <a name="create-a-deployment-ready-artifact"></a><span data-ttu-id="56cdb-153">배포 준비된 아티팩트 만들기</span><span class="sxs-lookup"><span data-stu-id="56cdb-153">Create a deployment-ready artifact</span></span>

<span data-ttu-id="56cdb-154">toopublish 스프링 부팅 앱 배포 준비 아티팩트 toocreate 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-154">toopublish your Spring Boot app, you need toocreate a deployment-ready artifact.</span></span> <span data-ttu-id="56cdb-155">단계를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-155">Use hello following steps:</span></span>

1. <span data-ttu-id="56cdb-156">IntelliJ의 웹앱 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-156">Open your web app project in IntelliJ.</span></span>

1. <span data-ttu-id="56cdb-157">**파일**을 클릭한 다음 **프로젝트 구조**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-157">Click **File**, and then click **Project Structure**.</span></span>

   ![프로젝트 구조 명령][ART01]

1. <span data-ttu-id="56cdb-159">녹색 더하기 hello 클릭 (**+**) tooadd 아티팩트 기호를 클릭 **JAR**, 클릭 하 고 **빈**합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-159">Click hello green plus (**+**) symbol tooadd an artifact, click **JAR**, and then click **Empty**.</span></span>

   ![아티팩트 추가][ART02]

1. <span data-ttu-id="56cdb-161">하지 tooadd hello ".jar" 확장 한 다음 Maven 출력 hello에 대 한 hello 대상 폴더를 지정 하 여 아티팩트를 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-161">Name your artifact while making sure not tooadd hello ".jar" extension, and then specify hello target folder for hello Maven output.</span></span>

   ![아티팩트 속성 지정][ART03]

1. <span data-ttu-id="56cdb-163">아티팩트에 대한 매니페스트를 만듭니다(선택 사항).</span><span class="sxs-lookup"><span data-stu-id="56cdb-163">Create a manifest for your artifact (optional):</span></span>

   <span data-ttu-id="56cdb-164">a.</span><span class="sxs-lookup"><span data-stu-id="56cdb-164">a.</span></span> <span data-ttu-id="56cdb-165">**매니페스트 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-165">Click **Create Manifest**.</span></span>

      ![Hello 매니페스트 만들기 단추를 클릭 합니다.][ART04a]

   <span data-ttu-id="56cdb-167">b.</span><span class="sxs-lookup"><span data-stu-id="56cdb-167">b.</span></span> <span data-ttu-id="56cdb-168">Hello 아티팩트에 대 한 hello 기본 경로 선택한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-168">Choose hello default path for hello artifact, and then click **OK**.</span></span>

      ![아티팩트 경로 지정][ART04b]

   <span data-ttu-id="56cdb-170">c.</span><span class="sxs-lookup"><span data-stu-id="56cdb-170">c.</span></span> <span data-ttu-id="56cdb-171">Hello 줄임표를 클릭 (**...** ) toolocate hello 주 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-171">Click hello ellipsis (**...**) toolocate hello main class.</span></span>

      ![기본 클래스 찾기][ART04c]

   <span data-ttu-id="56cdb-173">ㄹ.</span><span class="sxs-lookup"><span data-stu-id="56cdb-173">d.</span></span> <span data-ttu-id="56cdb-174">기본 클래스를 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-174">Choose your main class, and then click **OK**.</span></span>

      ![기본 클래스 지정][ART04d]

1. <span data-ttu-id="56cdb-176">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-176">Click **OK**.</span></span>

   ![Hello 프로젝트 구조 대화 상자를 닫습니다][ART05]

> [!NOTE]
> <span data-ttu-id="56cdb-178">IntelliJ에서 아티팩트를 만드는 방법에 대 한 자세한 내용은 참조 [아티팩트 구성] hello JetBrains 웹 사이트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-178">For more information about creating artifacts in IntelliJ, see [Configuring Artifacts] on hello JetBrains website.</span></span>
>

### <a name="build-hello-artifact-for-deployment"></a><span data-ttu-id="56cdb-179">빌드 배포에 대 한 hello 아티팩트</span><span class="sxs-lookup"><span data-stu-id="56cdb-179">Build hello artifact for deployment</span></span>

1. <span data-ttu-id="56cdb-180">**빌드**를 클릭한 다음 **아티팩트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-180">Click **Build**, and then click **Artifacts**.</span></span>

   ![아티팩트 빌드 명령][BU04]

1. <span data-ttu-id="56cdb-182">Hello 때 **빌드 아티팩트** 상황에 맞는 메뉴에 표시 되 면 클릭 **빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-182">When hello **Build Artifact** context menu appears, click **Build**.</span></span>

   ![아티팩트 빌드 컨텍스트 메뉴][BU05]

<span data-ttu-id="56cdb-184">IntelliJ는 hello 프로젝트 도구 창에서 스프링 부팅 앱에 대 한 완료 hello 아티팩트를 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-184">IntelliJ should display hello completed artifact for your Spring Boot app in hello project tool window.</span></span>

   ![만든 아티팩트][BU06]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="56cdb-186">Docker 컨테이너를 사용 하 여 웹 응용 프로그램 tooAzure 게시</span><span class="sxs-lookup"><span data-stu-id="56cdb-186">Publish your web app tooAzure by using a Docker container</span></span>

1. <span data-ttu-id="56cdb-187">Tooyour Azure 계정에에서 등록 하지 않은 경우 hello 단계에 따라 [로그인에 대 한 지침 Azure 도구 키트 hello IntelliJ][Azure Sign In for IntelliJ]합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-187">If you have not signed in tooyour Azure account, follow hello steps in [Sign-in instructions for hello Azure Toolkit for IntelliJ][Azure Sign In for IntelliJ].</span></span>

1. <span data-ttu-id="56cdb-188">Hello 프로젝트 탐색기 도구 창에서 hello 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 선택 **Azure** > **Docker 컨테이너로 게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-188">In hello Project Explorer tool window, right-click hello project, and then select **Azure** > **Publish as Docker Container**.</span></span>

   ![Docker 컨테이너로 게시 명령][PU01]

1. <span data-ttu-id="56cdb-190">Hello 때 **Azure에서 Docker 컨테이너 배포** 대화 상자가 나타나면, 기존 Docker 호스트가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-190">When hello **Deploy Docker Container on Azure** dialog box appears, any existing Docker hosts are displayed.</span></span> <span data-ttu-id="56cdb-191">Toodeploy tooan 기존 호스트를 선택 하면 toostep 4를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-191">If you choose toodeploy tooan existing host, you can skip toostep 4.</span></span> <span data-ttu-id="56cdb-192">그렇지 않으면 다음 단계 toocreate 호스트 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-192">Otherwise, use hello following steps toocreate a host:</span></span>

   <span data-ttu-id="56cdb-193">a.</span><span class="sxs-lookup"><span data-stu-id="56cdb-193">a.</span></span> <span data-ttu-id="56cdb-194">녹색 더하기 hello 클릭 (**+**) 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-194">Click hello green plus (**+**) symbol.</span></span>

      ![새 Docker 호스트 추가][PU02]

   <span data-ttu-id="56cdb-196">b.</span><span class="sxs-lookup"><span data-stu-id="56cdb-196">b.</span></span> <span data-ttu-id="56cdb-197">Hello 때 **Docker 호스트 만들기** 대화 상자가 표시 됩니다, tooaccept hello 기본값을 선택 하거나 새 Docker 호스트에 대 한 사용자 지정 설정을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-197">When hello **Create Docker Host** dialog box appears, you can choose tooaccept hello defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="56cdb-198">(다양 한 설정, 참조에 대 한 자세한 설명은 hello [IntelliJ 용 Azure 도구 키트 hello를 사용 하 여 Docker 컨테이너와 웹 응용 프로그램을 게시할][Publish Container with Azure Toolkit].) 클릭 **다음** 어떤 설정 toouse 지정 했으면 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-198">(For detailed descriptions of hello various settings, see [Publish a web app as a Docker container by using hello Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings toouse.</span></span>

      ![Docker 호스트 옵션 지정][PU03a]

   <span data-ttu-id="56cdb-200">c.</span><span class="sxs-lookup"><span data-stu-id="56cdb-200">c.</span></span> <span data-ttu-id="56cdb-201">Azure 키 자격 증명 모음에서 toouse 기존 로그인 자격 증명을 선택할 수 있습니다 또는 새 Docker에 대 한 로그인 자격 증명 tooenter를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-201">You can choose toouse existing login credentials from an Azure key vault, or you can choose tooenter new Docker login credentials.</span></span> <span data-ttu-id="56cdb-202">옵션을 지정하면 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-202">Click **Finish** when you have specified your options.</span></span>

      ![Docker 호스트 자격 증명 지정][PU03b]

1. <span data-ttu-id="56cdb-204">Docker 호스트를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-204">Select your Docker host, and then click **Next**.</span></span>

   ![Hello Docker 호스트 toouse 선택][PU04]

1. <span data-ttu-id="56cdb-206">Hello hello의 마지막 페이지에 **Azure에서 Docker 컨테이너 배포** 대화 상자 hello 다음 옵션을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-206">On hello last page of hello **Deploy Docker Container on Azure** dialog box, specify hello following options:</span></span>

   <span data-ttu-id="56cdb-207">a.</span><span class="sxs-lookup"><span data-stu-id="56cdb-207">a.</span></span> <span data-ttu-id="56cdb-208">Docker 컨테이너를 호스팅할 hello 컨테이너에 대 한 사용자 지정 이름을 toospecify를 선택할 수 있습니다 또는 hello 기본값을 그대로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-208">You can choose toospecify a custom name for hello container that will host your Docker container, or you can accept hello default.</span></span>

   <span data-ttu-id="56cdb-209">b.</span><span class="sxs-lookup"><span data-stu-id="56cdb-209">b.</span></span> <span data-ttu-id="56cdb-210">구문 다음 hello를 사용 하 여 docker 호스트에 대 한 hello TCP 포트를 입력: *[외부 포트]*:*[내부 포트]*합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-210">Enter hello TCP ports for your docker host by using hello following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="56cdb-211">예를 들어 **80:8080** 외부 포트 80 및 hello 기본 내부 스프링 부팅 포트 8080 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-211">For example, **80:8080** specifies an external port of 80 and hello default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="56cdb-212">내부 포트 (예를 들어 파일 편집 하 여 hello application.yml) 사용자 지정을 Azure의 hello 올바른 라우팅 toooccur toospecify hello 포트 번호가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-212">If you have customized your internal port (for example, by editing hello application.yml file), you need toospecify hello port number for hello correct routing toooccur in Azure.</span></span>

   <span data-ttu-id="56cdb-213">c.</span><span class="sxs-lookup"><span data-stu-id="56cdb-213">c.</span></span> <span data-ttu-id="56cdb-214">이러한 옵션을 구성했으면 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-214">After you have configured these options, click **Finish**.</span></span>

   ![Azure에 Docker 컨테이너 배포][PU05]

1. <span data-ttu-id="56cdb-216">Azure 도구 키트 hello 게시 완료 되 면 hello Azure 활동 로그 표시 **게시 됨** hello 상태에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-216">When hello Azure Toolkit has finished publishing, hello Azure Activity Log displays **Published** for hello status.</span></span>

   ![Docker 호스트를 성공적으로 배포][PU06]

## <a name="next-steps"></a><span data-ttu-id="56cdb-218">다음 단계</span><span class="sxs-lookup"><span data-stu-id="56cdb-218">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<span data-ttu-id="56cdb-219">toolearn IntelliJ를 사용 하 여 스프링 부팅 앱을 만들기 위한 추가 방법에 대 한 참조 [스프링 부팅 프로젝트 만들기](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) hello JetBrains 웹 사이트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56cdb-219">toolearn about additional methods for creating Spring Boot apps by using IntelliJ, see [Creating Spring Boot Projects](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) on hello JetBrains website.</span></span>

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Sign In for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[아티팩트 구성]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[스프링 부팅]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL01.png
[CL02a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02a.png
[CL02b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02b.png
[CL03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL09.png
[CL10]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL10.png
[CL11]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL11.png
[CL12]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL12.png
[CL13]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL13.png
[CL14]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL14.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART03.png
[ART04a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04a.png
[ART04b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04b.png
[ART04c]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04c.png
[ART04d]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04d.png
[ART05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART05.png

[BU01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU02.png
[BU03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU03.png
[BU04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU04.png
[BU05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU05.png
[BU06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU06.png

[PU01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU02.png
[PU03a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03a.png
[PU03b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03b.png
[PU04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU06.png
