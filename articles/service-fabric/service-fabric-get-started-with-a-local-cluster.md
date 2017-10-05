---
title: "Azure 마이크로 서비스 로컬로 배포 및 업그레이드 | Microsoft Docs"
description: "로컬 서비스 패브릭 클러스터를 설정하고 기존 응용 프로그램을 거기에 배포한 다음 해당 응용 프로그램을 업그레이드하는방법을 알아봅니다."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 60a1f6a5-5478-46c0-80a8-18fe62da17a8
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi;mikhegn
ms.openlocfilehash: 359677972c7e1fa3f7435052021ddfae5b1ed85e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-deploying-and-upgrading-applications-on-your-local-cluster"></a><span data-ttu-id="bb0fc-103">로컬 클러스터에서 응용 프로그램 배포 및 업그레이드 시작</span><span class="sxs-lookup"><span data-stu-id="bb0fc-103">Get started with deploying and upgrading applications on your local cluster</span></span>
<span data-ttu-id="bb0fc-104">Azure 서비스 패브릭 SDK에서는 전체 로컬 개발 환경을 포함하고 로컬 클러스터에서 응용 프로그램을 배포 및 관리하는 작업을 빠르게 시작하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-104">The Azure Service Fabric SDK includes a full local development environment that you can use to quickly get started with deploying and managing applications on a local cluster.</span></span> <span data-ttu-id="bb0fc-105">이 문서에서는 Windows PowerShell에서 로컬 클러스터를 만들고 기존 응용 프로그램을 거기에 배포한 다음 새 버전으로 해당 응용 프로그램을 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-105">In this article, you create a local cluster, deploy an existing application to it, and then upgrade that application to a new version, all from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="bb0fc-106">이 문서는 이미 [개발 환경을 설정](service-fabric-get-started.md)한 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-106">This article assumes that you already [set up your development environment](service-fabric-get-started.md).</span></span>
> 
> 

## <a name="create-a-local-cluster"></a><span data-ttu-id="bb0fc-107">로컬 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="bb0fc-107">Create a local cluster</span></span>
<span data-ttu-id="bb0fc-108">서비스 패브릭 클러스터는 응용 프로그램을 배포할 수 있는 하드웨어 리소스의 집합을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-108">A Service Fabric cluster represents a set of hardware resources that you can deploy applications to.</span></span> <span data-ttu-id="bb0fc-109">일반적으로 클러스터는 다섯 대부터 수천 대에 이르는 컴퓨터로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-109">Typically, a cluster is made up of anywhere from five to many thousands of machines.</span></span> <span data-ttu-id="bb0fc-110">그러나 서비스 패브릭 SDK는 단일 컴퓨터에서 실행할 수 있는 클러스터 구성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-110">However, the Service Fabric SDK includes a cluster configuration that can run on a single machine.</span></span>

<span data-ttu-id="bb0fc-111">서비스 패브릭 로컬 클러스터는 에뮬레이터 또는 시뮬레이터가 아니라는 점을 이해하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-111">It is important to understand that the Service Fabric local cluster is not an emulator or simulator.</span></span> <span data-ttu-id="bb0fc-112">다중 컴퓨터 클러스터에 있는 동일한 플랫폼 코드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-112">It runs the same platform code that is found on multi-machine clusters.</span></span> <span data-ttu-id="bb0fc-113">유일한 차이점은 한 컴퓨터에 다섯 대의 컴퓨터에 분산된 플랫폼 프로세스를 실행한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-113">The only difference is that it runs the platform processes that are normally spread across five machines on one machine.</span></span>

<span data-ttu-id="bb0fc-114">SDK는 Windows PowerShell 스크립트 및 로컬 클러스터 관리자 시스템 트레이 앱과 같이 로컬 클러스터를 설치하는 두 가지 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-114">The SDK provides two ways to set up a local cluster: a Windows PowerShell script and the Local Cluster Manager system tray app.</span></span> <span data-ttu-id="bb0fc-115">이 자습서에서는 PowerShell 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-115">In this tutorial, we use the PowerShell script.</span></span>

> [!NOTE]
> <span data-ttu-id="bb0fc-116">Visual Studio에서 응용 프로그램을 배포하여 이미 로컬 클러스터를 만든 경우 이 섹션을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-116">If you have already created a local cluster by deploying an application from Visual Studio, you can skip this section.</span></span>
> 
> 

1. <span data-ttu-id="bb0fc-117">새 PowerShell 창을 관리자 권한으로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-117">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="bb0fc-118">SDK 폴더에서 클러스터 설치 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-118">Run the cluster setup script from the SDK folder:</span></span>
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"
    ```
   
    <span data-ttu-id="bb0fc-119">클러스터 설치는 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-119">Cluster setup takes a few moments.</span></span> <span data-ttu-id="bb0fc-120">설치가 완료된 후 다음과 같은 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-120">After setup is finished, you should see output similar to:</span></span>
   
    ![클러스터 설정 출력][cluster-setup-success]
   
    <span data-ttu-id="bb0fc-122">이제 클러스터에 응용 프로그램 배포를 시도할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-122">You are now ready to try deploying an application to your cluster.</span></span>

## <a name="deploy-an-application"></a><span data-ttu-id="bb0fc-123">응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="bb0fc-123">Deploy an application</span></span>
<span data-ttu-id="bb0fc-124">서비스 패브릭 SDK는 응용 프로그램을 만들기 위한 다양한 개발자 도구 및 프레임워크의 집합을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-124">The Service Fabric SDK includes a rich set of frameworks and developer tooling for creating applications.</span></span> <span data-ttu-id="bb0fc-125">Visual Studio에서 응용 프로그램을 만드는 방법에 관심이 있는 경우 [Visual Studio에서 서비스 패브릭 응용 프로그램 처음 만들기](service-fabric-create-your-first-application-in-visual-studio.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-125">If you are interested in learning how to create applications in Visual Studio, see [Create your first Service Fabric application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span></span>

<span data-ttu-id="bb0fc-126">이 자습서에서는 기존 샘플 응용 프로그램(WordCount라고 함)을 사용하므로 플랫폼의 관리 측면인 배포, 모니터링 및 업그레이드에 중점을 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-126">In this tutorial, you use an existing sample application (called WordCount) so that you can focus on the management aspects of the platform: deployment, monitoring, and upgrade.</span></span>

1. <span data-ttu-id="bb0fc-127">새 PowerShell 창을 관리자 권한으로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-127">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="bb0fc-128">서비스 패브릭 SDK PowerShell 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-128">Import the Service Fabric SDK PowerShell module.</span></span>
   
    ```powershell
    Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
    ```
3. <span data-ttu-id="bb0fc-129">다운로드하고 배포할 응용 프로그램을 저장할 디렉터리(예: C:\ServiceFabric)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-129">Create a directory to store the application that you download and deploy, such as C:\ServiceFabric.</span></span>
   
    ```powershell
    mkdir c:\ServiceFabric\
    cd c:\ServiceFabric\
    ```
4. <span data-ttu-id="bb0fc-130">[WordCount 응용 프로그램을 다운로드](http://aka.ms/servicefabric-wordcountapp) 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-130">[Download the WordCount application](http://aka.ms/servicefabric-wordcountapp) to the location you created.</span></span>  <span data-ttu-id="bb0fc-131">참고: Microsoft Edge 브라우저는 *.zip* 으로 확장된 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-131">Note: the Microsoft Edge browser saves the file with a *.zip* extension.</span></span>  <span data-ttu-id="bb0fc-132">파일 확장명을 *.sfpkg*로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-132">Change the file extension to *.sfpkg*.</span></span>
5. <span data-ttu-id="bb0fc-133">로컬 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-133">Connect to the local cluster:</span></span>
   
    ```powershell
    Connect-ServiceFabricCluster localhost:19000
    ```
6. <span data-ttu-id="bb0fc-134">이름 및 응용 프로그램 패키지에 대한 경로와 함께 SDK의 배포 명령을 사용하여 새 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-134">Create a new application using the SDK's deployment command with a name and a path to the application package.</span></span>
   
    ```powershell  
   Publish-NewServiceFabricApplication -ApplicationPackagePath c:\ServiceFabric\WordCountV1.sfpkg -ApplicationName "fabric:/WordCount"
    ```
   
    <span data-ttu-id="bb0fc-135">정상적으로 작동하면 다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-135">If all goes well, you should see the following output:</span></span>
   
    ![로컬 클러스터에 응용 프로그램 배포][deploy-app-to-local-cluster]
7. <span data-ttu-id="bb0fc-137">작업에서 응용 프로그램을 보려면 브라우저를 시작하고 [http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-137">To see the application in action, launch the browser and navigate to [http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html).</span></span> <span data-ttu-id="bb0fc-138">다음과 같은 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-138">You should see:</span></span>
   
    ![배포된 응용 프로그램 UI][deployed-app-ui]
   
    <span data-ttu-id="bb0fc-140">WordCount 응용 프로그램은 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-140">The WordCount application is simple.</span></span> <span data-ttu-id="bb0fc-141">클라이언트쪽 JavaScript 코드를 포함하여 임의의 다섯 개의 문자 "words"를 생성하며 이는 ASP.NET Web API를 통해 응용 프로그램에 릴레이됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-141">It includes client-side JavaScript code to generate random five-character "words", which are then relayed to the application via ASP.NET Web API.</span></span> <span data-ttu-id="bb0fc-142">상태 저장 서비스는 계산된 단어의 수를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-142">A stateful service tracks the number of words counted.</span></span> <span data-ttu-id="bb0fc-143">단어의 첫 번째 문자를 기준으로 분할됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-143">They are partitioned based on the first character of the word.</span></span> <span data-ttu-id="bb0fc-144">[클래식 샘플 시작](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount)에서 WordCount 앱에 대한 소스 코드를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-144">You can find the source code for the WordCount app in the [classic getting started samples](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).</span></span>
   
    <span data-ttu-id="bb0fc-145">배포된 응용 프로그램은 네 개의 파티션을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-145">The application that we deployed contains four partitions.</span></span> <span data-ttu-id="bb0fc-146">그러므로 A부터 G로 시작하는 단어는 첫 번째 파티션에 저장되고 H부터 N까지로 시작하는 단어는 두 번째 파티션에 저장되는 방식으로 계속됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-146">So words beginning with A through G are stored in the first partition, words beginning with H through N are stored in the second partition, and so on.</span></span>

## <a name="view-application-details-and-status"></a><span data-ttu-id="bb0fc-147">응용 프로그램 세부 정보 및 상태 보기</span><span class="sxs-lookup"><span data-stu-id="bb0fc-147">View application details and status</span></span>
<span data-ttu-id="bb0fc-148">응용 프로그램을 배포하였으므로 PowerShell의 앱 세부 정보 중 일부를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-148">Now that we have deployed the application, let's look at some of the app details in PowerShell.</span></span>

1. <span data-ttu-id="bb0fc-149">클러스터에 배포된 모든 응용 프로그램을 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-149">Query all deployed applications on the cluster:</span></span>
   
    ```powershell
    Get-ServiceFabricApplication
    ```
   
    <span data-ttu-id="bb0fc-150">WordCount 앱만 배포했다고 가정하면 다음과 같은 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-150">Assuming that you have only deployed the WordCount app, you see something similar to:</span></span>
   
    ![PowerShell에 배포된 모든 응용 프로그램 쿼리][ps-getsfapp]
2. <span data-ttu-id="bb0fc-152">WordCount 응용 프로그램에 포함된 서비스 집합을 쿼리하여 다음 수준으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-152">Go to the next level by querying the set of services that are included in the WordCount application.</span></span>
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![PowerShell에서 응용 프로그램에 대한 서비스 목록][ps-getsfsvc]
   
    <span data-ttu-id="bb0fc-154">응용 프로그램은 두 서비스, 즉 웹 프런트 엔드 및 단어를 관리하는 상태 저장 서비스로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-154">The application is made up of two services, the web front end, and the stateful service that manages the words.</span></span>
3. <span data-ttu-id="bb0fc-155">마지막으로 WordCountService에 대한 파티션의 목록을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-155">Finally, look at the list of partitions for WordCountService:</span></span>
   
    ```powershell
    Get-ServiceFabricPartition 'fabric:/WordCount/WordCountService'
    ```
   
    ![PowerShell에서 서비스 파티션 보기][ps-getsfpartitions]
   
    <span data-ttu-id="bb0fc-157">모든 서비스 패브릭 PowerShell 명령처럼 사용된 명령 집합은 로컬 또는 원격에 연결할 수 있는 모든 클러스터에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-157">The set of commands that you used, like all Service Fabric PowerShell commands, are available for any cluster that you might connect to, local or remote.</span></span>
   
    <span data-ttu-id="bb0fc-158">클러스터와의 상호 작용하는 보다 시각적인 방법의 경우 브라우저의 [http://localhost:19080/Explorer](http://localhost:19080/Explorer) 로 이동하여 웹 기반 서비스 패브릭 탐색기 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-158">For a more visual way to interact with the cluster, you can use the web-based Service Fabric Explorer tool by navigating to [http://localhost:19080/Explorer](http://localhost:19080/Explorer) in the browser.</span></span>
   
    ![서비스 패브릭 탐색기에서 응용 프로그램 세부 정보 보기][sfx-service-overview]
   
   > [!NOTE]
   > <span data-ttu-id="bb0fc-160">Service Fabric Explorer에 대해 자세히 알아보려면 [Service Fabric Explorer를 사용하여 클러스터 시각화](service-fabric-visualizing-your-cluster.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-160">To learn more about Service Fabric Explorer, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
   > 
   > 

## <a name="upgrade-an-application"></a><span data-ttu-id="bb0fc-161">응용 프로그램 업그레이드</span><span class="sxs-lookup"><span data-stu-id="bb0fc-161">Upgrade an application</span></span>
<span data-ttu-id="bb0fc-162">서비스 패브릭은 클러스터 전체에 걸쳐 롤백되므로 응용 프로그램의 상태를 모니터링하여 가동 중지 업그레이드가 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-162">Service Fabric provides no-downtime upgrades by monitoring the health of the application as it rolls out across the cluster.</span></span> <span data-ttu-id="bb0fc-163">WordCount 응용 프로그램 업그레이드를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-163">Perform an upgrade of the WordCount application.</span></span>

<span data-ttu-id="bb0fc-164">응용 프로그램의 새 버전은 모음으로 시작하는 단어만 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-164">The new version of the application now counts only words that begin with a vowel.</span></span> <span data-ttu-id="bb0fc-165">업그레이드가 출시되면 응용 프로그램의 동작에 두 가지 변경 사항이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-165">As the upgrade rolls out, we see two changes in the application's behavior.</span></span> <span data-ttu-id="bb0fc-166">첫째, 적은 단어 수가 계산되므로 수가 증가하면 속도는 느려져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-166">First, the rate at which the count grows should slow, since fewer words are being counted.</span></span> <span data-ttu-id="bb0fc-167">둘째, 첫 번째 파티션에 두 개의 모음(A 및 E)이 있고 다른 모든 파티션이 각각 하나만 포함하므로 결국 개수가 다른 파티션을 앞서도록 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-167">Second, since the first partition has two vowels (A and E) and all other partitions contain only one each, its count should eventually start to outpace the others.</span></span>

1. <span data-ttu-id="bb0fc-168">버전 1 패키지를 다운로드한 동일한 위치에 [WordCount 버전 2 패키지를 다운로드](http://aka.ms/servicefabric-wordcountappv2) 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-168">[Download the WordCount version 2 package](http://aka.ms/servicefabric-wordcountappv2) to the same location where you downloaded the version 1 package.</span></span>
2. <span data-ttu-id="bb0fc-169">PowerShell 창으로 돌아가서 SDK의 업그레이드 명령을 사용하여 클러스터의 새 버전을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-169">Return to your PowerShell window and use the SDK's upgrade command to register the new version in the cluster.</span></span> <span data-ttu-id="bb0fc-170">그런 다음 fabric:/WordCount 응용 프로그램을 업그레이드하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-170">Then begin upgrading the fabric:/WordCount application.</span></span>
   
    ```powershell
    Publish-UpgradedServiceFabricApplication -ApplicationPackagePath C:\ServiceFabric\WordCountV2.sfpkg -ApplicationName "fabric:/WordCount" -UpgradeParameters @{"FailureAction"="Rollback"; "UpgradeReplicaSetCheckTimeout"=1; "Monitored"=$true; "Force"=$true}
    ```
   
    <span data-ttu-id="bb0fc-171">업그레이드가 시작되면 PowerShell에 다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-171">You should see the following output in PowerShell as the upgrade begins.</span></span>
   
    ![PowerShell에서 업그레이드 진행률][ps-appupgradeprogress]
3. <span data-ttu-id="bb0fc-173">업그레이드를 진행하는 동안 서비스 패브릭 탐색기에서 해당 상태를 모니터링하는 작업이 쉬워집니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-173">While the upgrade is proceeding, you may find it easier to monitor its status from Service Fabric Explorer.</span></span> <span data-ttu-id="bb0fc-174">브라우저 창을 시작하고 [http://localhost:19080/Explorer](http://localhost:19080/Explorer)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-174">Launch a browser window and navigate to [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="bb0fc-175">왼쪽의 트리에서 **응용 프로그램**을 선택한 다음 **WordCount**, **패브릭:/WordCount**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-175">Expand **Applications** in the tree on the left, then choose **WordCount**, and finally **fabric:/WordCount**.</span></span> <span data-ttu-id="bb0fc-176">필수 탭에서 클러스터의 업그레이드 도메인을 통해 진행될 때 업그레이드의 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-176">In the essentials tab, you see the status of the upgrade as it proceeds through the cluster's upgrade domains.</span></span>
   
    ![서비스 패브릭 탐색기에서 업그레이드 진행][sfx-upgradeprogress]
   
    <span data-ttu-id="bb0fc-178">각 도메인을 통해 업그레이드가 진행될 때 응용 프로그램이 제대로 작동되도록 상태 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-178">As the upgrade proceeds through each domain, health checks are performed to ensure that the application is behaving properly.</span></span>
4. <span data-ttu-id="bb0fc-179">fabric:/WordCount 응용 프로그램에 있는 서비스의 집합에 대한 이전 쿼리를 다시 실행하는 경우 WordCountService 버전이 변경되지만 WordCountWebService 버전은 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-179">If you rerun the earlier query for the set of services in the fabric:/WordCount application, notice that the WordCountService version changed but the WordCountWebService version did not:</span></span>
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![업그레이드 후 응용 프로그램 서비스 쿼리][ps-getsfsvc-postupgrade]
   
    <span data-ttu-id="bb0fc-181">이 예제는 Service Fabric이 응용 프로그램 업그레이드를 관리하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-181">This example highlights how Service Fabric manages application upgrades.</span></span> <span data-ttu-id="bb0fc-182">이렇게 하면 이는 변경된 서비스 집합(또는 해당 서비스 내에서 코드/구성 패키지)을 터치하고 보다 빠르고 안정적으로 업그레이드 프로세스를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-182">It touches only the set of services (or code/configuration packages within those services) that have changed, which makes the process of upgrading faster and more reliable.</span></span>
5. <span data-ttu-id="bb0fc-183">마지막으로 브라우저로 돌아와서 응용 프로그램의 새 버전의 동작을 관찰합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-183">Finally, return to the browser to observe the behavior of the new application version.</span></span> <span data-ttu-id="bb0fc-184">예상된 대로 개수 프로세스는 느려지고 첫 번째 파티션은 볼륨이 더 증가하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-184">As expected, the count progresses more slowly, and the first partition ends up with slightly more of the volume.</span></span>
   
    ![브라우저에서 응용 프로그램의 새 버전 보기][deployed-app-ui-v2]

## <a name="cleaning-up"></a><span data-ttu-id="bb0fc-186">정리</span><span class="sxs-lookup"><span data-stu-id="bb0fc-186">Cleaning up</span></span>
<span data-ttu-id="bb0fc-187">마무리하기 전에, 로컬 클러스터가 존재한다는 것을 기억하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-187">Before wrapping up, it's important to remember that the local cluster is real.</span></span> <span data-ttu-id="bb0fc-188">응용 프로그램은 제거될 때까지 백그라운드에서 계속 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-188">Applications continue to run in the background until you remove them.</span></span>  <span data-ttu-id="bb0fc-189">앱의 특성에 따라서, 앱을 실행하면 컴퓨터에서 상당한 리소스를 차지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-189">Depending on the nature of your apps, a running app can take up significant resources on your machine.</span></span> <span data-ttu-id="bb0fc-190">응용 프로그램과 클러스터를 관리하는 몇 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-190">You have several options to manage applications and the cluster:</span></span>

1. <span data-ttu-id="bb0fc-191">개별 응용 프로그램 및 모든 데이터를 제거하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-191">To remove an individual application and all it's data, run the following command:</span></span>
   
    ```powershell
    Unpublish-ServiceFabricApplication -ApplicationName "fabric:/WordCount"
    ```
   
    <span data-ttu-id="bb0fc-192">또는 Service Fabric Explorer **ACTIONS** 메뉴 또는 왼쪽 창 응용 프로그램 목록 보기에 있는 상황에 맞는 메뉴에서 응용 프로그램을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-192">Or, delete the application from the Service Fabric Explorer **ACTIONS** menu or the context menu in the left-hand application list view.</span></span>
   
    ![서비스 패브릭 탐색기에서 응용 프로그램 삭제][sfe-delete-application]
2. <span data-ttu-id="bb0fc-194">클러스터에서 응용 프로그램을 삭제한 후에 WordCount 응용 프로그램 형식의 버전 1.0.0 및 2.0.0의 등록을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-194">After deleting the application from the cluster, unregister versions 1.0.0 and 2.0.0 of the WordCount application type.</span></span> <span data-ttu-id="bb0fc-195">삭제하면 클러스터 이미지 저장소에서 코드와 구성을 포함한 응용 프로그램 패키지를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-195">Deletion removes the application packages, including the code and configuration, from the cluster's image store.</span></span>
   
    ```powershell
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 2.0.0
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 1.0.0
    ```
   
    <span data-ttu-id="bb0fc-196">또는 Service Fabric Explorer에서 응용 프로그램에 **프로비전 해제 형식** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-196">Or, in Service Fabric Explorer, choose **Unprovision Type** for the application.</span></span>
3. <span data-ttu-id="bb0fc-197">클러스터는 끄되 응용 프로그램 데이터와 추적은 유지하려면 시스템 트레이 앱에서 **로컬 클러스터 중지** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-197">To shut down the cluster but keep the application data and traces, click **Stop Local Cluster** in the system tray app.</span></span>
4. <span data-ttu-id="bb0fc-198">클러스터를 완전히 제거하려면 시스템 트레이 앱에서 **로컬 클러스터 제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-198">To delete the cluster entirely, click **Remove Local Cluster** in the system tray app.</span></span> <span data-ttu-id="bb0fc-199">다음에 Visual Studio에서 F5 키를 누르면 이 옵션이 다른 느린 배포를 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-199">This option will result in another slow deployment the next time you press F5 in Visual Studio.</span></span> <span data-ttu-id="bb0fc-200">일정 시간 동안 로컬 클러스터를 사용하지 않거나 또는 리소스를 확보해야 할 경우에만 로컬 클러스트를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-200">Remove the local cluster only if you don't intend to use it for some time or if you need to reclaim resources.</span></span>

## <a name="one-node-and-five-node-cluster-mode"></a><span data-ttu-id="bb0fc-201">1개 노드 및 5개 노드 클러스터 모드</span><span class="sxs-lookup"><span data-stu-id="bb0fc-201">One-node and five-node cluster mode</span></span>
<span data-ttu-id="bb0fc-202">응용 프로그램을 개발할 때 종종 코드 작성, 디버깅, 코드 변경, 디버깅을 빠르게 반복하여 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-202">When developing applications, you often find yourself doing quick iterations of writing code, debugging, changing code, and debugging.</span></span> <span data-ttu-id="bb0fc-203">이 프로세스를 최적화할 수 있기 위해 로컬 클러스터는 1개 노드 및 5개 노드 등 두 가지 모드에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-203">To help optimize this process, the local cluster can run in two modes: one-node or five-node.</span></span> <span data-ttu-id="bb0fc-204">클러스터 모드는 모두 해당되는 혜택이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-204">Both cluster modes have their benefits.</span></span> <span data-ttu-id="bb0fc-205">5개 노드 클러스터 모드를 사용하면 실제 클러스터와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-205">Five-node cluster mode enables you to work with a real cluster.</span></span> <span data-ttu-id="bb0fc-206">장애 조치 시나리오를 테스트하고 더 많은 인스턴스 및 서비스의 복제본을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-206">You can test failover scenarios, work with more instances and replicas of your services.</span></span> <span data-ttu-id="bb0fc-207">1개 노드 클러스터 모드는 서비스를 빠르게 배포하고 등록하는 데 최적화되어 Service Fabric 런타임을 사용하여 신속하게 코드의 유효성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-207">One-node cluster mode is optimized to do quick deployment and registration of services, to help you quickly validate code using the Service Fabric runtime.</span></span>

<span data-ttu-id="bb0fc-208">1개 노드 클러스터 또는 5개 노드 클러스터 모드 모두 에뮬레이터 또는 시뮬레이터가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-208">Neither one-node cluster or five-node cluster modes are an emulator or simulator.</span></span> <span data-ttu-id="bb0fc-209">컬 개발 클러스터는 다중 컴퓨터 클러스터에 있는 동일한 플랫폼 코드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-209">The local development cluster runs the same platform code that is found on multi-machine clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="bb0fc-210">클러스터 모드를 변경할 때 현재 클러스터가 시스템에서 제거되고 새 클러스터가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-210">When you change the cluster mode, the current cluster is removed from your system and a new cluster is created.</span></span> <span data-ttu-id="bb0fc-211">클러스터 모드를 변경할 때 클러스터에 저장해야 하는 데이터가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-211">The data stored in the cluster is deleted when you change cluster mode.</span></span>
> 
> 

<span data-ttu-id="bb0fc-212">모드를 1개 노드 클러스터로 변경하려면 Service Fabric Local Cluster Manager에서 **클러스터 모드 전환**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-212">To change the mode to one-node cluster, select **Switch Cluster Mode** in the Service Fabric Local Cluster Manager.</span></span>

![클러스터 모드 전환][switch-cluster-mode]

<span data-ttu-id="bb0fc-214">또는 PowerShell을 사용하여 클러스터 모드를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-214">Or, change the cluster mode using PowerShell:</span></span>

1. <span data-ttu-id="bb0fc-215">새 PowerShell 창을 관리자 권한으로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-215">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="bb0fc-216">SDK 폴더에서 클러스터 설치 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-216">Run the cluster setup script from the SDK folder:</span></span>
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1" -CreateOneNodeCluster
    ```
   
    <span data-ttu-id="bb0fc-217">클러스터 설치는 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-217">Cluster setup takes a few moments.</span></span> <span data-ttu-id="bb0fc-218">설치가 완료된 후 다음과 같은 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-218">After setup is finished, you should see output similar to:</span></span>
   
    ![클러스터 설정 출력][cluster-setup-success-1-node]

## <a name="next-steps"></a><span data-ttu-id="bb0fc-220">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bb0fc-220">Next steps</span></span>
* <span data-ttu-id="bb0fc-221">미리 작성된 응용 프로그램을 배포하고 업그레이드했으니 [Visual Studio에서 응용 프로그램 빌드](service-fabric-create-your-first-application-in-visual-studio.md)를 수행해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-221">Now that you have deployed and upgraded some pre-built applications, you can [try building your own in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span></span>
* <span data-ttu-id="bb0fc-222">이 문서의 로컬 클러스터에 수행된 작업은 모두 [Azure 클러스터](service-fabric-cluster-creation-via-portal.md) 에서도 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-222">All the actions performed on the local cluster in this article can be performed on an [Azure cluster](service-fabric-cluster-creation-via-portal.md) as well.</span></span>
* <span data-ttu-id="bb0fc-223">이 문서에서 수행된 업그레이드는 기본이었습니다.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-223">The upgrade that we performed in this article was basic.</span></span> <span data-ttu-id="bb0fc-224">서비스 패브릭 업그레이드의 성능과 유연성에 대해 자세히 알아보려면 [업그레이드 설명서](service-fabric-application-upgrade.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bb0fc-224">See the [upgrade documentation](service-fabric-application-upgrade.md) to learn more about the power and flexibility of Service Fabric upgrades.</span></span>

<!-- Images -->

[cluster-setup-success]: ./media/service-fabric-get-started-with-a-local-cluster/LocalClusterSetup.png
[extracted-app-package]: ./media/service-fabric-get-started-with-a-local-cluster/ExtractedAppPackage.png
[deploy-app-to-local-cluster]: ./media/service-fabric-get-started-with-a-local-cluster/DeployAppToLocalCluster.png
[deployed-app-ui]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-v1.png
[deployed-app-ui-v2]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-PostUpgrade.png
[sfx-app-instance]: ./media/service-fabric-get-started-with-a-local-cluster/SfxAppInstance.png
[sfx-two-app-instances-different-partitions]: ./media/service-fabric-get-started-with-a-local-cluster/SfxTwoAppInstances-DifferentPartitionCount.png
[ps-getsfapp]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFApp.png
[ps-getsfsvc]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc.png
[ps-getsfpartitions]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFPartitions.png
[ps-appupgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/PS-AppUpgradeProgress.png
[ps-getsfsvc-postupgrade]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc-PostUpgrade.png
[sfx-upgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/SfxUpgradeOverview.png
[sfx-service-overview]: ./media/service-fabric-get-started-with-a-local-cluster/sfx-service-overview.png
[sfe-delete-application]: ./media/service-fabric-get-started-with-a-local-cluster/sfe-delete-application.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
[switch-cluster-mode]: ./media/service-fabric-get-started-with-a-local-cluster/switch-cluster-mode.png
