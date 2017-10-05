---
title: "Azure Cosmos DB의 지역별 장애 조치(failover) | Microsoft Docs"
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
ms.openlocfilehash: 3d8ba08bc9f99cb77c9f03949fc5db299eb222c8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="automatic-regional-failover-for-business-continuity-in-azure-cosmos-db"></a><span data-ttu-id="0877d-103">비즈니스 연속성을 위한 Azure Cosmos DB의 자동 지역별 장애 조치(failover)</span><span class="sxs-lookup"><span data-stu-id="0877d-103">Automatic regional failover for business continuity in Azure Cosmos DB</span></span>
<span data-ttu-id="0877d-104">Azure Cosmos DB는 일관성, 가용성, 성능을 적절히 보증하면서 서로 간에 명확히 절충하는 완전 관리형 [다중 지역 데이터베이스 계정](distribute-data-globally.md)을 제공하여 글로벌 데이터 배포를 단순화합니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-104">Azure Cosmos DB simplifies the global distribution of data by offering fully managed, [multi-region database accounts](distribute-data-globally.md) that provide clear tradeoffs between consistency, availability, and performance, all with corresponding guarantees.</span></span> <span data-ttu-id="0877d-105">Cosmos DB 계정은 고가용성, 짧은 대기 시간(한 자릿수 ms), [잘 정의된 일관성 수준](consistency-levels.md), multi-homing API를 사용한 투명한 지역별 장애 조치(failover) 및 전 세계적으로 처리량과 저장소를 탄력적으로 확장할 수 있는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-105">Cosmos DB accounts offer high availability, single digit ms latencies, [well-defined consistency levels](consistency-levels.md), transparent regional failover with multi-homing APIs, and the ability to elastically scale throughput and storage across the globe.</span></span> 

<span data-ttu-id="0877d-106">Cosmos DB는 명시적 장애 조치(failover)와 정책 기반 장애 조치를 둘 다 지원하므로 장애 발생 시 종단 간 시스템 동작을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-106">Cosmos DB supports both explicit and policy driven failovers that allow you to control the end-to-end system behavior in the event of failures.</span></span> <span data-ttu-id="0877d-107">이 문서에서 다음을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-107">In this article, we look at:</span></span>

* <span data-ttu-id="0877d-108">수동 장애 조치(failover)가 Cosmos DB에서 작동하는 방식</span><span class="sxs-lookup"><span data-stu-id="0877d-108">How do manual failovers work in Cosmos DB?</span></span>
* <span data-ttu-id="0877d-109">Cosmos DB에서 자동 장애 조치(failover)가 작동하는 방식 및 데이터 센터가 다운될 때 발생하는 결과</span><span class="sxs-lookup"><span data-stu-id="0877d-109">How do automatic failovers work in Cosmos DB and what happens when a data center goes down?</span></span>
* <span data-ttu-id="0877d-110">응용 프로그램 아키텍처에서 수동 장애 조치를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="0877d-110">How can you use manual failovers in application architectures?</span></span>

<span data-ttu-id="0877d-111">Scott Hanselman과 수석 엔지니어링 관리자 Karthik Raman이 진행하는 이 Azure Friday 비디오를 통해 지역 장애 조치에 대해서도 자세히 알아 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-111">You can also learn about regional failovers in this Azure Friday video with Scott Hanselman and Principal Engineering Manager Karthik Raman.</span></span>

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

## <span data-ttu-id="0877d-112"><a id="ConfigureMultiRegionApplications"></a>다중 지역 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="0877d-112"><a id="ConfigureMultiRegionApplications"></a>Configuring multi-region applications</span></span>
<span data-ttu-id="0877d-113">장애 조치 모드로 들어가기 전에 지역별 장애 조치에 직면하여 다중 지역 가용성을 활용하고 탄력적으로 대처할 수 있도록 응용 프로그램을 구성하는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-113">Before we dive into failover modes, we look at how you can configure an application to take advantage of multi-region availability and be resilient in the face of regional failovers.</span></span>

* <span data-ttu-id="0877d-114">먼저 여러 지역에 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-114">First, deploy your application in multiple regions</span></span>
* <span data-ttu-id="0877d-115">응용 프로그램이 배포된 모든 지역에서 짧은 대기 시간 액세스를 보장하려면 지원되는 SDK 중 하나를 통해 각 지역에 해당하는 [기본 지역 목록](https://msdn.microsoft.com/library/microsoft.azure.documents.client.connectionpolicy.preferredlocations.aspx#P:Microsoft.Azure.Documents.Client.ConnectionPolicy.PreferredLocations)을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-115">To ensure low latency access from every region your application is deployed, configure the corresponding [preferred regions list](https://msdn.microsoft.com/library/microsoft.azure.documents.client.connectionpolicy.preferredlocations.aspx#P:Microsoft.Azure.Documents.Client.ConnectionPolicy.PreferredLocations) for each region via one of the supported SDKs.</span></span>

<span data-ttu-id="0877d-116">다음 코드 조각에서는 다중 지역 응용 프로그램을 초기화하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-116">The following snippet shows how to initialize a multi-region application.</span></span> <span data-ttu-id="0877d-117">여기서는 Azure Cosmos DB 계정 `contoso.documents.azure.com`이 미국 서부와 북유럽의 두 지역으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-117">Here, the Azure Cosmos DB account `contoso.documents.azure.com` is configured with two regions - West US and North Europe.</span></span> 

* <span data-ttu-id="0877d-118">응용 프로그램은 미국 서부 지역에 배포됩니다(예: Azure App Services 사용).</span><span class="sxs-lookup"><span data-stu-id="0877d-118">The application is deployed in the West US region (using Azure App Services for example)</span></span> 
* <span data-ttu-id="0877d-119">`West US`가 짧은 대기 시간 읽기를 위해 첫 번째 기본 지역으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-119">Configured with `West US` as the first preferred region for low latency reads</span></span>
* <span data-ttu-id="0877d-120">`North Europe`이 지역 장애 시의 고가용성을 위해 두 번째 기본 지역으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-120">Configured with `North Europe` as the second preferred region (for high availability during regional failures)</span></span>

<span data-ttu-id="0877d-121">DocumentDB API에서 이 구성은 다음 코드 조각과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-121">In the DocumentDB API, this configuration looks like the following snippet:</span></span>

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

또한 응용 프로그램이 기본 지역의 순서를 바꿔 북유럽 지역에도 배포됩니다. 즉 북유럽 지역이 짧은 대기 시간 읽기에 대해 첫 번째로 지정됩니다. <span data-ttu-id="0877d-124">그런 다음 미국 서부 지역이 지역 장애 시 고가용성을 위해 두 번째 기본 지역으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-124">Then, the West US region is specified as the second preferred region for high availability during regional failures.</span></span>

<span data-ttu-id="0877d-125">다음 아키텍처 다이어그램에서는 Cosmos DB 및 응용 프로그램이 4개의 Azure 지리적 하위 지역에서 사용할 수 있도록 구성된 다중 지역 응용 프로그램 배포를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-125">The following architecture diagram shows a multi-region application deployment where Cosmos DB and the application are configured to be available in four Azure geographic regions.</span></span>  

![Azure Cosmos DB를 통해 전역으로 분산된 응용 프로그램 배포](./media/regional-failover/app-deployment.png)

<span data-ttu-id="0877d-127">이제 Cosmos DB 서비스에서 자동 장애 조치(failover)를 통해 지역 장애를 처리하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-127">Now, let's look at how the Cosmos DB service handles regional failures via automatic failovers.</span></span> 

## <span data-ttu-id="0877d-128"><a id="AutomaticFailovers"></a>자동 장애 조치</span><span class="sxs-lookup"><span data-stu-id="0877d-128"><a id="AutomaticFailovers"></a>Automatic Failovers</span></span>
<span data-ttu-id="0877d-129">드물게 발생하는 Azure 지역 가동 중단 또는 데이터 센터 가동 중단의 경우 Cosmos DB는 영향을 받은 지역에 있는 모든 Cosmos DB 계정의 장애 조치를 자동으로 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-129">In the rare event of an Azure regional outage or data center outage, Cosmos DB automatically triggers failovers of all Cosmos DB accounts with a presence in the affected region.</span></span> 

<span data-ttu-id="0877d-130">**읽기 지역에 가동 중단이 발생하면 어떻게 됩니까?**</span><span class="sxs-lookup"><span data-stu-id="0877d-130">**What happens if a read region has an outage?**</span></span>

<span data-ttu-id="0877d-131">영향을 받은 지역 중 하나에 읽기 지역이 있는 Cosmos DB 계정은 자동으로 쓰기 지역과의 연결이 끊어지고 오프라인으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-131">Cosmos DB accounts with a read region in one of the affected regions are automatically disconnected from their write region and marked offline.</span></span> <span data-ttu-id="0877d-132">Cosmos DB SDK에서 지역 검색 프로토콜을 구현하여 지역을 사용할 수 있는 시기를 자동으로 감지하고 기본 지역 목록에서 사용 가능한 다음 지역으로 읽기 호출을 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-132">The Cosmos DB SDKs implement a regional discovery protocol that allows them to automatically detect when a region is available and redirect read calls to the next available region in the preferred region list.</span></span> <span data-ttu-id="0877d-133">기본 지역 목록의 어느 지역도 사용할 수 없는 경우 호출은 현재 쓰기 지역으로 자동으로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-133">If none of the regions in the preferred region list is available, calls automatically fall back to the current write region.</span></span> <span data-ttu-id="0877d-134">지역별 장애 조치를 처리하기 위해 응용 프로그램 코드를 변경할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-134">No changes are required in your application code to handle regional failovers.</span></span> <span data-ttu-id="0877d-135">이 프로세스 전체에서 Cosmos DB를 통해 일관성이 계속 보장되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-135">During this entire process, consistency guarantees continue to be honored by Cosmos DB.</span></span>

![Azure Cosmos DB의 읽기 지역 장애](./media/regional-failover/read-region-failures.png)

<span data-ttu-id="0877d-137">영향을 받은 지역이 가동 중단에서 복구되면 해당 지역에서 영향을 받은 모든 Cosmos DB 계정이 서비스에서 자동으로 복구됩니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-137">Once the affected region recovers from the outage, all the affected Cosmos DB accounts in the region are automatically recovered by the service.</span></span> <span data-ttu-id="0877d-138">영향을 받은 지역에 읽기 지역이 있는 Cosmos DB 계정은 자동으로 현재 쓰기 지역과 동기화되고 온라인 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-138">Cosmos DB accounts that had a read region in the affected region will then automatically sync with current write region and turn online.</span></span> <span data-ttu-id="0877d-139">Cosmos DB SDK에서 새로운 지역의 가용성을 검색하고 응용 프로그램이 구성한 기본 지역 목록을 기반으로 하여 해당 지역을 현재 읽기 지역으로 선택해야 하는지 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-139">The Cosmos DB SDKs discover the availability of the new region and evaluate whether the region should be selected as the current read region based on the preferred region list configured by the application.</span></span> <span data-ttu-id="0877d-140">후속 읽기는 응용 프로그램 코드를 변경하지 않고도 복구된 지역으로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-140">Subsequent reads are redirected to the recovered region without requiring any changes to your application code.</span></span>

<span data-ttu-id="0877d-141">**쓰기 지역에 가동 중단이 발생하면 어떻게 됩니까?**</span><span class="sxs-lookup"><span data-stu-id="0877d-141">**What happens if a write region has an outage?**</span></span>

<span data-ttu-id="0877d-142">영향을 받은 지역이 지정된 Cosmos DB 계정의 현재 쓰기 지역이면 해당 지역이 자동으로 오프라인으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-142">If the affected region is the current write region for a given Cosmos DB account, then the region will be automatically marked as offline.</span></span> <span data-ttu-id="0877d-143">그런 다음 대체 지역이 영향을 받은 각 Cosmos DB 계정의 쓰기 지역으로 승격됩니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-143">Then, an alternative region is promoted as the write region each affected Cosmos DB account.</span></span> <span data-ttu-id="0877d-144">Azure Portal을 통하거나 [프로그래밍 방식](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_FailoverPriorityChange)으로 Cosmos DB 계정의 지역 선택 순서를 완전히 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-144">You can fully control the region selection order for your Cosmos DB accounts via the Azure portal or [programmatically](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_FailoverPriorityChange).</span></span> 

![Azure Cosmos DB의 장애 조치(failover) 우선 순위](./media/regional-failover/failover-priorities.png)

<span data-ttu-id="0877d-146">자동 장애 조치(failover) 중에는 Cosmos DB가 지정된 우선 순위에 따라 지정된 Cosmos DB 계정의 다음 쓰기 지역을 자동으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-146">During automatic failovers, Cosmos DB automatically chooses the next write region for a given Cosmos DB account based on the specified priority order.</span></span> 

![Azure Cosmos DB의 쓰기 지역 장애](./media/regional-failover/write-region-failures.png)

<span data-ttu-id="0877d-148">영향을 받은 지역이 가동 중단에서 복구되면 해당 지역에서 영향을 받은 모든 Cosmos DB 계정이 서비스에서 자동으로 복구됩니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-148">Once the affected region recovers from the outage, all the affected Cosmos DB accounts in the region are automatically recovered by the service.</span></span> 

* <span data-ttu-id="0877d-149">영향을 받은 지역에 이전 쓰기 지역이 있는 Cosmos DB 계정은 지역 복구 후에도 읽기 가능한 상태의 오프라인 모드로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-149">Cosmos DB accounts with their previous write region in the affected region will stay in an offline mode with read availability even after the recovery of the region.</span></span> 
* <span data-ttu-id="0877d-150">이 지역을 쿼리하여 현재 쓰기 지역에서 사용 가능한 데이터와 비교함으로써 가동 중단 중에 복제되지 않은 쓰기를 모두 계산할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-150">You can query this region to compute any unreplicated writes during the outage by comparing with the data available in the current write region.</span></span> <span data-ttu-id="0877d-151">응용 프로그램의 요구에 따라 병합 및/또는 충돌 해결을 수행하고 변경 내용의 최종 집합을 현재 쓰기 지역에 다시 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-151">Based on the needs of your application, you can perform merge and/or conflict resolution and write the final set of changes back to the current write region.</span></span> 
* <span data-ttu-id="0877d-152">변경 내용 병합을 완료한 후 지역을 제거했다가 Cosmos DB 계정에 다시 추가하면 영향을 받은 지역을 다시 온라인 상태로 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-152">Once you've completed merging changes, you can bring the affected region back online by removing and readding the region to your Cosmos DB account.</span></span> <span data-ttu-id="0877d-153">지역이 다시 추가되면 Azure Portal을 통하거나 [프로그래밍 방식](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_CreateOrUpdate)으로 수동 장애 조치를 수행하여 쓰기 지역으로 다시 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-153">Once the region is added back, you can configure it back as the write region by performing a manual failover via the Azure portal or [programmatically](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_CreateOrUpdate).</span></span>

## <span data-ttu-id="0877d-154"><a id="ManualFailovers"></a>수동 장애 조치</span><span class="sxs-lookup"><span data-stu-id="0877d-154"><a id="ManualFailovers"></a>Manual Failovers</span></span>

<span data-ttu-id="0877d-155">자동 장애(failover) 조치 외에도 지정된 Cosmos DB 계정의 현재 쓰기 지역을 기존 읽기 지역 중 하나로 직접 동적으로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-155">In addition to automatic failovers, the current write region of a given Cosmos DB account can be manually changed dynamically to one of the existing read regions.</span></span> <span data-ttu-id="0877d-156">수동 장애 조치는 Azure Portal을 통하거나 [프로그래밍 방식](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_CreateOrUpdate)으로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-156">Manual failovers can be initiated via the Azure portal or [programmatically](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_CreateOrUpdate).</span></span> 

<span data-ttu-id="0877d-157">수동 장애 조치(failover)는 **데이터 무손실** 및 **가용성 무손실**을 보장하고 이전 쓰기 지역의 쓰기 상태를 지정된 Cosmos DB 계정의 새 쓰기 지역으로 정상적으로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-157">Manual failovers ensure **zero data loss** and **zero availability** loss and gracefully transfer write status from the old write region to the new one for the specified Cosmos DB account.</span></span> <span data-ttu-id="0877d-158">자동 장애 조치(failover)와 마찬가지로 Cosmos DB SDK는 수동 장애 조치 중에 쓰기 지역 변경을 자동으로 처리하고 호출이 자동으로 새 쓰기 지역으로 리디렉션되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-158">Like in automatic failovers, the Cosmos DB SDK automatically handles write region changes during manual failovers and ensures that calls are automatically redirected to the new write region.</span></span> <span data-ttu-id="0877d-159">장애 조치를 관리하기 위해 응용 프로그램 코드 또는 구성을 변경할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-159">No code or configuration changes are required in your application to manage failovers.</span></span> 

![Azure Cosmos DB에서의 수동 장애 조치(failover)](./media/regional-failover/manual-failovers.png)

<span data-ttu-id="0877d-161">수동 장애 조치가 유용할 수 있는 몇 가지 일반적인 시나리오는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-161">Some of the common scenarios where manual failover can be useful are:</span></span>

<span data-ttu-id="0877d-162">**시계 모델 준수** - 응용 프로그램에 하루 중 시간을 기준으로 예측 가능한 트래픽 패턴이 있는 경우 이 기준에 따라 쓰기 상태를 가장 활동적인 지역으로 주기적으로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-162">**Follow the clock model**: If your applications have predictable traffic patterns based on the time of the day, you can periodically change the write status to the most active geographic region based on time of the day.</span></span>

<span data-ttu-id="0877d-163">**서비스 업데이트** - 전 세계에 분산된 응용 프로그램 배포에는 예정된 서비스 업데이트 중에 트래픽 관리자를 통해 다른 지역으로 트래픽을 다시 라우팅하는 작업이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-163">**Service update**: Certain globally distributed application deployment may involve rerouting traffic to different region via traffic manager during their planned service update.</span></span> <span data-ttu-id="0877d-164">이러한 응용 프로그램 배포는 이제 수동 장애 조치를 사용하여 서비스 업데이트 기간 동안 활성 트래픽이 될 지역에 대한 쓰기 상태를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-164">Such application deployment now can use manual failover to keep the write status to the region where there is going to be active traffic during the service update window.</span></span>

<span data-ttu-id="0877d-165">**BCDR(비즈니스 연속성 및 재해 복구) 및 HADR(고가용성 및 재해 복구) 절차** - 대부분의 엔터프라이즈 응용 프로그램에는 개발 및 릴리스 프로세스의 일부로 비즈니스 연속성 테스트가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-165">**Business Continuity and Disaster Recovery (BCDR) and High Availability and Disaster Recovery (HADR) drills**: Most enterprise applications include business continuity tests as part of their development and release process.</span></span> <span data-ttu-id="0877d-166">BCDR 및 HADR 테스트는 종종 지역 가동 중단 위반의 경우 규정 준수 인증 및 서비스 가용성 보장의 중요한 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-166">BCDR and HADR testing is often an important step in compliance certifications and guaranteeing service availability in the case of regional outages.</span></span> <span data-ttu-id="0877d-167">Cosmos DB 계정의 수동 장애 조치(failover)를 트리거하거나 지역을 동적으로 추가 및 제거하여 저장소에 Cosmos DB를 사용하는 응용 프로그램의 BCDR 준비 상태를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-167">You can test the BCDR readiness of your applications that use Cosmos DB for storage by triggering a manual failover of your Cosmos DB account and/or adding and removing a region dynamically.</span></span>

<span data-ttu-id="0877d-168">이 문서에서는 Cosmos DB에서 수동 및 자동 장애 조치(failover)가 작동하는 방식 및 전역으로 사용할 수 있도록 Cosmos DB 계정과 응용 프로그램을 구성하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-168">In this article, we reviewed how manual and automatic failovers work in Cosmos DB, and how you can configure your Cosmos DB accounts and applications to be globally available.</span></span> <span data-ttu-id="0877d-169">Cosmos DB의 글로벌 복제 지원을 사용하면 종단 간 대기 시간을 향상시키고 지역 장애 발생 시에도 가용성을 높일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-169">By using Cosmos DB's global replication support, you can improve end-to-end latency and ensure that they are highly available even in the event of region failures.</span></span> 

## <span data-ttu-id="0877d-170"><a id="NextSteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="0877d-170"><a id="NextSteps"></a>Next Steps</span></span>
* <span data-ttu-id="0877d-171">Cosmos DB에서 [글로벌 배포](distribute-data-globally.md)를 지원하는 방법에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="0877d-171">Learn about how Cosmos DB supports [global distribution](distribute-data-globally.md)</span></span>
* <span data-ttu-id="0877d-172">[Azure Cosmos DB를 통한 전역 일관성](consistency-levels.md)에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="0877d-172">Learn about [global consistency with Azure Cosmos DB](consistency-levels.md)</span></span>
* <span data-ttu-id="0877d-173">Azure Cosmos DB의 [DocumentDB API](../cosmos-db/tutorial-global-distribution-documentdb.md)를 사용하여 여러 지역으로 개발</span><span class="sxs-lookup"><span data-stu-id="0877d-173">Develop with multiple regions using Azure Cosmos DB's [DocumentDB API](../cosmos-db/tutorial-global-distribution-documentdb.md)</span></span>
* <span data-ttu-id="0877d-174">Azure DocumentDB로 [다중 지역 기록기 아키텍처](multi-region-writers.md)를 작성하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0877d-174">Learn how to build [Multi-region writer architectures](multi-region-writers.md) with Azure DocumentDB</span></span>

