---
title: "로컬 Service Fabric 클러스터 설정 문제 해결 | Microsoft Docs"
description: "이 문서에서는 로컬 개발 클러스터 문제 해결을 위한 여러 제안 사항을 다룹니다."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 97f4feaa-bba0-47af-8fdd-07f811fe2202
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: aa393f884b564cee81fcf75cc2eff895efea9471
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-your-local-development-cluster-setup"></a><span data-ttu-id="a4f72-103">로컬 개발 클러스터 설정 문제 해결</span><span class="sxs-lookup"><span data-stu-id="a4f72-103">Troubleshoot your local development cluster setup</span></span>
<span data-ttu-id="a4f72-104">로컬 Azure 서비스 패브릭 개발 클러스터와 상호 작용하는 동안 문제가 발생할 경우 다음 제안 사항에서 잠재적인 해결 방법이 있는지 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="a4f72-104">If you run into an issue while interacting with your local Azure Service Fabric development cluster, review the following suggestions for potential solutions.</span></span>

## <a name="cluster-setup-failures"></a><span data-ttu-id="a4f72-105">클러스터 설정 오류</span><span class="sxs-lookup"><span data-stu-id="a4f72-105">Cluster setup failures</span></span>
### <a name="cannot-clean-up-service-fabric-logs"></a><span data-ttu-id="a4f72-106">서비스 패브릭 로그를 정리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a4f72-106">Cannot clean up Service Fabric logs</span></span>
#### <a name="problem"></a><span data-ttu-id="a4f72-107">문제</span><span class="sxs-lookup"><span data-stu-id="a4f72-107">Problem</span></span>
<span data-ttu-id="a4f72-108">DevClusterSetup 스크립트를 실행하는 동안 다음과 같은 오류가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4f72-108">While running the DevClusterSetup script, you see an error like this:</span></span>

    Cannot clean up C:\SfDevCluster\Log fully as references are likely being held to items in it. Please remove those and run this script again.
    At line:1 char:1 + .\DevClusterSetup.ps1
    + ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,DevClusterSetup.ps1


#### <a name="solution"></a><span data-ttu-id="a4f72-109">해결 방법</span><span class="sxs-lookup"><span data-stu-id="a4f72-109">Solution</span></span>
<span data-ttu-id="a4f72-110">현재 Powershell 창을 닫고 관리자 권한으로 새 Powershell 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a4f72-110">Close the current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="a4f72-111">이제 성공적으로 스크립트를 실행할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4f72-111">You should now be able to successfully run the script.</span></span>

## <a name="cluster-connection-failures"></a><span data-ttu-id="a4f72-112">클러스터 연결 오류</span><span class="sxs-lookup"><span data-stu-id="a4f72-112">Cluster connection failures</span></span>
### <a name="service-fabric-powershell-cmdlets-are-not-recognized-in-azure-powershell"></a><span data-ttu-id="a4f72-113">서비스 패브릭 PowerShell cmdlet이 Azure PowerShell에서 인식되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a4f72-113">Service Fabric PowerShell cmdlets are not recognized in Azure PowerShell</span></span>
#### <a name="problem"></a><span data-ttu-id="a4f72-114">문제</span><span class="sxs-lookup"><span data-stu-id="a4f72-114">Problem</span></span>
<span data-ttu-id="a4f72-115">Azure PowerShell 창에서 `Connect-ServiceFabricCluster` 와 같은 서비스 패브릭 PowerShell cmdlet을 실행하려고 하면 cmdlet이 인식되지 않는다는 메시지를 표시하면서 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a4f72-115">If you try to run any of the Service Fabric PowerShell cmdlets, such as `Connect-ServiceFabricCluster` in an Azure PowerShell window, it fails, saying that the cmdlet is not recognized.</span></span> <span data-ttu-id="a4f72-116">Azure PowerShell에서는 32비트 버전의 Windows PowerShell을 사용(64비트 OS 버전에서도 동일)하는 반면 서비스 패브릭 cmdlet은 64비트 환경에서만 작동하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="a4f72-116">The reason for this is that Azure PowerShell uses the 32-bit version of Windows PowerShell (even on 64-bit OS versions), whereas the Service Fabric cmdlets only work in 64-bit environments.</span></span>

#### <a name="solution"></a><span data-ttu-id="a4f72-117">해결 방법</span><span class="sxs-lookup"><span data-stu-id="a4f72-117">Solution</span></span>
<span data-ttu-id="a4f72-118">항상 서비스 패브릭 cmdlet을 Windows PowerShell에서 직접 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a4f72-118">Always run Service Fabric cmdlets directly from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="a4f72-119">최신 버전의 Azure PowerShell에서 특수 바로 가기를 만들지 않으므로 더 이상 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a4f72-119">The latest version of Azure PowerShell does not create a special shortcut, so this should no longer occur.</span></span>
> 
> 

### <a name="type-initialization-exception"></a><span data-ttu-id="a4f72-120">형식 초기화 예외</span><span class="sxs-lookup"><span data-stu-id="a4f72-120">Type Initialization exception</span></span>
#### <a name="problem"></a><span data-ttu-id="a4f72-121">문제</span><span class="sxs-lookup"><span data-stu-id="a4f72-121">Problem</span></span>
<span data-ttu-id="a4f72-122">PowerShell에서 클러스터에 연결할 때 System.Fabric.Common.AppTrace에 대해 TypeInitializationException 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4f72-122">When you are connecting to the cluster in PowerShell, you see the error TypeInitializationException for System.Fabric.Common.AppTrace.</span></span>

#### <a name="solution"></a><span data-ttu-id="a4f72-123">해결 방법</span><span class="sxs-lookup"><span data-stu-id="a4f72-123">Solution</span></span>
<span data-ttu-id="a4f72-124">설치하는 동안 경로 변수가 올바르게 설정되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="a4f72-124">Your path variable was not correctly set during installation.</span></span> <span data-ttu-id="a4f72-125">Windows에서 로그아웃하고 다시 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a4f72-125">Sign out of Windows and sign back in.</span></span> <span data-ttu-id="a4f72-126">경로를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="a4f72-126">This refreshes your path.</span></span>

### <a name="cluster-connection-fails-with-object-is-closed"></a><span data-ttu-id="a4f72-127">“개체 닫힘"으로 인해 클러스터 연결 실패</span><span class="sxs-lookup"><span data-stu-id="a4f72-127">Cluster connection fails with "Object is closed"</span></span>
#### <a name="problem"></a><span data-ttu-id="a4f72-128">문제</span><span class="sxs-lookup"><span data-stu-id="a4f72-128">Problem</span></span>
<span data-ttu-id="a4f72-129">다음과 같은 오류와 함께 Connect-ServiceFabricCluster 호출에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="a4f72-129">A call to Connect-ServiceFabricCluster fails with an error like this:</span></span>

    Connect-ServiceFabricCluster : The object is closed.
    At line:1 char:1
    + Connect-ServiceFabricCluster
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : InvalidOperation: (:) [Connect-ServiceFabricCluster], FabricObjectClosedException
    + FullyQualifiedErrorId : CreateClusterConnectionErrorId,Microsoft.ServiceFabric.Powershell.ConnectCluster

#### <a name="solution"></a><span data-ttu-id="a4f72-130">해결 방법</span><span class="sxs-lookup"><span data-stu-id="a4f72-130">Solution</span></span>
<span data-ttu-id="a4f72-131">현재 Powershell 창을 닫고 관리자 권한으로 새 Powershell 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a4f72-131">Close the current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="a4f72-132">이제 성공적으로 연결할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4f72-132">You should now be able to successfully connect.</span></span>

### <a name="fabric-connection-denied-exception"></a><span data-ttu-id="a4f72-133">패브릭 연결 거부 예외</span><span class="sxs-lookup"><span data-stu-id="a4f72-133">Fabric Connection Denied exception</span></span>
#### <a name="problem"></a><span data-ttu-id="a4f72-134">문제</span><span class="sxs-lookup"><span data-stu-id="a4f72-134">Problem</span></span>
<span data-ttu-id="a4f72-135">Visual Studio에서 디버그 시 FabricConnectionDeniedException 오류가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a4f72-135">When debugging from Visual Studio, you get a FabricConnectionDeniedException error.</span></span>

#### <a name="solution"></a><span data-ttu-id="a4f72-136">해결 방법</span><span class="sxs-lookup"><span data-stu-id="a4f72-136">Solution</span></span>
<span data-ttu-id="a4f72-137">이 오류는 일반적으로 Service Fabric 런타임이 자동으로 시작되게 하는 대신 서비스 호스트 프로세스를 수동으로 시작하려고 할 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="a4f72-137">This error usually occurs when you try to start a service host process manually, rather than allowing the Service Fabric runtime to start it for you.</span></span>

<span data-ttu-id="a4f72-138">솔루션에서 시작 프로젝트로 설정된 서비스 프로젝트가 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4f72-138">Ensure that you do not have any service projects set as startup projects in your solution.</span></span> <span data-ttu-id="a4f72-139">서비스 패브릭 응용프로그램 프로젝트만 시작 프로젝트로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4f72-139">Only Service Fabric application projects should be set as startup projects.</span></span>

> [!TIP]
> <span data-ttu-id="a4f72-140">설치를 수행할 때 로컬 클러스터가 비정상적으로 동작을 시작하는 경우 로컬 클러스터 관리자 시스템 트레이 응용 프로그램을 사용하여 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4f72-140">If, following setup, your local cluster begins to behave abnormally, you can reset it using the local cluster manager system tray application.</span></span> <span data-ttu-id="a4f72-141">기존 클러스터를 제거하고 새로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a4f72-141">This removes the existing cluster and set up a new one.</span></span> <span data-ttu-id="a4f72-142">배포된 모든 응용 프로그램 및 연결된 데이터가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4f72-142">Note that all deployed applications and associated data is removed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a4f72-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a4f72-143">Next steps</span></span>
* [<span data-ttu-id="a4f72-144">시스템 상태 보고서와 함께 클러스터 이해 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="a4f72-144">Understand and troubleshoot your cluster with system health reports</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [<span data-ttu-id="a4f72-145">서비스 패브릭 탐색기로 클러스터 시각화</span><span class="sxs-lookup"><span data-stu-id="a4f72-145">Visualize your cluster with Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

