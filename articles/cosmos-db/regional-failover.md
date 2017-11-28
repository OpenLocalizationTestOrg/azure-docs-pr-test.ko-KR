---
title: "Azure Cosmos DB에서 장애 조치 aaaRegional | Microsoft Docs"
description: "Azure Cosmos DB에서 수동 및 자동 장애 조치(failover)가 작동하는 방식에 대해 알아봅니다."
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: 446e2580-ff49-4485-8e53-ae34e08d997f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/24/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d2fdc7b0e8958d129ab027e4b11193b12961ddae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automatic-regional-failover-for-business-continuity-in-azure-cosmos-db"></a><span data-ttu-id="517f1-103">비즈니스 연속성을 위한 Azure Cosmos DB의 자동 지역별 장애 조치(failover)</span><span class="sxs-lookup"><span data-stu-id="517f1-103">Automatic regional failover for business continuity in Azure Cosmos DB</span></span>
<span data-ttu-id="517f1-104">Azure Cosmos DB hello 글로벌 데이터 배포를 제공 하 여 단순화 완전히 관리 [다중 지역 데이터베이스 계정](distribute-data-globally.md) 일관성, 가용성 및 성능에 해당 하는 포함 된 모든 간 지우기 균형을 제공 하는 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-104">Azure Cosmos DB simplifies hello global distribution of data by offering fully managed, [multi-region database accounts](distribute-data-globally.md) that provide clear tradeoffs between consistency, availability, and performance, all with corresponding guarantees.</span></span> <span data-ttu-id="517f1-105">Cosmos DB 계정을 제공 고가용성을 단일 숫자 ms 대기 시간, [잘 정의 된 일관성 수준이](consistency-levels.md), 멀티 호 밍 Api hello 기능 tooelastically 배율 처리량 및 저장소 지역 투명 한 장애 조치 hello 전세계 합니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-105">Cosmos DB accounts offer high availability, single digit ms latencies, [well-defined consistency levels](consistency-levels.md), transparent regional failover with multi-homing APIs, and hello ability tooelastically scale throughput and storage across hello globe.</span></span> 

<span data-ttu-id="517f1-106">Cosmos DB 명시적 모두 지원, 정책 기반 장애 조치 하는 수 toocontrol hello 종단 간 시스템 동작은 실패의 hello 이벤트에서.</span><span class="sxs-lookup"><span data-stu-id="517f1-106">Cosmos DB supports both explicit and policy driven failovers that allow you toocontrol hello end-to-end system behavior in hello event of failures.</span></span> <span data-ttu-id="517f1-107">이 문서에서 다음을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-107">In this article, we look at:</span></span>

* <span data-ttu-id="517f1-108">수동 장애 조치(failover)가 Cosmos DB에서 작동하는 방식</span><span class="sxs-lookup"><span data-stu-id="517f1-108">How do manual failovers work in Cosmos DB?</span></span>
* <span data-ttu-id="517f1-109">Cosmos DB에서 자동 장애 조치(failover)가 작동하는 방식 및 데이터 센터가 다운될 때 발생하는 결과</span><span class="sxs-lookup"><span data-stu-id="517f1-109">How do automatic failovers work in Cosmos DB and what happens when a data center goes down?</span></span>
* <span data-ttu-id="517f1-110">응용 프로그램 아키텍처에서 수동 장애 조치를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="517f1-110">How can you use manual failovers in application architectures?</span></span>

<span data-ttu-id="517f1-111">Scott Hanselman과 수석 엔지니어링 관리자 Karthik Raman이 진행하는 이 Azure Friday 비디오를 통해 지역 장애 조치에 대해서도 자세히 알아 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-111">You can also learn about regional failovers in this Azure Friday video with Scott Hanselman and Principal Engineering Manager Karthik Raman.</span></span>

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

## <span data-ttu-id="517f1-112"><a id="ConfigureMultiRegionApplications"></a>다중 지역 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="517f1-112"><a id="ConfigureMultiRegionApplications"></a>Configuring multi-region applications</span></span>
<span data-ttu-id="517f1-113">장애 조치 모드에 들어가기 전에 다중 지역 가용성의 응용 프로그램 tootake 장점은 구성 국가별 장애 조치의 hello 면에서 복원 하는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-113">Before we dive into failover modes, we look at how you can configure an application tootake advantage of multi-region availability and be resilient in hello face of regional failovers.</span></span>

* <span data-ttu-id="517f1-114">먼저 여러 지역에 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-114">First, deploy your application in multiple regions</span></span>
* <span data-ttu-id="517f1-115">응용 프로그램을 배포한 모든 지역에서 대기 시간이 짧은 액세스 tooensure hello에 해당 구성 [기본 지역 목록](https://msdn.microsoft.com/library/microsoft.azure.documents.client.connectionpolicy.preferredlocations.aspx#P:Microsoft.Azure.Documents.Client.ConnectionPolicy.PreferredLocations) hello 중 하나를 통해 각 지역의 지원 되는 Sdk에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-115">tooensure low latency access from every region your application is deployed, configure hello corresponding [preferred regions list](https://msdn.microsoft.com/library/microsoft.azure.documents.client.connectionpolicy.preferredlocations.aspx#P:Microsoft.Azure.Documents.Client.ConnectionPolicy.PreferredLocations) for each region via one of hello supported SDKs.</span></span>

<span data-ttu-id="517f1-116">조각과 방법을 따르는 hello tooinitialize 다중 지역 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-116">hello following snippet shows how tooinitialize a multi-region application.</span></span> <span data-ttu-id="517f1-117">여기에서는 Azure Cosmos DB 계정 hello `contoso.documents.azure.com` 두 영역-유럽 북부 및 미국 서 부로 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-117">Here, hello Azure Cosmos DB account `contoso.documents.azure.com` is configured with two regions - West US and North Europe.</span></span> 

* <span data-ttu-id="517f1-118">hello 응용 프로그램 (예: Azure 응용 프로그램 서비스 사용) hello 미국 서 부 지역에 배포 되어</span><span class="sxs-lookup"><span data-stu-id="517f1-118">hello application is deployed in hello West US region (using Azure App Services for example)</span></span> 
* <span data-ttu-id="517f1-119">구성 된 `West US` hello 짧은 대기 시간에 대 한 첫 번째 기본 영역으로 읽기</span><span class="sxs-lookup"><span data-stu-id="517f1-119">Configured with `West US` as hello first preferred region for low latency reads</span></span>
* <span data-ttu-id="517f1-120">구성 된 `North Europe` hello (국가별 실패 하는 동안 고가용성)에 대 한 두 번째 기본 영역으로</span><span class="sxs-lookup"><span data-stu-id="517f1-120">Configured with `North Europe` as hello second preferred region (for high availability during regional failures)</span></span>

<span data-ttu-id="517f1-121">DocumentDB API hello,이 구성은 다음 코드 조각 hello 같습니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-121">In hello DocumentDB API, this configuration looks like hello following snippet:</span></span>

```cs
ConnectionPolicy usConnectionPolicy = new ConnectionPolicy 
{ 
    ConnectionMode = ConnectionMode.Direct,
    ConnectionProtocol = Protocol.Tcp
};

usConnectionPolicy.PreferredLocations.Add(LocationNames.WestUS);
usConnectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope);

DocumentClient usClient = new DocumentClient(
    new Uri("https://contosodb.documents.azure.com"),
    "memf7qfF89n6KL9vcb7rIQl6tfgZsRt5gY5dh3BIjesarJanYIcg2Edn9uPOUIVwgkAugOb2zUdCR2h0PTtMrA==",
    usConnectionPolicy);
```

hello 응용 프로그램은도 hello 순서를 반대로 하는 기본 지역에 hello 유럽 북부 지역에 배포 됩니다. 즉, 짧은 대기 시간 읽기에 대 한 hello 북부 유럽 지역의 먼저 지정 됩니다. <span data-ttu-id="517f1-124">그런 다음 hello 미국 서 부 지역 국가별 실패 하는 동안 고가용성을 위해 두 번째 기본 영역은 hello로 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-124">Then, hello West US region is specified as hello second preferred region for high availability during regional failures.</span></span>

<span data-ttu-id="517f1-125">hello 다음 아키텍처 다이어그램은 다중 지역 응용 프로그램 배포를 있는 보여 줍니다 Cosmos DB 및 hello 응용 프로그램 구성된 toobe Azure 4 개의 지리적 지역에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-125">hello following architecture diagram shows a multi-region application deployment where Cosmos DB and hello application are configured toobe available in four Azure geographic regions.</span></span>  

![Azure Cosmos DB를 통해 전역으로 분산된 응용 프로그램 배포](./media/regional-failover/app-deployment.png)

<span data-ttu-id="517f1-127">이제 hello Cosmos DB 서비스에서 자동 장애 조치를 통해 지역 오류를 처리 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-127">Now, let's look at how hello Cosmos DB service handles regional failures via automatic failovers.</span></span> 

## <span data-ttu-id="517f1-128"><a id="AutomaticFailovers"></a>자동 장애 조치</span><span class="sxs-lookup"><span data-stu-id="517f1-128"><a id="AutomaticFailovers"></a>Automatic Failovers</span></span>
<span data-ttu-id="517f1-129">Azure 지역 가동 중단 또는 데이터 센터 중단의 hello 드문 이벤트에서 Cosmos DB 영향을 받는 hello 지역에 있으면 모든 Cosmos DB 계정의 장애 조치를 자동으로 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-129">In hello rare event of an Azure regional outage or data center outage, Cosmos DB automatically triggers failovers of all Cosmos DB accounts with a presence in hello affected region.</span></span> 

<span data-ttu-id="517f1-130">**읽기 지역에 가동 중단이 발생하면 어떻게 됩니까?**</span><span class="sxs-lookup"><span data-stu-id="517f1-130">**What happens if a read region has an outage?**</span></span>

<span data-ttu-id="517f1-131">Cosmos DB 계정은 hello 영향을 받는 영역 중 하나에 있는 읽기 영역으로는 자동으로 해당 쓰기 지역에서 연결이 끊어지고 오프 라인으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-131">Cosmos DB accounts with a read region in one of hello affected regions are automatically disconnected from their write region and marked offline.</span></span> <span data-ttu-id="517f1-132">hello Cosmos DB Sdk 구현 tooautomatically 수 있게 해 주는 국가별 검색 프로토콜 영역에 사용할 수 있고 리디렉션 호출 toohello 다음 사용 가능한 지역 hello 기본 지역 목록에서 읽기를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-132">hello Cosmos DB SDKs implement a regional discovery protocol that allows them tooautomatically detect when a region is available and redirect read calls toohello next available region in hello preferred region list.</span></span> <span data-ttu-id="517f1-133">Hello의 hello 영역 중 우선 지역 목록을 사용할 수 있는, 호출 자동으로 대체할 toohello 현재 쓰기 지역.</span><span class="sxs-lookup"><span data-stu-id="517f1-133">If none of hello regions in hello preferred region list is available, calls automatically fall back toohello current write region.</span></span> <span data-ttu-id="517f1-134">응용 프로그램 코드 toohandle 국가별 장애 변경 없이 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-134">No changes are required in your application code toohandle regional failovers.</span></span> <span data-ttu-id="517f1-135">이 전체 프로세스 동안 일관성 보증이 toobe Cosmos DB에 의해 적용을 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-135">During this entire process, consistency guarantees continue toobe honored by Cosmos DB.</span></span>

![Azure Cosmos DB의 읽기 지역 장애](./media/regional-failover/read-region-failures.png)

<span data-ttu-id="517f1-137">Hello 영향을 받는 영역 hello 중단에서 복구 되 면 hello 지역에 있는 모든 영향을 받는 hello Cosmos DB 계정은 hello 서비스에 의해 자동으로 복구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-137">Once hello affected region recovers from hello outage, all hello affected Cosmos DB accounts in hello region are automatically recovered by hello service.</span></span> <span data-ttu-id="517f1-138">Cosmos DB 계정 hello 영향을 받는 영역에 읽기 영역을 보유 한 다음 자동으로 현재 쓰기 지역와 동기화 하 고 온라인 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-138">Cosmos DB accounts that had a read region in hello affected region will then automatically sync with current write region and turn online.</span></span> <span data-ttu-id="517f1-139">hello Cosmos DB Sdk hello 가용성 hello 새 영역을 찾아 hello 현재 읽기 영역 hello 응용 프로그램에서 구성한 hello 기본 영역 목록을 기반으로 hello 영역을 선택 해야 하는지 여부를 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-139">hello Cosmos DB SDKs discover hello availability of hello new region and evaluate whether hello region should be selected as hello current read region based on hello preferred region list configured by hello application.</span></span> <span data-ttu-id="517f1-140">후속 읽기는 변경 내용을 tooyour 응용 프로그램 코드를 사용할 필요 없이 리디렉션된 toohello 복구 된 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-140">Subsequent reads are redirected toohello recovered region without requiring any changes tooyour application code.</span></span>

<span data-ttu-id="517f1-141">**쓰기 지역에 가동 중단이 발생하면 어떻게 됩니까?**</span><span class="sxs-lookup"><span data-stu-id="517f1-141">**What happens if a write region has an outage?**</span></span>

<span data-ttu-id="517f1-142">지정한 Cosmos DB 계정에 대 한 현재 쓰기 영역 hello hello 영향을 받은 영역을 사용 하는 경우 다음 hello 지역 자동으로 표시될지 오프 라인으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-142">If hello affected region is hello current write region for a given Cosmos DB account, then hello region will be automatically marked as offline.</span></span> <span data-ttu-id="517f1-143">그런 다음 대체 지역은 hello 영향을 받는 각 Cosmos DB 계정 영역을 작성할 때 수준이 올려집니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-143">Then, an alternative region is promoted as hello write region each affected Cosmos DB account.</span></span> <span data-ttu-id="517f1-144">Hello Azure 포털을 통해 프로그램 Cosmos DB 계정에 대 한 hello 지역 선택 순서를 완벽 하 게 제어할 수 있습니다 또는 [프로그래밍 방식으로](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_FailoverPriorityChange)합니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-144">You can fully control hello region selection order for your Cosmos DB accounts via hello Azure portal or [programmatically](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_FailoverPriorityChange).</span></span> 

![Azure Cosmos DB의 장애 조치(failover) 우선 순위](./media/regional-failover/failover-priorities.png)

<span data-ttu-id="517f1-146">자동 장애 조치 하는 동안 Cosmos DB 자동으로 선택 hello 다음 쓰기 영역 지정한 Cosmos DB에 대 한 계정 hello에 따라 우선 순위 순서를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-146">During automatic failovers, Cosmos DB automatically chooses hello next write region for a given Cosmos DB account based on hello specified priority order.</span></span> 

![Azure Cosmos DB의 쓰기 지역 장애](./media/regional-failover/write-region-failures.png)

<span data-ttu-id="517f1-148">Hello 영향을 받는 영역 hello 중단에서 복구 되 면 hello 지역에 있는 모든 영향을 받는 hello Cosmos DB 계정은 hello 서비스에 의해 자동으로 복구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-148">Once hello affected region recovers from hello outage, all hello affected Cosmos DB accounts in hello region are automatically recovered by hello service.</span></span> 

* <span data-ttu-id="517f1-149">해당 이전 쓰기 지역 hello 영향을 받는 영역에 있는 DB cosmos 계정 hello 영역의 hello 복구 후에 오프 라인 모드에서 읽기 가용성은 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-149">Cosmos DB accounts with their previous write region in hello affected region will stay in an offline mode with read availability even after hello recovery of hello region.</span></span> 
* <span data-ttu-id="517f1-150">쿼리할 수 있습니다이 지역 toocompute 복제 되지 않은 한 쓰기가 hello 비활성 동안 hello hello 현재 쓰기 지역에서 사용할 수 있는 데이터와 비교 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-150">You can query this region toocompute any unreplicated writes during hello outage by comparing with hello data available in hello current write region.</span></span> <span data-ttu-id="517f1-151">응용 프로그램의 hello 요구에 따라, 병합 및/또는 충돌 해결을 수행 하 고 hello 최종 집합 변경 내용 다시 toohello 현재 쓰기 영역을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-151">Based on hello needs of your application, you can perform merge and/or conflict resolution and write hello final set of changes back toohello current write region.</span></span> 
* <span data-ttu-id="517f1-152">병합 변경 내용을 마친 후 있습니다 수 hello 영향을 받는 영역 다시 온라인 상태로 전환 제거 하 고 hello 지역 tooyour Cosmos DB 계정에 다시 추가 중입니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-152">Once you've completed merging changes, you can bring hello affected region back online by removing and readding hello region tooyour Cosmos DB account.</span></span> <span data-ttu-id="517f1-153">Hello 영역 다시 추가 되 면 구성할 수 있습니다 hello 쓰기 지역 변수로 다시 hello Azure 포털을 통해 수동 장애 조치를 수행 하 여 또는 [프로그래밍 방식으로](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_CreateOrUpdate)합니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-153">Once hello region is added back, you can configure it back as hello write region by performing a manual failover via hello Azure portal or [programmatically](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_CreateOrUpdate).</span></span>

## <span data-ttu-id="517f1-154"><a id="ManualFailovers"></a>수동 장애 조치</span><span class="sxs-lookup"><span data-stu-id="517f1-154"><a id="ManualFailovers"></a>Manual Failovers</span></span>

<span data-ttu-id="517f1-155">또한 현재 hello tooautomatic 장애 조치 지정한 Cosmos DB 계정의 지역 수동으로 동적 변경할 수 hello 기존 읽기 영역의 tooone을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-155">In addition tooautomatic failovers, hello current write region of a given Cosmos DB account can be manually changed dynamically tooone of hello existing read regions.</span></span> <span data-ttu-id="517f1-156">Hello Azure 포털을 통해 수동 장애 조치를 시작할 수 있습니다 또는 [프로그래밍 방식으로](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_CreateOrUpdate)합니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-156">Manual failovers can be initiated via hello Azure portal or [programmatically](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_CreateOrUpdate).</span></span> 

<span data-ttu-id="517f1-157">수동 장애 조치 되도록 **데이터 손실을 0** 및 **가용성 0** 손실 되 고 정상적으로 이전 hello에서 전송 쓰기 상태 쓰기 지역 toohello 새 hello 지정한 Cosmos DB 계정에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-157">Manual failovers ensure **zero data loss** and **zero availability** loss and gracefully transfer write status from hello old write region toohello new one for hello specified Cosmos DB account.</span></span> <span data-ttu-id="517f1-158">자동 장애 조치 Cosmos DB SDK를 자동으로 hello와 같은 지역 수동 장애 조치 중에 변경 및 호출을 자동으로 리디렉션된 toohello 새 쓰기 영역 핸들 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-158">Like in automatic failovers, hello Cosmos DB SDK automatically handles write region changes during manual failovers and ensures that calls are automatically redirected toohello new write region.</span></span> <span data-ttu-id="517f1-159">응용 프로그램 toomanage 장애 코드 또는 구성 변경 내용이 없습니다 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-159">No code or configuration changes are required in your application toomanage failovers.</span></span> 

![Azure Cosmos DB에서의 수동 장애 조치(failover)](./media/regional-failover/manual-failovers.png)

<span data-ttu-id="517f1-161">수동 장애 조치 유용할 수 있습니다 hello 일반적인 시나리오는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-161">Some of hello common scenarios where manual failover can be useful are:</span></span>

<span data-ttu-id="517f1-162">**Hello 클록 모델**: 응용 프로그램 hello hello 시간에 따라 예측 가능한 트래픽 패턴을 있으면 hello 쓰기 상태 toohello 가장 활동적인 지리적 지역 hello 하루 중 시간에 따라 주기적으로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-162">**Follow hello clock model**: If your applications have predictable traffic patterns based on hello time of hello day, you can periodically change hello write status toohello most active geographic region based on time of hello day.</span></span>

<span data-ttu-id="517f1-163">**서비스 업데이트**: 특정 전 세계적으로 분산된 응용 프로그램 배포의 계획 된 서비스 업데이트 하는 동안 트래픽 관리자를 통해 트래픽을 toodifferent 영역 경로 재정의 해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-163">**Service update**: Certain globally distributed application deployment may involve rerouting traffic toodifferent region via traffic manager during their planned service update.</span></span> <span data-ttu-id="517f1-164">이제 이러한 응용 프로그램 배포에 있는 되기 toobe 활성 트래픽 hello 서비스 업데이트 기간 동안 수동 장애 조치 tookeep hello 쓰기 상태 toohello 영역을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-164">Such application deployment now can use manual failover tookeep hello write status toohello region where there is going toobe active traffic during hello service update window.</span></span>

<span data-ttu-id="517f1-165">**BCDR(비즈니스 연속성 및 재해 복구) 및 HADR(고가용성 및 재해 복구) 절차** - 대부분의 엔터프라이즈 응용 프로그램에는 개발 및 릴리스 프로세스의 일부로 비즈니스 연속성 테스트가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-165">**Business Continuity and Disaster Recovery (BCDR) and High Availability and Disaster Recovery (HADR) drills**: Most enterprise applications include business continuity tests as part of their development and release process.</span></span> <span data-ttu-id="517f1-166">BCDR 및 HADR 테스트 종종는 규정 준수 인증의 중요 한 단계 및 지역 가동 중단의 hello 경우에서 서비스 가용성을 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-166">BCDR and HADR testing is often an important step in compliance certifications and guaranteeing service availability in hello case of regional outages.</span></span> <span data-ttu-id="517f1-167">Cosmos DB 계정의 수동 장애 조치를 트리거하 및/또는 추가 및 영역을 동적으로 제거 하 여 저장소에 대 한 Cosmos DB를 사용 하는 응용 프로그램의 hello BCDR 준비 상태를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-167">You can test hello BCDR readiness of your applications that use Cosmos DB for storage by triggering a manual failover of your Cosmos DB account and/or adding and removing a region dynamically.</span></span>

<span data-ttu-id="517f1-168">이 문서에서는 Cosmos DB에서 어떻게 수동 및 자동 장애 조치 작업 및 사용자 Cosmos DB 계정 및 응용 프로그램 toobe 전체적으로 사용 가능한 구성 하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="517f1-168">In this article, we reviewed how manual and automatic failovers work in Cosmos DB, and how you can configure your Cosmos DB accounts and applications toobe globally available.</span></span> <span data-ttu-id="517f1-169">Cosmos DB의 전체 복제 지원을 사용 하 여 종단 간 대기 시간을 향상 시킬 수 있으며 지역 오류의 hello 이벤트에도 항상 사용 가능한 되는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="517f1-169">By using Cosmos DB's global replication support, you can improve end-to-end latency and ensure that they are highly available even in hello event of region failures.</span></span> 

## <span data-ttu-id="517f1-170"><a id="NextSteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="517f1-170"><a id="NextSteps"></a>Next Steps</span></span>
* <span data-ttu-id="517f1-171">Cosmos DB에서 [글로벌 배포](distribute-data-globally.md)를 지원하는 방법에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="517f1-171">Learn about how Cosmos DB supports [global distribution](distribute-data-globally.md)</span></span>
* <span data-ttu-id="517f1-172">[Azure Cosmos DB를 통한 전역 일관성](consistency-levels.md)에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="517f1-172">Learn about [global consistency with Azure Cosmos DB](consistency-levels.md)</span></span>
* <span data-ttu-id="517f1-173">Azure Cosmos DB의 [DocumentDB API](../cosmos-db/tutorial-global-distribution-documentdb.md)를 사용하여 여러 지역으로 개발</span><span class="sxs-lookup"><span data-stu-id="517f1-173">Develop with multiple regions using Azure Cosmos DB's [DocumentDB API](../cosmos-db/tutorial-global-distribution-documentdb.md)</span></span>
* <span data-ttu-id="517f1-174">자세한 내용은 방법 toobuild [다중 지역 기록기 아키텍처](multi-region-writers.md) Azure documentdb</span><span class="sxs-lookup"><span data-stu-id="517f1-174">Learn how toobuild [Multi-region writer architectures](multi-region-writers.md) with Azure DocumentDB</span></span>

