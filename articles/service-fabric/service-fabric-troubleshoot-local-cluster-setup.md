---
title: "aaaTroubleshoot 로컬 서비스 패브릭 클러스터 설치 프로그램 | Microsoft Docs"
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
ms.openlocfilehash: ce36f62a4bc69d2cd5b6c3df4abda6ca88fa84f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-your-local-development-cluster-setup"></a><span data-ttu-id="c2008-103">로컬 개발 클러스터 설정 문제 해결</span><span class="sxs-lookup"><span data-stu-id="c2008-103">Troubleshoot your local development cluster setup</span></span>
<span data-ttu-id="c2008-104">로컬 개발 Azure 서비스 패브릭 클러스터와의 상호 작용 하는 동안 문제를 실행 하면 다음 잠재적 해결 방법에 대 한 제안을 hello를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2008-104">If you run into an issue while interacting with your local Azure Service Fabric development cluster, review hello following suggestions for potential solutions.</span></span>

## <a name="cluster-setup-failures"></a><span data-ttu-id="c2008-105">클러스터 설정 오류</span><span class="sxs-lookup"><span data-stu-id="c2008-105">Cluster setup failures</span></span>
### <a name="cannot-clean-up-service-fabric-logs"></a><span data-ttu-id="c2008-106">서비스 패브릭 로그를 정리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c2008-106">Cannot clean up Service Fabric logs</span></span>
#### <a name="problem"></a><span data-ttu-id="c2008-107">문제</span><span class="sxs-lookup"><span data-stu-id="c2008-107">Problem</span></span>
<span data-ttu-id="c2008-108">Hello DevClusterSetup 스크립트를 실행 하는 동안 이와 같은 오류를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2008-108">While running hello DevClusterSetup script, you see an error like this:</span></span>

    Cannot clean up C:\SfDevCluster\Log fully as references are likely being held tooitems in it. Please remove those and run this script again.
    At line:1 char:1 + .\DevClusterSetup.ps1
    + ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,DevClusterSetup.ps1


#### <a name="solution"></a><span data-ttu-id="c2008-109">해결 방법</span><span class="sxs-lookup"><span data-stu-id="c2008-109">Solution</span></span>
<span data-ttu-id="c2008-110">현재 PowerShell 창을 hello를 관리자 권한으로 새 PowerShell 창을 닫지 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2008-110">Close hello current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="c2008-111">이제 수 toosuccessfully hello 스크립트를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2008-111">You should now be able toosuccessfully run hello script.</span></span>

## <a name="cluster-connection-failures"></a><span data-ttu-id="c2008-112">클러스터 연결 오류</span><span class="sxs-lookup"><span data-stu-id="c2008-112">Cluster connection failures</span></span>
### <a name="service-fabric-powershell-cmdlets-are-not-recognized-in-azure-powershell"></a><span data-ttu-id="c2008-113">서비스 패브릭 PowerShell cmdlet이 Azure PowerShell에서 인식되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c2008-113">Service Fabric PowerShell cmdlets are not recognized in Azure PowerShell</span></span>
#### <a name="problem"></a><span data-ttu-id="c2008-114">문제</span><span class="sxs-lookup"><span data-stu-id="c2008-114">Problem</span></span>
<span data-ttu-id="c2008-115">시도 하면 toorun hello 서비스 패브릭 PowerShell cmdlet의 예: `Connect-ServiceFabricCluster` Azure PowerShell 창에서 실패를 알리는 hello cmdlet은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c2008-115">If you try toorun any of hello Service Fabric PowerShell cmdlets, such as `Connect-ServiceFabricCluster` in an Azure PowerShell window, it fails, saying that hello cmdlet is not recognized.</span></span> <span data-ttu-id="c2008-116">hello 이유는 hello 서비스 패브릭 cmdlet에만 64 비트 환경에서 작동 하지만 Azure PowerShell (64 비트 OS 버전) 에서도 hello 32 비트 버전의 Windows PowerShell을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2008-116">hello reason for this is that Azure PowerShell uses hello 32-bit version of Windows PowerShell (even on 64-bit OS versions), whereas hello Service Fabric cmdlets only work in 64-bit environments.</span></span>

#### <a name="solution"></a><span data-ttu-id="c2008-117">해결 방법</span><span class="sxs-lookup"><span data-stu-id="c2008-117">Solution</span></span>
<span data-ttu-id="c2008-118">항상 서비스 패브릭 cmdlet을 Windows PowerShell에서 직접 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c2008-118">Always run Service Fabric cmdlets directly from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="c2008-119">더 이상 발생 해야 하므로 hello 최신 버전의 Azure PowerShell 특수 바로 가기를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c2008-119">hello latest version of Azure PowerShell does not create a special shortcut, so this should no longer occur.</span></span>
> 
> 

### <a name="type-initialization-exception"></a><span data-ttu-id="c2008-120">형식 초기화 예외</span><span class="sxs-lookup"><span data-stu-id="c2008-120">Type Initialization exception</span></span>
#### <a name="problem"></a><span data-ttu-id="c2008-121">문제</span><span class="sxs-lookup"><span data-stu-id="c2008-121">Problem</span></span>
<span data-ttu-id="c2008-122">PowerShell에서 toohello 클러스터를 연결 하는 hello 오류 TypeInitializationException System.Fabric.Common.AppTrace 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2008-122">When you are connecting toohello cluster in PowerShell, you see hello error TypeInitializationException for System.Fabric.Common.AppTrace.</span></span>

#### <a name="solution"></a><span data-ttu-id="c2008-123">해결 방법</span><span class="sxs-lookup"><span data-stu-id="c2008-123">Solution</span></span>
<span data-ttu-id="c2008-124">설치하는 동안 경로 변수가 올바르게 설정되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="c2008-124">Your path variable was not correctly set during installation.</span></span> <span data-ttu-id="c2008-125">Windows에서 로그아웃하고 다시 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c2008-125">Sign out of Windows and sign back in.</span></span> <span data-ttu-id="c2008-126">경로를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="c2008-126">This refreshes your path.</span></span>

### <a name="cluster-connection-fails-with-object-is-closed"></a><span data-ttu-id="c2008-127">“개체 닫힘"으로 인해 클러스터 연결 실패</span><span class="sxs-lookup"><span data-stu-id="c2008-127">Cluster connection fails with "Object is closed"</span></span>
#### <a name="problem"></a><span data-ttu-id="c2008-128">문제</span><span class="sxs-lookup"><span data-stu-id="c2008-128">Problem</span></span>
<span data-ttu-id="c2008-129">호출 tooConnect ServiceFabricCluster 다음과 같은 오류와 함께 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="c2008-129">A call tooConnect-ServiceFabricCluster fails with an error like this:</span></span>

    Connect-ServiceFabricCluster : hello object is closed.
    At line:1 char:1
    + Connect-ServiceFabricCluster
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : InvalidOperation: (:) [Connect-ServiceFabricCluster], FabricObjectClosedException
    + FullyQualifiedErrorId : CreateClusterConnectionErrorId,Microsoft.ServiceFabric.Powershell.ConnectCluster

#### <a name="solution"></a><span data-ttu-id="c2008-130">해결 방법</span><span class="sxs-lookup"><span data-stu-id="c2008-130">Solution</span></span>
<span data-ttu-id="c2008-131">현재 PowerShell 창을 hello를 관리자 권한으로 새 PowerShell 창을 닫지 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2008-131">Close hello current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="c2008-132">이제 있어야 toosuccessfully 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2008-132">You should now be able toosuccessfully connect.</span></span>

### <a name="fabric-connection-denied-exception"></a><span data-ttu-id="c2008-133">패브릭 연결 거부 예외</span><span class="sxs-lookup"><span data-stu-id="c2008-133">Fabric Connection Denied exception</span></span>
#### <a name="problem"></a><span data-ttu-id="c2008-134">문제</span><span class="sxs-lookup"><span data-stu-id="c2008-134">Problem</span></span>
<span data-ttu-id="c2008-135">Visual Studio에서 디버그 시 FabricConnectionDeniedException 오류가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c2008-135">When debugging from Visual Studio, you get a FabricConnectionDeniedException error.</span></span>

#### <a name="solution"></a><span data-ttu-id="c2008-136">해결 방법</span><span class="sxs-lookup"><span data-stu-id="c2008-136">Solution</span></span>
<span data-ttu-id="c2008-137">이 오류는 일반적으로 hello 서비스 패브릭 런타임에서 toostart 허용 하는 대신 toostart 서비스 호스트 프로세스를 수동으로 시도할 때 발생에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2008-137">This error usually occurs when you try toostart a service host process manually, rather than allowing hello Service Fabric runtime toostart it for you.</span></span>

<span data-ttu-id="c2008-138">솔루션에서 시작 프로젝트로 설정된 서비스 프로젝트가 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2008-138">Ensure that you do not have any service projects set as startup projects in your solution.</span></span> <span data-ttu-id="c2008-139">서비스 패브릭 응용프로그램 프로젝트만 시작 프로젝트로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2008-139">Only Service Fabric application projects should be set as startup projects.</span></span>

> [!TIP]
> <span data-ttu-id="c2008-140">설치를 수행 하는 경우에 로컬 클러스터 toobehave를 비정상적으로 시작, hello 로컬 클러스터 관리자 시스템 트레이 응용 프로그램을 사용 하 여 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2008-140">If, following setup, your local cluster begins toobehave abnormally, you can reset it using hello local cluster manager system tray application.</span></span> <span data-ttu-id="c2008-141">기존 클러스터 hello 및 새를 설정 하는이 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2008-141">This removes hello existing cluster and set up a new one.</span></span> <span data-ttu-id="c2008-142">배포된 모든 응용 프로그램 및 연결된 데이터가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2008-142">Note that all deployed applications and associated data is removed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="c2008-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c2008-143">Next steps</span></span>
* [<span data-ttu-id="c2008-144">시스템 상태 보고서와 함께 클러스터 이해 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="c2008-144">Understand and troubleshoot your cluster with system health reports</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [<span data-ttu-id="c2008-145">서비스 패브릭 탐색기로 클러스터 시각화</span><span class="sxs-lookup"><span data-stu-id="c2008-145">Visualize your cluster with Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

