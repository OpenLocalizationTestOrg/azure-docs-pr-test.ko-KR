---
title: "Azure에서 .NET Service Fabric 응용 프로그램 만들기 | Microsoft Docs"
description: "Service Fabric 빠른 시작 샘플을 사용하여 Azure에 대한 .NET 응용 프로그램을 만듭니다."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: msfussell
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: mikhegn
ms.openlocfilehash: d11b9af982112db8ba94b62110c18be843f1abb1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-net-service-fabric-application-in-azure"></a><span data-ttu-id="f328e-103">Azure에서 .NET Service Fabric 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="f328e-103">Create a .NET Service Fabric application in Azure</span></span>
<span data-ttu-id="f328e-104">Azure Service Fabric은 확장성 있고 안정성이 뛰어난 마이크로 서비스 및 컨테이너를 배포 및 관리하기 위한 분산 시스템 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-104">Azure Service Fabric is a distributed systems platform for deploying and managing scalable and reliable microservices and containers.</span></span> 

<span data-ttu-id="f328e-105">이 빠른 시작에서는 Service Fabric에 첫 번째 .NET 응용 프로그램을 배포하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-105">This quickstart shows how to deploy your first .NET application to Service Fabric.</span></span> <span data-ttu-id="f328e-106">완료하면 투표 결과를 클러스터의 상태 저장 백 엔드 서비스에 저장하는 ASP.NET Core 웹 프런트 엔드가 있는 투표 응용 프로그램이 생깁니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-106">When you're finished, you have a voting application with an ASP.NET Core web front-end that saves voting results in a stateful back-end service in the cluster.</span></span>

![응용 프로그램 스크린샷](./media/service-fabric-quickstart-dotnet/application-screenshot.png)

<span data-ttu-id="f328e-108">이 응용 프로그램을 사용하여 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-108">Using this application you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="f328e-109">.NET 및 Service Fabric을 사용하여 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="f328e-109">Create an application using .NET and Service Fabric</span></span>
> * <span data-ttu-id="f328e-110">웹 프런트 엔드로 ASP.NET core 사용</span><span class="sxs-lookup"><span data-stu-id="f328e-110">Use ASP.NET core as a web front-end</span></span>
> * <span data-ttu-id="f328e-111">상태 저장 서비스에 응용 프로그램 데이터 저장</span><span class="sxs-lookup"><span data-stu-id="f328e-111">Store application data in a stateful service</span></span>
> * <span data-ttu-id="f328e-112">로컬에서 응용 프로그램 디버그</span><span class="sxs-lookup"><span data-stu-id="f328e-112">Debug your application locally</span></span>
> * <span data-ttu-id="f328e-113">Azure에서 응용 프로그램을 클러스터에 배포</span><span class="sxs-lookup"><span data-stu-id="f328e-113">Deploy the application to a cluster in Azure</span></span>
> * <span data-ttu-id="f328e-114">응용 프로그램을 여러 노드에 걸쳐 스케일 아웃</span><span class="sxs-lookup"><span data-stu-id="f328e-114">Scale-out the application across multiple nodes</span></span>
> * <span data-ttu-id="f328e-115">응용 프로그램 롤링 업그레이드 수행</span><span class="sxs-lookup"><span data-stu-id="f328e-115">Perform a rolling application upgrade</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f328e-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f328e-116">Prerequisites</span></span>
<span data-ttu-id="f328e-117">이 빠른 시작을 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-117">To complete this quickstart:</span></span>
1. <span data-ttu-id="f328e-118">**Azure 개발**과 **ASP.NET 및 웹 개발** 워크로드가 있는 [Visual Studio 2017 설치](https://www.visualstudio.com/)</span><span class="sxs-lookup"><span data-stu-id="f328e-118">[Install Visual Studio 2017](https://www.visualstudio.com/) with the **Azure development** and **ASP.NET and web development** workloads.</span></span>
2. [<span data-ttu-id="f328e-119">Git 설치</span><span class="sxs-lookup"><span data-stu-id="f328e-119">Install Git</span></span>](https://git-scm.com/)
3. [<span data-ttu-id="f328e-120">Microsoft Azure Service Fabric SDK 설치</span><span class="sxs-lookup"><span data-stu-id="f328e-120">Install the Microsoft Azure Service Fabric SDK</span></span>](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK)
4. <span data-ttu-id="f328e-121">다음 명령을 실행하여 Visual Studio에서 로컬 Service Fabric 클러스터에 배포하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-121">Run the following command to enable Visual Studio to deploy to the local Service Fabric cluster:</span></span>
    ```powershell
    Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
    ```

## <a name="download-the-sample"></a><span data-ttu-id="f328e-122">샘플 다운로드</span><span class="sxs-lookup"><span data-stu-id="f328e-122">Download the sample</span></span>
<span data-ttu-id="f328e-123">명령 창에서 다음 명령을 실행하여 로컬 컴퓨터에 샘플 앱 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-123">In a command window, run the following command to clone the sample app repository to your local machine.</span></span>
```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="run-the-application-locally"></a><span data-ttu-id="f328e-124">로컬에서 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="f328e-124">Run the application locally</span></span>
<span data-ttu-id="f328e-125">시작 메뉴에서 Visual Studio 아이콘을 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-125">Right-click the Visual Studio icon in the Start Menu and choose **Run as administrator**.</span></span> <span data-ttu-id="f328e-126">디버거를 서비스에 연결하려면 관리자 권한으로 Visual Studio를 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-126">In order to attach the debugger to your services, you need to run Visual Studio as administrator.</span></span>

<span data-ttu-id="f328e-127">복제한 리포지토리에서 **Voting.sln** Visual Studio 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-127">Open the **Voting.sln** Visual Studio solution from the repository you cloned.</span></span>

<span data-ttu-id="f328e-128">응용 프로그램을 배포하려면 **F5** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-128">To deploy the application, press **F5**.</span></span>

> [!NOTE]
> <span data-ttu-id="f328e-129">처음으로 응용 프로그램을 실행하고 배포할 때 Visual Studio는 디버깅을 위해 로컬 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-129">The first time you run and deploy the application, Visual Studio creates a local cluster for debugging.</span></span> <span data-ttu-id="f328e-130">이 작업에는 다소 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-130">This operation may take some time.</span></span> <span data-ttu-id="f328e-131">Visual Studio 출력 창에 클러스터 생성 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-131">The cluster creation status is displayed in the Visual Studio output window.</span></span>

<span data-ttu-id="f328e-132">배포가 완료되면 브라우저를 시작하고 응용 프로그램의 웹 프런트 엔드인 페이지(`http://localhost:8080`)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-132">When the deployment is complete, launch a browser and open this page: `http://localhost:8080` - the web front-end of the application.</span></span>

![응용 프로그램 프런트 엔드](./media/service-fabric-quickstart-dotnet/application-screenshot-new.png)

<span data-ttu-id="f328e-134">이제 투표 옵션 집합을 추가하고 투표 하기를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-134">You can now add a set of voting options, and start taking votes.</span></span> <span data-ttu-id="f328e-135">응용 프로그램이 실행되고 모든 데이터가 Service Fabric 클러스터에 저장되며 별도의 데이터베이스가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-135">The application runs and stores all data in your Service Fabric cluster, without the need for a separate database.</span></span>

## <a name="walk-through-the-voting-sample-application"></a><span data-ttu-id="f328e-136">투표 응용 프로그램 예제 연습</span><span class="sxs-lookup"><span data-stu-id="f328e-136">Walk through the voting sample application</span></span>
<span data-ttu-id="f328e-137">투표 응용 프로그램은 두 가지 서비스로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-137">The voting application consists of two services:</span></span>
- <span data-ttu-id="f328e-138">웹 프런트 엔드 서비스(VotingWeb) - ASP.NET Core 웹 프런트 엔드 서비스로, 웹 페이지를 제공하며 백 엔드 서비스와 통신하기 위한 Web API를 공개합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-138">Web front-end service (VotingWeb)- An ASP.NET Core web front-end service, which serves the web page and exposes web APIs to communicate with the backend service.</span></span>
- <span data-ttu-id="f328e-139">백 엔드 서비스(VotingData) - ASP.NET Core 웹 서비스로, 투표 결과를 디스크에 보관된 신뢰할 수 있는 사전에 저장하기 위한 API를 공개합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-139">Back-end service (VotingData)- An ASP.NET Core web service, which exposes an API to store the vote results in a reliable dictionary persisted on disk.</span></span>

![응용 프로그램 다이어그램](./media/service-fabric-quickstart-dotnet/application-diagram.png)

<span data-ttu-id="f328e-141">응용 프로그램에 투표하는 경우 다음 이벤트가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-141">When you vote in the application the following events occur:</span></span>
1. <span data-ttu-id="f328e-142">JavaScript가 투표 요청을 웹 프런트 엔드 서비스의 Web API에 HTTP PUT 요청으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-142">A JavaScript sends the vote request to the web API in the web front-end service as an HTTP PUT request.</span></span>

2. <span data-ttu-id="f328e-143">웹 프런트 엔드 서비스는 프록시를 사용하여 HTTP PUT 요청을 찾아 백 엔드 서비스에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-143">The web front-end service uses a proxy to locate and forward an HTTP PUT request to the back-end service.</span></span>

3. <span data-ttu-id="f328e-144">백 엔드 서비스는 들어오는 요청을 받고 업데이트된 결과를, 클러스터 내의 여러 노드에 복제되고 디스크에 보관된 신뢰할 수 있는 사전에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-144">The back-end service takes the incoming request, and stores the updated result in a reliable dictionary, which gets replicated to multiple nodes within the cluster and persisted on disk.</span></span> <span data-ttu-id="f328e-145">응용 프로그램의 모든 데이터가 클러스터에 저장되므로 데이터베이스가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-145">All the application's data is stored in the cluster, so no database is needed.</span></span>

## <a name="debug-in-visual-studio"></a><span data-ttu-id="f328e-146">Visual Studio에서 디버그</span><span class="sxs-lookup"><span data-stu-id="f328e-146">Debug in Visual Studio</span></span>
<span data-ttu-id="f328e-147">Visual Studio에서 응용 프로그램을 디버깅할 때 로컬 Service Fabric 개발 클러스터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-147">When debugging application in Visual Studio, you are using a local Service Fabric development cluster.</span></span> <span data-ttu-id="f328e-148">사용자 시나리오에 대해 디버깅 환경을 조정하는 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-148">You have the option to adjust your debugging experience to your scenario.</span></span> <span data-ttu-id="f328e-149">이 응용 프로그램에서는 신뢰할 수 있는 사전을 사용하여 데이터를 백 엔드 서비스에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-149">In this application, we store data in our back-end service, using a reliable dictionary.</span></span> <span data-ttu-id="f328e-150">Visual Studio는 디버거를 중지하는 경우 기본값에 대해 응용 프로그램을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-150">Visual Studio removes the application per default when you stop the debugger.</span></span> <span data-ttu-id="f328e-151">응용 프로그램을 제거하면 백 엔드 서비스의 데이터도 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-151">Removing the application causes the data in the back-end service to also be removed.</span></span> <span data-ttu-id="f328e-152">디버깅 세션 간에 데이터를 유지하려면 **응용 프로그램 디버그 모드**를 Visual Studio에서 **Voting** 프로젝트의 속성으로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-152">To persist the data between debugging sessions, you can change the **Application Debug Mode** as a property on the **Voting** project in Visual Studio.</span></span>

<span data-ttu-id="f328e-153">코드에서 수행되는 작업을 살펴보려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-153">To look at what happens in the code, complete the following steps:</span></span>
1. <span data-ttu-id="f328e-154">**VotesController.cs** 파일을 열고 Web API의 **Put** 메서드(47줄)에서 중단점을 설정합니다. Visual Studio의 솔루션 탐색기에서 파일을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-154">Open the **VotesController.cs** file and set a breakpoint in the web API's **Put** method (line 47) - You can search for the file in the Solution Explorer in Visual Studio.</span></span>

2. <span data-ttu-id="f328e-155">**VoteDataController.cs** 파일을 열고 이 Web API의 **Put** 메서드(50줄)에서 중단점을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-155">Open the **VoteDataController.cs** file and set a breakpoint in this web API's **Put** method (line 50).</span></span>

3. <span data-ttu-id="f328e-156">브라우저로 돌아가서 투표 옵션을 클릭하거나 새 투표 옵션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-156">Go back to the browser and click a voting option or add a new voting option.</span></span> <span data-ttu-id="f328e-157">웹 프런트 엔드의 api 컨트롤러에서 첫 번째 중단점에 도달합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-157">You hit the first breakpoint in the web front-end's api controller.</span></span>
    - <span data-ttu-id="f328e-158">여기서 브라우저의 JavaScript가 프런트 엔드 서비스의 Web API 컨트롤러에 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-158">This is where the JavaScript in the browser sends a request to the web API controller in the front-end service.</span></span>
    
    ![투표 프런트 엔드 서비스 추가](./media/service-fabric-quickstart-dotnet/addvote-frontend.png)

    - <span data-ttu-id="f328e-160">먼저 백 엔드 서비스 **(1)**에 대해 ReverseProxy에 대한 URL을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-160">First we construct the URL to the ReverseProxy for our back-end service **(1)**.</span></span>
    - <span data-ttu-id="f328e-161">그런 다음 ReverseProxy **(2)**에 HTTP PUT 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-161">Then we send the HTTP PUT Request to the ReverseProxy **(2)**.</span></span>
    - <span data-ttu-id="f328e-162">마지막으로로 백 엔드 서비스로부터 클라이언트 **(3)**에 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-162">Finally the we return the response from the back-end service to the client **(3)**.</span></span>

4. <span data-ttu-id="f328e-163">계속하려면 **F5** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-163">Press **F5** to continue</span></span>
    - <span data-ttu-id="f328e-164">이제 백 엔드 서비스의 중단점에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-164">You are now at the break point in the back-end service.</span></span>
    
    ![투표 백 엔드 서비스 추가](./media/service-fabric-quickstart-dotnet/addvote-backend.png)

    - <span data-ttu-id="f328e-166">메서드의 첫 번째 줄**(1)**에서는 신뢰할 수 있는 사전 `counts`를 가져오거나 추가하기 위해 `StateManager`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-166">In the first line in the method **(1)** we are using the `StateManager` to get or add a reliable dictionary called `counts`.</span></span>
    - <span data-ttu-id="f328e-167">신뢰할 수 있는 사전에 있는 값과의 모든 상호 작용에는 트랜잭션이 필요하며 using 문**(2)**으로 트랜잭션이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-167">All interactions with values in a reliable dictionary require a transaction, this using statement **(2)** creates that transaction.</span></span>
    - <span data-ttu-id="f328e-168">트랜잭션에서는 투표 옵션에 대한 관련 키 값을 업데이트하고 작업을 커밋합니다**(3)**.</span><span class="sxs-lookup"><span data-stu-id="f328e-168">In the transaction, we then update the value of the relevant key for the voting option and commits the operation **(3)**.</span></span> <span data-ttu-id="f328e-169">커밋 메서드가 반환되면 사전에 데이터가 업데이트되고 클러스터의 다른 노드에 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-169">Once the commit method returns, the data is updated in the dictionary and replicated to other nodes in the cluster.</span></span> <span data-ttu-id="f328e-170">이제 데이터는 클러스터에 안전하게 저장되며 백 엔드 서비스는 데이터를 계속 제공하면서 다른 노드로 장애 조치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-170">The data is now safely stored in the cluster, and the back-end service can fail over to other nodes, still having the data available.</span></span>
5. <span data-ttu-id="f328e-171">계속하려면 **F5** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-171">Press **F5** to continue</span></span>

<span data-ttu-id="f328e-172">디버깅 세션을 중지하려면 **Shift+F5** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-172">To stop the debugging session, press **Shift+F5**.</span></span>

## <a name="deploy-the-application-to-azure"></a><span data-ttu-id="f328e-173">Azure에 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="f328e-173">Deploy the application to Azure</span></span>
<span data-ttu-id="f328e-174">응용 프로그램을 Azure의 클러스터에 배포하려면 사용자 고유의 클러스터를 만들거나 Party 클러스터를 만들도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-174">To deploy the application to a cluster in Azure, you can either choose to create your own cluster, or use a Party Cluster.</span></span>

<span data-ttu-id="f328e-175">Party 클러스터는 평가판으로, Azure에서 호스트되고 Service Fabric 팀이 실행하는 제한 시간 Service Fabric 클러스터입니다. 여기서 누구나 응용 프로그램을 배포하고 플랫폼에 대해 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-175">Party clusters are free, limited-time Service Fabric clusters hosted on Azure and run by the Service Fabric team where anyone can deploy applications and learn about the platform.</span></span> <span data-ttu-id="f328e-176">파티 클러스터에 대한 액세스 권한을 얻으려면 [지침에 따릅니다](http://aka.ms/tryservicefabric).</span><span class="sxs-lookup"><span data-stu-id="f328e-176">To get access to a Party Cluster, [follow the instructions](http://aka.ms/tryservicefabric).</span></span> 

<span data-ttu-id="f328e-177">사용자 고유의 클러스터를 만드는 방법은 [Azure에서 첫 번째 Service Fabric 클러스터 만들기](service-fabric-get-started-azure-cluster.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f328e-177">For information about creating your own cluster, see [Create your first Service Fabric cluster on Azure](service-fabric-get-started-azure-cluster.md).</span></span>

> [!Note]
> <span data-ttu-id="f328e-178">웹 프런트 엔드 서비스는 들어오는 트래픽에 대해 포트 8080에서 수신 대기하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-178">The web front-end service is configured to listen on port 8080 for incoming traffic.</span></span> <span data-ttu-id="f328e-179">클러스터에 대해 포트가 열려 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-179">Make sure that port is open in your cluster.</span></span> <span data-ttu-id="f328e-180">Party 클러스터를 사용하는 경우 이 포트가 열려 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-180">If you are using the Party Cluster, this port is open.</span></span>
>

### <a name="deploy-the-application-using-visual-studio"></a><span data-ttu-id="f328e-181">Visual Studio를 사용하여 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="f328e-181">Deploy the application using Visual Studio</span></span>
<span data-ttu-id="f328e-182">응용 프로그램이 준비되면 Visual Studio에서 클러스터에 직접 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-182">Now that the application is ready, you can deploy it to a cluster directly from Visual Studio.</span></span>

1. <span data-ttu-id="f328e-183">솔루션 탐색기에서 **Voting**을 마우스 오른쪽 단추로 클릭하고 **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-183">Right-click **Voting** in the Solution Explorer and choose **Publish**.</span></span> <span data-ttu-id="f328e-184">[게시] 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-184">The Publish dialog appears.</span></span>

    ![[게시] 대화 상자](./media/service-fabric-quickstart-dotnet/publish-app.png)

2. <span data-ttu-id="f328e-186">**연결 끝점** 필드에 클러스터의 연결 끝점을 입력하고 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-186">Type in the Connection Endpoint of the cluster in the **Connection Endpoint** field and click **Publish**.</span></span> <span data-ttu-id="f328e-187">Party 클러스터에 등록하면 연결 끝점이 브라우저에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-187">When signing up for the Party Cluster, the Connection Endpoint is provided in the browser.</span></span> <span data-ttu-id="f328e-188">- 예를 들면 `winh1x87d1d.westus.cloudapp.azure.com:19000`입니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-188">- for example, `winh1x87d1d.westus.cloudapp.azure.com:19000`.</span></span>

3. <span data-ttu-id="f328e-189">브라우저를 열고 클러스터 주소에 입력합니다(예: `http://winh1x87d1d.westus.cloudapp.azure.com`).</span><span class="sxs-lookup"><span data-stu-id="f328e-189">Open a browser and type in the cluster address - for example, `http://winh1x87d1d.westus.cloudapp.azure.com`.</span></span> <span data-ttu-id="f328e-190">이제 Azure의 클러스터에서 실행 중인 응용 프로그램이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-190">You should now see the application running in the cluster in Azure.</span></span>

![응용 프로그램 프런트 엔드](./media/service-fabric-quickstart-dotnet/application-screenshot-new-azure.png)

## <a name="scale-applications-and-services-in-a-cluster"></a><span data-ttu-id="f328e-192">클러스터에서 응용 프로그램 및 서비스 크기 조정</span><span class="sxs-lookup"><span data-stu-id="f328e-192">Scale applications and services in a cluster</span></span>
<span data-ttu-id="f328e-193">Service Fabric 서비스는 해당 서비스에 대한 로드 변동량을 수용하도록 클러스터 간에 쉽게 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-193">Service Fabric services can easily be scaled across a cluster to accommodate for a change in the load on the services.</span></span> <span data-ttu-id="f328e-194">클러스터에서 실행되는 인스턴스 수를 변경하여 서비스 크기를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-194">You scale a service by changing the number of instances running in the cluster.</span></span> <span data-ttu-id="f328e-195">서비스의 크기를 조정하는 여러 가지 방법이 있으며 PowerShell 또는 Service Fabric CLI(sfctl)의 스크립트 또는 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-195">You have multiple ways of scaling your services, you can use scripts or commands from PowerShell or Service Fabric CLI (sfctl).</span></span> <span data-ttu-id="f328e-196">이 예제에서는 Service Fabric Explorer를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-196">In this example, we are using Service Fabric Explorer.</span></span>

<span data-ttu-id="f328e-197">Service Fabric Explorer는 모든 Service Fabric 클러스터에서 실행되고 클러스터 HTTP 관리 포트(19080)로 이동하여 브라우저에서 액세스할 수 있습니다(예: `http://winh1x87d1d.westus.cloudapp.azure.com:19080`).</span><span class="sxs-lookup"><span data-stu-id="f328e-197">Service Fabric Explorer runs in all Service Fabric clusters and can be accessed from a browser, by browsing to the clusters HTTP management port (19080), for example, `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span></span>

<span data-ttu-id="f328e-198">웹 프런트 엔드 서비스의 크기를 조정하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-198">To scale the web front-end service, do the following steps:</span></span>

1. <span data-ttu-id="f328e-199">클러스터에서 Service Fabric Explorer를 엽니다(예: `http://winh1x87d1d.westus.cloudapp.azure.com:19080`).</span><span class="sxs-lookup"><span data-stu-id="f328e-199">Open Service Fabric Explorer in your cluster - for example,`http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span></span>
2. <span data-ttu-id="f328e-200">트리 뷰에서 **fabric:/Voting/VotingWeb** 노드 옆에 있는 줄임표(...)를 클릭하고 **Scale Service**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-200">Click on the ellipsis (three dots) next to the **fabric:/Voting/VotingWeb** node in the treeview and choose **Scale Service**.</span></span>

    ![Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/service-fabric-explorer-scale.png)

    <span data-ttu-id="f328e-202">이제 웹 프런트 엔드 서비스의 인스턴스 수를 조정하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-202">You can now choose to scale the number of instances of the web front-end service.</span></span>

3. <span data-ttu-id="f328e-203">이 수를 **2**로 변경하고 **Scale Service**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-203">Change the number to **2** and click **Scale Service**.</span></span>
4. <span data-ttu-id="f328e-204">트리 뷰에서 **fabric:/Voting/VotingWeb** 노드를 클릭하고 파티션 노드(GUID로 표현됨)를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-204">Click on the **fabric:/Voting/VotingWeb** node in the tree-view and expand the partition node (represented by a GUID).</span></span>

    ![Service Fabric Explorer Scale Service](./media/service-fabric-quickstart-dotnet/service-fabric-explorer-scaled-service.png)

    <span data-ttu-id="f328e-206">이제 두 개의 인스턴스가 있는 서비스를 인스턴스가 실행되는 노드를 볼 수 있는 트리 뷰에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-206">You can now see that the service has two instances, and in the tree view you see which nodes the instances run on.</span></span>

<span data-ttu-id="f328e-207">이 간단한 관리 작업으로 사용자 로드를 처리하는 프런트 엔드 서비스에 사용 가능한 리소스를 두 배로 증가시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-207">By this simple management task, we doubled the resources available for our front-end service to process user load.</span></span> <span data-ttu-id="f328e-208">서비스를 안정적으로 실행하기 위해 서비스의 여러 인스턴스가 필요하지 않다는 것을 이해하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-208">It's important to understand that you do not need multiple instances of a service to have it run reliably.</span></span> <span data-ttu-id="f328e-209">서비스가 실패하면 Service Fabric은 클러스터에서 새 서비스 인스턴스가 실행되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-209">If a service fails, Service Fabric makes sure a new service instance runs in the cluster.</span></span>

## <a name="perform-a-rolling-application-upgrade"></a><span data-ttu-id="f328e-210">응용 프로그램 롤링 업그레이드 수행</span><span class="sxs-lookup"><span data-stu-id="f328e-210">Perform a rolling application upgrade</span></span>
<span data-ttu-id="f328e-211">새 업데이트를 응용 프로그램에 배포할 때는 Service Fabric이 안전한 방식으로 업데이트를 공개합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-211">When deploying new updates to your application, Service Fabric rolls out the update in a safe way.</span></span> <span data-ttu-id="f328e-212">롤링 업그레이드를 사용하면 업그레이드하는 동안 가동 중지 시간이 없으며 오류가 발생하면 자동화된 롤백을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-212">Rolling upgrades gives you no downtime while upgrading as well as automated rollback should errors occur.</span></span>

<span data-ttu-id="f328e-213">응용 프로그램을 업그레이드하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-213">To upgrade the application, do the following:</span></span>

1. <span data-ttu-id="f328e-214">Visual Studio에서 **Index.cshtml** 파일을 엽니다. Visual Studio의 솔루션 탐색기에서 파일을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-214">Open the **Index.cshtml** file in Visual Studio - You can search for the file in the Solution Explorer in Visual Studio.</span></span>
2. <span data-ttu-id="f328e-215">예를 들어 일부 텍스트를 추가하여 페이지 머리글을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-215">Change the heading on the page by adding some text - for example.</span></span>
    ```html
        <div class="col-xs-8 col-xs-offset-2 text-center">
            <h2>Service Fabric Voting Sample v2</h2>
        </div>
    ```
3. <span data-ttu-id="f328e-216">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-216">Save the file.</span></span>
4. <span data-ttu-id="f328e-217">솔루션 탐색기에서 **Voting**을 마우스 오른쪽 단추로 클릭하고 **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-217">Right-click **Voting** in the Solution Explorer and choose **Publish**.</span></span> <span data-ttu-id="f328e-218">[게시] 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-218">The Publish dialog appears.</span></span>
5. <span data-ttu-id="f328e-219">**매니페스트 버전** 단추를 클릭하여 서비스 및 응용 프로그램의 버전을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-219">Click the **Manifest Version** button to change the version of the service and application.</span></span>
6. <span data-ttu-id="f328e-220">**VotingWebPkg** 아래에서 **Code** 요소의 버전을, 예를 들어 “2.0.0”으로 변경하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-220">Change the version of the **Code** element under **VotingWebPkg** to "2.0.0", for example, and click **Save**.</span></span>

    ![[버전 변경] 대화 상자](./media/service-fabric-quickstart-dotnet/change-version.png)
7. <span data-ttu-id="f328e-222">**Service Fabric 응용 프로그램 게시** 대화 상자에서 [응용 프로그램 업그레이드] 확인란을 선택하고 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-222">In the **Publish Service Fabric Application** dialog, check the Upgrade the Application checkbox, and click **Publish**.</span></span>

    ![게시 대화 상자 업그레이드 설정](./media/service-fabric-quickstart-dotnet/upgrade-app.png)
8. <span data-ttu-id="f328e-224">브라우저를 열고 포트 19080에서 클러스터 주소로 이동합니다(예: `http://winh1x87d1d.westus.cloudapp.azure.com:19080`).</span><span class="sxs-lookup"><span data-stu-id="f328e-224">Open your browser and browse to the cluster address on port 19080 - for example, `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span></span>
9. <span data-ttu-id="f328e-225">트리 뷰의 **응용 프로그램** 노드를 클릭한 후 오른쪽 창에서 **Upgrades in Progress(진행 중인 업그레이드)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-225">Click on the **Applications** node in the tree view, and then **Upgrades in Progress** in the right-hand pane.</span></span> <span data-ttu-id="f328e-226">업그레이드가 클러스터에서 업그레이드 도메인을 어떻게 통과하고 다음으로 진행하기 전에 각 도메인 상태가 정상인지 확인하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-226">You see how the upgrade rolls through the upgrade domains in your cluster, making sure each domain is healthy before proceeding to the next.</span></span>
    <span data-ttu-id="f328e-227">![Service Fabric Explorer에서 업그레이드 보기](./media/service-fabric-quickstart-dotnet/upgrading.png)</span><span class="sxs-lookup"><span data-stu-id="f328e-227">![Upgrade View in Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/upgrading.png)</span></span>

    <span data-ttu-id="f328e-228">Service Fabric에서는 클러스터의 각 노드에서 서비스를 업그레이드 한 후 2분 대기함으로써 안전하게 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-228">Service Fabric makes upgrades safe by waiting two minutes after upgrading the service on each node in the cluster.</span></span> <span data-ttu-id="f328e-229">전체 업데이트에는 약 8분이 소요될 것으로 예상됩니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-229">Expect the entire update to take approximately eight minutes.</span></span>

10. <span data-ttu-id="f328e-230">업그레이드가 실행되는 동안 응용 프로그램을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-230">While the upgrade is running, you can still use the application.</span></span> <span data-ttu-id="f328e-231">클러스터에서 실행되는 서비스에는 두 인스턴스가 있으므로 일부 요청은 응용 프로그램의 업그레이드된 버전을 가질 수 있는 반면 일부는 이전 버전을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-231">Because you have two instances of the service running in the cluster, some of your requests may get an upgraded version of the application, while others may still get the old version.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f328e-232">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f328e-232">Next steps</span></span>
<span data-ttu-id="f328e-233">이 빠른 시작에서는 다음을 수행하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-233">In this quickstart, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f328e-234">.NET 및 Service Fabric을 사용하여 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="f328e-234">Create an application using .NET and Service Fabric</span></span>
> * <span data-ttu-id="f328e-235">웹 프런트 엔드로 ASP.NET core 사용</span><span class="sxs-lookup"><span data-stu-id="f328e-235">Use ASP.NET core as a web front-end</span></span>
> * <span data-ttu-id="f328e-236">상태 저장 서비스에 응용 프로그램 데이터 저장</span><span class="sxs-lookup"><span data-stu-id="f328e-236">Store application data in a stateful service</span></span>
> * <span data-ttu-id="f328e-237">로컬에서 응용 프로그램 디버그</span><span class="sxs-lookup"><span data-stu-id="f328e-237">Debug your application locally</span></span>
> * <span data-ttu-id="f328e-238">Azure에서 응용 프로그램을 클러스터에 배포</span><span class="sxs-lookup"><span data-stu-id="f328e-238">Deploy the application to a cluster in Azure</span></span>
> * <span data-ttu-id="f328e-239">응용 프로그램을 여러 노드에 걸쳐 스케일 아웃</span><span class="sxs-lookup"><span data-stu-id="f328e-239">Scale-out the application across multiple nodes</span></span>
> * <span data-ttu-id="f328e-240">응용 프로그램 롤링 업그레이드 수행</span><span class="sxs-lookup"><span data-stu-id="f328e-240">Perform a rolling application upgrade</span></span>

<span data-ttu-id="f328e-241">Service Fabric 및 .NET에 대해 자세히 알아보기 위해 다음 자습서를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f328e-241">To learn more about Service Fabric and .NET, take a look at this tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="f328e-242">Service Fabric에서 .NET 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="f328e-242">.NET application on Service Fabric</span></span>](service-fabric-tutorial-create-dotnet-app.md)