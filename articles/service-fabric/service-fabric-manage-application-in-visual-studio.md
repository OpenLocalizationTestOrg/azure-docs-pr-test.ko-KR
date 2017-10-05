---
title: "Visual Studio에서 응용 프로그램 관리 | Microsoft Docs"
description: "Visual Studio를 사용하여 서비스 패브릭 응용 프로그램과 서비스를 만들고, 개발하고, 배포하며 디버그합니다."
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
ms.openlocfilehash: 3f6a47a15b74a7ceb6504b2834be62e76ab70bcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-visual-studio-to-simplify-writing-and-managing-your-service-fabric-applications"></a><span data-ttu-id="7ca13-103">Visual Studio를 사용하여 서비스 패브릭 응용 프로그램 쓰기 및 관리 단순화하기</span><span class="sxs-lookup"><span data-stu-id="7ca13-103">Use Visual Studio to simplify writing and managing your Service Fabric applications</span></span>
<span data-ttu-id="7ca13-104">Visual Studio를 통해 Azure 서비스 패브릭 응용 프로그램 및 서비스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ca13-104">You can manage your Azure Service Fabric applications and services through Visual Studio.</span></span> <span data-ttu-id="7ca13-105">[개발 환경을 설정](service-fabric-get-started.md)한 후, Visual Studio를 사용하여 로컬 개발 클러스터에서 서비스 패브릭 응용 프로그램을 만들거나 서비스를 추가하거나 응용 프로그램의 패키징, 등록 및 배포를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ca13-105">Once you've [set up your development environment](service-fabric-get-started.md), you can use Visual Studio to create Service Fabric applications, add services, or package, register, and deploy applications in your local development cluster.</span></span>

## <a name="deploy-your-service-fabric-application"></a><span data-ttu-id="7ca13-106">서비스 패브릭 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="7ca13-106">Deploy your Service Fabric application</span></span>
<span data-ttu-id="7ca13-107">기본적으로 응용 프로그램을 배포하는 작업은 다음 단계를 하나의 간단한 작업으로 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="7ca13-107">By default, deploying an application combines the following steps into one simple operation:</span></span>

1. <span data-ttu-id="7ca13-108">응용 프로그램 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="7ca13-108">Creating the application package</span></span>
2. <span data-ttu-id="7ca13-109">이미지 저장소에 응용 프로그램 패키지 업로드</span><span class="sxs-lookup"><span data-stu-id="7ca13-109">Uploading the application package to the image store</span></span>
3. <span data-ttu-id="7ca13-110">응용 프로그램 유형 등록</span><span class="sxs-lookup"><span data-stu-id="7ca13-110">Registering the application type</span></span>
4. <span data-ttu-id="7ca13-111">실행 중인 모든 응용 프로그램 인스턴스 제거</span><span class="sxs-lookup"><span data-stu-id="7ca13-111">Removing any running application instances</span></span>
5. <span data-ttu-id="7ca13-112">응용 프로그램 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="7ca13-112">Creating an application instance</span></span>

<span data-ttu-id="7ca13-113">Visual Studio에서 **F5** 키를 누르면 응용 프로그램이 배포되고 모든 응용 프로그램 인스턴스에 디버거가 첨부됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ca13-113">In Visual Studio, pressing **F5** deploys your application and attach the debugger to all application instances.</span></span> <span data-ttu-id="7ca13-114">**Ctrl+F5** 를 사용하여 디버그하지 않고 응용 프로그램을 배포하거나, 게시 프로필을 사용하여 로컬 또는 원격 클러스터에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ca13-114">You can use **Ctrl+F5** to deploy an application without debugging, or you can publish to a local or remote cluster by using the publish profile.</span></span> <span data-ttu-id="7ca13-115">자세한 내용은 [Visual Studio를 사용하여 원격 클러스터에 응용 프로그램 게시](service-fabric-publish-app-remote-cluster.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ca13-115">For more information, see [Publish an application to a remote cluster by using Visual Studio](service-fabric-publish-app-remote-cluster.md).</span></span>

### <a name="application-debug-mode"></a><span data-ttu-id="7ca13-116">응용 프로그램 디버그 모드</span><span class="sxs-lookup"><span data-stu-id="7ca13-116">Application Debug Mode</span></span>
<span data-ttu-id="7ca13-117">Visual Studio는 Visual Studio에서 디버깅의 일부로 응용 프로그램 배포를 처리하는 방법을 제어하는 **응용 프로그램 디버그 모드** 라는 속성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7ca13-117">Visual Studio provide a property called **Application Debug Mode**, which controls how you want Visual Studios to handle Application deployment as part of debugging.</span></span>

#### <a name="to-set-the-application-debug-mode-property"></a><span data-ttu-id="7ca13-118">응용 프로그램 디버그 모드 속성을 설정하려면</span><span class="sxs-lookup"><span data-stu-id="7ca13-118">To set the Application Debug Mode property</span></span>
1. <span data-ttu-id="7ca13-119">Service Fabric 응용 프로그램 프로젝트의 (*.sfproj) 바로 가기 메뉴에서 **속성** 을 선택합니다. (또는 **F4** 키를 누릅니다.)</span><span class="sxs-lookup"><span data-stu-id="7ca13-119">On the Service Fabric application project's (*.sfproj) shortcut menu, choose **Properties** (or press the **F4** key).</span></span>
2. <span data-ttu-id="7ca13-120">**속성** 창에서 **응용 프로그램 디버그 모드** 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ca13-120">In the **Properties** window, set the **Application Debug Mode** property.</span></span>

![응용 프로그램 디버그 모드 속성 설정][debugmodeproperty]

#### <a name="application-debug-modes"></a><span data-ttu-id="7ca13-122">응용 프로그램 디버그 모드</span><span class="sxs-lookup"><span data-stu-id="7ca13-122">Application Debug Modes</span></span>

1. <span data-ttu-id="7ca13-123">**응용 프로그램 새로 고침** 이 모드를 사용하면 코드를 신속하게 변경하고 디버그할 수 있으며 디버깅하는 동안 정적 웹 파일 편집을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7ca13-123">**Refresh Application** This mode enables you to quickly change and debug your code and supports editing static web files while debugging.</span></span> <span data-ttu-id="7ca13-124">이 모드는 로컬 개발 클러스터가 [1-노드 모드](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode)에 있는 경우에만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="7ca13-124">This mode only works if your local development cluster is in [1-Node mode](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).</span></span>
2. <span data-ttu-id="7ca13-125">**응용 프로그램 제거** 를 선택하면 디버그 세션이 종료될 때 응용 프로그램이 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ca13-125">**Remove Application** causes the application to be removed when the debug session ends.</span></span>
3. <span data-ttu-id="7ca13-126">**자동 업그레이드** 디버그 세션이 종료될 때 응용 프로그램이 계속 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ca13-126">**Auto Upgrade** The application continues to run when the debug session ends.</span></span> <span data-ttu-id="7ca13-127">다음 디버그 세션은 업그레이드로 배포를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="7ca13-127">The next debug session will treat the deployment as an upgrade.</span></span> <span data-ttu-id="7ca13-128">업그레이드 프로세스는 이전 디버그 세션에서 입력한 모든 데이터를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="7ca13-128">The upgrade process preserves any data that you entered in a previous debug session.</span></span>
4. <span data-ttu-id="7ca13-129">**응용 프로그램 유지** 디버그 세션이 종료될 때 클러스터에서 응용 프로그램이 계속 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ca13-129">**Keep Application** The application keeps running in the cluster when the debug session ends.</span></span> <span data-ttu-id="7ca13-130">다음 디버그 세션의 시작 부분에서 응용 프로그램이 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ca13-130">At the beginning of the next debug session, the application will be removed.</span></span>

<span data-ttu-id="7ca13-131">**자동 업그레이드**의 경우 데이터는 Service Fabric의 응용 프로그램 업그레이드 기능을 적용하여 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ca13-131">For **Auto Upgrade** data is preserved by applying the application upgrade capabilities of Service Fabric.</span></span> <span data-ttu-id="7ca13-132">응용 프로그램 업그레이드 및 실제 환경에서 업그레이드를 수행하는 방법에 대한 자세한 내용은 [서비스 패브릭 응용 프로그램 업그레이드](service-fabric-application-upgrade.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ca13-132">For more information about upgrading applications and how you might perform an upgrade in a real environment, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="add-a-service-to-your-service-fabric-application"></a><span data-ttu-id="7ca13-133">서비스 패브릭 응용 프로그램에 서비스 추가</span><span class="sxs-lookup"><span data-stu-id="7ca13-133">Add a service to your Service Fabric application</span></span>
<span data-ttu-id="7ca13-134">응용 프로그램에 새 서비스를 추가하여 기능을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ca13-134">You can add new services to your application to extend its functionality.</span></span>  <span data-ttu-id="7ca13-135">응용 프로그램 패키지에 서비스가 포함되도록 하려면 **새 패브릭 서비스...** 메뉴 항목을 통해 서비스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7ca13-135">To ensure that the service is included in your application package, add the service through the **New Fabric Service...** menu item.</span></span>

![새 Service Fabric 서비스 추가][newservice]

<span data-ttu-id="7ca13-137">응용 프로그램에 추가할 서비스 패브릭 프로젝트 유형을 선택하고 서비스의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ca13-137">Select a Service Fabric project type to add to your application, and specify a name for the service.</span></span>  <span data-ttu-id="7ca13-138">사용할 서비스 유형을 결정하는 데 도움이 필요하면 [서비스를 위한 프레임워크 선택](service-fabric-choose-framework.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ca13-138">See [Choosing a framework for your service](service-fabric-choose-framework.md) to help you decide which service type to use.</span></span>

![응용 프로그램에 추가할 Service Fabric 서비스 프로젝트 유형 선택][addserviceproject]

<span data-ttu-id="7ca13-140">새 서비스가 솔루션 및 기존 응용 프로그램 패키지에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ca13-140">The new service is added to your solution and existing application package.</span></span> <span data-ttu-id="7ca13-141">서비스 참조 및 기본 서비스 인스턴스는 다음에 응용 프로그램을 배포할 때 서비스가 만들어지고 시작되도록 응용 프로그램 매니페스트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ca13-141">The service references and a default service instance will be added to the application manifest, causing the service to be created and started the next time you deploy the application.</span></span>

![새 서비스가 응용 프로그램 매니페스트에 추가됩니다.][newserviceapplicationmanifest]

## <a name="package-your-service-fabric-application"></a><span data-ttu-id="7ca13-143">서비스 패브릭 응용 프로그램 패키징</span><span class="sxs-lookup"><span data-stu-id="7ca13-143">Package your Service Fabric application</span></span>
<span data-ttu-id="7ca13-144">응용 프로그램 및 해당 서비스를 클러스터에 배포하려면 응용 프로그램 패키지를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ca13-144">To deploy the application and its services to a cluster, you need to create an application package.</span></span>  <span data-ttu-id="7ca13-145">패키지는 응용 프로그램 매니페스트, 서비스 매니페스트 및 특정 레이아웃에서 필요한 기타 파일로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ca13-145">The package organizes the application manifest, service manifests, and other necessary files in a specific layout.</span></span>  <span data-ttu-id="7ca13-146">Visual Studio는 응용 프로그램 프로젝트의 폴더인 'pkg' 디렉터리에서 패키지를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="7ca13-146">Visual Studio sets up and manages the package in the application project's folder, in the 'pkg' directory.</span></span>  <span data-ttu-id="7ca13-147">**응용 프로그램** 상황에 맞는 메뉴에서 **패키지**를 클릭하면 응용 프로그램 패키지가 생성되거나 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ca13-147">Clicking **Package** from the **Application** context menu creates or updates the application package.</span></span>

## <a name="remove-applications-and-application-types-using-cloud-explorer"></a><span data-ttu-id="7ca13-148">클라우드 탐색기를 사용하여 응용 프로그램 및 응용 프로그램 유형 제거</span><span class="sxs-lookup"><span data-stu-id="7ca13-148">Remove applications and application types using Cloud Explorer</span></span>
<span data-ttu-id="7ca13-149">**보기** 메뉴에서 시작할 수 있는 클라우드 탐색기를 사용하여 Visual Studio 내에서 기본 클러스터 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ca13-149">You can perform basic cluster management operations from within Visual Studio using Cloud Explorer, which you can launch from the **View** menu.</span></span> <span data-ttu-id="7ca13-150">예를 들어 응용 프로그램을 삭제하고 로컬 또는 원격 클러스터에서 응용 프로그램 유형을 프로비전 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ca13-150">For instance, you can delete applications and unprovision application types on local or remote clusters.</span></span>

![응용 프로그램 제거][removeapplication]

> [!TIP]
> <span data-ttu-id="7ca13-152">다양한 클러스터 관리 기능은 [Service Fabric Explorer로 클러스터 시각화](service-fabric-visualizing-your-cluster.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ca13-152">For richer cluster management functionality, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="7ca13-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7ca13-153">Next steps</span></span>
* [<span data-ttu-id="7ca13-154">서비스 패브릭 응용 프로그램 모델</span><span class="sxs-lookup"><span data-stu-id="7ca13-154">Service Fabric application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="7ca13-155">서비스 패브릭 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="7ca13-155">Service Fabric application deployment</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="7ca13-156">여러 환경에 대한 응용 프로그램 매개 변수 관리</span><span class="sxs-lookup"><span data-stu-id="7ca13-156">Managing application parameters for multiple environments</span></span>](service-fabric-manage-multiple-environment-app-configuration.md)
* [<span data-ttu-id="7ca13-157">서비스 패브릭 응용 프로그램 디버깅</span><span class="sxs-lookup"><span data-stu-id="7ca13-157">Debugging your Service Fabric application</span></span>](service-fabric-debugging-your-application.md)
* [<span data-ttu-id="7ca13-158">서비스 패브릭 탐색기를 사용하여 클러스터 시각화</span><span class="sxs-lookup"><span data-stu-id="7ca13-158">Visualizing your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

<!--Image references-->
[addserviceproject]:./media/service-fabric-manage-application-in-visual-studio/addserviceproject.png
[manageservicefabric]: ./media/service-fabric-manage-application-in-visual-studio/manageservicefabric.png
[newservice]:./media/service-fabric-manage-application-in-visual-studio/newservice.png
[newserviceapplicationmanifest]:./media/service-fabric-manage-application-in-visual-studio/newserviceapplicationmanifest.png
[debugmodeproperty]:./media/service-fabric-manage-application-in-visual-studio/debugmodeproperty.png
[removeapplication]:./media/service-fabric-manage-application-in-visual-studio/removeapplication.png