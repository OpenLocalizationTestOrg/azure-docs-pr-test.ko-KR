---
title: "Service Fabric 앱 업그레이드 자습서 | Microsoft Docs"
description: "이 문서는 Visual Studio를 사용하여 서비스 패브릭 응용 프로그램의 배포, 코드 변경, 업그레이드 롤아웃 환경을 안내합니다."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: a3181a7a-9ab1-4216-b07a-05b79bd826a4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 940440688ec770a4aeb932b574bd6be173f494d4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="service-fabric-application-upgrade-tutorial-using-visual-studio"></a><span data-ttu-id="265d4-103">Visual Studio를 사용하여 서비스 패브릭 응용 프로그램 업그레이드 자습서</span><span class="sxs-lookup"><span data-stu-id="265d4-103">Service Fabric application upgrade tutorial using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="265d4-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="265d4-104">PowerShell</span></span>](service-fabric-application-upgrade-tutorial-powershell.md)
> * [<span data-ttu-id="265d4-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="265d4-105">Visual Studio</span></span>](service-fabric-application-upgrade-tutorial.md)
> 
> 

<br/>

<span data-ttu-id="265d4-106">Azure 서비스 패브릭을 사용하면 변경된 서비스만 업그레이드하고, 업그레이드 프로세스를 통해 응용 프로그램 상태를 모니터링하여 클라우드 응용 프로그램 업그레이드 프로세스를 간소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-106">Azure Service Fabric simplifies the process of upgrading cloud applications by ensuring that only changed services are upgraded, and that application health is monitored throughout the upgrade process.</span></span> <span data-ttu-id="265d4-107">문제가 발생할 경우 응용 프로그램이 자동으로 이전 버전으로 롤백합니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-107">It also automatically rolls back the application to the previous version upon encountering issues.</span></span> <span data-ttu-id="265d4-108">서비스 패브릭 응용 프로그램 업그레이드는 *가동 중지 시간 없이*응용 프로그램을 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-108">Service Fabric application upgrades are *Zero Downtime*, since the application can be upgraded with no downtime.</span></span> <span data-ttu-id="265d4-109">이 자습서에서는 Visual Studio를 사용하여 롤링 업그레이드를 완료하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-109">This tutorial covers how to complete a rolling upgrade from Visual Studio.</span></span>

## <a name="step-1-build-and-publish-the-visual-objects-sample"></a><span data-ttu-id="265d4-110">1단계: 시각적 개체 샘플 빌드 및 게시</span><span class="sxs-lookup"><span data-stu-id="265d4-110">Step 1: Build and publish the Visual Objects sample</span></span>
<span data-ttu-id="265d4-111">먼저 GitHub에서 [Visual Objects](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Actors/VisualObjects) 응용 프로그램을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-111">First, download the [Visual Objects](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Actors/VisualObjects) application from GitHub.</span></span> <span data-ttu-id="265d4-112">그런 후 응용 프로그램 프로젝트 **VisualObjects**를 마우스 오른쪽 단추로 클릭하고 서비스 패브릭 메뉴 항목에서 **게시** 명령을 선택하여 응용 프로그램을 구축 및 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-112">Then, build and publish the application by right-clicking on the application project, **VisualObjects**, and selecting the **Publish** command in the Service Fabric menu item.</span></span>

![서비스 패브릭 응용 프로그램의 상황에 맞는 메뉴][image1]

<span data-ttu-id="265d4-114">**게시**를 선택하면 팝업이 표시되며 **대상 프로필**을 **PublishProfiles\Local.xml**로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-114">Selecting **Publish** brings up a popup, and you can set the **Target profile** to **PublishProfiles\Local.xml**.</span></span> <span data-ttu-id="265d4-115">**게시**를 클릭하기 전의 창 모양은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-115">The window should look like the following before you click **Publish**.</span></span>

![서비스 패브릭 응용 프로그램 게시][image2]

<span data-ttu-id="265d4-117">이제 대화 상자에서 **게시** 를 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-117">Now you can click **Publish** in the dialog box.</span></span> <span data-ttu-id="265d4-118">[클러스터 및 응용 프로그램을 보는 서비스 패브릭 탐색기](service-fabric-visualizing-your-cluster.md)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-118">You can use [Service Fabric Explorer to view the cluster and the application](service-fabric-visualizing-your-cluster.md).</span></span> <span data-ttu-id="265d4-119">Visual Objects 응용 프로그램에는 브라우저의 주소 표시줄에 [http://localhost:8081/visualobjects/](http://localhost:8081/visualobjects/)를 입력해서 이동할 수 있는 웹 서비스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-119">The Visual Objects application has a web service that you can go to by typing [http://localhost:8081/visualobjects/](http://localhost:8081/visualobjects/) in the address bar of your browser.</span></span>  <span data-ttu-id="265d4-120">화면에서 10개의 부동 시각적 개체가 움직이는 것을 볼 수 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-120">You should see 10 floating visual objects moving around on the screen.</span></span>

<span data-ttu-id="265d4-121">**참고:** `Cloud.xml` 프로필(Azure 서비스 패브릭)에 배포하는 경우 **http://{ServiceFabricName}.{Region}.cloudapp.azure.com:8081/visualobjects/**에서 응용 프로그램을 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-121">**NOTE:** If deploying to `Cloud.xml` profile (Azure Service Fabric), the application should then be available at **http://{ServiceFabricName}.{Region}.cloudapp.azure.com:8081/visualobjects/**.</span></span> <span data-ttu-id="265d4-122">부하 분산 장치에 `8081/TCP`가 구성되었는지 확인합니다(Serivce Fabric 인스턴스와 동일한 리소스 그룹에 부하 분산 장치 찾기).</span><span class="sxs-lookup"><span data-stu-id="265d4-122">Make sure you do have `8081/TCP` configured in the Load Balancer (find the Load Balancer in the same resource group as the Service Fabric instance).</span></span>

## <a name="step-2-update-the-visual-objects-sample"></a><span data-ttu-id="265d4-123">2단계: 시각적 개체 샘플 업데이트</span><span class="sxs-lookup"><span data-stu-id="265d4-123">Step 2: Update the Visual Objects sample</span></span>
<span data-ttu-id="265d4-124">1단계에서 배포된 버전에서 알 수 있듯이 시각적 개체는 회전하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-124">You might notice that with the version that was deployed in step 1, the visual objects do not rotate.</span></span> <span data-ttu-id="265d4-125">이 응용 프로그램을 시각적 개체도 회전하도록 업그레이드하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-125">Let's upgrade this application to one where the visual objects also rotate.</span></span>

<span data-ttu-id="265d4-126">VisualObjects 솔루션에서 VisualObjects.ActorService 프로젝트를 선택하고 **VisualObjectActor.cs** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-126">Select the VisualObjects.ActorService project within the VisualObjects solution, and open the **VisualObjectActor.cs** file.</span></span> <span data-ttu-id="265d4-127">해당 파일 내에서 `MoveObject` 메서드로 이동하고 `visualObject.Move(false)`를 주석 처리하고 `visualObject.Move(true)`의 주석 처리를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-127">Within that file, go to the method `MoveObject`, comment out `visualObject.Move(false)`, and uncomment `visualObject.Move(true)`.</span></span> <span data-ttu-id="265d4-128">이렇게 코드를 변경하면 서비스가 업그레이드된 후 개체가 회전됩니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-128">This code change rotates the objects after the service is upgraded.</span></span>  <span data-ttu-id="265d4-129">**이제 수정된 프로젝트를 빌드할 수 있는 솔루션**을 빌드(다시 빌드 아님)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-129">**Now you can build (not rebuild) the solution**, which builds the modified projects.</span></span> <span data-ttu-id="265d4-130">*모두 다시 빌드*를 선택하는 경우 모든 프로젝트의 버전을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-130">If you select *Rebuild all*, you have to update the versions for all the projects.</span></span>

<span data-ttu-id="265d4-131">또한 응용 프로그램의 버전을 관리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-131">We also need to version our application.</span></span> <span data-ttu-id="265d4-132">**VisualObjects** 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 버전을 변경하려면 Visual Studio **매니페스트 파일 편집** 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-132">To make the version changes after you right-click on the **VisualObjects** project, you can use the Visual Studio **Edit Manifest Versions** option.</span></span> <span data-ttu-id="265d4-133">이 옵션을 선택하면 다음과 같이 버전에 대한 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-133">Selecting this option brings up the dialog box for edition versions as follows:</span></span>

![버전 관리 대화 상자][image3]

<span data-ttu-id="265d4-135">수정된 프로젝트 및 해당 코드 패키지의 버전을 응용 프로그램과 같이 2.0.0으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-135">Update the versions for the modified projects and their code packages, along with the application to version 2.0.0.</span></span> <span data-ttu-id="265d4-136">변경 후 매니페스트 버전은 다음과 같이 설정됩니다(굵은 글씨가 변경된 부분임).</span><span class="sxs-lookup"><span data-stu-id="265d4-136">After the changes are made, the manifest should look like the following (bold portions show the changes):</span></span>

![버전 업데이트][image4]

<span data-ttu-id="265d4-138">**응용 프로그램 및 서비스 버전 자동 업데이트**를 선택하는 경우 Visual Studio 도구는 버전의 자동 롤업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-138">The Visual Studio tools can do automatic rollups of versions upon selecting **Automatically update application and service versions**.</span></span> <span data-ttu-id="265d4-139">[SemVer](http://www.semver.org)를 사용하는 경우 해당 옵션이 선택된 경우 코드 및/또는 구성 패키지 버전을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-139">If you use [SemVer](http://www.semver.org), you need to update the code and/or configuration package version alone if that option is selected.</span></span>

<span data-ttu-id="265d4-140">변경 내용을 저장하고 이제 **Upgrade the Application** (응용 프로그램 업그레이드) 상자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-140">Save the changes, and now check the **Upgrade the Application** box.</span></span>

## <a name="step-3--upgrade-your-application"></a><span data-ttu-id="265d4-141">3단계: 응용 프로그램 업그레이드</span><span class="sxs-lookup"><span data-stu-id="265d4-141">Step 3:  Upgrade your application</span></span>
<span data-ttu-id="265d4-142">[응용 프로그램 업그레이드 매개 변수](service-fabric-application-upgrade-parameters.md) 및 [업그레이드 프로세스](service-fabric-application-upgrade.md)를 파악하여 다양한 업그레이드 매개 변수, 제한 시간 및 적용될 수 있는 상태 조건을 잘 이해하세요.</span><span class="sxs-lookup"><span data-stu-id="265d4-142">Familiarize yourself with the [application upgrade parameters](service-fabric-application-upgrade-parameters.md) and the [upgrade process](service-fabric-application-upgrade.md) to get a good understanding of the various upgrade parameters, time-outs, and health criterion that can be applied.</span></span> <span data-ttu-id="265d4-143">이 연습에서는 서비스 상태 평가 조건을 기본값(모니터링되지 않음 모드)으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-143">For this walkthrough, the service health evaluation criterion is set to the default (unmonitored mode).</span></span> <span data-ttu-id="265d4-144">**업그레이드 설정 구성** 을 선택한 다음 매개 변수를 원하는 대로 수정하여 이러한 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-144">You can configure these settings by selecting **Configure Upgrade Settings** and then modifying the parameters as desired.</span></span>

<span data-ttu-id="265d4-145">이제 응용 프로그램 업그레이드를 시작하기 위한 모든 설정이 완료되었으므로 **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-145">Now we are all set to start the application upgrade by selecting **Publish**.</span></span> <span data-ttu-id="265d4-146">이 옵션을 선택하면 응용 프로그램 버전이 2.0.0으로 업그레이드되고 개체가 회전됩니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-146">This option upgrades your application to version 2.0.0, in which the objects rotate.</span></span> <span data-ttu-id="265d4-147">서비스 패브릭은 업데이트 도메인을 한 번에 하나씩 업그레이드하며(일부 개체가 먼저 업데이트되고 나머지는 다음에 업데이트됨) 업그레이드 중에 서비스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-147">Service Fabric upgrades one update domain at a time (some objects are updated first, followed by others), and the service remains accessible during the upgrade.</span></span> <span data-ttu-id="265d4-148">클라이언트(브라우저)를 통해 서비스에 대한 액세스를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-148">Access to the service can be checked through your client (browser).</span></span>  

<span data-ttu-id="265d4-149">응용 프로그램 업그레이드가 진행되는 동안 응용 프로그램 아래의 **Upgrades in Progress** (진행 중인 업그레이드) 탭을 사용하여 Service Fabric Explorer로 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-149">Now, as the application upgrade proceeds, you can monitor it with Service Fabric Explorer, by using the **Upgrades in Progress** tab under the applications.</span></span>

<span data-ttu-id="265d4-150">잠시 후 모든 업데이트 도메인이 업그레이드(완료)되고 Visual Studio 출력 창에 업그레이드 완료를 알리는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-150">In a few minutes, all update domains should be upgraded (completed), and the Visual Studio output window should also state that the upgrade is completed.</span></span> <span data-ttu-id="265d4-151">브라우저 창에서 이제 *모든* 시각적 개체가 회전되는 것을 볼 수 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-151">And you should find that *all* the visual objects in your browser window are now rotating!</span></span>

<span data-ttu-id="265d4-152">버전을 변경하고 연습처럼 버전 2.0.0에서 버전 3.0.0으로 바꾸거나 버전 2.0.0에서 버전 1.0.0으로 바꾸려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-152">You may want to try changing the versions, and moving from version 2.0.0 to version 3.0.0 as an exercise, or even from version 2.0.0 back to version 1.0.0.</span></span> <span data-ttu-id="265d4-153">제한 시간과 상태 정책을 변경해 보면서 익숙해지십시오.</span><span class="sxs-lookup"><span data-stu-id="265d4-153">Play with time-outs and health policies to make yourself familiar with them.</span></span> <span data-ttu-id="265d4-154">로컬 클러스터가 아닌 Azure 클러스터에 배포하는 경우 다른 매개 변수를 사용해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-154">When deploying to an Azure cluster as opposed to a local cluster, the parameters used may have to differ.</span></span> <span data-ttu-id="265d4-155">제한 시간을 신중하게 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-155">We recommend that you set the time-outs conservatively.</span></span>

## <a name="next-steps"></a><span data-ttu-id="265d4-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="265d4-156">Next steps</span></span>
<span data-ttu-id="265d4-157">[Powershell을 사용하여 응용 프로그램 업그레이드](service-fabric-application-upgrade-tutorial-powershell.md) 에서는 PowerShell을 사용하여 응용 프로그램 업그레이드를 진행하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-157">[Upgrading your application using PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="265d4-158">[업그레이드 매개 변수](service-fabric-application-upgrade-parameters.md)를 사용하여 응용 프로그램 업그레이드 방법을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-158">Control how your application is upgraded by using [upgrade parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="265d4-159">[데이터 직렬화](service-fabric-application-upgrade-data-serialization.md)사용 방법을 익혀 응용 프로그램 업그레이드와 호환되도록 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-159">Make your application upgrades compatible by learning how to use [data serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="265d4-160">[고급 항목](service-fabric-application-upgrade-advanced.md)을 참조하여 응용 프로그램을 업그레이드하는 동안 고급 기능을 사용하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-160">Learn how to use advanced functionality while upgrading your application by referring to [Advanced topics](service-fabric-application-upgrade-advanced.md).</span></span>

<span data-ttu-id="265d4-161">[응용 프로그램 업그레이드 문제 해결](service-fabric-application-upgrade-troubleshooting.md)의 단계를 참조하여 응용 프로그램 업그레이드 중 발생하는 일반적인 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="265d4-161">Fix common problems in application upgrades by referring to the steps in [Troubleshooting application upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>

[image1]: media/service-fabric-application-upgrade-tutorial/upgrade7.png
[image2]: media/service-fabric-application-upgrade-tutorial/upgrade1.png
[image3]: media/service-fabric-application-upgrade-tutorial/upgrade5.png
[image4]: media/service-fabric-application-upgrade-tutorial/upgrade6.png
