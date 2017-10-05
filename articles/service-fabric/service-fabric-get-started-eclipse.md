---
title: "Eclipse용 Azure Service Fabric 플러그 인 | Microsoft Docs"
description: "Eclipse용 Azure Service Fabric 플러그 인을 시작합니다."
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/21/2016
ms.author: saysa
ms.openlocfilehash: 98c1b99972b9ad7a396d72b98e727286f6822e42
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="service-fabric-plug-in-for-eclipse-java-application-development"></a><span data-ttu-id="d8b3d-103">Eclipse Java 응용 프로그램 배포를 위한 Azure Service Fabric 플러그 인</span><span class="sxs-lookup"><span data-stu-id="d8b3d-103">Service Fabric plug-in for Eclipse Java application development</span></span>
<span data-ttu-id="d8b3d-104">Eclipse는 가장 널리 사용되는 Java 개발자를 위한 IDE(통합 개발 환경) 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-104">Eclipse is one of the most widely used integrated development environments (IDEs) for Java developers.</span></span> <span data-ttu-id="d8b3d-105">이 문서에서는 Azure Service Fabric 작업을 수행하기 위해 Eclipse 개발 환경을 설정하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-105">In this article, we describe how to set up your Eclipse development environment to work with Azure Service Fabric.</span></span> <span data-ttu-id="d8b3d-106">Service Fabric 플러그 인을 설치하고 Service Fabric 응용 프로그램을 만들며 Service Fabric 응용 프로그램을 Eclipse Neon의 로컬 또는 원격 Service Fabric 클러스터에 배포하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-106">Learn how to install the Service Fabric plug-in, create a Service Fabric application, and deploy your Service Fabric application to a local or remote Service Fabric cluster in Eclipse Neon.</span></span>

## <a name="install-or-update-the-service-fabric-plug-in-in-eclipse-neon"></a><span data-ttu-id="d8b3d-107">Eclipse Neon에서 Service Fabric 플러그 인 설치 또는 업데이트</span><span class="sxs-lookup"><span data-stu-id="d8b3d-107">Install or update the Service Fabric plug-in in Eclipse Neon</span></span>
<span data-ttu-id="d8b3d-108">Eclipse에서 Service Fabric 플러그 인을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-108">You can install a Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="d8b3d-109">플러그 인은 Java 서비스를 빌드하고 배포하는 프로세스를 간소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-109">The plug-in can help simplify the process of building and deploying Java services.</span></span>

1.  <span data-ttu-id="d8b3d-110">최신 버전의 Eclipse Neon 및 최신 버전의 Buildship(1.0.17 이상 버전)을 설치했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-110">Ensure that you have the latest version of Eclipse Neon and the latest version of Buildship (1.0.17 or a later version) installed:</span></span>
    -   <span data-ttu-id="d8b3d-111">설치된 구성 요소의 버전을 확인하려면 Eclipse Neon에서 **도움말** > **설치 세부 정보**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-111">To check the versions of installed components, in Eclipse Neon, go to **Help** > **Installation Details**.</span></span>
    -   <span data-ttu-id="d8b3d-112">Buildship을 업데이트하려면 [Eclipse Buildship: Gradle용 Eclipse 플러그 인][buildship-update]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-112">To update Buildship, see [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].</span></span>
    -   <span data-ttu-id="d8b3d-113">Eclipse Neon에 대한 업데이트를 확인하고 설치하려면 **도움말** > **업데이트 확인**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-113">To check for and install updates for Eclipse Neon, go to **Help** > **Check for Updates**.</span></span>

2.  <span data-ttu-id="d8b3d-114">Service Fabric 플러그 인을 설치하려면 Eclipse Neon에서 **도움말** > **새 소프트웨어 설치**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-114">To install the Service Fabric plug-in, in Eclipse Neon, go to **Help** > **Install New Software**.</span></span>
  1.    <span data-ttu-id="d8b3d-115">**Work with**(사용할 플러그인) 상자에 **http://dl.microsoft.com/eclipse**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-115">In the **Work with** box, enter **http://dl.microsoft.com/eclipse**.</span></span>
  2.    <span data-ttu-id="d8b3d-116">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-116">Click **Add**.</span></span>

         ![Eclipse Neon용 Service Fabric 플러그 인][sf-eclipse-plugin-install]
  3.    <span data-ttu-id="d8b3d-118">Service Fabric 플러그 인을 선택한 다음 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-118">Select the Service Fabric plug-in, and then click **Next**.</span></span>
  4.    <span data-ttu-id="d8b3d-119">설치 단계를 완료한 다음 Microsoft 소프트웨어 사용 조건에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-119">Complete the installation steps, and then accept the Microsoft Software License Terms.</span></span>

<span data-ttu-id="d8b3d-120">Service Fabric 플러그 인이 이미 설치된 경우 최신 버전인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-120">If you already have the Service Fabric plug-in installed, make sure that you have the latest version.</span></span> <span data-ttu-id="d8b3d-121">사용 가능한 업데이트를 확인하려면 **도움말** > **설치 세부 정보**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-121">To check for available updates, go to **Help** > **Installation Details**.</span></span> <span data-ttu-id="d8b3d-122">설치된 플러그 인 목록에서 Service Fabric을 선택하고 **업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-122">In the list of installed plug-ins, select Service Fabric, and then click **Update**.</span></span> <span data-ttu-id="d8b3d-123">사용 가능한 업데이트가 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-123">Available updates will be installed.</span></span>

> [!NOTE]
> <span data-ttu-id="d8b3d-124">Service Fabric 플러그 인 설치 또는 업데이트가 느려지는 경우 Eclipse 설정 때문일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-124">If installing or updating the Service Fabric plug-in is slow, it might be due to an Eclipse setting.</span></span> <span data-ttu-id="d8b3d-125">Eclipse는 Eclipse 인스턴스에 등록되어 있는 사이트를 업데이트하는 모든 변경 내용에 대한 메타데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-125">Eclipse collects metadata on all changes to update sites that are registered with your Eclipse instance.</span></span> <span data-ttu-id="d8b3d-126">Service Fabric 플러그 인 업데이트를 확인하고 설치하는 프로세스 의 속도를 촉진하려면 **사용 가능한 소프트웨어 사이트**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-126">To speed up the process of checking for and installing a Service Fabric plug-in update, go to **Available Software Sites**.</span></span> <span data-ttu-id="d8b3d-127">Service Fabric 플러그 인 위치(http://dl.microsoft.com/eclipse/azure/servicefabric)를 가리키는 확인란을 제외하고 모든 사이트에 대한 확인란의 선택을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-127">Clear the check boxes for all sites except for the one that points to the Service Fabric plug-in location (http://dl.microsoft.com/eclipse/azure/servicefabric).</span></span>

## <a name="create-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="d8b3d-128">Eclipse에서 Service Fabric 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="d8b3d-128">Create a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="d8b3d-129">Eclipse Neon에서 **파일** > **새로 만들기** > **기타**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-129">In Eclipse Neon, go to **File** > **New** > **Other**.</span></span> <span data-ttu-id="d8b3d-130">**Service Fabric 프로젝트**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-130">Select  **Service Fabric Project**, and then click **Next**.</span></span>

    ![Service Fabric 새 프로젝트 페이지 1][create-application/p1]

2.  <span data-ttu-id="d8b3d-132">프로젝트의 이름을 입력하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-132">Enter a name for your project, and then click **Next**.</span></span>

    ![Service Fabric 새 프로젝트 페이지 2][create-application/p2]

3.  <span data-ttu-id="d8b3d-134">템플릿 목록에서 **서비스 템플릿**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-134">In the list of templates, select **Service Template**.</span></span> <span data-ttu-id="d8b3d-135">서비스 템플릿 유형(행위자, 상태 비저장, 컨테이너 또는 게스트 이진 파일)을 선택한 다음 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-135">Select your service template type (Actor, Stateless, Container, or Guest Binary), and then click **Next**.</span></span>

    ![Service Fabric 새 프로젝트 페이지 3][create-application/p3]

4.  <span data-ttu-id="d8b3d-137">서비스 이름 및 서비스 세부 정보를 입력한 다음 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-137">Enter the service name and service details, and then click **Finish**.</span></span>

    ![Service Fabric 새 프로젝트 페이지 4][create-application/p4]

5. <span data-ttu-id="d8b3d-139">첫 번째 Service Fabric 프로젝트를 만들 경우 **연결된 큐브 뷰 열기** 대화 상자에서 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-139">When you create your first Service Fabric project, in the **Open Associated Perspective** dialog box, click **Yes**.</span></span>

    ![Service Fabric 새 프로젝트 페이지 5][create-application/p5]

6.  <span data-ttu-id="d8b3d-141">새 프로젝트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-141">Your new project looks like this:</span></span>

    ![Service Fabric 새 프로젝트 페이지 6][create-application/p6]

## <a name="build-and-deploy-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="d8b3d-143">Eclipse에서 Service Fabric 응용 프로그램 빌드 및 배포</span><span class="sxs-lookup"><span data-stu-id="d8b3d-143">Build and deploy a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="d8b3d-144">새 Service Fabric 응용 프로그램을 마우스 오른쪽 단추로 클릭한 다음 **Service Fabric**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-144">Right-click your new Service Fabric application, and then select **Service Fabric**.</span></span>

    ![Service Fabric 마우스 오른쪽 클릭 메뉴][publish/RightClick]

2. <span data-ttu-id="d8b3d-146">하위 메뉴에서 원하는 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-146">In the submenu, select the option you want:</span></span>
    -   <span data-ttu-id="d8b3d-147">정리하지 않고 응용 프로그램을 빌드하려면 **응용 프로그램 빌드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-147">To build the application without cleaning, click **Build Application**.</span></span>
    -   <span data-ttu-id="d8b3d-148">응용 프로그램의 정리-빌드를 수행하려면 **응용 프로그램 다시 빌드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-148">To do a clean build of the application, click **Rebuild Application**.</span></span>
    -   <span data-ttu-id="d8b3d-149">빌드한 아티팩트의 응용 프로그램을 정리하려면 **응용 프로그램 정리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-149">To clean the application of built artifacts, click **Clean Application**.</span></span>

3.  <span data-ttu-id="d8b3d-150">이 메뉴에서 응용 프로그램을 배포, 배포 취소 및 게시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-150">From this menu, you also can deploy, undeploy, and publish your application:</span></span>
    -   <span data-ttu-id="d8b3d-151">로컬 클러스터에 배포하려면 **응용 프로그램 배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-151">To deploy to your local cluster, click **Deploy Application**.</span></span>
    -   <span data-ttu-id="d8b3d-152">**응용 프로그램 게시** 대화 상자에서 게시 프로필을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-152">In the **Publish Application** dialog box, select a publish profile:</span></span>
        -  <span data-ttu-id="d8b3d-153">**Local.json**</span><span class="sxs-lookup"><span data-stu-id="d8b3d-153">**Local.json**</span></span>
        -  <span data-ttu-id="d8b3d-154">**Cloud.json**</span><span class="sxs-lookup"><span data-stu-id="d8b3d-154">**Cloud.json**</span></span>

     <span data-ttu-id="d8b3d-155">이러한 JSON(JavaScript Object Notation) 파일은 로컬 또는 클라우드 (Azure) 클러스터에 연결하는 데 필요한 정보(예: 연결 끝점 및 보안 정보)를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-155">These JavaScript Object Notation (JSON) files store information (such as connection endpoints and security information) that is required to connect to your local or cloud (Azure) cluster.</span></span>

  ![Service Fabric 게시 메뉴][publish/Publish]

<span data-ttu-id="d8b3d-157">Service Fabric 응용 프로그램을 배포할 수 있는 다른 방법은 Eclipse 실행 구성을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-157">An alternate way to deploy your Service Fabric application is by using Eclipse run configurations.</span></span>

  1.    <span data-ttu-id="d8b3d-158">**실행** > **실행 구성**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-158">Go to **Run** > **Run Configurations**.</span></span>
  2.    <span data-ttu-id="d8b3d-159">**등급 프로젝트** 아래에서 **ServiceFabricDeployer** 실행 구성을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-159">Under **Gradle Project**, select the **ServiceFabricDeployer** run configuration.</span></span>
  3.    <span data-ttu-id="d8b3d-160">오른쪽 창의 **인수** 탭 아래에서 **publishProfile**에 **로컬** 또는 **클라우드**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-160">In the right pane, on the **Arguments** tab, for **publishProfile**, select **local** or **cloud**.</span></span>  <span data-ttu-id="d8b3d-161">기본값은 **로컬**입니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-161">The default is **local**.</span></span> <span data-ttu-id="d8b3d-162">원격 또는 클라우드 클러스터에 배포하려면 **클라우드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-162">To deploy to a remote or cloud cluster, select **cloud**.</span></span>
  4.    <span data-ttu-id="d8b3d-163">게시 프로필에서 적절한 정보가 채워졌는지 확인하려면 필요에 따라 **Local.json** 또는 **Cloud.json**을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-163">To ensure that the proper information is populated in the publish profiles, edit **Local.json** or **Cloud.json** as needed.</span></span> <span data-ttu-id="d8b3d-164">끝점 세부 정보 및 보안 자격 증명을 추가하거나 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-164">You can add or update endpoint details and security credentials.</span></span>
  5.    <span data-ttu-id="d8b3d-165">**작업 디렉터리**가 배포하려는 응용 프로그램을 가리키도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-165">Ensure that **Working Directory** points to the application you want to deploy.</span></span> <span data-ttu-id="d8b3d-166">응용 프로그램을 변경하려면 **작업 영역** 단추를 클릭한 다음 원하는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-166">To change the application, click the **Workspace** button, and then select the application you want.</span></span>
  6.    <span data-ttu-id="d8b3d-167">**적용**을 클릭한 다음 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-167">Click **Apply**, and then click **Run**.</span></span>

<span data-ttu-id="d8b3d-168">몇 분 내로 응용 프로그램을 빌드하고 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-168">Your application builds and deploys within a few moments.</span></span> <span data-ttu-id="d8b3d-169">Service Fabric Explorer에서 배포 상태를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-169">You can monitor the deployment status in Service Fabric Explorer.</span></span>  

## <a name="add-a-service-fabric-service-to-your-service-fabric-application"></a><span data-ttu-id="d8b3d-170">Service Fabric 응용 프로그램에 Service Fabric 서비스 추가</span><span class="sxs-lookup"><span data-stu-id="d8b3d-170">Add a Service Fabric service to your Service Fabric application</span></span>

<span data-ttu-id="d8b3d-171">Service Fabric 서비스를 기존 Service Fabric 응용 프로그램에 추가하려면 다음 단계에 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-171">To add a Service Fabric service to an existing Service Fabric application, do the following steps:</span></span>

1.  <span data-ttu-id="d8b3d-172">서비스를 추가하려는 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **Service Fabric**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-172">Right-click the project you want to add a service to, and then click **Service Fabric**.</span></span>

    ![Service Fabric 서비스 추가 페이지 1][add-service/p1]

2.  <span data-ttu-id="d8b3d-174">**Service Fabric 서비스 추가**를 클릭하고 서비스 프로젝트에 추가하는 일련의 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-174">Click **Add Service Fabric Service**, and complete the set of steps to add a service to the project.</span></span>
3.  <span data-ttu-id="d8b3d-175">프로젝트에 추가할 서비스 템플릿을 선택한 다음 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-175">Select the service template you want to add to your project, and then click **Next**.</span></span>

    ![Service Fabric 서비스 추가 페이지 2][add-service/p2]

4.  <span data-ttu-id="d8b3d-177">서비스 이름(및 필요에 따라 기타 세부 정보)를 입력한 다음 **서비스 추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-177">Enter the service name (and other details, as needed), and then click the **Add Service** button.</span></span>  

    ![Service Fabric 서비스 추가 페이지 3][add-service/p3]

5.  <span data-ttu-id="d8b3d-179">서비스를 추가하면 전체 프로젝트 구조가 다음 프로젝트와 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-179">After the service is added, your overall project structure looks similar to the following project:</span></span>

    ![Service Fabric 서비스 추가 페이지 4][add-service/p4]

## <a name="edit-manifest-versions-of-your-service-fabric-java-application"></a><span data-ttu-id="d8b3d-181">Service Fabric Java 응용 프로그램의 매니페스트 버전 편집</span><span class="sxs-lookup"><span data-stu-id="d8b3d-181">Edit Manifest versions of your Service Fabric Java application</span></span>

<span data-ttu-id="d8b3d-182">매니페스트 버전을 편집하려면 프로젝트를 클릭하고 **Service Fabric**으로 이동하여 드롭다운 메뉴에서 **매니페스트 버전 편집...**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-182">To edit manifest versions, right click on the project, go to **Service Fabric** and select **Edit Manifest Versions...** from the menu dropdown.</span></span> <span data-ttu-id="d8b3d-183">마법사에서 응용 프로그램 매니페스트, 서비스 매니페스트의 매니페스트 버전 및 **코드**, **구성** 및 **데이터** 패키지의 버전을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-183">In the wizard, you can update the manifest versions for application manifest, service manifest and the versions for **Code**, **Config** and **Data** packages.</span></span>

<span data-ttu-id="d8b3d-184">**응용 프로그램 및 서비스 버전 자동 업데이트** 옵션을 확인한 다음 버전을 업데이트하면 매니페스트 버전이 자동으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-184">If you check the option **Automatically update application and service versions** and then update a version, then the manifest versions will be automatically updated.</span></span> <span data-ttu-id="d8b3d-185">예를 들어 확인란을 먼저 선택한 다음 **코드** 버전을 0.0.0에서 0.0.1로 업데이트하고 **마침**을 클릭하면 서비스 매니페스트 버전 및 응용 프로그램 매니페스트 버전이 0.0.1로 자동 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-185">To give an example, you first select the check-box, then update the version of **Code** version from 0.0.0 to 0.0.1 and click on **Finish**, then service manifest version and application manifest version will be automatically updated to 0.0.1.</span></span>

## <a name="upgrade-your-service-fabric-java-application"></a><span data-ttu-id="d8b3d-186">Service Fabric Java 응용 프로그램 업그레이드</span><span class="sxs-lookup"><span data-stu-id="d8b3d-186">Upgrade your Service Fabric Java application</span></span>

<span data-ttu-id="d8b3d-187">업그레이드 시나리오의 경우 Eclipse에서 Service Fabric 플러그 인을 사용하여 **App1** 프로젝트를 만들었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-187">For an upgrade scenario, say you created the **App1** project by using the Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="d8b3d-188">**fabric:/App1Application**라는 응용 프로그램을 만드는 플러그 인을 사용하여 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-188">You deployed it by using the plug-in to create an application named **fabric:/App1Application**.</span></span> <span data-ttu-id="d8b3d-189">응용 프로그램 유형은 **App1AppicationType**이고 응용 프로그램 버전은 1.0입니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-189">The application type is **App1AppicationType**, and the application version is 1.0.</span></span> <span data-ttu-id="d8b3d-190">이제 가용성을 해치지 않고 응용 프로그램을 업그레이드하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-190">Now, you want to upgrade your application without interrupting availability.</span></span>

<span data-ttu-id="d8b3d-191">먼저 응용 프로그램을 변경하고 수정된 서비스를 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-191">First, make any changes to your application, and then rebuild the modified service.</span></span> <span data-ttu-id="d8b3d-192">수정된 서비스의 매니페스트 파일(ServiceManifest.xml)을 업데이트된 버전의 서비스(및 관련된 코드, 구성 또는 데이터)로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-192">Update the modified service’s manifest file (ServiceManifest.xml) with the updated versions for the service (and Code, Config, or Data, as relevant).</span></span> <span data-ttu-id="d8b3d-193">또한 응용 프로그램의 매니페스트(ApplicationManifest.xml)를 응용 프로그램에 대한 업데이트된 버전 번호와 수정된 서비스로 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-193">Also, modify the application’s manifest (ApplicationManifest.xml) with the updated version number for the application and the modified service.</span></span>  

<span data-ttu-id="d8b3d-194">Eclipse Neon을 사용하여 응용 프로그램을 업그레이드하려면 중복 실행 구성 프로필을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-194">To upgrade your application by using Eclipse Neon, you can create a duplicate run configuration profile.</span></span> <span data-ttu-id="d8b3d-195">그런 다음 필요에 따라 응용 프로그램을 업그레이드하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-195">Then, use it to upgrade your application as needed.</span></span>

1.  <span data-ttu-id="d8b3d-196">**실행** > **실행 구성**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-196">Go to **Run** > **Run Configurations**.</span></span> <span data-ttu-id="d8b3d-197">왼쪽 창에서 **등급 프로젝트**의 왼쪽에 있는 작은 화살표를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-197">In the left pane, click the small arrow to the left of **Gradle Project**.</span></span>
2.  <span data-ttu-id="d8b3d-198">**ServiceFabricDeployer**를 마우스 오른쪽 단추로 클릭하고 **중복**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-198">Right-click **ServiceFabricDeployer**, and then select **Duplicate**.</span></span> <span data-ttu-id="d8b3d-199">예를 들어 **ServiceFabricUpgrader**와 같이 이 구성의 새 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-199">Enter a new name for this configuration, for example, **ServiceFabricUpgrader**.</span></span>
3.  <span data-ttu-id="d8b3d-200">오른쪽 패널의 **인수** 탭에서 **-Pconfig='deploy'**를 **-Pconfig='upgrade'**로 변경한 다음 **적용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-200">In the right panel, on the **Arguments** tab, change **-Pconfig='deploy'** to **-Pconfig='upgrade'**, and then click **Apply**.</span></span>

<span data-ttu-id="d8b3d-201">이 프로세스는 응용 프로그램을 업그레이드하기 위해 언제든지 사용할 수 있는 실행 구성 프로필을 만들고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-201">This process creates and saves a run configuration profile you can use at any time to upgrade your application.</span></span> <span data-ttu-id="d8b3d-202">그러면 응용 프로그램 매니페스트 파일에서 최신 업데이트된 응용 프로그램 유형 버전을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-202">It also gets the latest updated application type version from the application manifest file.</span></span>

<span data-ttu-id="d8b3d-203">응용 프로그램 업그레이드에는 몇 분 정도가 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-203">The application upgrade takes a few minutes.</span></span> <span data-ttu-id="d8b3d-204">Service Fabric Explorer에서 응용 프로그램 업그레이드를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-204">You can monitor the application upgrade in Service Fabric Explorer.</span></span>

## <a name="migrating-old-service-fabric-java-applications-to-be-used-with-maven"></a><span data-ttu-id="d8b3d-205">이전의 Service Fabric Java 응용 프로그램을 마이그레이션하여 Maven에서 사용</span><span class="sxs-lookup"><span data-stu-id="d8b3d-205">Migrating old Service Fabric Java applications to be used with Maven</span></span>
<span data-ttu-id="d8b3d-206">최근에 Service Fabric Java 라이브러리를 Service Fabric Java SDK에서 Maven 리포지토리로 이동했습니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-206">We have recently moved Service Fabric Java libraries from Service Fabric Java SDK to Maven repository.</span></span> <span data-ttu-id="d8b3d-207">Eclipse를 사용하여 생성한 새 응용 프로그램은 최신 업데이트된 프로젝트를 생성하는 반면(Maven에서 작업할 수 있음) Maven에서 Service Fabric Java 종속성을 사용하기 위해 이전에 Service Fabric Java SDK를 사용했던 기존 Service Fabric 상태 비저장 또는 작업자 Java 응용 프로그램을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-207">While the new applications you generate using Eclipse, will generate latest updated projects (which will be able to work with Maven), you can update your existing Service Fabric stateless or actor Java applications, which were using the Service Fabric Java SDK earlier, to use the Service Fabric Java dependencies from Maven.</span></span> <span data-ttu-id="d8b3d-208">[여기](service-fabric-migrate-old-javaapp-to-use-maven.md)에서 언급한 단계에 따라 Maven에서 이전의 응용 프로그램이 작동되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b3d-208">Please follow the steps mentioned [here](service-fabric-migrate-old-javaapp-to-use-maven.md) to ensure your older application works with Maven.</span></span>

<!-- Images -->

[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-eclipse/service-fabric-eclipse-plugin.png

[create-application/p1]:./media/service-fabric-get-started-eclipse/create-application/p1.png
[create-application/p2]:./media/service-fabric-get-started-eclipse/create-application/p2.png
[create-application/p3]:./media/service-fabric-get-started-eclipse/create-application/p3.png
[create-application/p4]:./media/service-fabric-get-started-eclipse/create-application/p4.png
[create-application/p5]:./media/service-fabric-get-started-eclipse/create-application/p5.png
[create-application/p6]:./media/service-fabric-get-started-eclipse/create-application/p6.png

[publish/Publish]: ./media/service-fabric-get-started-eclipse/publish/Publish.png
[publish/RightClick]: ./media/service-fabric-get-started-eclipse/publish/RightClick.png

[add-service/p1]: ./media/service-fabric-get-started-eclipse/add-service/p1.png
[add-service/p2]: ./media/service-fabric-get-started-eclipse/add-service/p2.png
[add-service/p3]: ./media/service-fabric-get-started-eclipse/add-service/p3.png
[add-service/p4]: ./media/service-fabric-get-started-eclipse/add-service/p4.png

<!-- Links -->
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
