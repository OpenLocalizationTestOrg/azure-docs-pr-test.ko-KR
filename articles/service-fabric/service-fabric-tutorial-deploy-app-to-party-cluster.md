---
title: "Azure 서비스 패브릭 응용 프로그램 tooa 파티 클러스터 aaaDeploy | Microsoft Docs"
description: "자세한 내용은 응용 프로그램 tooa toodeploy 파티 클러스터링 하는 방법입니다."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: msfussell
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: mikhegn
ms.openlocfilehash: db16b6418fa2533ed915c8b6e612b7a8e7311bed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-party-cluster-in-azure"></a><span data-ttu-id="05ce7-103">응용 프로그램 tooa Azure의 파티 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="05ce7-103">Deploy an application tooa Party Cluster in Azure</span></span>
<span data-ttu-id="05ce7-104">이 자습서 부분 2는 일련의이 고 표시 하는 Azure 서비스 패브릭 응용 프로그램 tooa Azure의 파티 클러스터 toodeploy 합니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-104">This tutorial is part two of a series and shows you how toodeploy an Azure Service Fabric application tooa Party Cluster in Azure.</span></span>

<span data-ttu-id="05ce7-105">Hello 자습서 시리즈의 2 부에서는 학습 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="05ce7-105">In part two of hello tutorial series, you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="05ce7-106">Visual Studio를 사용 하 여 응용 프로그램 tooa 원격 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="05ce7-106">Deploy an application tooa remote cluster using Visual Studio</span></span>
> * <span data-ttu-id="05ce7-107">Service Fabric Explorer를 사용하여 클러스터에서 응용 프로그램 제거</span><span class="sxs-lookup"><span data-stu-id="05ce7-107">Remove an application from a cluster using Service Fabric Explorer</span></span>

<span data-ttu-id="05ce7-108">이 자습서 시리즈에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-108">In this tutorial series you learn how to:</span></span>
> [!div class="checklist"]
> * [<span data-ttu-id="05ce7-109">.NET Service Fabric 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="05ce7-109">Build a .NET Service Fabric application</span></span>](service-fabric-tutorial-create-dotnet-app.md)
> * <span data-ttu-id="05ce7-110">Hello 응용 프로그램 tooa 원격 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="05ce7-110">Deploy hello application tooa remote cluster</span></span>
> * [<span data-ttu-id="05ce7-111">Visual Studio Team Services를 사용하여 CI/CD 구성</span><span class="sxs-lookup"><span data-stu-id="05ce7-111">Configure CI/CD using Visual Studio Team Services</span></span>](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a><span data-ttu-id="05ce7-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="05ce7-112">Prerequisites</span></span>
<span data-ttu-id="05ce7-113">이 자습서를 시작하기 전에:</span><span class="sxs-lookup"><span data-stu-id="05ce7-113">Before you begin this tutorial:</span></span>
- <span data-ttu-id="05ce7-114">Azure 구독이 없는 경우 [평가판 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-114">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="05ce7-115">[Visual Studio 2017 설치](https://www.visualstudio.com/) hello를 설치 하 고 **Azure 개발** 및 **ASP.NET 및 웹 개발** 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-115">[Install Visual Studio 2017](https://www.visualstudio.com/) and install hello **Azure development** and **ASP.NET and web development** workloads.</span></span>
- [<span data-ttu-id="05ce7-116">Hello 서비스 패브릭 SDK 설치</span><span class="sxs-lookup"><span data-stu-id="05ce7-116">Install hello Service Fabric SDK</span></span>](service-fabric-get-started.md)

## <a name="download-hello-voting-sample-application"></a><span data-ttu-id="05ce7-117">Hello 응답 샘플 응용 프로그램 다운로드</span><span class="sxs-lookup"><span data-stu-id="05ce7-117">Download hello Voting sample application</span></span>
<span data-ttu-id="05ce7-118">hello 응답 예제 응용 프로그램을 작성 하지 않은 경우 [이 자습서 시리즈의 1 부](service-fabric-tutorial-create-dotnet-app.md)를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-118">If you did not build hello Voting sample application in [part one of this tutorial series](service-fabric-tutorial-create-dotnet-app.md), you can download it.</span></span> <span data-ttu-id="05ce7-119">명령 창에서 hello 명령 tooclone hello 샘플 응용 프로그램 저장소 tooyour 로컬 컴퓨터에 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-119">In a command window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="set-up-a-party-cluster"></a><span data-ttu-id="05ce7-120">Party 클러스터 설정</span><span class="sxs-lookup"><span data-stu-id="05ce7-120">Set up a Party Cluster</span></span>
<span data-ttu-id="05ce7-121">파티 클러스터는 무료, 제한 시간 서비스 패브릭 클러스터 Azure에서 호스트 및 누구 든 지 수 응용 프로그램을 배포 하 고 hello 플랫폼에 대 한 자세한 내용은 hello 서비스 패브릭 팀에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-121">Party clusters are free, limited-time Service Fabric clusters hosted on Azure and run by hello Service Fabric team where anyone can deploy applications and learn about hello platform.</span></span> <span data-ttu-id="05ce7-122">평가판으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-122">For free!</span></span>

<span data-ttu-id="05ce7-123">tooget 액세스 tooa 파티 클러스터 toothis 사이트 탐색: http://aka.ms/tryservicefabric 읽고 준수 hello 지침 tooget 액세스 tooa 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-123">tooget access tooa Party Cluster, browse toothis site: http://aka.ms/tryservicefabric and follow hello instructions tooget access tooa cluster.</span></span> <span data-ttu-id="05ce7-124">Facebook 또는 GitHub 계정 tooget 액세스 tooa 파티 클러스터 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-124">You need a Facebook or GitHub account tooget access tooa Party Cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="05ce7-125">파티 클러스터 응용 프로그램 및 여기에 배치 된 데이터 표시 tooothers 않을 보호 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-125">Party clusters are not secured, so your applications and any data you put in them may be visible tooothers.</span></span> <span data-ttu-id="05ce7-126">다른 사용자가 아무 것도 배포 하지 않으려는 toosee 합니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-126">Don't deploy anything you don't want others toosee.</span></span> <span data-ttu-id="05ce7-127">Hello에 대 한 세부 정보를 모두에 대 한 계약의 사용을 통해 있는지 tooread 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-127">Be sure tooread over our Terms of Use for all hello details.</span></span>

## <a name="configure-hello-listening-port"></a><span data-ttu-id="05ce7-128">Hello 수신 대기 포트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-128">Configure hello listening port</span></span>
<span data-ttu-id="05ce7-129">Hello VotingWeb 프런트 엔드 서비스를 만들면 Visual Studio에서 서비스 toolisten hello에 대 한 포트를 임의로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-129">When hello VotingWeb front-end service is created, Visual Studio randomly selects a port for hello service toolisten on.</span></span>  <span data-ttu-id="05ce7-130">hello VotingWeb 서비스 역할을이 응용 프로그램에 대 한 프런트 엔드 hello 및 외부 트래픽이 허용, 이제 해당 서비스 tooa 고정 바인딩한 포트를 잘 알고 합니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-130">hello VotingWeb service acts as hello front-end for this application and accepts external traffic, so let's bind that service tooa fixed and well-know port.</span></span> <span data-ttu-id="05ce7-131">솔루션 탐색기에서 *VotingWeb/PackageRoot/ServiceManifest.xml*을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-131">In Solution Explorer, open  *VotingWeb/PackageRoot/ServiceManifest.xml*.</span></span>  <span data-ttu-id="05ce7-132">Hello **끝점** hello에 대 한 리소스 **리소스** 섹션 및 hello 변경 **포트** 값 too80 합니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-132">Find hello **Endpoint** resource in hello **Resources** section and change hello **Port** value too80.</span></span>

```xml
<Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" Port="80" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="05ce7-133">또한 'F5'를 사용 하 여 디버깅할 때 웹 브라우저 toohello 올바른 포트를 열리도록 hello 응답 프로젝트의 hello 응용 프로그램 URL 속성 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-133">Also update hello Application URL property value in hello Voting project so a web browser opens toohello correct port when you debug using 'F5'.</span></span>  <span data-ttu-id="05ce7-134">솔루션 탐색기에서 선택 hello **응답** 프로젝트 및 업데이트 hello **응용 프로그램 URL** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-134">In Solution Explorer, select hello **Voting** project and update hello **Application URL** property.</span></span>

![응용 프로그램 URL](./media/service-fabric-tutorial-deploy-app-to-party-cluster/application-url.png)

## <a name="deploy-hello-app-toohello-azure"></a><span data-ttu-id="05ce7-136">Hello 앱 toohello Azure 배포</span><span class="sxs-lookup"><span data-stu-id="05ce7-136">Deploy hello app toohello Azure</span></span>
<span data-ttu-id="05ce7-137">Hello 응용 프로그램 준비 되 면 했으므로 toohello 파티 클러스터 Visual Studio에서 직접 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-137">Now that hello application is ready, you can deploy it toohello Party Cluster direct from Visual Studio.</span></span>

1. <span data-ttu-id="05ce7-138">마우스 오른쪽 단추로 클릭 **응답** hello 솔루션 탐색기에서 선택한 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-138">Right-click **Voting** in hello Solution Explorer and choose **Publish**.</span></span>

    ![[게시] 대화 상자](./media/service-fabric-tutorial-deploy-app-to-party-cluster/publish-app.png)

2. <span data-ttu-id="05ce7-140">Hello에 파티 클러스터 hello 유형의 연결 끝점 hello **연결 끝점** 필드를 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-140">Type in hello Connection Endpoint of hello Party Cluster in hello **Connection Endpoint** field and click **Publish**.</span></span>

    <span data-ttu-id="05ce7-141">Hello 게시 한 후에 완료 해야 수 toosend 브라우저를 통해 요청 toohello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-141">Once hello publish has finished, you should be able toosend a request toohello application via a browser.</span></span>

3. <span data-ttu-id="05ce7-142">열기 기본 설정 표준 브라우저와 hello 클러스터 주소 (hello hello 포트 정보-예를 들어 win1kw5649s.westus.cloudapp.azure.com 없는 끝점 연결)를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-142">Open you preferred browser and type in hello cluster address (hello connection endpoint without hello port information - for example, win1kw5649s.westus.cloudapp.azure.com).</span></span>

    <span data-ttu-id="05ce7-143">이제 hello 같은 결과 hello 응용 프로그램을 로컬로 실행 하는 경우 본 것 처럼 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-143">You should now see hello same result as you saw when running hello application locally.</span></span>

    ![클러스터에서 API 응답](./media/service-fabric-tutorial-deploy-app-to-party-cluster/response-from-cluster.png)

## <a name="remove-hello-application-from-a-cluster-using-service-fabric-explorer"></a><span data-ttu-id="05ce7-145">서비스 패브릭 탐색기를 사용 하는 클러스터에서 hello 응용 프로그램 제거</span><span class="sxs-lookup"><span data-stu-id="05ce7-145">Remove hello application from a cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="05ce7-146">서비스 패브릭 탐색기 그래픽 사용자 인터페이스 tooexplore 이며 서비스 패브릭 클러스터에 응용 프로그램을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-146">Service Fabric Explorer is a graphical user interface tooexplore and manage applications in a Service Fabric cluster.</span></span>

<span data-ttu-id="05ce7-147">tooremove hello hello 파티 클러스터에서에서 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="05ce7-147">tooremove hello application from hello Party Cluster:</span></span>

1. <span data-ttu-id="05ce7-148">Toohello hello 파티 클러스터 등록 페이지에서 제공 하는 hello 링크를 사용 하 여 서비스 패브릭 탐색기를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-148">Browse toohello Service Fabric Explorer, using hello link provided by hello Party Cluster sign-up page.</span></span> <span data-ttu-id="05ce7-149">예를 들어 http://win1kw5649s.westus.cloudapp.azure.com:19080/Explorer/index.html입니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-149">For example, http://win1kw5649s.westus.cloudapp.azure.com:19080/Explorer/index.html.</span></span>

2. <span data-ttu-id="05ce7-150">서비스 패브릭 탐색기에서 탐색 toohello **fabric://Voting** hello 왼쪽에 hello treeview의 노드.</span><span class="sxs-lookup"><span data-stu-id="05ce7-150">In Service Fabric Explorer, navigate toohello **fabric://Voting** node in hello treeview on hello left-hand side.</span></span>

3. <span data-ttu-id="05ce7-151">Hello 클릭 **동작** hello 오른쪽의 단추 **Essentials** 창에서 선택한 **응용 프로그램 삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-151">Click hello **Action** button in hello right-hand **Essentials** pane, and choose **Delete Application**.</span></span> <span data-ttu-id="05ce7-152">Hello 클러스터에서 실행 중인 응용 프로그램의 hello 인스턴스를 제거 하는 삭제 hello 응용 프로그램 인스턴스를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-152">Confirm deleting hello application instance, which removes hello instance of our application running in hello cluster.</span></span>

![Service Fabric Explorer에서 응용 프로그램 삭제](./media/service-fabric-tutorial-deploy-app-to-party-cluster/delete-application.png)

## <a name="remove-hello-application-type-from-a-cluster-using-service-fabric-explorer"></a><span data-ttu-id="05ce7-154">서비스 패브릭 탐색기를 사용 하 여 클러스터에서 hello 응용 프로그램 종류를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-154">Remove hello application type from a cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="05ce7-155">응용 프로그램은 여러 인스턴스 및 hello 클러스터 내에서 실행 되는 hello 응용 프로그램의 버전 toohave 있습니다 수 있도록 하는 서비스 패브릭 클러스터에서 응용 프로그램 형식으로 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-155">Applications are deployed as application types in a Service Fabric cluster, which enables you toohave multiple instances and versions of hello application running within hello cluster.</span></span> <span data-ttu-id="05ce7-156">응용 프로그램의 인스턴스를 실행 하는 hello 제거도 hello 유형, hello 배포의 toocomplete hello 정리를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-156">After having removed hello running instance of our application, we can also remove hello type, toocomplete hello cleanup of hello deployment.</span></span>

<span data-ttu-id="05ce7-157">서비스 패브릭에서 hello 응용 프로그램 모델에 대 한 자세한 내용은 참조 [서비스 패브릭에서 응용 프로그램 모델](service-fabric-application-model.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-157">For more information about hello application model in Service Fabric, see [Model an application in Service Fabric](service-fabric-application-model.md).</span></span>

1. <span data-ttu-id="05ce7-158">Toohello 이동 **VotingType** hello treeview의 노드.</span><span class="sxs-lookup"><span data-stu-id="05ce7-158">Navigate toohello **VotingType** node in hello treeview.</span></span>

2. <span data-ttu-id="05ce7-159">Hello 클릭 **작업** hello 오른쪽의 단추 **Essentials** 창에서 선택한 **해제 형식**합니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-159">Click hello **Action** button in hello right-hand **Essentials** pane, and choose **Unprovision Type**.</span></span> <span data-ttu-id="05ce7-160">Hello 응용 프로그램 유형을 구축 해제를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-160">Confirm unprovisioning hello application type.</span></span>

![Service Fabric Explorer에서 응용 프로그램 형식 프로비전 해제](./media/service-fabric-tutorial-deploy-app-to-party-cluster/unprovision-type.png)

<span data-ttu-id="05ce7-162">이것으로 hello 자습서를 마칩니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-162">This concludes hello tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05ce7-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="05ce7-163">Next steps</span></span>
<span data-ttu-id="05ce7-164">이 자습서에서는 다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="05ce7-164">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="05ce7-165">Visual Studio를 사용 하 여 응용 프로그램 tooa 원격 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="05ce7-165">Deploy an application tooa remote cluster using Visual Studio</span></span>
> * <span data-ttu-id="05ce7-166">Service Fabric Explorer를 사용하여 클러스터에서 응용 프로그램 제거</span><span class="sxs-lookup"><span data-stu-id="05ce7-166">Remove an application from a cluster using Service Fabric Explorer</span></span>

<span data-ttu-id="05ce7-167">고급 toohello 다음 자습서:</span><span class="sxs-lookup"><span data-stu-id="05ce7-167">Advance toohello next tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="05ce7-168">Visual Studio Team Services를 사용하여 연속 통합 설정</span><span class="sxs-lookup"><span data-stu-id="05ce7-168">Set up continuous integration using Visual Studio Team Services</span></span>](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)