---
title: "Eclipse 용 플러그 인 서비스 패브릭 aaaAzure | Microsoft Docs"
description: "시작 서비스 패브릭 플러그 인 hello Eclipse 용 하세요."
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
ms.openlocfilehash: 4ba5a28a6282387249a2bd4e62314e891ff04162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-plug-in-for-eclipse-java-application-development"></a><span data-ttu-id="ec0f3-103">Eclipse Java 응용 프로그램 배포를 위한 Azure Service Fabric 플러그 인</span><span class="sxs-lookup"><span data-stu-id="ec0f3-103">Service Fabric plug-in for Eclipse Java application development</span></span>
<span data-ttu-id="ec0f3-104">Eclipse를 사용 하면 가장 널리 사용 되는 hello 중 하나인 Java 개발자를 위한 개발 환경 (Ide)를 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-104">Eclipse is one of hello most widely used integrated development environments (IDEs) for Java developers.</span></span> <span data-ttu-id="ec0f3-105">이 문서에서는 설명 어떻게 tooset Azure 서비스 패브릭는 Eclipse 개발 환경 toowork 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-105">In this article, we describe how tooset up your Eclipse development environment toowork with Azure Service Fabric.</span></span> <span data-ttu-id="ec0f3-106">Tooinstall hello 플러그 인을 서비스 패브릭 서비스 패브릭 응용 프로그램을 만들고 배포 방법 서비스 패브릭 응용 프로그램 tooa 로컬 또는 원격 서비스 패브릭 클러스터 Eclipse Neon에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-106">Learn how tooinstall hello Service Fabric plug-in, create a Service Fabric application, and deploy your Service Fabric application tooa local or remote Service Fabric cluster in Eclipse Neon.</span></span>

## <a name="install-or-update-hello-service-fabric-plug-in-in-eclipse-neon"></a><span data-ttu-id="ec0f3-107">Hello 서비스 패브릭 Eclipse Neon에 플러그 인을 설치 또는</span><span class="sxs-lookup"><span data-stu-id="ec0f3-107">Install or update hello Service Fabric plug-in in Eclipse Neon</span></span>
<span data-ttu-id="ec0f3-108">Eclipse에서 Service Fabric 플러그 인을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-108">You can install a Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="ec0f3-109">플러그 인 hello hello 프로세스의 구축 및 Java 서비스 배포를 간소화 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-109">hello plug-in can help simplify hello process of building and deploying Java services.</span></span>

1.  <span data-ttu-id="ec0f3-110">Eclipse Neon의 최신 버전 hello와 hello Buildship의 최신 버전에 있는지 확인 (1.0.17 또는 이후 버전) 설치:</span><span class="sxs-lookup"><span data-stu-id="ec0f3-110">Ensure that you have hello latest version of Eclipse Neon and hello latest version of Buildship (1.0.17 or a later version) installed:</span></span>
    -   <span data-ttu-id="ec0f3-111">toocheck hello 버전의 Eclipse Neon에 설치 된 구성 요소를 너무 이동**도움말** > **설치 세부 정보**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-111">toocheck hello versions of installed components, in Eclipse Neon, go too**Help** > **Installation Details**.</span></span>
    -   <span data-ttu-id="ec0f3-112">tooupdate Buildship, 참조 [Eclipse Buildship: Eclipse 플러그 인에 대 한 Gradle][buildship-update]합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-112">tooupdate Buildship, see [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].</span></span>
    -   <span data-ttu-id="ec0f3-113">에 대 한 toocheck 고 Eclipse Neon에 대 한 업데이트 설치 실행을 너무**도움말** > **업데이트 확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-113">toocheck for and install updates for Eclipse Neon, go too**Help** > **Check for Updates**.</span></span>

2.  <span data-ttu-id="ec0f3-114">서비스 패브릭 Eclipse Neon에 플러그 인 tooinstall hello 너무 이동**도움말** > **새 소프트웨어 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-114">tooinstall hello Service Fabric plug-in, in Eclipse Neon, go too**Help** > **Install New Software**.</span></span>
  1.    <span data-ttu-id="ec0f3-115">Hello에 **작업할** 상자에 입력 **http://dl.microsoft.com/eclipse**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-115">In hello **Work with** box, enter **http://dl.microsoft.com/eclipse**.</span></span>
  2.    <span data-ttu-id="ec0f3-116">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-116">Click **Add**.</span></span>

         ![Eclipse Neon용 Service Fabric 플러그 인][sf-eclipse-plugin-install]
  3.    <span data-ttu-id="ec0f3-118">Hello 서비스 패브릭 플러그 인을 선택한 다음 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-118">Select hello Service Fabric plug-in, and then click **Next**.</span></span>
  4.    <span data-ttu-id="ec0f3-119">Hello 설치 단계를 완료 하 고 hello Microsoft 소프트웨어 사용 조건에 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-119">Complete hello installation steps, and then accept hello Microsoft Software License Terms.</span></span>

<span data-ttu-id="ec0f3-120">서비스 패브릭 플러그 인 설치 hello 이미 있는 경우 hello 최신 버전이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-120">If you already have hello Service Fabric plug-in installed, make sure that you have hello latest version.</span></span> <span data-ttu-id="ec0f3-121">사용 가능한 업데이트에 대 한 toocheck 너무 이동**도움말** > **설치 세부 정보**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-121">toocheck for available updates, go too**Help** > **Installation Details**.</span></span> <span data-ttu-id="ec0f3-122">설치 된 플러그 인 hello 목록에서 서비스 패브릭 선택한 다음 클릭 **업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-122">In hello list of installed plug-ins, select Service Fabric, and then click **Update**.</span></span> <span data-ttu-id="ec0f3-123">사용 가능한 업데이트가 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-123">Available updates will be installed.</span></span>

> [!NOTE]
> <span data-ttu-id="ec0f3-124">설치 하거나 업데이트할 hello 플러그 인 서비스 패브릭 느린 경우 tooan Eclipse 설정을 인해 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-124">If installing or updating hello Service Fabric plug-in is slow, it might be due tooan Eclipse setting.</span></span> <span data-ttu-id="ec0f3-125">Eclipse는 Eclipse 인스턴스와 함께 등록 된 모든 변경 내용 tooupdate 사이트 메타 데이터를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-125">Eclipse collects metadata on all changes tooupdate sites that are registered with your Eclipse instance.</span></span> <span data-ttu-id="ec0f3-126">서비스 패브릭 플러그 인 업데이트를 설치 및 확인 하는 hello 프로세스를 toospeed 너무 이동**사용 가능한 소프트웨어 사이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-126">toospeed up hello process of checking for and installing a Service Fabric plug-in update, go too**Available Software Sites**.</span></span> <span data-ttu-id="ec0f3-127">Hello hello toohello 서비스 패브릭 플러그 인 (http://dl.microsoft.com/eclipse/azure/servicefabric) 위치를 가리키는 하나를 제외한 모든 사이트에 대 한 확인란의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-127">Clear hello check boxes for all sites except for hello one that points toohello Service Fabric plug-in location (http://dl.microsoft.com/eclipse/azure/servicefabric).</span></span>

## <a name="create-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="ec0f3-128">Eclipse에서 Service Fabric 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="ec0f3-128">Create a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="ec0f3-129">너무 Eclipse Neon 이동**파일** > **새로** > **다른**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-129">In Eclipse Neon, go too**File** > **New** > **Other**.</span></span> <span data-ttu-id="ec0f3-130">**Service Fabric 프로젝트**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-130">Select  **Service Fabric Project**, and then click **Next**.</span></span>

    ![Service Fabric 새 프로젝트 페이지 1][create-application/p1]

2.  <span data-ttu-id="ec0f3-132">프로젝트의 이름을 입력하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-132">Enter a name for your project, and then click **Next**.</span></span>

    ![Service Fabric 새 프로젝트 페이지 2][create-application/p2]

3.  <span data-ttu-id="ec0f3-134">Hello 템플릿 목록에서 선택 **서비스 템플릿을**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-134">In hello list of templates, select **Service Template**.</span></span> <span data-ttu-id="ec0f3-135">서비스 템플릿 유형(행위자, 상태 비저장, 컨테이너 또는 게스트 이진 파일)을 선택한 다음 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-135">Select your service template type (Actor, Stateless, Container, or Guest Binary), and then click **Next**.</span></span>

    ![Service Fabric 새 프로젝트 페이지 3][create-application/p3]

4.  <span data-ttu-id="ec0f3-137">Hello 서비스 이름을 입력 하 고 세부 정보를 처리 한 다음 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-137">Enter hello service name and service details, and then click **Finish**.</span></span>

    ![Service Fabric 새 프로젝트 페이지 4][create-application/p4]

5. <span data-ttu-id="ec0f3-139">Hello 첫 번째 서비스 패브릭 프로젝트를 만들 때 **연결 된 큐브 뷰 열기** 대화 상자를 클릭 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-139">When you create your first Service Fabric project, in hello **Open Associated Perspective** dialog box, click **Yes**.</span></span>

    ![Service Fabric 새 프로젝트 페이지 5][create-application/p5]

6.  <span data-ttu-id="ec0f3-141">새 프로젝트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-141">Your new project looks like this:</span></span>

    ![Service Fabric 새 프로젝트 페이지 6][create-application/p6]

## <a name="build-and-deploy-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="ec0f3-143">Eclipse에서 Service Fabric 응용 프로그램 빌드 및 배포</span><span class="sxs-lookup"><span data-stu-id="ec0f3-143">Build and deploy a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="ec0f3-144">새 Service Fabric 응용 프로그램을 마우스 오른쪽 단추로 클릭한 다음 **Service Fabric**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-144">Right-click your new Service Fabric application, and then select **Service Fabric**.</span></span>

    ![Service Fabric 마우스 오른쪽 클릭 메뉴][publish/RightClick]

2. <span data-ttu-id="ec0f3-146">Hello 하위 메뉴에서 원하는 hello 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-146">In hello submenu, select hello option you want:</span></span>
    -   <span data-ttu-id="ec0f3-147">toobuild hello 응용 프로그램을 삭제 하지 않은 채 클릭 **응용 프로그램 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-147">toobuild hello application without cleaning, click **Build Application**.</span></span>
    -   <span data-ttu-id="ec0f3-148">toodo hello 응용 프로그램의 클린 빌드를 클릭 하 여 **다시 작성 하는 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-148">toodo a clean build of hello application, click **Rebuild Application**.</span></span>
    -   <span data-ttu-id="ec0f3-149">빌드된 아티팩트의 tooclean hello 응용 프로그램 클릭 **클린 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-149">tooclean hello application of built artifacts, click **Clean Application**.</span></span>

3.  <span data-ttu-id="ec0f3-150">이 메뉴에서 응용 프로그램을 배포, 배포 취소 및 게시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-150">From this menu, you also can deploy, undeploy, and publish your application:</span></span>
    -   <span data-ttu-id="ec0f3-151">toodeploy tooyour 로컬 클러스터 클릭 **응용 프로그램 배포**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-151">toodeploy tooyour local cluster, click **Deploy Application**.</span></span>
    -   <span data-ttu-id="ec0f3-152">Hello에 **응용 프로그램 게시** 대화 상자에서 게시 프로필을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-152">In hello **Publish Application** dialog box, select a publish profile:</span></span>
        -  <span data-ttu-id="ec0f3-153">**Local.json**</span><span class="sxs-lookup"><span data-stu-id="ec0f3-153">**Local.json**</span></span>
        -  <span data-ttu-id="ec0f3-154">**Cloud.json**</span><span class="sxs-lookup"><span data-stu-id="ec0f3-154">**Cloud.json**</span></span>

     <span data-ttu-id="ec0f3-155">이러한 개체 JSON (JavaScript Notation) 파일은 필요한 tooconnect tooyour 로컬 또는 클라우드 (Azure) 클러스터는 (예: 연결 끝점 및 보안 정보) 정보를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-155">These JavaScript Object Notation (JSON) files store information (such as connection endpoints and security information) that is required tooconnect tooyour local or cloud (Azure) cluster.</span></span>

  ![Service Fabric 게시 메뉴][publish/Publish]

<span data-ttu-id="ec0f3-157">대체 방식으로 toodeploy 서비스 패브릭 응용 프로그램은 Eclipse를 사용 하 여 구성은 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-157">An alternate way toodeploy your Service Fabric application is by using Eclipse run configurations.</span></span>

  1.    <span data-ttu-id="ec0f3-158">너무 이동**실행** > **실행 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-158">Go too**Run** > **Run Configurations**.</span></span>
  2.    <span data-ttu-id="ec0f3-159">아래 **Gradle 프로젝트**선택, hello **ServiceFabricDeployer** 구성을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-159">Under **Gradle Project**, select hello **ServiceFabricDeployer** run configuration.</span></span>
  3.    <span data-ttu-id="ec0f3-160">Hello에 hello 오른쪽 창에서 **인수** 탭에 대 한 **publishProfile**선택, **로컬** 또는 **클라우드**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-160">In hello right pane, on hello **Arguments** tab, for **publishProfile**, select **local** or **cloud**.</span></span>  <span data-ttu-id="ec0f3-161">hello 기본값은 **로컬**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-161">hello default is **local**.</span></span> <span data-ttu-id="ec0f3-162">원격 toodeploy tooa 또는 클라우드 클러스터 **클라우드**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-162">toodeploy tooa remote or cloud cluster, select **cloud**.</span></span>
  4.    <span data-ttu-id="ec0f3-163">hello에 적절 한 정보 hello 채워지도록 tooensure 게시 프로필에서 편집 **Local.json** 또는 **Cloud.json** 필요에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-163">tooensure that hello proper information is populated in hello publish profiles, edit **Local.json** or **Cloud.json** as needed.</span></span> <span data-ttu-id="ec0f3-164">끝점 세부 정보 및 보안 자격 증명을 추가하거나 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-164">You can add or update endpoint details and security credentials.</span></span>
  5.    <span data-ttu-id="ec0f3-165">되도록 **작업 디렉터리** toodeploy 원하는 toohello 응용 프로그램을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-165">Ensure that **Working Directory** points toohello application you want toodeploy.</span></span> <span data-ttu-id="ec0f3-166">toochange hello 응용 프로그램을 hello 클릭 **작업 영역** 단추를 선택한 다음 원하는 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-166">toochange hello application, click hello **Workspace** button, and then select hello application you want.</span></span>
  6.    <span data-ttu-id="ec0f3-167">**적용**을 클릭한 다음 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-167">Click **Apply**, and then click **Run**.</span></span>

<span data-ttu-id="ec0f3-168">몇 분 내로 응용 프로그램을 빌드하고 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-168">Your application builds and deploys within a few moments.</span></span> <span data-ttu-id="ec0f3-169">서비스 패브릭 탐색기에서 hello 배포 상태를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-169">You can monitor hello deployment status in Service Fabric Explorer.</span></span>  

## <a name="add-a-service-fabric-service-tooyour-service-fabric-application"></a><span data-ttu-id="ec0f3-170">서비스 패브릭 서비스 tooyour 서비스 패브릭 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="ec0f3-170">Add a Service Fabric service tooyour Service Fabric application</span></span>

<span data-ttu-id="ec0f3-171">다음 단계 tooadd 서비스 패브릭 서비스 tooan 기존 서비스 패브릭 응용 프로그램을 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-171">tooadd a Service Fabric service tooan existing Service Fabric application, do hello following steps:</span></span>

1.  <span data-ttu-id="ec0f3-172">마우스 오른쪽 단추로 클릭 hello 프로젝트 원하는 tooadd 서비스를 선택한 다음 클릭 **서비스 패브릭**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-172">Right-click hello project you want tooadd a service to, and then click **Service Fabric**.</span></span>

    ![Service Fabric 서비스 추가 페이지 1][add-service/p1]

2.  <span data-ttu-id="ec0f3-174">클릭 **서비스 패브릭 서비스 추가**, 서비스 toohello 프로젝트 단계 tooadd의 전체 hello 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-174">Click **Add Service Fabric Service**, and complete hello set of steps tooadd a service toohello project.</span></span>
3.  <span data-ttu-id="ec0f3-175">선택 hello 서비스 템플릿을 tooadd tooyour 프로젝트를 선택 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-175">Select hello service template you want tooadd tooyour project, and then click **Next**.</span></span>

    ![Service Fabric 서비스 추가 페이지 2][add-service/p2]

4.  <span data-ttu-id="ec0f3-177">Hello 서비스 이름 (및 필요에 따라 기타 정보)을 입력 하 고 hello 클릭 **서비스 추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-177">Enter hello service name (and other details, as needed), and then click hello **Add Service** button.</span></span>  

    ![Service Fabric 서비스 추가 페이지 3][add-service/p3]

5.  <span data-ttu-id="ec0f3-179">Hello 서비스를 추가한 후 프로젝트를 수행 하는 비슷한 toohello 전체 프로젝트 구조에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-179">After hello service is added, your overall project structure looks similar toohello following project:</span></span>

    ![Service Fabric 서비스 추가 페이지 4][add-service/p4]

## <a name="edit-manifest-versions-of-your-service-fabric-java-application"></a><span data-ttu-id="ec0f3-181">Service Fabric Java 응용 프로그램의 매니페스트 버전 편집</span><span class="sxs-lookup"><span data-stu-id="ec0f3-181">Edit Manifest versions of your Service Fabric Java application</span></span>

<span data-ttu-id="ec0f3-182">tooedit 매니페스트 버전 hello 프로젝트를 마우스 오른쪽 단추로 클릭, 너무 이동**서비스 패브릭** 선택 **매니페스트 버전 편집...**  hello 메뉴 드롭다운에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-182">tooedit manifest versions, right click on hello project, go too**Service Fabric** and select **Edit Manifest Versions...** from hello menu dropdown.</span></span> <span data-ttu-id="ec0f3-183">Hello 마법사에서 서비스 매니페스트를 매니페스트, 응용 프로그램에 대 한 hello 매니페스트 버전 hello에 및 버전을 업데이트할 수 있습니다 **코드**, **Config** 및 **데이터** 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-183">In hello wizard, you can update hello manifest versions for application manifest, service manifest and hello versions for **Code**, **Config** and **Data** packages.</span></span>

<span data-ttu-id="ec0f3-184">Hello 옵션을 선택 하는 경우 **응용 프로그램 및 서비스 버전을 자동으로 업데이트** 다음 버전을 업데이트 하 고, 다음 hello 매니페스트 버전 자동으로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-184">If you check hello option **Automatically update application and service versions** and then update a version, then hello manifest versions will be automatically updated.</span></span> <span data-ttu-id="ec0f3-185">예 toogive을 먼저 선택 하면 hello 확인란, 업데이트 hello 버전을 **코드** 0.0.0에서 버전 too0.0.1 고를 클릭 **마침**, 다음 서비스 매니페스트 버전 및 응용 프로그램 매니페스트 버전을 자동으로 업데이트 된 too0.0.1 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-185">toogive an example, you first select hello check-box, then update hello version of **Code** version from 0.0.0 too0.0.1 and click on **Finish**, then service manifest version and application manifest version will be automatically updated too0.0.1.</span></span>

## <a name="upgrade-your-service-fabric-java-application"></a><span data-ttu-id="ec0f3-186">Service Fabric Java 응용 프로그램 업그레이드</span><span class="sxs-lookup"><span data-stu-id="ec0f3-186">Upgrade your Service Fabric Java application</span></span>

<span data-ttu-id="ec0f3-187">업그레이드 시나리오에 대 한 hello 만든 예를 들어 **App1** hello 서비스 패브릭 Eclipse에서 플러그 인을 사용 하 여 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-187">For an upgrade scenario, say you created hello **App1** project by using hello Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="ec0f3-188">배포 플러그 인 toocreate hello를 사용 하 여 이라는 응용 프로그램 **패브릭: / App1Application**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-188">You deployed it by using hello plug-in toocreate an application named **fabric:/App1Application**.</span></span> <span data-ttu-id="ec0f3-189">hello 응용 프로그램 유형은 **App1AppicationType**, 및 hello 응용 프로그램 버전은 1.0입니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-189">hello application type is **App1AppicationType**, and hello application version is 1.0.</span></span> <span data-ttu-id="ec0f3-190">이제 원하는 tooupgrade 응용 프로그램 가용성을 해치지 않고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-190">Now, you want tooupgrade your application without interrupting availability.</span></span>

<span data-ttu-id="ec0f3-191">첫째, tooyour 응용 프로그램을 변경 하 고 수정 하는 hello 서비스를 다시 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-191">First, make any changes tooyour application, and then rebuild hello modified service.</span></span> <span data-ttu-id="ec0f3-192">업데이트 hello hello 서비스 (및 코드, 구성, 또는 데이터에 관련)에 대 한 hello 업데이트 버전으로 서비스의 매니페스트 파일 (ServiceManifest.xml)을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-192">Update hello modified service’s manifest file (ServiceManifest.xml) with hello updated versions for hello service (and Code, Config, or Data, as relevant).</span></span> <span data-ttu-id="ec0f3-193">또한 hello 응용 프로그램에 대 한 버전 번호를 업데이트 하는 hello hello 응용 프로그램 매니페스트 (ApplicationManifest.xml)를 수정 하 고 수정 된 서비스 hello.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-193">Also, modify hello application’s manifest (ApplicationManifest.xml) with hello updated version number for hello application and hello modified service.</span></span>  

<span data-ttu-id="ec0f3-194">tooupgrade Neon Eclipse를 사용 하 여 응용 프로그램 실행된 중복 구성 프로필을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-194">tooupgrade your application by using Eclipse Neon, you can create a duplicate run configuration profile.</span></span> <span data-ttu-id="ec0f3-195">그런 다음 tooupgrade 사용 필요에 따라 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-195">Then, use it tooupgrade your application as needed.</span></span>

1.  <span data-ttu-id="ec0f3-196">너무 이동**실행** > **실행 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-196">Go too**Run** > **Run Configurations**.</span></span> <span data-ttu-id="ec0f3-197">Hello 왼쪽된 창에서 hello toohello 왼쪽의 작은 화살표를 클릭 **Gradle 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-197">In hello left pane, click hello small arrow toohello left of **Gradle Project**.</span></span>
2.  <span data-ttu-id="ec0f3-198">**ServiceFabricDeployer**를 마우스 오른쪽 단추로 클릭하고 **중복**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-198">Right-click **ServiceFabricDeployer**, and then select **Duplicate**.</span></span> <span data-ttu-id="ec0f3-199">예를 들어 **ServiceFabricUpgrader**와 같이 이 구성의 새 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-199">Enter a new name for this configuration, for example, **ServiceFabricUpgrader**.</span></span>
3.  <span data-ttu-id="ec0f3-200">Hello에 hello 오른쪽 패널에서 **인수** 탭으로 변경 **-Pconfig '배포' =** 너무**-Pconfig '업그레이드' =**, 클릭 하 고 **적용**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-200">In hello right panel, on hello **Arguments** tab, change **-Pconfig='deploy'** too**-Pconfig='upgrade'**, and then click **Apply**.</span></span>

<span data-ttu-id="ec0f3-201">이 프로세스를 만들고 실행된 구성 프로필 저장 응용 프로그램 시간 tooupgrade 든 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-201">This process creates and saves a run configuration profile you can use at any time tooupgrade your application.</span></span> <span data-ttu-id="ec0f3-202">또한 hello 응용 프로그램 매니페스트 파일에서 hello 최신 업데이트 된 응용 프로그램 종류 버전을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-202">It also gets hello latest updated application type version from hello application manifest file.</span></span>

<span data-ttu-id="ec0f3-203">응용 프로그램 업그레이드: hello 몇 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-203">hello application upgrade takes a few minutes.</span></span> <span data-ttu-id="ec0f3-204">서비스 패브릭 탐색기에 응용 프로그램 업그레이드 hello를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-204">You can monitor hello application upgrade in Service Fabric Explorer.</span></span>

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a><span data-ttu-id="ec0f3-205">Maven 함께 사용 하는 기존 서비스 패브릭 Java 응용 프로그램 toobe 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="ec0f3-205">Migrating old Service Fabric Java applications toobe used with Maven</span></span>
<span data-ttu-id="ec0f3-206">서비스 패브릭 Java SDK tooMaven 리포지토리에서 최근 서비스 패브릭 Java 라이브러리 전환 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-206">We have recently moved Service Fabric Java libraries from Service Fabric Java SDK tooMaven repository.</span></span> <span data-ttu-id="ec0f3-207">기존 서비스 패브릭 상태 비저장 또는 hello 서비스 패브릭 Java SDK를 사용 하는 행위자 Java 응용 프로그램 hello 새 응용 프로그램 Eclipse를 사용 하 여 생성 됩니다 (Maven으로 수 toowork 됩니다)는 최신 버전에 업데이트 된 프로젝트를 생성 하는 동안 업데이트할 수 있습니다. 이전 버전에서 toouse hello 서비스 패브릭 Java Maven에서 종속성입니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-207">While hello new applications you generate using Eclipse, will generate latest updated projects (which will be able toowork with Maven), you can update your existing Service Fabric stateless or actor Java applications, which were using hello Service Fabric Java SDK earlier, toouse hello Service Fabric Java dependencies from Maven.</span></span> <span data-ttu-id="ec0f3-208">언급 된 hello 단계를 따르십시오 [여기](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure Maven으로 오래 된 응용 프로그램이 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec0f3-208">Please follow hello steps mentioned [here](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure your older application works with Maven.</span></span>

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
