---
title: "Eclipse용 Azure 도구 키트를 사용하여 Spring Boot 앱을 Docker 컨테이너로 게시 | Microsoft Docs"
description: "Eclipse용 Azure 도구 키트를 사용하여 Docker 컨테이너로 Microsoft Azure에 웹앱을 게시하는 방법을 알아봅니다."
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
ms.openlocfilehash: fcb60fcfbda26f5f37bfb0edcb01f8737188b6bc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="1f882-103">Eclipse용 Azure 도구 키트를 사용하여 Spring Boot 앱을 Docker 컨테이너로 게시</span><span class="sxs-lookup"><span data-stu-id="1f882-103">Publish a Spring Boot app as a Docker container by using the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="1f882-104">[Spring Framework]는 Java 개발자가 엔터프라이즈 수준의 응용 프로그램을 만드는 데 도움이 되는 오픈 소스 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-104">The [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="1f882-105">해당 플랫폼을 기반으로 하여 빌드되는 인기 있는 프로젝트 중 하나가 [Spring Boot]입니다. 이 프로젝트는 독립 실행형 Java 응용 프로그램을 만드는 간단한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-105">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="1f882-106">[Docker]는 개발자가 컨테이너에서 실행되는 응용 프로그램의 배포, 크기 조정 및 관리를 자동화하는 데 도움이 되는 오픈 소스 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-106">[Docker] is an open-source solution that helps developers automate the deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="1f882-107">이 자습서에서는 Eclipse용 Azure 도구 키트를 사용하여 Microsoft Azure에 Docker 컨테이너로 Spring Boot 응용 프로그램을 배포하는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-107">This tutorial walks you through the steps to deploy a Spring Boot application as a Docker container to Microsoft Azure by using the Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="clone-the-default-spring-boot-docker-repository"></a><span data-ttu-id="1f882-108">기본 Spring Boot Docker 리포지토리 복제</span><span class="sxs-lookup"><span data-stu-id="1f882-108">Clone the default Spring Boot Docker repository</span></span>

### <a name="import-the-public-repository"></a><span data-ttu-id="1f882-109">공용 리포지토리 가져오기</span><span class="sxs-lookup"><span data-stu-id="1f882-109">Import the public repository</span></span>

<span data-ttu-id="1f882-110">다음 단계는 IntelliJ를 사용하여 Spring Boot Docker 리포지토리를 로컬 컴퓨터로 복제하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-110">The following steps walk you through cloning the Spring Boot Docker repository to your local computer by using IntelliJ.</span></span> <span data-ttu-id="1f882-111">명령줄을 사용하려면 [Azure Container Service에서 Linux에 Spring Boot 응용 프로그램 배포][Deploy Spring Boot on Linux in ACS]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f882-111">If you want to use a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].</span></span>

1. <span data-ttu-id="1f882-112">Eclipse를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-112">Open Eclipse.</span></span>

1. <span data-ttu-id="1f882-113">**File** > **Import**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-113">Click **File** > **Import**.</span></span>

   ![File Import 메뉴][CL01]

1. <span data-ttu-id="1f882-115">**Import** 대화 상자가 열리면:</span><span class="sxs-lookup"><span data-stu-id="1f882-115">When the **Import** dialog box opens:</span></span>

   <span data-ttu-id="1f882-116">a.</span><span class="sxs-lookup"><span data-stu-id="1f882-116">a.</span></span> <span data-ttu-id="1f882-117">**Git**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-117">Expand **Git**.</span></span>

   <span data-ttu-id="1f882-118">b.</span><span class="sxs-lookup"><span data-stu-id="1f882-118">b.</span></span> <span data-ttu-id="1f882-119">**Projects from Git**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-119">Select **Projects from Git**.</span></span>
   
   <span data-ttu-id="1f882-120">c.</span><span class="sxs-lookup"><span data-stu-id="1f882-120">c.</span></span> <span data-ttu-id="1f882-121">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-121">Click **Next**.</span></span>

   ![Import 대화 상자][CL02]

1. <span data-ttu-id="1f882-123">**Select Repository Source** 페이지에서:</span><span class="sxs-lookup"><span data-stu-id="1f882-123">On the **Select Repository Source** page:</span></span>

   <span data-ttu-id="1f882-124">a.</span><span class="sxs-lookup"><span data-stu-id="1f882-124">a.</span></span> <span data-ttu-id="1f882-125">**Clone URI**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-125">Select **Clone URI**.</span></span>
   
   <span data-ttu-id="1f882-126">b.</span><span class="sxs-lookup"><span data-stu-id="1f882-126">b.</span></span> <span data-ttu-id="1f882-127">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-127">Click **Next**.</span></span>

   ![Select Repository Source 페이지][CL03]

1. <span data-ttu-id="1f882-129">**Source Git Repository** 페이지에서:</span><span class="sxs-lookup"><span data-stu-id="1f882-129">On the **Source Git Repository** page:</span></span>

   <span data-ttu-id="1f882-130">a.</span><span class="sxs-lookup"><span data-stu-id="1f882-130">a.</span></span> <span data-ttu-id="1f882-131">**URI**에 대해 `https://github.com/spring-guides/gs-spring-boot-docker.git`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-131">For **URI**, enter `https://github.com/spring-guides/gs-spring-boot-docker.git`.</span></span> <span data-ttu-id="1f882-132">이 단계에서는 **Host** 및 **Repository path** 필드에 올바른 값을 자동으로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-132">This step should automatically populate the **Host** and **Repository path** fields with the correct values.</span></span>
   
   <span data-ttu-id="1f882-133">b.</span><span class="sxs-lookup"><span data-stu-id="1f882-133">b.</span></span> <span data-ttu-id="1f882-134">Spring Boot 리포지토리는 공개되어 있으므로 Git 사용자 이름과 암호를 입력하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-134">The Spring Boot repository is public, so you should not have to enter your Git username and password.</span></span>
   
   <span data-ttu-id="1f882-135">c.</span><span class="sxs-lookup"><span data-stu-id="1f882-135">c.</span></span> <span data-ttu-id="1f882-136">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-136">Click **Next**.</span></span>

   ![Source Git Repository 페이지][CL04]

1. <span data-ttu-id="1f882-138">**Branch Selection** 페이지에서 **Next**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-138">On the **Branch Selection** page, click **Next**.</span></span>

   ![Branch Selection 페이지][CL05]

1. <span data-ttu-id="1f882-140">**Local Destination** 페이지에서:</span><span class="sxs-lookup"><span data-stu-id="1f882-140">On the **Local Destination** page:</span></span>

   <span data-ttu-id="1f882-141">a.</span><span class="sxs-lookup"><span data-stu-id="1f882-141">a.</span></span> <span data-ttu-id="1f882-142">로컬 리포지토리를 저장할 로컬 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-142">Specify the local folder where you want your local repo.</span></span>
   
   <span data-ttu-id="1f882-143">b.</span><span class="sxs-lookup"><span data-stu-id="1f882-143">b.</span></span> <span data-ttu-id="1f882-144">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-144">Click **Next**.</span></span>

   ![Local Destination 페이지][CL06]

1. <span data-ttu-id="1f882-146">**Select a wizard to use for importing projects** 페이지에서:</span><span class="sxs-lookup"><span data-stu-id="1f882-146">On the **Select a wizard to use for importing projects** page:</span></span>

   <span data-ttu-id="1f882-147">a.</span><span class="sxs-lookup"><span data-stu-id="1f882-147">a.</span></span> <span data-ttu-id="1f882-148">**Import as a general project**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-148">Select **Import as a general project**.</span></span>
   
   <span data-ttu-id="1f882-149">b.</span><span class="sxs-lookup"><span data-stu-id="1f882-149">b.</span></span> <span data-ttu-id="1f882-150">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-150">Click **Next**.</span></span>

   !["Select a wizard to use for importing projects" 페이지][CL07]

1. <span data-ttu-id="1f882-152">**Import Projects** 페이지에서:</span><span class="sxs-lookup"><span data-stu-id="1f882-152">On the **Import Projects** page:</span></span>

   <span data-ttu-id="1f882-153">a.</span><span class="sxs-lookup"><span data-stu-id="1f882-153">a.</span></span> <span data-ttu-id="1f882-154">프로젝트 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-154">Specify your project name.</span></span>
   
   <span data-ttu-id="1f882-155">b.</span><span class="sxs-lookup"><span data-stu-id="1f882-155">b.</span></span> <span data-ttu-id="1f882-156">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-156">Click **Finish**.</span></span>

   ![Import Projects 페이지][CL08]

1. <span data-ttu-id="1f882-158">리포지토리가 성공적으로 복제되면 Eclipse에 나열된 모든 파일을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-158">When the repository is cloned successfully, you see all the files listed in Eclipse.</span></span>

   ![로컬 리포지토리][CL09]

### <a name="create-a-maven-project-from-your-local-repository"></a><span data-ttu-id="1f882-160">로컬 리포지토리에서 Maven 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="1f882-160">Create a Maven project from your local repository</span></span>

<span data-ttu-id="1f882-161">Spring Boot Docker 리포지토리는 이 자습서에서 사용할 완성된 Maven 프로젝트를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-161">The Spring Boot Docker repository contains a completed Maven project, which you will use for this tutorial.</span></span> 

1. <span data-ttu-id="1f882-162">**File** > **Import**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-162">Click **File** > **Import**.</span></span>

   ![File 메뉴의 Import 명령][CL01]

1. <span data-ttu-id="1f882-164">**Import** 대화 상자가 열리면:</span><span class="sxs-lookup"><span data-stu-id="1f882-164">When the **Import** dialog box opens:</span></span>

   <span data-ttu-id="1f882-165">a.</span><span class="sxs-lookup"><span data-stu-id="1f882-165">a.</span></span> <span data-ttu-id="1f882-166">**Maven**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-166">Expand **Maven**.</span></span>
   
   <span data-ttu-id="1f882-167">b.</span><span class="sxs-lookup"><span data-stu-id="1f882-167">b.</span></span> <span data-ttu-id="1f882-168">**Existing Maven Projects**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-168">Select **Existing Maven Projects**.</span></span>
   
   <span data-ttu-id="1f882-169">c.</span><span class="sxs-lookup"><span data-stu-id="1f882-169">c.</span></span> <span data-ttu-id="1f882-170">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-170">Click **Next**.</span></span>

   ![Import 대화 상자][MV01]

1. <span data-ttu-id="1f882-172">**Maven Projects** 페이지에서:</span><span class="sxs-lookup"><span data-stu-id="1f882-172">On the **Maven Projects** page:</span></span>

   <span data-ttu-id="1f882-173">a.</span><span class="sxs-lookup"><span data-stu-id="1f882-173">a.</span></span> <span data-ttu-id="1f882-174">**Root Directory**에 대해 로컬 리포지토리의 **전체** 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-174">For **Root Directory**, specify the **complete** folder in your local repository.</span></span>
   
   <span data-ttu-id="1f882-175">b.</span><span class="sxs-lookup"><span data-stu-id="1f882-175">b.</span></span> <span data-ttu-id="1f882-176">**Advanced** 섹션을 펼치고 **Name template**에 사용자 지정 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-176">Expand the **Advanced** section, and enter a custom name for **Name template**.</span></span>
   
   <span data-ttu-id="1f882-177">c.</span><span class="sxs-lookup"><span data-stu-id="1f882-177">c.</span></span> <span data-ttu-id="1f882-178">프로젝트에서 **pom.xml** 파일에 대한 상자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-178">Select the box for the **pom.xml** file in the project.</span></span>
   
   <span data-ttu-id="1f882-179">ㄹ.</span><span class="sxs-lookup"><span data-stu-id="1f882-179">d.</span></span> <span data-ttu-id="1f882-180">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-180">Click **Finish**.</span></span>

   ![Maven Projects 페이지][MV02]

1. <span data-ttu-id="1f882-182">Maven 프로젝트가 성공적으로 열리면 Eclipse에 나열된 두 번째 프로젝트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-182">When the Maven project is opened successfully, you see a second project listed in Eclipse.</span></span>

   ![로컬 Maven 프로젝트][MV03]

## <a name="build-your-spring-boot-app-by-using-maven"></a><span data-ttu-id="1f882-184">Maven을 사용하여 Spring Boot 앱 빌드</span><span class="sxs-lookup"><span data-stu-id="1f882-184">Build your Spring Boot app by using Maven</span></span>

1. <span data-ttu-id="1f882-185">Eclipse Project Explorer에서 Maven 프로젝트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-185">In the Eclipse Project Explorer, select the Maven project.</span></span>

1. <span data-ttu-id="1f882-186">**Run** > **Run As** > **Maven build**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-186">Click **Run** > **Run As** > **Maven build**.</span></span>

   ![Maven build로 실행하는 명령][BU01]

1. <span data-ttu-id="1f882-188">응용 프로그램이 성공적으로 빌드되면 콘솔 창에 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-188">When your application is successfully built, the console window shows the status.</span></span>

   ![성공적인 Maven 빌드][BU02]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="1f882-190">Docker 컨테이너를 사용하여 Azure에 웹앱 게시</span><span class="sxs-lookup"><span data-stu-id="1f882-190">Publish your web app to Azure by using a Docker container</span></span>

1. <span data-ttu-id="1f882-191">Eclipse Project Explorer에서 Maven 프로젝트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-191">In the Eclipse Project Explorer, select the Maven project.</span></span>

1. <span data-ttu-id="1f882-192">Azure **Publish** 메뉴를 클릭한 다음 **Publish as Docker Container**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-192">Click the Azure **Publish** menu, and then click **Publish as Docker Container**.</span></span>

   ![Publish as Docker Container 명령][PU01]

1. <span data-ttu-id="1f882-194">**Deploying Docker Container on Azure** 대화 상자가 표시되면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-194">When the **Deploying Docker Container on Azure** dialog box appears:</span></span>

   <span data-ttu-id="1f882-195">a.</span><span class="sxs-lookup"><span data-stu-id="1f882-195">a.</span></span> <span data-ttu-id="1f882-196">사용자 지정 Docker 이미지 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-196">Enter a custom Docker image name.</span></span>
   
   <span data-ttu-id="1f882-197">b.</span><span class="sxs-lookup"><span data-stu-id="1f882-197">b.</span></span> <span data-ttu-id="1f882-198">**Artifact to deploy**에 대해 방금 빌드한 **gs-spring-boot-docker-0.1.0.jar** 파일의 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-198">For **Artifact to deploy**, specify the path to the **gs-spring-boot-docker-0.1.0.jar** file you just built.</span></span>

   ![Docker 옵션 지정][PU02]

   <span data-ttu-id="1f882-200">기존의 모든 Docker 호스트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-200">Any existing Docker hosts are displayed.</span></span> 

1. <span data-ttu-id="1f882-201">기존 호스트에 배포하려는 경우 5단계로 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-201">If you choose to deploy to an existing host, you can skip to step 5.</span></span> <span data-ttu-id="1f882-202">그렇지 않으면 다음 단계에 따라 호스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-202">Otherwise, use the following steps to create a host:</span></span>

   <span data-ttu-id="1f882-203">a.</span><span class="sxs-lookup"><span data-stu-id="1f882-203">a.</span></span> <span data-ttu-id="1f882-204">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-204">Click **Add**.</span></span>

      ![새 Docker 호스트 추가][PU03]

   <span data-ttu-id="1f882-206">b.</span><span class="sxs-lookup"><span data-stu-id="1f882-206">b.</span></span> <span data-ttu-id="1f882-207">**Create Docker Host** 대화 상자가 표시되면 기본값을 그대로 허용하도록 선택하거나 새 Docker 호스트에 대한 사용자 지정 설정을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-207">When the **Create Docker Host** dialog box appears, you can choose to accept the defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="1f882-208">다양한 설정에 대한 자세한 설명은 [IntelliJ용 Azure 도구 키트를 사용하여 웹앱을 Docker 컨테이너로 게시][Publish Container with Azure Toolkit]를 참조하세요. 사용할 설정을 지정하면 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-208">(For detailed descriptions of the various settings, see [Publish a web app as a Docker container by using the Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings to use.</span></span>

      ![Docker 호스트 옵션 지정][PU04]

   <span data-ttu-id="1f882-210">c.</span><span class="sxs-lookup"><span data-stu-id="1f882-210">c.</span></span> <span data-ttu-id="1f882-211">Azure Key Vault에서 기존 로그인 자격 증명을 사용하도록 선택하거나 새 Docker 로그인 자격 증명을 입력하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-211">You can choose to use existing login credentials from an Azure key vault, or you can choose to enter new Docker login credentials.</span></span> <span data-ttu-id="1f882-212">옵션을 지정하면 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-212">Click **Finish** when you have specified your options.</span></span>

      ![Docker 호스트 자격 증명 지정][PU05]

1. <span data-ttu-id="1f882-214">Docker 호스트를 선택하고 **Next**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-214">Select your Docker host, and then click **Next**.</span></span>

   ![사용할 Docker 호스트 선택][PU06]

1. <span data-ttu-id="1f882-216">**Deploying Docker Container on Azure** 대화 상자의 마지막 페이지에서 다음 옵션을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-216">On the last page of the **Deploying Docker Container on Azure** dialog box, specify the following options:</span></span>

   <span data-ttu-id="1f882-217">a.</span><span class="sxs-lookup"><span data-stu-id="1f882-217">a.</span></span> <span data-ttu-id="1f882-218">Docker 컨테이너를 호스팅할 컨테이너에 대한 사용자 지정 이름을 지정하도록 선택하거나 기본값을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-218">You can choose to specify a custom name for the container that will host your Docker container, or you can accept the default.</span></span>

   <span data-ttu-id="1f882-219">b.</span><span class="sxs-lookup"><span data-stu-id="1f882-219">b.</span></span> <span data-ttu-id="1f882-220">*[외부 포트]*:*[내부 포트]* 구문을 사용하여 Docker 호스트에 대한 TCP 포트를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-220">Enter the TCP ports for your docker host by using the following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="1f882-221">예를 들어 **80:8080**은 80 외부 포트 및 8080 기본 내부 Spring Boot 포트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-221">For example, **80:8080** specifies an external port of 80 and the default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="1f882-222">내부 포트를 사용자 지정한 경우(예: application.yml 파일 편집) Azure에서 올바른 라우팅을 수행할 포트 번호를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-222">If you have customized your internal port (for example, by editing the application.yml file), you need to specify the port number for the correct routing to occur in Azure.</span></span>

   <span data-ttu-id="1f882-223">c.</span><span class="sxs-lookup"><span data-stu-id="1f882-223">c.</span></span> <span data-ttu-id="1f882-224">이러한 옵션을 구성했으면 **Finish**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-224">After you configure these options, click **Finish**.</span></span>

   ![Azure에 Docker 컨테이너 배포][PU07]

1. <span data-ttu-id="1f882-226">Azure 도구 키트에서 게시를 완료하면 Azure 활동 로그에 **게시됨** 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f882-226">When the Azure Toolkit has finished publishing, the Azure Activity Log displays **Published** for the status.</span></span>

   ![Docker 호스트를 성공적으로 배포][PU08]

## <a name="next-steps"></a><span data-ttu-id="1f882-228">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1f882-228">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
<span data-ttu-id="1f882-229">[Docker]: https://www.docker.com/</span><span class="sxs-lookup"><span data-stu-id="1f882-229">[Docker]: https://www.docker.com/</span></span>
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
<span data-ttu-id="1f882-230">[Spring Boot]: http://projects.spring.io/spring-boot/</span><span class="sxs-lookup"><span data-stu-id="1f882-230">[Spring Boot]: http://projects.spring.io/spring-boot/</span></span>
<span data-ttu-id="1f882-231">[Spring Framework]: https://spring.io/</span><span class="sxs-lookup"><span data-stu-id="1f882-231">[Spring Framework]: https://spring.io/</span></span>

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
