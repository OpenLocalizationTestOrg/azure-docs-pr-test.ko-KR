---
title: "aaaManage Visual Studio에서 응용 프로그램 | Microsoft Docs"
description: "Visual Studio toocreate를 사용 하 여, 패키지를 개발, 배포 및 서비스 패브릭 응용 프로그램 및 서비스를 디버그 합니다."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: c317cb7e-7eae-466e-ba41-6aa2518be5cf
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: b2d5803d85e4f9645dcbece33a2208bc0955498d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-visual-studio-toosimplify-writing-and-managing-your-service-fabric-applications"></a><span data-ttu-id="28832-103">Visual Studio toosimplify 작성 하 고 서비스 패브릭 응용 프로그램 관리를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="28832-103">Use Visual Studio toosimplify writing and managing your Service Fabric applications</span></span>
<span data-ttu-id="28832-104">Visual Studio를 통해 Azure 서비스 패브릭 응용 프로그램 및 서비스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28832-104">You can manage your Azure Service Fabric applications and services through Visual Studio.</span></span> <span data-ttu-id="28832-105">한 후 [개발 환경 설정](service-fabric-get-started.md), Visual Studio toocreate 서비스 패브릭 응용 프로그램을 사용 하, 서비스 또는 패키지의 경우 레지스터를 추가 하 고 로컬 개발 클러스터에 응용 프로그램을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28832-105">Once you've [set up your development environment](service-fabric-get-started.md), you can use Visual Studio toocreate Service Fabric applications, add services, or package, register, and deploy applications in your local development cluster.</span></span>

## <a name="deploy-your-service-fabric-application"></a><span data-ttu-id="28832-106">서비스 패브릭 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="28832-106">Deploy your Service Fabric application</span></span>
<span data-ttu-id="28832-107">응용 프로그램 배포를 기본적으로 하나의 간단한 작업에 단계를 수행 하는 hello를 결합 합니다.</span><span class="sxs-lookup"><span data-stu-id="28832-107">By default, deploying an application combines hello following steps into one simple operation:</span></span>

1. <span data-ttu-id="28832-108">Hello 응용 프로그램 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="28832-108">Creating hello application package</span></span>
2. <span data-ttu-id="28832-109">Hello 응용 프로그램 패키지 toohello 이미지 저장소를 업로드 하는 중</span><span class="sxs-lookup"><span data-stu-id="28832-109">Uploading hello application package toohello image store</span></span>
3. <span data-ttu-id="28832-110">Hello 응용 프로그램 종류를 등록 하는 중</span><span class="sxs-lookup"><span data-stu-id="28832-110">Registering hello application type</span></span>
4. <span data-ttu-id="28832-111">실행 중인 모든 응용 프로그램 인스턴스 제거</span><span class="sxs-lookup"><span data-stu-id="28832-111">Removing any running application instances</span></span>
5. <span data-ttu-id="28832-112">응용 프로그램 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="28832-112">Creating an application instance</span></span>

<span data-ttu-id="28832-113">Visual Studio에서 키를 누르면 **F5** 응용 프로그램을 배포 하 고 hello 디버거 tooall 응용 프로그램 인스턴스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="28832-113">In Visual Studio, pressing **F5** deploys your application and attach hello debugger tooall application instances.</span></span> <span data-ttu-id="28832-114">사용할 수 있습니다 **Ctrl + f 5** toodeploy 디버깅 또는 있습니다 하지 않는 응용 프로그램 로컬 tooa 하거나 hello를 사용 하 여 원격 클러스터 프로필 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28832-114">You can use **Ctrl+F5** toodeploy an application without debugging, or you can publish tooa local or remote cluster by using hello publish profile.</span></span> <span data-ttu-id="28832-115">자세한 내용은 참조 [Visual Studio를 사용 하 여 응용 프로그램 tooa 원격 클러스터 게시](service-fabric-publish-app-remote-cluster.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="28832-115">For more information, see [Publish an application tooa remote cluster by using Visual Studio](service-fabric-publish-app-remote-cluster.md).</span></span>

### <a name="application-debug-mode"></a><span data-ttu-id="28832-116">응용 프로그램 디버그 모드</span><span class="sxs-lookup"><span data-stu-id="28832-116">Application Debug Mode</span></span>
<span data-ttu-id="28832-117">Visual Studio 라는 속성을 제공 **응용 프로그램 디버그 모드**, 원하는 디버깅의 일부로 Visual Studio toohandle 응용 프로그램 배포를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="28832-117">Visual Studio provide a property called **Application Debug Mode**, which controls how you want Visual Studios toohandle Application deployment as part of debugging.</span></span>

#### <a name="tooset-hello-application-debug-mode-property"></a><span data-ttu-id="28832-118">tooset hello 응용 프로그램 디버그 모드 속성</span><span class="sxs-lookup"><span data-stu-id="28832-118">tooset hello Application Debug Mode property</span></span>
1. <span data-ttu-id="28832-119">Hello 서비스 패브릭 응용 프로그램 프로젝트의 (*.sfproj)에서 바로 가기 메뉴를 선택 **속성** (또는 키를 눌러 hello **F4** 키)입니다.</span><span class="sxs-lookup"><span data-stu-id="28832-119">On hello Service Fabric application project's (*.sfproj) shortcut menu, choose **Properties** (or press hello **F4** key).</span></span>
2. <span data-ttu-id="28832-120">Hello에 **속성** 창, 집합 hello **응용 프로그램 디버그 모드** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="28832-120">In hello **Properties** window, set hello **Application Debug Mode** property.</span></span>

![응용 프로그램 디버그 모드 속성 설정][debugmodeproperty]

#### <a name="application-debug-modes"></a><span data-ttu-id="28832-122">응용 프로그램 디버그 모드</span><span class="sxs-lookup"><span data-stu-id="28832-122">Application Debug Modes</span></span>

1. <span data-ttu-id="28832-123">**응용 프로그램 새로 고침** 이 모드는 tooquickly 변경을 활성화 하 고 디버그 코드 및 정적 웹 파일을 디버깅 하는 동안 편집을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="28832-123">**Refresh Application** This mode enables you tooquickly change and debug your code and supports editing static web files while debugging.</span></span> <span data-ttu-id="28832-124">이 모드는 로컬 개발 클러스터가 [1-노드 모드](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode)에 있는 경우에만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="28832-124">This mode only works if your local development cluster is in [1-Node mode](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).</span></span>
2. <span data-ttu-id="28832-125">**응용 프로그램을 제거** 원인을 hello 응용 프로그램 toobe hello 디버그 세션이 종료 될 때 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="28832-125">**Remove Application** causes hello application toobe removed when hello debug session ends.</span></span>
3. <span data-ttu-id="28832-126">**자동으로 업그레이드** hello 디버그 세션이 종료 될 때 toorun hello 응용 프로그램에 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="28832-126">**Auto Upgrade** hello application continues toorun when hello debug session ends.</span></span> <span data-ttu-id="28832-127">hello 다음 디버그 세션으로 처리 될 hello 배포 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="28832-127">hello next debug session will treat hello deployment as an upgrade.</span></span> <span data-ttu-id="28832-128">hello 업그레이드 프로세스는 이전 디버그 세션에서 입력 한 모든 데이터를 보존 합니다.</span><span class="sxs-lookup"><span data-stu-id="28832-128">hello upgrade process preserves any data that you entered in a previous debug session.</span></span>
4. <span data-ttu-id="28832-129">**응용 프로그램이 유지** 때 hello hello 클러스터에서 실행 되는 hello 응용 프로그램 유지 디버그 세션이 종료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28832-129">**Keep Application** hello application keeps running in hello cluster when hello debug session ends.</span></span> <span data-ttu-id="28832-130">Hello 시작 시 hello 다음 디버그 세션을 hello 응용 프로그램을 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28832-130">At hello beginning of hello next debug session, hello application will be removed.</span></span>

<span data-ttu-id="28832-131">에 대 한 **자동 업그레이드가** 서비스 패브릭의 hello 응용 프로그램 업그레이드 기능을 적용 하 여 데이터 보존 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28832-131">For **Auto Upgrade** data is preserved by applying hello application upgrade capabilities of Service Fabric.</span></span> <span data-ttu-id="28832-132">응용 프로그램 업그레이드 및 실제 환경에서 업그레이드를 수행하는 방법에 대한 자세한 내용은 [서비스 패브릭 응용 프로그램 업그레이드](service-fabric-application-upgrade.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="28832-132">For more information about upgrading applications and how you might perform an upgrade in a real environment, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="add-a-service-tooyour-service-fabric-application"></a><span data-ttu-id="28832-133">서비스 tooyour 서비스 패브릭 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="28832-133">Add a service tooyour Service Fabric application</span></span>
<span data-ttu-id="28832-134">새 서비스 tooyour 응용 프로그램 tooextend 기능을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28832-134">You can add new services tooyour application tooextend its functionality.</span></span>  <span data-ttu-id="28832-135">hello 통해 hello 서비스를 추가 하는 hello 서비스 응용 프로그램 패키지에 포함 되어 tooensure **새 패브릭 서비스...**  메뉴 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="28832-135">tooensure that hello service is included in your application package, add hello service through hello **New Fabric Service...** menu item.</span></span>

![새 Service Fabric 서비스 추가][newservice]

<span data-ttu-id="28832-137">서비스 패브릭 프로젝트 형식 tooadd tooyour 응용 프로그램을 선택 하 고 hello 서비스에 대 한 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="28832-137">Select a Service Fabric project type tooadd tooyour application, and specify a name for hello service.</span></span>  <span data-ttu-id="28832-138">참조 [서비스 프레임 워크를 선택](service-fabric-choose-framework.md) 어떤 서비스 결정 toohelp toouse를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="28832-138">See [Choosing a framework for your service](service-fabric-choose-framework.md) toohelp you decide which service type toouse.</span></span>

![서비스 패브릭 서비스 프로젝트 형식 tooadd tooyour 응용 프로그램을 선택 합니다.][addserviceproject]

<span data-ttu-id="28832-140">새 서비스 hello tooyour 솔루션 및 기존 응용 프로그램 패키지에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28832-140">hello new service is added tooyour solution and existing application package.</span></span> <span data-ttu-id="28832-141">기본 서비스 인스턴스와 hello 서비스 참조 추가 toohello 응용 프로그램 매니페스트 됩니다, 그리고 바꾸지 hello 서비스 toobe 만들어지고 hello 응용 프로그램을 배포한 다음에 hello를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="28832-141">hello service references and a default service instance will be added toohello application manifest, causing hello service toobe created and started hello next time you deploy hello application.</span></span>

![새 서비스 hello tooyour 응용 프로그램 매니페스트 추가][newserviceapplicationmanifest]

## <a name="package-your-service-fabric-application"></a><span data-ttu-id="28832-143">서비스 패브릭 응용 프로그램 패키징</span><span class="sxs-lookup"><span data-stu-id="28832-143">Package your Service Fabric application</span></span>
<span data-ttu-id="28832-144">toodeploy hello 응용 프로그램 및 서비스 tooa 클러스터 toocreate 응용 프로그램 패키지 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="28832-144">toodeploy hello application and its services tooa cluster, you need toocreate an application package.</span></span>  <span data-ttu-id="28832-145">hello 패키지 hello 응용 프로그램 매니페스트, 서비스 매니페스트 및 기타 필요한 파일이 특정 레이아웃으로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="28832-145">hello package organizes hello application manifest, service manifests, and other necessary files in a specific layout.</span></span>  <span data-ttu-id="28832-146">Visual Studio를 설정 하 고 hello hello 'pkg' 디렉터리에 hello 응용 프로그램 프로젝트의 폴더에는 패키지를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="28832-146">Visual Studio sets up and manages hello package in hello application project's folder, in hello 'pkg' directory.</span></span>  <span data-ttu-id="28832-147">클릭 하면 **패키지** hello에서 **응용 프로그램** 업데이트 hello 응용 프로그램 패키지 또는 상황에 맞는 메뉴를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="28832-147">Clicking **Package** from hello **Application** context menu creates or updates hello application package.</span></span>

## <a name="remove-applications-and-application-types-using-cloud-explorer"></a><span data-ttu-id="28832-148">클라우드 탐색기를 사용하여 응용 프로그램 및 응용 프로그램 유형 제거</span><span class="sxs-lookup"><span data-stu-id="28832-148">Remove applications and application types using Cloud Explorer</span></span>
<span data-ttu-id="28832-149">Hello에서 시작할 수 있는 클라우드 탐색기를 사용 하 여 Visual Studio 내에서 기본 클러스터 관리 작업을 수행할 수 있습니다 **보기** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="28832-149">You can perform basic cluster management operations from within Visual Studio using Cloud Explorer, which you can launch from hello **View** menu.</span></span> <span data-ttu-id="28832-150">예를 들어 응용 프로그램을 삭제하고 로컬 또는 원격 클러스터에서 응용 프로그램 유형을 프로비전 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28832-150">For instance, you can delete applications and unprovision application types on local or remote clusters.</span></span>

![응용 프로그램 제거][removeapplication]

> [!TIP]
> <span data-ttu-id="28832-152">다양한 클러스터 관리 기능은 [Service Fabric Explorer로 클러스터 시각화](service-fabric-visualizing-your-cluster.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="28832-152">For richer cluster management functionality, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="28832-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="28832-153">Next steps</span></span>
* [<span data-ttu-id="28832-154">서비스 패브릭 응용 프로그램 모델</span><span class="sxs-lookup"><span data-stu-id="28832-154">Service Fabric application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="28832-155">서비스 패브릭 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="28832-155">Service Fabric application deployment</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="28832-156">여러 환경에 대한 응용 프로그램 매개 변수 관리</span><span class="sxs-lookup"><span data-stu-id="28832-156">Managing application parameters for multiple environments</span></span>](service-fabric-manage-multiple-environment-app-configuration.md)
* [<span data-ttu-id="28832-157">서비스 패브릭 응용 프로그램 디버깅</span><span class="sxs-lookup"><span data-stu-id="28832-157">Debugging your Service Fabric application</span></span>](service-fabric-debugging-your-application.md)
* [<span data-ttu-id="28832-158">서비스 패브릭 탐색기를 사용하여 클러스터 시각화</span><span class="sxs-lookup"><span data-stu-id="28832-158">Visualizing your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

<!--Image references-->
[addserviceproject]:./media/service-fabric-manage-application-in-visual-studio/addserviceproject.png
[manageservicefabric]: ./media/service-fabric-manage-application-in-visual-studio/manageservicefabric.png
[newservice]:./media/service-fabric-manage-application-in-visual-studio/newservice.png
[newserviceapplicationmanifest]:./media/service-fabric-manage-application-in-visual-studio/newserviceapplicationmanifest.png
[debugmodeproperty]:./media/service-fabric-manage-application-in-visual-studio/debugmodeproperty.png
[removeapplication]:./media/service-fabric-manage-application-in-visual-studio/removeapplication.png