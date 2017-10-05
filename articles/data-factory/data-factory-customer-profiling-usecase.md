---
title: "사용 사례 - 고객 프로파일링"
description: "Azure 데이터 팩터리로 데이터 기반 워크플로를(파이프라인) 만들어 게임 고객을 프로파일링하는 방법을 알아봅니다."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: e07d55cf-8051-4203-9966-bdfa1035104b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 4ee4c3a979a3cdd7ec793d12f812e5b126a2ce94
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-case---customer-profiling"></a><span data-ttu-id="12355-103">사용 사례 - 고객 프로파일링</span><span class="sxs-lookup"><span data-stu-id="12355-103">Use Case - Customer Profiling</span></span>
<span data-ttu-id="12355-104">Azure Data Factory는 솔루션 가속기의 Cortana Intelligence Suite를 구현하는 데 사용되는 다양한 서비스 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="12355-104">Azure Data Factory is one of many services used to implement the Cortana Intelligence Suite of solution accelerators.</span></span>  <span data-ttu-id="12355-105">Cortana Intelligence에 대한 자세한 내용은 [Cortana Intelligence Suite](http://www.microsoft.com/cortanaanalytics)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12355-105">For more information about Cortana Intelligence, visit [Cortana Intelligence Suite](http://www.microsoft.com/cortanaanalytics).</span></span> <span data-ttu-id="12355-106">이 문서에서는 Azure 데이터 팩터리가 어떻게 일반적인 분석 문제를 해결할 수 있는지를 이해하기 시작하는 데 도움이 되는 간단한 사용 사례를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="12355-106">In this document, we describe a simple use case to help you get started with understanding how Azure Data Factory can solve common analytics problems.</span></span>

## <a name="scenario"></a><span data-ttu-id="12355-107">시나리오</span><span class="sxs-lookup"><span data-stu-id="12355-107">Scenario</span></span>
<span data-ttu-id="12355-108">Contoso는 게임 콘솔, 핸드헬드 장치, PC(개인용 컴퓨터) 등 다양한 플랫폼용 게임을 만드는 게임 회사입니다.</span><span class="sxs-lookup"><span data-stu-id="12355-108">Contoso is a gaming company that creates games for multiple platforms: game consoles, hand held devices, and personal computers (PCs).</span></span> <span data-ttu-id="12355-109">플레이어가 이러한 게임을 플레이하면 사용 패턴, 게임 스타일 및 사용자 기본 설정을 추적하는 많은 양의 로그 데이터가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="12355-109">As players play these games, large volume of log data is produced that tracks the usage patterns, gaming style, and preferences of the user.</span></span>  <span data-ttu-id="12355-110">인구 통계, 지역 및 제품 데이터가 결합되는 경우 Contoso는 분석을 수행하여 플레이어의 환경을 개선하고 업그레이드 및 게임 내 구매를 특정화하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="12355-110">When combined with demographic, regional, and product data, Contoso can perform analytics to guide them about how to enhance players’ experience and target them for upgrades and in-game purchases.</span></span> 

<span data-ttu-id="12355-111">Contoso의 목표는 플레이어의 게임 기록을 기반으로 상향 판매/교차 판매 기회를 식별하고 매력적인 기능을 추가하여 비즈니스를 성장시키고 고객에게 더 나은 환경을 제공하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="12355-111">Contoso’s goal is to identify up-sell/cross-sell opportunities based on the gaming history of its players and add compelling features to drive business growth and provide a better experience to customers.</span></span> <span data-ttu-id="12355-112">이 사용 사례의 경우 비즈니스의 예로 게임 회사를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="12355-112">For this use case, we use a gaming company as an example of a business.</span></span> <span data-ttu-id="12355-113">이 회사에서는 플레이어의 동작에 따라 게임을 최적화하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="12355-113">The company wants to optimize its games based on players’ behavior.</span></span> <span data-ttu-id="12355-114">이러한 원칙은 상품 및 서비스에 고객을 참여시키고 고객의 환경을 개선하고자 하는 모든 비즈니스에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="12355-114">These principles apply to any business that wants to engage its customers around its goods and services and enhance their customers’ experience.</span></span>

<span data-ttu-id="12355-115">이 솔루션에서는 Contoso가 최근 시작한 마케팅 캠페인의 효과를 평가하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="12355-115">In this solution, Contoso wants to evaluate the effectiveness of a marketing campaign it has recently launched.</span></span> <span data-ttu-id="12355-116">원시 게임 로그로 시작하여, 지리적 위치 데이터를 처리하고 보강하고, 광고 참조 데이터와 조인하고 마지막으로 Azure SQL Database에 복사하여 캠페인의 영향을 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="12355-116">We start with the raw gaming logs, process and enrich them with geolocation data, join it with advertising reference data, and lastly copy them into an Azure SQL Database to analyze the campaign’s impact.</span></span>

## <a name="deploy-solution"></a><span data-ttu-id="12355-117">솔루션 배포</span><span class="sxs-lookup"><span data-stu-id="12355-117">Deploy Solution</span></span>
<span data-ttu-id="12355-118">액세스하여 이 간단한 사용 사례를 시도하는데 필요한 것은 [Azure 구독](https://azure.microsoft.com/pricing/free-trial/), [Azure Blob Storage 계정](../storage/common/storage-create-storage-account.md#create-a-storage-account) 및 [Azure SQL Database](../sql-database/sql-database-get-started.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="12355-118">All you need to access and try out this simple use case is an [Azure subscription](https://azure.microsoft.com/pricing/free-trial/), an [Azure Blob storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account), and an [Azure SQL Database](../sql-database/sql-database-get-started.md).</span></span> <span data-ttu-id="12355-119">데이터 팩터리의 홈 페이지에 **샘플 파이프라인** 타일에서 파이프라인을 프로파일링하는 고객을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="12355-119">You deploy the customer profiling pipeline from the **Sample pipelines** tile on the home page of your data factory.</span></span>

1. <span data-ttu-id="12355-120">데이터 팩터리를 만들거나 기존 데이터 팩터리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="12355-120">Create a data factory or open an existing data factory.</span></span> <span data-ttu-id="12355-121">Data Factory를 만드는 단계는 [Data Factory를 사용하여 Blob 저장소에서 SQL Database로 데이터 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12355-121">See [Copy data from Blob Storage to SQL Database using Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for steps to create a data factory.</span></span>
2. <span data-ttu-id="12355-122">데이터 팩터리의 **데이터 팩터리** 블레이드에서 **샘플 파이프라인** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12355-122">In the **DATA FACTORY** blade for the data factory, click the **Sample pipelines** tile.</span></span>

    ![샘플 파이프라인 타일](./media/data-factory-samples/SamplePipelinesTile.png)
3. <span data-ttu-id="12355-124">**샘플 파이프라인** 블레이드에서 배포할 **고객 프로파일링**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12355-124">In the **Sample pipelines** blade, click the **Customer profiling** that you want to deploy.</span></span>

    ![샘플 파이프라인 블레이드](./media/data-factory-samples/SampleTile.png)
4. <span data-ttu-id="12355-126">샘플에 대한 구성 설정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="12355-126">Specify configuration settings for the sample.</span></span> <span data-ttu-id="12355-127">예를 들어 Azure Storage 계정 이름과 키, Azure SQL Server 이름, 데이터베이스, 사용자 ID, 암호 등입니다.</span><span class="sxs-lookup"><span data-stu-id="12355-127">For example, your Azure storage account name and key, Azure SQL server name, database, User ID, and password.</span></span>

    ![샘플 블레이드](./media/data-factory-samples/SampleBlade.png)
5. <span data-ttu-id="12355-129">구성 설정 지정을 마쳤으면 **만들기** 를 클릭하여 샘플 파이프라인 및 파이프라인에서 사용되는 연결된 서비스/테이블을 만듭니다/배포합니다.</span><span class="sxs-lookup"><span data-stu-id="12355-129">After you are done with specifying the configuration settings, click **Create** to create/deploy the sample pipelines and linked services/tables used by the pipelines.</span></span>
6. <span data-ttu-id="12355-130">이전에 **샘플 파이프라인** 블레이드에서 클릭한 샘플 타일에 배포 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="12355-130">You see the status of deployment on the sample tile you clicked earlier on the **Sample pipelines** blade.</span></span>

    ![배포 상태](./media/data-factory-samples/DeploymentStatus.png)
7. <span data-ttu-id="12355-132">샘플 타일에 **배포 성공** 메시지가 표시되면 **샘플 파이프라인** 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="12355-132">When you see the **Deployment succeeded** message on the tile for the sample, close the **Sample pipelines** blade.</span></span>  
8. <span data-ttu-id="12355-133">**데이터 팩터리** 블레이드에서 연결된 서비스, 데이터 집합 및 파이프라인이 데이터 팩터리에 추가된 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12355-133">On **DATA FACTORY** blade, you see that linked services, data sets, and pipelines are added to your data factory.</span></span>  

    ![데이터 팩터리 블레이드](./media/data-factory-samples/DataFactoryBladeAfter.png)

## <a name="solution-overview"></a><span data-ttu-id="12355-135">솔루션 개요</span><span class="sxs-lookup"><span data-stu-id="12355-135">Solution Overview</span></span>
<span data-ttu-id="12355-136">이 간단한 사용 사례는 Azure 데이터 팩터리를 사용하여 데이터를 수집, 준비, 변환, 분석 및 게시하는 방법의 예로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12355-136">This simple use case can be used as an example of how you can use Azure Data Factory to ingest, prepare, transform, analyze, and publish data.</span></span>

![종단 간 워크플로](./media/data-factory-customer-profiling-usecase/EndToEndWorkflow.png)

<span data-ttu-id="12355-138">이 그림은 배포된 후 Azure 포털에서 데이터 파이프라인을 표시하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="12355-138">This Figure depicts how the data pipelines appear in the Azure portal after they have been deployed.</span></span>

1. <span data-ttu-id="12355-139">**PartitionGameLogsPipeline** 은 Blob 저장소에서 원시 게임 이벤트를 읽고 연도, 월 및 일을 기준으로 파티션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="12355-139">The **PartitionGameLogsPipeline** reads the raw game events from blob storage and creates partitions based on year, month, and day.</span></span>
2. <span data-ttu-id="12355-140">**EnrichGameLogsPipeline** 은 분할된 게임 이벤트를 지역 코드 참조 데이터와 조인하고 IP 주소를 해당하는 지리적 위치에 매핑하여 데이터를 강화합니다.</span><span class="sxs-lookup"><span data-stu-id="12355-140">The **EnrichGameLogsPipeline** joins partitioned game events with geo code reference data and enriches the data by mapping IP addresses to the corresponding geo-locations.</span></span>
3. <span data-ttu-id="12355-141">**AnalyzeMarketingCampaignPipeline** 파이프라인은 강화된 데이터를 사용하고 이 데이터를 광고 데이터와 함께 처리하여 마케팅 캠페인 효과가 포함된 최종 출력을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="12355-141">The **AnalyzeMarketingCampaignPipeline** pipeline uses the enriched data and processes it with the advertising data to create the final output that contains marketing campaign effectiveness.</span></span>

<span data-ttu-id="12355-142">이 예에서 Data Factory는 입력 데이터의 복사, 변환 및 처리를 조정하고 Azure SQL Database로 최종 데이터를 출력하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="12355-142">In this example, Data Factory is used to orchestrate activities that copy input data, transform, and process the data, and output the final data to an Azure SQL Database.</span></span>  <span data-ttu-id="12355-143">또한 데이터 파이프라인의 네트워크를 시각화하고 관리하며 UI에서 상태를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12355-143">You can also visualize the network of data pipelines, manage them, and monitor their status from the UI.</span></span>

## <a name="benefits"></a><span data-ttu-id="12355-144">이점</span><span class="sxs-lookup"><span data-stu-id="12355-144">Benefits</span></span>
<span data-ttu-id="12355-145">사용자 프로필 분석을 최적화하고 비즈니스 목표에 맞추어 게임 회사는 신속하게 사용 패턴을 수집하고 마케팅 캠페인의 효과를 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12355-145">By optimizing their user profile analytics and aligning it with business goals, gaming company is able to quickly collect usage patterns, and analyze the effectiveness of its marketing campaigns.</span></span>

