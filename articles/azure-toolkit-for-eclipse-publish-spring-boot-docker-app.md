---
title: "사용 하 여 Docker 컨테이너 스프링 부팅 앱 aaaPublish hello Azure Toolkit for Eclipse | Microsoft Docs"
description: "자세한 방법을 사용 하 여 Docker 컨테이너도 Azure는 웹 응용 프로그램 tooMicrosoft toopublish hello Azure Toolkit for Eclipse."
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
ms.openlocfilehash: 29390c49c339a1ebb87cb3951b21cea01c0da15f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a><span data-ttu-id="fd28c-103">Eclipse 용 Azure 도구 키트 hello를 사용 하 여 Docker 컨테이너 스프링 부팅 앱 게시</span><span class="sxs-lookup"><span data-stu-id="fd28c-103">Publish a Spring Boot app as a Docker container by using hello Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="fd28c-104">hello [Spring Framework] 은 오픈 소스 솔루션으로 Java 개발자가 엔터프라이즈 수준의 응용 프로그램을 만들 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-104">hello [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="fd28c-105">중 만들어지는 hello 더 이상 인기 있는 프로젝트의 플랫폼은 [스프링 부팅], 독립 실행형 Java 응용 프로그램을 만들기 위한 있는 간단한 접근 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-105">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="fd28c-106">[Docker] hello 배포, 배율 및 컨테이너에서 실행 되는 응용 프로그램의 관리 하는데 도움이 되는 오픈 소스 솔루션 자동화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-106">[Docker] is an open-source solution that helps developers automate hello deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="fd28c-107">이 자습서에서는 hello 단계 toodeploy 스프링 부팅 응용 프로그램으로 Docker 컨테이너 tooMicrosoft Azure Eclipse 용 Azure 도구 키트 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-107">This tutorial walks you through hello steps toodeploy a Spring Boot application as a Docker container tooMicrosoft Azure by using hello Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repository"></a><span data-ttu-id="fd28c-108">Hello 기본 스프링 부팅 Docker 리포지토리 복제</span><span class="sxs-lookup"><span data-stu-id="fd28c-108">Clone hello default Spring Boot Docker repository</span></span>

### <a name="import-hello-public-repository"></a><span data-ttu-id="fd28c-109">Hello 공개 저장소 가져오기</span><span class="sxs-lookup"><span data-stu-id="fd28c-109">Import hello public repository</span></span>

<span data-ttu-id="fd28c-110">hello 다음 단계에 관한 IntelliJ를 사용 하 여 hello 스프링 부팅 Docker 리포지토리 tooyour 로컬 컴퓨터를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-110">hello following steps walk you through cloning hello Spring Boot Docker repository tooyour local computer by using IntelliJ.</span></span> <span data-ttu-id="fd28c-111">Toouse 명령줄 참조 [컨테이너 서비스를 Azure에서 Linux에서 스프링 부팅 응용 프로그램 배포][Deploy Spring Boot on Linux in ACS]합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-111">If you want toouse a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].</span></span>

1. <span data-ttu-id="fd28c-112">Eclipse를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-112">Open Eclipse.</span></span>

1. <span data-ttu-id="fd28c-113">**File** > **Import**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-113">Click **File** > **Import**.</span></span>

   ![File Import 메뉴][CL01]

1. <span data-ttu-id="fd28c-115">Hello 때 **가져오기** 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-115">When hello **Import** dialog box opens:</span></span>

   <span data-ttu-id="fd28c-116">a.</span><span class="sxs-lookup"><span data-stu-id="fd28c-116">a.</span></span> <span data-ttu-id="fd28c-117">**Git**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-117">Expand **Git**.</span></span>

   <span data-ttu-id="fd28c-118">b.</span><span class="sxs-lookup"><span data-stu-id="fd28c-118">b.</span></span> <span data-ttu-id="fd28c-119">**Projects from Git**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-119">Select **Projects from Git**.</span></span>
   
   <span data-ttu-id="fd28c-120">c.</span><span class="sxs-lookup"><span data-stu-id="fd28c-120">c.</span></span> <span data-ttu-id="fd28c-121">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-121">Click **Next**.</span></span>

   ![Import 대화 상자][CL02]

1. <span data-ttu-id="fd28c-123">Hello에 **리포지토리 원본 선택** 페이지:</span><span class="sxs-lookup"><span data-stu-id="fd28c-123">On hello **Select Repository Source** page:</span></span>

   <span data-ttu-id="fd28c-124">a.</span><span class="sxs-lookup"><span data-stu-id="fd28c-124">a.</span></span> <span data-ttu-id="fd28c-125">**Clone URI**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-125">Select **Clone URI**.</span></span>
   
   <span data-ttu-id="fd28c-126">b.</span><span class="sxs-lookup"><span data-stu-id="fd28c-126">b.</span></span> <span data-ttu-id="fd28c-127">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-127">Click **Next**.</span></span>

   ![Select Repository Source 페이지][CL03]

1. <span data-ttu-id="fd28c-129">Hello에 **소스 Git 리포지토리에** 페이지:</span><span class="sxs-lookup"><span data-stu-id="fd28c-129">On hello **Source Git Repository** page:</span></span>

   <span data-ttu-id="fd28c-130">a.</span><span class="sxs-lookup"><span data-stu-id="fd28c-130">a.</span></span> <span data-ttu-id="fd28c-131">**URI**에 대해 `https://github.com/spring-guides/gs-spring-boot-docker.git`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-131">For **URI**, enter `https://github.com/spring-guides/gs-spring-boot-docker.git`.</span></span> <span data-ttu-id="fd28c-132">이 단계는 자동으로 hello 채워야 **호스트** 및 **리포지토리 경로** hello로 필드 값을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-132">This step should automatically populate hello **Host** and **Repository path** fields with hello correct values.</span></span>
   
   <span data-ttu-id="fd28c-133">b.</span><span class="sxs-lookup"><span data-stu-id="fd28c-133">b.</span></span> <span data-ttu-id="fd28c-134">Git 사용자 이름 및 암호 tooenter 있어서는 안 되므로 hello 스프링 부팅 저장소는 public입니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-134">hello Spring Boot repository is public, so you should not have tooenter your Git username and password.</span></span>
   
   <span data-ttu-id="fd28c-135">c.</span><span class="sxs-lookup"><span data-stu-id="fd28c-135">c.</span></span> <span data-ttu-id="fd28c-136">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-136">Click **Next**.</span></span>

   ![Source Git Repository 페이지][CL04]

1. <span data-ttu-id="fd28c-138">Hello에 **분기 선택** 페이지 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-138">On hello **Branch Selection** page, click **Next**.</span></span>

   ![Branch Selection 페이지][CL05]

1. <span data-ttu-id="fd28c-140">Hello에 **로컬 대상** 페이지:</span><span class="sxs-lookup"><span data-stu-id="fd28c-140">On hello **Local Destination** page:</span></span>

   <span data-ttu-id="fd28c-141">a.</span><span class="sxs-lookup"><span data-stu-id="fd28c-141">a.</span></span> <span data-ttu-id="fd28c-142">사용자의 로컬 리포지토리를 넣을 hello 로컬 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-142">Specify hello local folder where you want your local repo.</span></span>
   
   <span data-ttu-id="fd28c-143">b.</span><span class="sxs-lookup"><span data-stu-id="fd28c-143">b.</span></span> <span data-ttu-id="fd28c-144">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-144">Click **Next**.</span></span>

   ![Local Destination 페이지][CL06]

1. <span data-ttu-id="fd28c-146">Hello에 **프로젝트 가져오기 마법사 toouse 선택** 페이지:</span><span class="sxs-lookup"><span data-stu-id="fd28c-146">On hello **Select a wizard toouse for importing projects** page:</span></span>

   <span data-ttu-id="fd28c-147">a.</span><span class="sxs-lookup"><span data-stu-id="fd28c-147">a.</span></span> <span data-ttu-id="fd28c-148">**Import as a general project**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-148">Select **Import as a general project**.</span></span>
   
   <span data-ttu-id="fd28c-149">b.</span><span class="sxs-lookup"><span data-stu-id="fd28c-149">b.</span></span> <span data-ttu-id="fd28c-150">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-150">Click **Next**.</span></span>

   !["프로젝트 가져오기 마법사 toouse 선택" 페이지][CL07]

1. <span data-ttu-id="fd28c-152">Hello에 **가져오기 프로젝트** 페이지:</span><span class="sxs-lookup"><span data-stu-id="fd28c-152">On hello **Import Projects** page:</span></span>

   <span data-ttu-id="fd28c-153">a.</span><span class="sxs-lookup"><span data-stu-id="fd28c-153">a.</span></span> <span data-ttu-id="fd28c-154">프로젝트 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-154">Specify your project name.</span></span>
   
   <span data-ttu-id="fd28c-155">b.</span><span class="sxs-lookup"><span data-stu-id="fd28c-155">b.</span></span> <span data-ttu-id="fd28c-156">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-156">Click **Finish**.</span></span>

   ![Import Projects 페이지][CL08]

1. <span data-ttu-id="fd28c-158">Hello 리포지토리 복제 했습니다. Eclipse에서 나와 hello 파일 중 일부만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-158">When hello repository is cloned successfully, you see all hello files listed in Eclipse.</span></span>

   ![로컬 리포지토리][CL09]

### <a name="create-a-maven-project-from-your-local-repository"></a><span data-ttu-id="fd28c-160">로컬 리포지토리에서 Maven 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="fd28c-160">Create a Maven project from your local repository</span></span>

<span data-ttu-id="fd28c-161">hello 스프링 부팅 Docker 리포지토리가이 자습서에 사용 하 여 완료 된 Maven 프로젝트가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-161">hello Spring Boot Docker repository contains a completed Maven project, which you will use for this tutorial.</span></span> 

1. <span data-ttu-id="fd28c-162">**File** > **Import**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-162">Click **File** > **Import**.</span></span>

   ![가져오기 hello 파일 메뉴 명령][CL01]

1. <span data-ttu-id="fd28c-164">Hello 때 **가져오기** 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-164">When hello **Import** dialog box opens:</span></span>

   <span data-ttu-id="fd28c-165">a.</span><span class="sxs-lookup"><span data-stu-id="fd28c-165">a.</span></span> <span data-ttu-id="fd28c-166">**Maven**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-166">Expand **Maven**.</span></span>
   
   <span data-ttu-id="fd28c-167">b.</span><span class="sxs-lookup"><span data-stu-id="fd28c-167">b.</span></span> <span data-ttu-id="fd28c-168">**Existing Maven Projects**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-168">Select **Existing Maven Projects**.</span></span>
   
   <span data-ttu-id="fd28c-169">c.</span><span class="sxs-lookup"><span data-stu-id="fd28c-169">c.</span></span> <span data-ttu-id="fd28c-170">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-170">Click **Next**.</span></span>

   ![Import 대화 상자][MV01]

1. <span data-ttu-id="fd28c-172">Hello에 **Maven 프로젝트** 페이지:</span><span class="sxs-lookup"><span data-stu-id="fd28c-172">On hello **Maven Projects** page:</span></span>

   <span data-ttu-id="fd28c-173">a.</span><span class="sxs-lookup"><span data-stu-id="fd28c-173">a.</span></span> <span data-ttu-id="fd28c-174">에 대 한 **루트 디렉터리**, hello 지정 **완료** 로컬 리포지토리 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-174">For **Root Directory**, specify hello **complete** folder in your local repository.</span></span>
   
   <span data-ttu-id="fd28c-175">b.</span><span class="sxs-lookup"><span data-stu-id="fd28c-175">b.</span></span> <span data-ttu-id="fd28c-176">Hello 확장 **고급** 섹션을 사용자 지정 이름을 입력 **이름 템플릿**합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-176">Expand hello **Advanced** section, and enter a custom name for **Name template**.</span></span>
   
   <span data-ttu-id="fd28c-177">c.</span><span class="sxs-lookup"><span data-stu-id="fd28c-177">c.</span></span> <span data-ttu-id="fd28c-178">Hello에 대 한 선택 hello 상자 **pom.xml** hello 프로젝트 파일에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-178">Select hello box for hello **pom.xml** file in hello project.</span></span>
   
   <span data-ttu-id="fd28c-179">d.</span><span class="sxs-lookup"><span data-stu-id="fd28c-179">d.</span></span> <span data-ttu-id="fd28c-180">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-180">Click **Finish**.</span></span>

   ![Maven Projects 페이지][MV02]

1. <span data-ttu-id="fd28c-182">Hello Maven 프로젝트를 성공적으로 열면 Eclipse에 나열 된 두 번째 프로젝트를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-182">When hello Maven project is opened successfully, you see a second project listed in Eclipse.</span></span>

   ![로컬 Maven 프로젝트][MV03]

## <a name="build-your-spring-boot-app-by-using-maven"></a><span data-ttu-id="fd28c-184">Maven을 사용하여 Spring Boot 앱 빌드</span><span class="sxs-lookup"><span data-stu-id="fd28c-184">Build your Spring Boot app by using Maven</span></span>

1. <span data-ttu-id="fd28c-185">Hello Eclipse 프로젝트 탐색기에서에서 hello Maven 프로젝트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-185">In hello Eclipse Project Explorer, select hello Maven project.</span></span>

1. <span data-ttu-id="fd28c-186">**Run** > **Run As** > **Maven build**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-186">Click **Run** > **Run As** > **Maven build**.</span></span>

   ![Maven 빌드 명령 toorun][BU01]

1. <span data-ttu-id="fd28c-188">응용 프로그램을 성공적으로 빌드되면 hello 상태가 hello 콘솔 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-188">When your application is successfully built, hello console window shows hello status.</span></span>

   ![성공적인 Maven 빌드][BU02]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="fd28c-190">Docker 컨테이너를 사용 하 여 웹 응용 프로그램 tooAzure 게시</span><span class="sxs-lookup"><span data-stu-id="fd28c-190">Publish your web app tooAzure by using a Docker container</span></span>

1. <span data-ttu-id="fd28c-191">Hello Eclipse 프로젝트 탐색기에서에서 hello Maven 프로젝트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-191">In hello Eclipse Project Explorer, select hello Maven project.</span></span>

1. <span data-ttu-id="fd28c-192">Azure hello 클릭 **게시** 메뉴를 차례로 클릭 **Docker 컨테이너로 게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-192">Click hello Azure **Publish** menu, and then click **Publish as Docker Container**.</span></span>

   ![Docker 컨테이너로 게시 명령][PU01]

1. <span data-ttu-id="fd28c-194">Hello 때 **Azure에서 Docker 컨테이너 배포** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-194">When hello **Deploying Docker Container on Azure** dialog box appears:</span></span>

   <span data-ttu-id="fd28c-195">a.</span><span class="sxs-lookup"><span data-stu-id="fd28c-195">a.</span></span> <span data-ttu-id="fd28c-196">사용자 지정 Docker 이미지 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-196">Enter a custom Docker image name.</span></span>
   
   <span data-ttu-id="fd28c-197">b.</span><span class="sxs-lookup"><span data-stu-id="fd28c-197">b.</span></span> <span data-ttu-id="fd28c-198">에 대 한 **아티팩트 toodeploy**, hello 경로 toohello 지정 **gs-스프링-부팅-docker-0.1.0.jar** 방금 빌드한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-198">For **Artifact toodeploy**, specify hello path toohello **gs-spring-boot-docker-0.1.0.jar** file you just built.</span></span>

   ![Docker 옵션 지정][PU02]

   <span data-ttu-id="fd28c-200">기존의 모든 Docker 호스트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-200">Any existing Docker hosts are displayed.</span></span> 

1. <span data-ttu-id="fd28c-201">Toodeploy tooan 기존 호스트를 선택 하면 toostep 5를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-201">If you choose toodeploy tooan existing host, you can skip toostep 5.</span></span> <span data-ttu-id="fd28c-202">그렇지 않으면 다음 단계 toocreate 호스트 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-202">Otherwise, use hello following steps toocreate a host:</span></span>

   <span data-ttu-id="fd28c-203">a.</span><span class="sxs-lookup"><span data-stu-id="fd28c-203">a.</span></span> <span data-ttu-id="fd28c-204">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-204">Click **Add**.</span></span>

      ![새 Docker 호스트 추가][PU03]

   <span data-ttu-id="fd28c-206">b.</span><span class="sxs-lookup"><span data-stu-id="fd28c-206">b.</span></span> <span data-ttu-id="fd28c-207">Hello 때 **Docker 호스트 만들기** 대화 상자가 표시 됩니다, tooaccept hello 기본값을 선택 하거나 새 Docker 호스트에 대 한 사용자 지정 설정을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-207">When hello **Create Docker Host** dialog box appears, you can choose tooaccept hello defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="fd28c-208">(다양 한 설정, 참조에 대 한 자세한 설명은 hello [IntelliJ 용 Azure 도구 키트 hello를 사용 하 여 Docker 컨테이너와 웹 응용 프로그램을 게시할][Publish Container with Azure Toolkit].) 클릭 **다음** 어떤 설정 toouse 지정 했으면 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-208">(For detailed descriptions of hello various settings, see [Publish a web app as a Docker container by using hello Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings toouse.</span></span>

      ![Docker 호스트 옵션 지정][PU04]

   <span data-ttu-id="fd28c-210">c.</span><span class="sxs-lookup"><span data-stu-id="fd28c-210">c.</span></span> <span data-ttu-id="fd28c-211">Azure 키 자격 증명 모음에서 toouse 기존 로그인 자격 증명을 선택할 수 있습니다 또는 새 Docker에 대 한 로그인 자격 증명 tooenter를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-211">You can choose toouse existing login credentials from an Azure key vault, or you can choose tooenter new Docker login credentials.</span></span> <span data-ttu-id="fd28c-212">옵션을 지정하면 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-212">Click **Finish** when you have specified your options.</span></span>

      ![Docker 호스트 자격 증명 지정][PU05]

1. <span data-ttu-id="fd28c-214">Docker 호스트를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-214">Select your Docker host, and then click **Next**.</span></span>

   ![Docker 호스트 toouse 선택][PU06]

1. <span data-ttu-id="fd28c-216">Hello hello의 마지막 페이지에 **Azure에서 Docker 컨테이너 배포** 대화 상자 hello 다음 옵션을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-216">On hello last page of hello **Deploying Docker Container on Azure** dialog box, specify hello following options:</span></span>

   <span data-ttu-id="fd28c-217">a.</span><span class="sxs-lookup"><span data-stu-id="fd28c-217">a.</span></span> <span data-ttu-id="fd28c-218">Docker 컨테이너를 호스팅할 hello 컨테이너에 대 한 사용자 지정 이름을 toospecify를 선택할 수 있습니다 또는 hello 기본값을 그대로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-218">You can choose toospecify a custom name for hello container that will host your Docker container, or you can accept hello default.</span></span>

   <span data-ttu-id="fd28c-219">b.</span><span class="sxs-lookup"><span data-stu-id="fd28c-219">b.</span></span> <span data-ttu-id="fd28c-220">구문 다음 hello를 사용 하 여 docker 호스트에 대 한 hello TCP 포트를 입력: *[외부 포트]*:*[내부 포트]*합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-220">Enter hello TCP ports for your docker host by using hello following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="fd28c-221">예를 들어 **80:8080** 외부 포트 80 및 hello 기본 내부 스프링 부팅 포트 8080 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-221">For example, **80:8080** specifies an external port of 80 and hello default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="fd28c-222">내부 포트 (예를 들어 파일 편집 하 여 hello application.yml) 사용자 지정을 Azure의 hello 올바른 라우팅 toooccur toospecify hello 포트 번호가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-222">If you have customized your internal port (for example, by editing hello application.yml file), you need toospecify hello port number for hello correct routing toooccur in Azure.</span></span>

   <span data-ttu-id="fd28c-223">c.</span><span class="sxs-lookup"><span data-stu-id="fd28c-223">c.</span></span> <span data-ttu-id="fd28c-224">이러한 옵션을 구성했으면 **Finish**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-224">After you configure these options, click **Finish**.</span></span>

   ![Azure에 Docker 컨테이너 배포][PU07]

1. <span data-ttu-id="fd28c-226">Azure 도구 키트 hello 게시 완료 되 면 hello Azure 활동 로그 표시 **게시 됨** hello 상태에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd28c-226">When hello Azure Toolkit has finished publishing, hello Azure Activity Log displays **Published** for hello status.</span></span>

   ![Docker 호스트를 성공적으로 배포][PU08]

## <a name="next-steps"></a><span data-ttu-id="fd28c-228">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fd28c-228">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL01.png
[CL02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL02.png
[CL03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL09.png

[MV01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV01.png
[MV02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV02.png
[MV03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV03.png

[BU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU02.png

[PU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU02.png
[PU03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU03.png
[PU04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU06.png
[PU07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU07.png
[PU08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU08.png
